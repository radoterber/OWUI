# Role a skupiny

## OWUI role

OWUI rozlišuje tři uživatelské role. Role je přiřazena Adminem při zřízení účtu (nebo automaticky při prvním přihlášení přes SSO dle výchozího nastavení).

### User

Standardní přístup k platformě.

- Konverzace s modely a agenty (dle přidělených AD skupin)
- Osobní znalostní báze (nahrávání dokumentů pro vlastní použití)
- Osobní prompt šablony
- Historie konverzací

### PowerUser

Rozšířený přístup pro tvorbu a experimentování.

Vše co User, plus:

- **Workspace** – přístup k pokročilému rozhraní pro tvorbu agentů
- Tvorba vlastních **Tools (Python funkce)** a **Pipelines** pro osobní použití
- Pokročilá konfigurace agentů (systémový prompt, parametry modelu) pro osobní použití
- Možnost požádat o publikaci agenta nebo Tool pro další uživatele

> **Pravidlo sdílení:**
> Vlastní agenti, Tools a Pipelines vytvořené PowerUserem jsou ve výchozím stavu **dostupné pouze jejich autorovi**. **Jakékoliv sdílení s dalšími uživateli vyžaduje review a schválení Adminem** (proces viz [`governance.md`](governance.md)). Toto pravidlo platí stejně pro sdílení v rámci úzkého týmu i pro publikaci v rámci organizace.

### Admin

Plný přístup k platformě.

Vše co PowerUser, plus:

- Správa uživatelů – přiřazení rolí, zakládání účtů
- Konfigurace připojení k LiteLLM a modelům
- Správa AD skupin v OWUI (mapování skupin na modely a domény)
- Publikace agentů a Tools vytvořených PowerUsery
- Přístup k auditním logům a statistikám využití
- Konfigurace bezpečnostních politik (povolené modely, limity)

## AD skupiny – dvě dimenze

Přístup k funkcím platformy je řízen **dvěma nezávislými dimenzemi** AD skupin. Uživatel může být členem libovolného počtu skupin v obou dimenzích.

### Dimenze 1: Přístup k modelům

Členství v těchto skupinách zpřístupňuje konkrétní modely v OWUI.

| AD skupina | Zpřístupněné modely |
|---|---|
| `OWUI-MODEL-<název>` | _[placeholder – doplnit dle katalogu modelů]_ |

### Dimenze 2: Přístup k agentům business domén

Členství v těchto skupinách zpřístupňuje agenty příslušné business domény.

| AD skupina | Business doména | Agenti |
|---|---|---|
| `OWUI-DOMAIN-HR` | HR | Agenti pro HR agendu |
| `OWUI-DOMAIN-BANKERI` | Bankéři | Agenti pro bankovní poradce |
| `OWUI-DOMAIN-TRADING` | Trading | Agenti pro trading |
| `OWUI-DOMAIN-PROVOZ` | Provoz | Agenti pro provozní agendu |
| `OWUI-DOMAIN-IT` | IT | Agenti pro IT |

> Pojmenování AD skupin je návrh – finální názvy budou upřesněny ve spolupráci s týmem IAM.

## Matice oprávnění

| Funkce | User | PowerUser | Admin |
|---|:---:|:---:|:---:|
| Konverzace s modely a agenty | ✓ | ✓ | ✓ |
| Osobní znalostní báze | ✓ | ✓ | ✓ |
| Osobní prompt šablony | ✓ | ✓ | ✓ |
| Workspace (tvorba agentů pro osobní použití) | – | ✓ | ✓ |
| Tvorba vlastních Tools/Pipelines (osobní) | – | ✓ | ✓ |
| Žádost o sdílení agenta/Tool s dalšími uživateli | – | ✓ | ✓ |
| Schválení a publikace sdíleného agenta/Tool | – | – | ✓ |
| Správa uživatelů a rolí | – | – | ✓ |
| Správa AD skupin v OWUI | – | – | ✓ |
| Konfigurace modelů / LiteLLM | – | – | ✓ |
| Auditní logy | – | – | ✓ |

> Veškeré sdílení agenta nebo Tool s dalšími uživateli (i v rámci úzkého týmu) prochází review Adminem.
