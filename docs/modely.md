# Modely

## LiteLLM proxy

Všechny jazykové modely jsou dostupné výhradně přes **LiteLLM** – firemní LLM proxy. OWUI nekomunikuje s modely přímo. Přes LiteLLM jdou **všechna volání modelů**, včetně:

- volání iniciovaná uživatelem v základní konverzaci
- volání prováděná agenty business domén
- volání z Tools/Pipelines vytvořených v Workspace

LiteLLM zajišťuje:

- jednotný OpenAI-kompatibilní endpoint pro OWUI
- směrování požadavků na konkrétní modely
- centrální logování a monitoring využití
- správu API klíčů a limitů

## Řízení přístupu k modelům

Přístup k modelům je řízen členstvím v AD skupinách. Každá skupina opravňuje k použití jednoho nebo více modelů. Skupiny jsou mapovány přímo do OWUI.

```
AD skupina: OWUI-MODEL-<název>  →  zpřístupní model(y) <název> v OWUI
```

Uživatel vidí v OWUI pouze modely, ke kterým má přístup. Přidání/odebrání přístupu = změna členství v AD skupině (viz [`governance.md`](governance.md)).

## Katalog modelů

> Konkrétní modely, jejich parametry a doporučené použití budou doplněny po finalizaci dostupné nabídky přes LiteLLM.

| Model | AD skupina | Určení | Kontext |
|---|---|---|---|
| _[placeholder]_ | _[placeholder]_ | _[placeholder]_ | _[placeholder]_ |

### Kritéria pro zařazení modelu

Při zařazení nového modelu do nabídky se hodnotí:

- bezpečnostní schválení modelu (interní proces)
- dostupnost přes LiteLLM proxy
- vhodnost pro bankovní prostředí (citlivost dat, hallucination rate)
- náklady na provoz

Proces zařazení nového modelu viz [`governance.md`](governance.md).
