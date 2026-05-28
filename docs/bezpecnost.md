# Bezpečnost a širší governance aspekty

Souhrnný dokument pro security, risk a audit. Pokrývá bezpečnostní pilíře platformy OWUI i navazující governance principy. Detaily provozních procesů jsou v [`governance.md`](governance.md).

## Bezpečnostní pilíře

### Síť a perimetr

- OWUI, LiteLLM i MCP servery běží **výhradně v interní síti banky**
- Žádná komunikace s veřejnými AI službami; všechny modely jsou volány přes LiteLLM
- Externí web search probíhá řízeně přes schválenou komponentu
- Veškerá data zůstávají v perimetru banky

### Identita a autentizace

- Přihlašování výhradně přes **EntraID (SSO)** – žádné lokální účty
- OWUI nepoužívá vlastní hesla
- Identita uživatele je zachována při volání zdrojů přes MCP (OBO flow)
- Detaily viz [`pristup-ke-zdrojum.md`](pristup-ke-zdrojum.md)

### Autorizace

Dvouvrstvé řízení přístupu:

1. **Funkce platformy** – OWUI role (User / PowerUser / Admin), viz [`role-a-skupiny.md`](role-a-skupiny.md)
2. **Data a nástroje** – členství v AD skupinách:
   - dimenze "modely" – ke kterým modelům má uživatel přístup
   - dimenze "domény" – ke kterým doménovým agentům a zdrojům má uživatel přístup

Princip nejmenších oprávnění: uživatel získává přístupy explicitně, ne automaticky.

### Izolace

- Každá business doména má vlastní MCP server a vlastní sadu povolených zdrojů
- MCP server jedné domény nemůže volat zdroje jiné domény
- Osobní znalostní báze jsou izolovány per uživatel
- Sdílené znalostní báze jsou viditelné pouze členům příslušné AD skupiny

### Audit a logování

Logováno:

- přihlášení a odhlášení uživatelů
- konverzace (prompty + odpovědi)
- volání MCP serverů (kdo, kdy, jaký zdroj, výsledek)
- administrativní akce (změny v konfiguraci, publikace agentů)

Logy jsou dostupné platformovému a bezpečnostnímu týmu. Frekvence kontroly a retenční politika viz [`governance.md`](governance.md).

### Sandbox pro vlastní kód

Vlastní Tools (Python kód) psané PowerUsery představují bezpečnostní riziko (RCE, síťové volání, exfiltrace). Mitigace:

- Tools pro osobní použití běží v omezeném prostředí OWUI
- **Publikace pro ostatní uživatele vyžaduje vždy review a schválení Adminem** (zejména code review kódu)
- Proces viz [`governance.md`](governance.md)

## Datová klasifikace a citlivá data

OWUI a agenti pracují s daty různých úrovní citlivosti. Pravidla práce s daty se řídí firemním standardem datové klasifikace: `[doplnit odkaz na interní standard datové klasifikace]`.

Klíčové zásady:

- Uživatel nesmí vkládat do promptů ani znalostních bází data nad rámec své vlastní oprávnění
- Agent vrací pouze data, ke kterým má uživatel přístup v cílovém systému (zajištěno přes OBO – viz [`pristup-ke-zdrojum.md`](pristup-ke-zdrojum.md))
- Pro některé třídy citlivosti mohou platit dodatečná omezení (povolené modely, zákaz použití web search, povinný retenční režim) – konkrétní pravidla jsou součástí standardu

## Bezpečnostní rizika a mitigace

| Riziko | Mitigace |
|---|---|
| Únik citlivých dat do externí AI služby | Všechny modely pouze přes LiteLLM v interní síti |
| Neautorizovaný přístup ke zdrojům | OBO flow + autorizace na úrovni cílového systému |
| Záměna identity / sdílený servisní účet | Identita uživatele je zachována end-to-end |
| Škodlivý kód v PowerUser Tool | Povinný code review před publikací |
| Hallucinace agenta vedoucí k chybnému rozhodnutí | Edukace uživatelů, citace zdrojů, ověřování v primárním systému |
| Eskalace oprávnění přes přístup k více doménám | Pravidelný review oprávnění (viz `governance.md`) |
| Únik dat přes osobní znalostní bázi | Klasifikace dokumentů uživatelem, edukace |
| Kompromitace SSO účtu | Pokrývá firemní bezpečnostní politika EntraID (MFA, podmíněný přístup) |

## Compliance a regulatorní rámec

OWUI je interní nástroj. Práce s ním spadá pod:

- firemní bezpečnostní politiky a směrnice
- standard datové klasifikace `[doplnit odkaz]`
- regulatorní požadavky relevantní pro banku (GDPR, DORA, NIS2, AI Act – v rozsahu, v jakém se aplikují na interní AI nástroje)
- interní směrnice pro řízení AI nástrojů `[doplnit odkaz, pokud existuje]`

Konkrétní mapování na regulatorní požadavky je v gesci compliance a risk týmu.

## Kontaktní eskalační cesta

| Typ podnětu | Kontakt |
|---|---|
| Bezpečnostní incident | Bezpečnostní tým – `[doplnit kontakt]` |
| Provozní incident | Platformový tým – přes `[ticketovací systém]` |
| Otázky compliance / klasifikace dat | Compliance / DPO – `[doplnit kontakt]` |
| Žádost o audit log | Bezpečnostní tým |
