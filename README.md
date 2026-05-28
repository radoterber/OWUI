# Open-WebUI (OWUI) – Dokumentace

Dokumentace platformy **OWUI** nasazené v bankovním prostředí jako centrální AI hub. Platforma poskytuje přístup k jazykovým modelům a specializovaným agentům per business doménu, s přihlašováním přes SSO (EntraID) a řízením přístupu přes AD skupiny.

> **Verze dokumentace:** iniciální draft · **Platné k:** _[doplnit datum]_ · Historie změn: viz git log
> Vlastník dokumentace: platformový tým (viz [`docs/governance.md`](docs/governance.md))

## Stav platformy

| Komponenta | Stav |
|---|---|
| OWUI + základní konverzace | ✅ funkční |
| Web search | ✅ funkční |
| Napojení modelů přes LiteLLM | ✅ funkční |
| SSO (EntraID) | ✅ funkční |
| Agenti per business doména | 🔧 v přípravě |
| Přístup ke zdrojům (MCP) | 🔧 koncept |

## Obsah dokumentace

| Dokument | Popis |
|---|---|
| [`docs/architektura.md`](docs/architektura.md) | Komponenty, topologie, integrace |
| [`docs/modely.md`](docs/modely.md) | Dostupné modely, LiteLLM proxy, řízení přístupu |
| [`docs/role-a-skupiny.md`](docs/role-a-skupiny.md) | Role Admin / PowerUser / User, mapování AD skupin |
| [`docs/agenti.md`](docs/agenti.md) | Business domény, katalog agentů, datové zdroje |
| [`docs/pristup-ke-zdrojum.md`](docs/pristup-ke-zdrojum.md) | MCP servery, OBO autorizace – návrh a otevřené otázky |
| [`docs/governance.md`](docs/governance.md) | Provozní řád – zodpovědnosti, procesy změn, incidenty |
| [`docs/bezpecnost.md`](docs/bezpecnost.md) | Bezpečnost a širší governance aspekty – přehled pro security/risk/audit |
| [`docs/navod-uzivatele.md`](docs/navod-uzivatele.md) | Návod pro koncové uživatele |
| [`docs/glosar.md`](docs/glosar.md) | Glosář pojmů (OBO, MCP, RAG, LiteLLM, …) |

## Kontakt

Správce platformy: **[název týmu]** · Požadavky a hlášení chyb: **[ticketovací systém]**
