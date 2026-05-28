# Governance OWUI

## Zodpovědnosti

V aktuální fázi je správa platformy centralizována na **platformovém týmu** (Admin).

| Role | Zodpovědnost |
|---|---|
| Platformový tým (Admin) | Provoz a konfigurace OWUI, správa uživatelů a přístupů, schvalování agentů a Tools, koordinace s IAM a bezpečnostním týmem |
| IAM tým | Správa AD skupin a jejich napojení na OWUI |
| Bezpečnostní tým | Schvalování nových modelů, audit přístupu ke zdrojům |
| _[budoucí: Domain Owner]_ | _V budoucnu může být zodpovědnost za agenty dané domény delegována na zástupce business_ |

## Procesy

### Přidání / odebrání uživatele

1. Žadatel podá požadavek přes **[ticketovací systém]**
2. Platformový tým ověří oprávněnost požadavku (schválení nadřízeného)
3. IAM tým přidá / odebere uživatele z příslušných AD skupin
4. Přístup v OWUI se promítne automaticky při dalším přihlášení

### Povýšení uživatele na PowerUser

1. Žadatel (nebo jeho nadřízený) podá požadavek s odůvodněním (use-case, proč potřebuje Workspace)
2. Schválení nadřízeným žadatele
3. Platformový tým ověří, že žadatel rozumí pravidlům pro tvorbu agentů a Tools (krátký onboarding nebo potvrzení seznámení s [`navod-uzivatele.md`](navod-uzivatele.md) a [`bezpecnost.md`](bezpecnost.md))
4. Admin přiřadí roli PowerUser v OWUI
5. Odebrání role probíhá stejnou cestou (žádost, schválení, akce Adminem)

### Přidání nového modelu

1. Žadatel podá požadavek s odůvodněním (use-case, model, zdroj)
2. Bezpečnostní tým provede bezpečnostní posouzení modelu
3. Platformový tým zajistí zpřístupnění modelu přes LiteLLM
4. Platformový tým vytvoří příslušnou AD skupinu a aktualizuje katalog modelů v [`modely.md`](modely.md)
5. Přístup k modelu je řízen standardním procesem přidání uživatele

### Přidání nové business domény

1. Žadatel (business zástupce) podá požadavek s popisem domény a potřebných zdrojů
2. Platformový tým společně s bezpečnostním týmem posoudí požadavky na přístup ke zdrojům
3. Navrhne se MCP server a autorizační model (viz [`pristup-ke-zdrojum.md`](pristup-ke-zdrojum.md))
4. IAM tým vytvoří AD skupinu `OWUI-DOMAIN-<název>`
5. Platformový tým nakonfiguruje agenta, MCP server a znalostní bázi
6. Proběhne UAT s klíčovými uživateli domény
7. Doména je zprovozněna; aktualizuje se [`agenti.md`](agenti.md)

### Schválení sdílení agenta nebo Tool (PowerUser → sdílení)

Jakékoliv sdílení agenta nebo Tool s dalšími uživateli (i v rámci úzkého týmu) vyžaduje review Adminem.

1. PowerUser vytvoří agenta nebo Tool ve svém Workspace pro osobní použití
2. Podá žádost o sdílení přes **[ticketovací systém]** (popis funkce, cílová skupina uživatelů, případně AD skupina)
3. Platformový tým provede review:
   - funkčnost a kvalita systémového promptu
   - bezpečnost (u Tools: code review Python kódu)
   - soulad s firemním standardem datové klasifikace `[doplnit odkaz na interní standard datové klasifikace]`
   - soulad s compliance pravidly
4. Po schválení Admin publikuje agenta / Tool pro cílovou skupinu
5. V případě zamítnutí platformový tým sdělí důvody a doporučení k úpravě

### Odebrání / deaktivace agenta nebo modelu

1. Podnět může podat kdokoliv (platformový tým, bezpečnostní tým, uživatel)
2. Platformový tým posoudí a rozhodne o deaktivaci
3. Dotčení uživatelé jsou informováni s předstihem (minimálně _[doplnit]_ dní)
4. Agent / model je deaktivován; dokumentace je aktualizována

## Správa přístupu ke zdrojům (MCP)

Přístup agenta ke konkrétnímu zdroji (systému) musí být explicitně schválen:

1. Požadavek na přístup ke zdroji jako součást žádosti o novou doménu nebo rozšíření existující
2. Bezpečnostní tým a owner cílového systému schválí přístup
3. MCP server je nakonfigurován výhradně pro schválený rozsah přístupu
4. Přístup je pravidelně revidován (viz níže)

## Auditing a monitoring

- Veškeré přihlášení a konverzace jsou logovány v OWUI
- Volání MCP serverů jsou logována s identitou uživatele a časovou značkou
- Platformový tým provádí namátkovou kontrolu logů **[frekvence – doplnit]**
- Plný audit log je k dispozici bezpečnostnímu týmu na vyžádání

## Incidenty

| Typ incidentu | Postup |
|---|---|
| Bezpečnostní incident (únik dat, neautorizovaný přístup) | Okamžité nahlášení bezpečnostnímu týmu, deaktivace dotčené komponenty, postup dle interní směrnice pro bezpečnostní incidenty |
| Výpadek platformy | Nahlášení přes **[ticketovací systém]**, platformový tým řeší, SLA _[doplnit]_ |
| Chybný výstup agenta (hallucination, nesprávná data) | Nahlášení přes **[ticketovací systém]**, platformový tým prošetří a případně upraví agenta |
| Žádost o přístup k citlivým datům agentem | Bezpečnostní incident – viz první řádek |

## Review cyklus

| Artefakt | Frekvence review |
|---|---|
| Katalog modelů | Po každé změně + čtvrtletně |
| Katalog agentů a domén | Po každé změně + čtvrtletně |
| Matice AD skupin a oprávnění | Pololetně |
| Přístupy ke zdrojům (MCP) | Pololetně + po každé bezpečnostní události |
| Tento governance dokument | Ročně nebo při podstatné změně platformy |

## Vlastník a údržba dokumentace

- **Vlastník dokumentace:** platformový tým
- **Princip:** každá podstatná změna platformy (nový model, nová doména, změna procesu, změna autorizace) musí být doprovázena aktualizací příslušného dokumentu **ve stejné změně / pull requestu**
- **Verzování a historie:** historie změn je vedena přes git (commit history slouží jako changelog)
- **Návrhy úprav dokumentace:** kdokoliv může navrhnout změnu (pull request, ticket); schvaluje platformový tým
- **Periodický review:** dokumentace prochází plnou revizí ročně (viz tabulka výše)
