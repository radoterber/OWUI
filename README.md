# Open-WebUI (OWUI) – Dokumentace

Dokumentace platformy OWUI nasazené v bankovním prostředí. Pokrývá napojení modelů, práci s rozhraním, topologii agentů, správu rolí a governance.

## Obsah

| Dokument | Popis |
|---|---|
| [`docs/architektura.md`](docs/architektura.md) | Topologie nasazení, napojení modelů a agentů |
| [`docs/modely.md`](docs/modely.md) | Dostupné modely, parametry, doporučené použití |
| [`docs/agenti.md`](docs/agenti.md) | Katalog agentů, jejich schopnosti a konfigurace |
| [`docs/role.md`](docs/role.md) | Oprávnění rolí Admin / PowerUser / User |
| [`docs/navod.md`](docs/navod.md) | Návod k práci s OWUI pro koncové uživatele |
| [`docs/governance.md`](docs/governance.md) | Governance OWUI – procesy, schvalování, zodpovědnosti |

## Role – přehled

| Funkce | Admin | PowerUser | User |
|---|:---:|:---:|:---:|
| Správa uživatelů a připojení modelů | ✓ | – | – |
| Tvorba a sdílení agentů (org.) | ✓ | – | – |
| Tvorba a sdílení agentů (tým) | ✓ | ✓ | – |
| Správa sdílených znalostních bází | ✓ | ✓ | – |
| Osobní znalostní báze | ✓ | ✓ | ✓ |
| Konverzace s modely a agenty | ✓ | ✓ | ✓ |
| Auditní logy | ✓ | – | – |

## Kontakt

Správce platformy: **[název týmu]** · Požadavky: **[ticketovací systém]**
