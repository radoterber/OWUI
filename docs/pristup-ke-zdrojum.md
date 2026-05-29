# Přístup ke zdrojům

## Princip

Agenti business domén potřebují přistupovat k interním systémům (CRM, personální systém, ServiceDesk apod.). Klíčový požadavek: přístup musí probíhat **jménem přihlášeného uživatele** (on-behalf-of), nikoliv pod servisním účtem agenta. Důvody:

- auditovatelnost – každé volání je přiřazeno konkrétnímu uživateli
- oprávnění – uživatel vidí pouze data, ke kterým má sám přístup v daném systému
- bezpečnost – agenti nemohou obejít existující přístupová práva

## Navrhovaná architektura

### Mechanismus volání z OWUI

OWUI nativně neumí volat MCP servery – podporuje volání nástrojů přes **OpenAPI Tool Servers**. Zvažované varianty integrace:

- **MCP-to-OpenAPI proxy** (např. `mcpo`) – tenká vrstva, která vystaví MCP server jako OpenAPI a OWUI s ní komunikuje standardně
- **Nativní OpenAPI Tool Servers** – přeskočit MCP a implementovat doménové brány rovnou jako OpenAPI služby
- **Budoucí nativní MCP podpora v OWUI** – pokud bude přidána

> **Otevřená otázka:** Výběr konkrétního mechanismu (MCP + proxy vs. čistě OpenAPI). Volba má dopad na rychlost vývoje, znovupoužitelnost nástrojů a operační složitost.

### MCP server jako brána ke zdrojům

Každá business doména bude mít dedikovaný **MCP server** (Model Context Protocol), který:

- přijímá volání od agenta v OWUI
- ověřuje identitu a oprávnění volajícího uživatele
- provádí volání do cílového systému jménem uživatele
- vrací výsledek agentovi

```
[ OWUI – Agent ]
      |
      | volání MCP Tool (s identitou uživatele)
      v
[ MCP Server: <doména> ]
      |
      | ověření OBO tokenu (EntraID)
      v
[ Cílový systém (CRM, HR systém, ...) ]
```

### Autorizace – OAuth2 On-Behalf-Of (OBO) flow

Navrhovaný mechanismus přenosu identity:

1. Uživatel se přihlásí do OWUI přes EntraID (získá access token)
2. OWUI při volání MCP serveru předá token uživatele (nebo požádá EntraID o OBO token pro cílovou službu)
3. MCP server token validuje vůči EntraID
4. MCP server volá cílový systém s identitou uživatele

```
OWUI  ──[OBO token]──>  MCP Server  ──[user identity]──>  Cílový systém
         (EntraID)                        (EntraID)
```

> **Otevřená otázka:** Konkrétní implementace OBO flow závisí na tom, zda cílové systémy podporují OAuth2 / EntraID autentizaci přímo, nebo zda je nutná proxy vrstva. Je třeba prověřit pro každý systém zvlášť.

## Otevřené otázky

> **Otevřená otázka – token forwarding vs. service account:**
> Alternativou k OBO flow je použití servisního účtu per doména s explicitní autorizační kontrolou na úrovni MCP serveru (MCP server si sám ověří oprávnění uživatele vůči internímu autorizačnímu systému). Rozhodnutí závisí na možnostech cílových systémů.

> **Otevřená otázka – audit trail volání MCP:**
> Kde a jak logovat volání MCP serverů? Možnosti: centrální audit log platformy, logy na straně MCP serveru, logy v cílovém systému. Pravděpodobně kombinace.

> **Otevřená otázka – granularita oprávnění:**
> Oprávnění uživatele v cílovém systému (např. CRM) nemusí být binární. Je třeba definovat, jak MCP server zachází s parciálním přístupem (uživatel má přístup k části dat) a jak to komunikuje agentovi.

> **Otevřená otázka – dostupnost / fallback:**
> Pokud MCP server nebo cílový systém není dostupný, jak se agent zachová? Měl by to srozumitelně sdělit uživateli.

> **Otevřená otázka – zápisové (write) operace:**
> V iniciální fázi se počítá pouze se čtením. Zápisové operace (např. založení ticketu v ServiceDesku) vyžadují řešení idempotence, explicitního potvrzení uživatelem před provedením, a auditu změn. Zavedeny budou až po samostatném bezpečnostním posouzení.

> **Otevřená otázka – životnost OBO tokenu při vícekrokovém volání:**
> Pokud agent v rámci jedné odpovědi provede více kroků (více volání zdroje), token uživatele musí být platný po celou dobu. Pro dlouhotrvající operace nebo pipeline kroky je třeba navrhnout strategii (refresh tokenu, opakované vyžádání OBO tokenu, omezení délky volání).

## Bezpečnostní požadavky

- MCP servery jsou dostupné pouze z interní sítě banky
- Každý MCP server obsluhuje výhradně svou business doménu (izolace)
- Veškerá volání jsou logována s identitou uživatele
- MCP server nesmí cachovat tokeny uživatelů nad rámec doby platnosti

## Stav

| Komponenta | Stav |
|---|---|
| Konceptuální návrh (tento dokument) | ✅ |
| Výběr implementačního přístupu (OBO vs. service account) | 🔧 otevřená otázka |
| Proof-of-concept MCP server | 🔧 plánováno |
| Integrace první domény (pilot) | 🔧 plánováno |
