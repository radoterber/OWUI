# Návod pro uživatele

## Přihlášení

OWUI je dostupné na **[URL – doplnit]**. Přihlášení probíhá přes firemní SSO (Microsoft EntraID) – použijte stejné přihlašovací údaje jako do ostatních firemních systémů. Samostatná registrace ani heslo nejsou potřeba.

Po přihlášení vidíte pouze modely a agenty, ke kterým máte přidělený přístup (dle AD skupin).

## Základní konverzace

1. V levém panelu vyberte model nebo agenta
2. Napište dotaz do textového pole a odešlete Enterem nebo ikonou odeslání
3. Konverzace se automaticky ukládá do historie (viditelná pouze vám)

### Tipy

- Buďte konkrétní – čím přesnější otázka, tím lepší odpověď
- Pokud odpověď není správná, upřesněte nebo přeformulujte dotaz
- Modely mohou chybovat – kritické informace vždy ověřte v primárním zdroji

## Web search

Vybrané modely mají aktivován nástroj pro vyhledávání na webu. Agent jej použije automaticky, pokud to povaha dotazu vyžaduje. Zdroje použité při generování odpovědi jsou v odpovědi citovány.

## Práce s agentem domény

Agenti domén mají přístup k interním systémům banky. Přístup probíhá **jménem vašeho přihlášeného účtu** – vidíte pouze data, ke kterým máte přístup v daném systému.

Agenta vyberte ze seznamu v levém panelu. Každý agent je popsán – viz popis vedle jeho názvu.

> Pamatujte: agenti pracují s reálnými daty z interních systémů. Informace sdílejte pouze v rozsahu nezbytném pro splnění pracovního úkolu.

## Osobní znalostní báze

Do OWUI můžete nahrát vlastní dokumenty, na které se pak ptát.

1. Přejděte do sekce **Knowledge** (nebo **Znalostní báze**)
2. Nahrajte dokument (PDF, DOCX, TXT a další)
3. Při konverzaci aktivujte znalostní bázi – model bude čerpat z nahraných dokumentů

Nahrané dokumenty jsou viditelné pouze vám.

> Nenahrávejte dokumenty klasifikované nad rámec vašeho oprávnění pro daný systém.

## Osobní prompt šablony

Opakované typy dotazů si můžete uložit jako šablonu:

1. Napište prompt, který chcete uložit
2. Použijte funkci **Save as prompt** (nebo ekvivalent v aktuální verzi OWUI)
3. Šablonu vyvoláte příkazem `/` v textovém poli

## PowerUser – Workspace

Pokud máte roli PowerUser, máte přístup k sekci **Workspace**, kde můžete:

- vytvářet vlastní agenty s vlastním systémovým promptem
- psát vlastní Tools (Python funkce) pro rozšíření schopností agenta
- sdílet agenty se svým týmem (po schválení Adminem pro širší publikaci)

Více viz [`role-a-skupiny.md`](role-a-skupiny.md).

## FAQ

**V seznamu nevidím model nebo agenta, který bych potřeboval/a.**
Přístup je řízen členstvím v AD skupinách. Pokud máte oprávněný business důvod, požádejte o přidání do příslušné skupiny přes **[ticketovací systém]** (vyžaduje schválení nadřízeného).

**Mohu vkládat do promptů citlivá data klientů / interní informace?**
Pouze v rozsahu vlastních oprávnění k daným datům a v souladu s firemním standardem datové klasifikace (`[doplnit odkaz na interní standard datové klasifikace]`). Nikdy nevkládejte data nad rámec svého oprávnění.

**Existují limity počtu dotazů?**
Ano, limity jsou nastaveny na úrovni LiteLLM. Při dosažení limitu se zobrazí chybová zpráva. V případě potřeby vyššího limitu kontaktujte platformový tým.

**Můj agent vrátil chybnou nebo podivnou odpověď. Co s tím?**
Nahlaste to přes **[ticketovací systém]** s odkazem na konkrétní konverzaci. Kritická data vždy ověřte v primárním systému.

**Mohu sdílet svého vlastního agenta s kolegou (PowerUser)?**
Sdílení agenta nebo Tool s dalšími uživateli vyžaduje schválení Adminem. Proces viz [`role-a-skupiny.md`](role-a-skupiny.md) a [`governance.md`](governance.md).

## Kde hlásit problémy

- Technické problémy a chyby: **[ticketovací systém]**
- Chybný nebo nebezpečný výstup agenta: **[ticketovací systém]** – kategorie _AI incident_
- Žádost o přístup k dalším modelům nebo doménám: **[ticketovací systém]**
- Žádost o povýšení na PowerUser: **[ticketovací systém]** (proces viz [`governance.md`](governance.md))
