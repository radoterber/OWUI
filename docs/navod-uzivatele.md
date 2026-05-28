# Návod pro uživatele

## Přihlášení

OWUI je dostupné na **[URL – doplnit]**. Přihlášení probíhá přes firemní SSO (Microsoft EntraID) – použij stejné přihlašovací údaje jako do ostatních firemních systémů. Samostatná registrace ani heslo nejsou potřeba.

Po přihlášení vidíš pouze modely a agenty, ke kterým máš přidělený přístup (dle AD skupin).

## Základní konverzace

1. V levém panelu vyber model nebo agenta
2. Napiš dotaz do textového pole a odešli Enterem nebo ikonou odeslání
3. Konverzace se automaticky ukládá do historie (viditelná pouze tobě)

### Tipy

- Buď konkrétní – čím přesnější otázka, tím lepší odpověď
- Pokud odpověď není správná, upřesni nebo přeformuluj dotaz
- Modely mohou chybovat – kritické informace vždy ověř v primárním zdroji

## Web search

Vybrané modely mají aktivován nástroj pro vyhledávání na webu. Agent jej použije automaticky, pokud to povaha dotazu vyžaduje. Zdroje použité při generování odpovědi jsou v odpovědi citovány.

## Práce s agentem domény

Agenti domén mají přístup k interním systémům banky. Přístup probíhá **jménem tvého přihlášeného účtu** – vidíš pouze data, ke kterým máš přístup v daném systému.

Agenta vyber ze seznamu v levém panelu. Každý agent je popsán – viz popis vedle jeho názvu.

> Pamatuj: agenti pracují s reálnými daty z interních systémů. Informace sdílej pouze v rozsahu nezbytném pro splnění pracovního úkolu.

## Osobní znalostní báze

Do OWUI můžeš nahrát vlastní dokumenty, na které se pak ptát.

1. Přejdi do sekce **Knowledge** (nebo **Znalostní báze**)
2. Nahraj dokument (PDF, DOCX, TXT a další)
3. Při konverzaci aktivuj znalostní bázi – model bude čerpat z nahraných dokumentů

Nahrané dokumenty jsou viditelné pouze tobě.

> Nenahrávej dokumenty klasifikované nad rámec tvého oprávnění pro daný systém.

## Osobní prompt šablony

Opakované typy dotazů si můžeš uložit jako šablonu:

1. Napiš prompt, který chceš uložit
2. Použij funkci **Save as prompt** (nebo ekvivalent v aktuální verzi OWUI)
3. Šablonu vyvoláš příkazem `/` v textovém poli

## PowerUser – Workspace

Pokud máš roli PowerUser, máš přístup k sekci **Workspace**, kde můžeš:

- vytvářet vlastní agenty s vlastním systémovým promptem
- psát vlastní Tools (Python funkce) pro rozšíření schopností agenta
- sdílet agenty se svým týmem (po schválení Adminem pro širší publikaci)

Více viz [`role-a-skupiny.md`](role-a-skupiny.md).

## FAQ

**V seznamu nevidím model nebo agenta, který bych potřeboval/a.**
Přístup je řízen členstvím v AD skupinách. Pokud máš oprávněný business důvod, požádej o přidání do příslušné skupiny přes **[ticketovací systém]** (vyžaduje schválení nadřízeného).

**Mohu vkládat do promptů citlivá data klientů / interní informace?**
Pouze v rozsahu vlastních oprávnění k daným datům a v souladu s firemním standardem datové klasifikace (`[doplnit odkaz na interní standard datové klasifikace]`). Nikdy nevkládej data nad rámec své oprávnění.

**Existují limity počtu dotazů?**
Ano, limity jsou nastaveny na úrovni LiteLLM. Při dosažení limitu se zobrazí chybová zpráva. V případě potřeby vyššího limitu kontaktuj platformový tým.

**Můj agent vrátil chybnou nebo podivnou odpověď. Co s tím?**
Nahlas to přes **[ticketovací systém]** s odkazem na konkrétní konverzaci. Kritická data vždy ověř v primárním systému.

**Mohu sdílet svého vlastního agenta s kolegou (PowerUser)?**
Sdílení agenta nebo Tool s dalšími uživateli vyžaduje schválení Adminem. Proces viz [`role-a-skupiny.md`](role-a-skupiny.md) a [`governance.md`](governance.md).

## Kde hlásit problémy

- Technické problémy a chyby: **[ticketovací systém]**
- Chybný nebo nebezpečný výstup agenta: **[ticketovací systém]** – kategorie _AI incident_
- Žádost o přístup k dalším modelům nebo doménám: **[ticketovací systém]**
- Žádost o povýšení na PowerUser: **[ticketovací systém]** (proces viz [`governance.md`](governance.md))
