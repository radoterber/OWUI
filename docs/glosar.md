# Glosář pojmů

Stručný přehled pojmů používaných v dokumentaci OWUI.

## Platforma a komponenty

**OWUI (Open-WebUI)**
Webové rozhraní pro práci s jazykovými modely a agenty. Centrální AI hub banky.

**LiteLLM**
Firemní LLM proxy. Jediný vstupní bod, přes který OWUI (a agenti) volají všechny jazykové modely. Poskytuje OpenAI-kompatibilní API, centrální logování a správu klíčů.

**Workspace**
Sekce v OWUI dostupná roli PowerUser a Admin. Umožňuje tvorbu vlastních agentů, Tools a pipelines.

**Web search**
Vestavěný nástroj OWUI pro vyhledávání na webu během konverzace. Modely jej využívají automaticky podle povahy dotazu.

## Modely a interakce

**Model**
Jazykový model (LLM) provozovaný přes LiteLLM. Generuje odpovědi na základě vstupního promptu.

**Prompt**
Vstupní zadání pro model. Může být uživatelský dotaz, systémový prompt nebo prompt šablona.

**Systémový prompt**
Skrytá instrukce definující roli a chování agenta (např. "Jsi asistent pro HR oddělení…").

**Konverzace**
Posloupnost zpráv mezi uživatelem a modelem/agentem, uložená v historii uživatele.

## Agenti a rozšíření

**Agent**
Předkonfigurovaná instance modelu obohacená o systémový prompt, znalostní bázi (RAG) a nástroje (Tools). V OWUI také označovaný jako Model preset.

**Tool (nástroj)**
Funkce, kterou může model volat během konverzace (např. dotaz na CRM). V OWUI implementováno jako Python kód.

**Pipeline**
Řetězec kroků zpracování – předzpracování vstupu, volání modelu, postpracování výstupu.

**RAG (Retrieval-Augmented Generation)**
Technika obohacení odpovědi modelu o informace dohledané ve znalostní bázi.

**Znalostní báze**
Sada dokumentů indexovaných pro RAG. Může být osobní (per uživatel) nebo sdílená (per doména/organizace).

## Identita a přístup

**SSO (Single Sign-On)**
Jednotné přihlašování. V OWUI realizováno přes EntraID.

**EntraID (Azure AD / AAD)**
Identity provider Microsoft. Spravuje firemní identity a AD skupiny.

**AD skupina**
Skupina uživatelů v EntraID. V OWUI slouží k řízení přístupu ke modelům a doménám.

**OWUI role**
Úroveň oprávnění v rámci OWUI: User, PowerUser, Admin. Nezávislá na členství v AD skupinách.

**Business doména**
Logická skupina agentů a zdrojů vázaná k oblasti banky (HR, Bankéři, Trading, Provoz, IT, …). Přístup k doméně je řízen členstvím v příslušné AD skupině.

## Přístup ke zdrojům

**MCP (Model Context Protocol)**
Protokol pro standardizovanou integraci modelů s externími zdroji a nástroji.

**MCP server**
Brána mezi agentem v OWUI a cílovým systémem (CRM, HR systém, …). Provádí volání jménem uživatele.

**OBO (On-Behalf-Of)**
OAuth2 flow, při kterém služba volá další službu se zachováním identity původního uživatele. V OWUI použito pro volání zdrojů jménem přihlášeného uživatele.

**Cílový systém**
Interní bankovní systém, ke kterému agent přistupuje (CRM, personální systém, ServiceDesk, …).

## Provoz a governance

**Platformový tým**
Tým zodpovědný za provoz a správu OWUI. Drží roli Admin.

**Domain Owner**
(plánováno do budoucna) Zástupce business, zodpovědný za agenty a zdroje konkrétní domény.

**Datová klasifikace**
Označení citlivosti dat dle interního standardu banky (např. Veřejné / Interní / Důvěrné / Tajné). Viz `[doplnit odkaz na interní standard datové klasifikace]`.

**Audit log**
Záznam všech podstatných akcí (přihlášení, konverzace, volání MCP). Slouží pro auditing a vyšetřování incidentů.
