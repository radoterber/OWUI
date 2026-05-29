# Agenti

## Co je agent

Agent je předkonfigurovaná instance modelu obohacená o:

- **systémový prompt** – definuje roli, chování a omezení agenta
- **znalostní bázi (RAG)** – přístup k relevantním interním dokumentům
- **nástroje (Tools)** – možnost volat externí zdroje přes MCP server

Agenti jsou organizováni podle business domén. Přístup k agentům domény je podmíněn členstvím v příslušné AD skupině (viz [`role-a-skupiny.md`](role-a-skupiny.md)).

> **Rozsah dat:** Agent vrací pouze data, ke kterým má uživatel přístup v cílovém systému. Volání zdrojů probíhá jménem přihlášeného uživatele (OBO) – uživatel tedy v žádném případě nezíská přes agenta data nad rámec svých vlastních oprávnění. Detail viz [`pristup-ke-zdrojum.md`](pristup-ke-zdrojum.md).

## Business domény

Seznam domén není finální a bude se průběžně rozrůstat podle potřeb organizace.

---

### HR

**AD skupina:** `OWUI-DOMAIN-HR`

| Zdroj | Typ přístupu | Poznámka |
|---|---|---|
| Personální systém | čtení | _[upřesnit – název systému]_ |
| Interní HR dokumenty / směrnice | RAG | |
| _[placeholder]_ | | |

Příklady use-cases:
- dotazy na HR procesy a směrnice
- vyhledávání informací o zaměstnancích (v rozsahu oprávnění uživatele)
- asistence při HR administrativě

---

### Bankéři

**AD skupina:** `OWUI-DOMAIN-BANKERI`

| Zdroj | Typ přístupu | Poznámka |
|---|---|---|
| CRM | čtení | _[upřesnit – název systému]_ |
| Zůstatky a pohyby na účtech klientů | čtení | v rozsahu oprávnění bankéře |
| Produktová dokumentace | RAG | |
| _[placeholder]_ | | |

Příklady use-cases:
- příprava na schůzku s klientem – shrnutí portfolia
- dotazy na produkty a podmínky
- asistence při sjednávání produktů

---

### Trading

**AD skupina:** `OWUI-DOMAIN-TRADING`

| Zdroj | Typ přístupu | Poznámka |
|---|---|---|
| Trading platforma | _[upřesnit]_ | _[placeholder]_ |
| Tržní data | _[upřesnit]_ | _[placeholder]_ |
| Interní předpisy pro trading | RAG | |

Příklady use-cases:
- _[placeholder – doplnit s business doménou]_

---

### Provoz

**AD skupina:** `OWUI-DOMAIN-PROVOZ`

| Zdroj | Typ přístupu | Poznámka |
|---|---|---|
| Interní systémy provozu | _[upřesnit]_ | _[placeholder]_ |
| Provozní dokumentace a postupy | RAG | |

Příklady use-cases:
- _[placeholder – doplnit s business doménou]_

---

### IT

**AD skupina:** `OWUI-DOMAIN-IT`

| Zdroj | Typ přístupu | Poznámka |
|---|---|---|
| ServiceDesk | čtení (zápis cílově) | _[upřesnit – název systému]_; zápis viz pozn. níže |
| CMDB | čtení | |
| Interní IT dokumentace | RAG | |

> **Zápisové operace (write):** V iniciální fázi pracují agenti se zdroji **pouze pro čtení**. Zápis (např. zakládání ticketů) je rizikovější (idempotence, potvrzení uživatelem, audit zápisů) a bude zaveden až po samostatném bezpečnostním posouzení a definici postupu v [`pristup-ke-zdrojum.md`](pristup-ke-zdrojum.md).

Příklady use-cases:
- asistence při zakládání a řešení ticketů
- vyhledávání v dokumentaci a known issues
- dotazy na konfiguraci systémů a infrastruktury

---

## Přidání nové domény

Domény jsou rozšiřitelné. Proces přidání nové domény viz [`governance.md`](governance.md).

Pro každou novou doménu je třeba definovat:

1. Název domény a příslušná AD skupina
2. Seznam datových zdrojů a typ přístupu
3. MCP server zajišťující přístup ke zdrojům (viz [`pristup-ke-zdrojum.md`](pristup-ke-zdrojum.md))
4. Systémový prompt agenta
5. Znalostní báze (dokumenty pro RAG)
