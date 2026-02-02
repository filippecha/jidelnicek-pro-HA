# 🥗 Home Assistant Meal Planner & Shopping List

Komplexní řešení pro plánování jídelníčku v Home Assistant. Umožňuje plánovat jídla na 14 dní dopředu (lichý/sudý týden), hlídá duplicity a jedním kliknutím generuje nákupní seznam rozdělený do kategorií (Pečivo, Maso, Chlaďáky...), včetně sčítání surovin.

![Home Assistant Meal Planner](https://via.placeholder.com/800x400.png?text=Sem+vlozte+screenshot+vasi+karty)
*(Zde doporučuji vložit screenshot vaší karty)*

## ✨ Funkce
* **📅 14denní plánovač:** Automaticky rozlišuje lichý a sudý týden.
* **🛒 Chytrý košík:** Tlačítko "Do košíku" rozebere recept na suroviny a roztřídí je do správných seznamů (např. *Šunka* -> *Chlaďáky*).
* **🔢 Sčítání položek:** Pokud máte 2x jídlo s vejci, v seznamu se objeví "2x Vejce".
* **🚫 Detekce duplicit:** Upozorní zčervenáním, pokud si naplánujete stejné jídlo vícekrát v jedné kategorii.
* **📱 Responzivní:** Na PC zobrazí 4 dny vedle sebe, na mobilu dny pod sebou.
* **📖 Databáze receptů:** Integrovaná databáze surovin pro každé jídlo.

---

## 🛠 Požadavky

### 1. Frontend doplňky (HACS)
Pro správné zobrazení karet musíte mít nainstalované:
* [Auto Entities](https://github.com/thomasloven/lovelace-auto-entities)
* [Card Mod](https://github.com/thomasloven/lovelace-card-mod)
* [Mushroom Cards](https://github.com/piitaya/lovelace-mushroom) (volitelné, pro hezčí vzhled seznamů)

### 2. Nákupní seznamy (Local To-do)
Tento balíček vyžaduje integraci **Local To-do** (Místní seznam úkolů).

1. Jděte do **Nastavení** -> **Zařízení a služby**.
2. Klikněte na **Přidat integraci** a vyhledejte **Místní seznam úkolů** (Local To-do).
3. Vytvořte následující seznamy. **Důležité:** Pojmenujte je tak, aby jejich `entity_id` odpovídalo níže uvedenému (nebo si musíte upravit skript):

| Název seznamu (Doporučený) | Vyžadované Entity ID |
| :--- | :--- |
| Nákup - Pečivo | `todo.nakupni_seznam_pecivo` |
| Nákup - Ovoce a Zelenina | `todo.nakupni_seznam_ovoce_a_zelenina` |
| Nákup - Chlaďáky | `todo.nakupni_seznam_chladaky` |
| Nákup - Maso | `todo.nakupni_seznam_maso` |
| Nákup - Mražené | `todo.nakupni_seznam_mrazene` |
| Nákup - Nápoje | `todo.nakupni_seznam_napoje` |
| Nákup - Drogerie | `todo.nakupni_seznam_drogerie_a_domacnost` |
| Nákup - Ostatní | `todo.nakupni_seznam_ostatni` |

*(Tip: Pokud se ID vytvoří jinak, můžete ho přejmenovat v Nastavení -> Entity).*

---

## 🚀 Instalace

### Krok 1: Backend (Balíček)
1. Stáhněte soubor `package/meal_planner.yaml` z tohoto repozitáře.
2. Nahrajte ho do složky `/config/packages/` ve vašem Home Assistantovi.
   * *Pokud složku `packages` nemáte, vytvořte ji a do `configuration.yaml` přidejte:*
     ```yaml
     homeassistant:
       packages: !include_dir_named packages
     ```
3. **Restartujte** Home Assistant.

### Krok 2: Frontend (Karty)
1. Na vašem Dashboardu vytvořte novou kartu (vyberte "Manual").
2. Zkopírujte kód ze souboru `frontend/dashboard_card.yaml` a vložte jej tam.
3. (Volitelné) Pro zobrazení receptů vytvořte další kartu s kódem z `frontend/recipe_card.yaml`.

---

## 👨‍🍳 Jak přidat vlastní jídla?
Jídla a suroviny jsou definovány na dvou místech. Pro přidání nového receptu musíte upravit:

1. **V balíčku (`package/meal_planner.yaml`):**
   * V sekci `input_select` přidejte název jídla do seznamů (Snídaně/Oběd...).
   * V sekci `script` -> `variables` -> `recepty` definujte suroviny pro dané jídlo.

2. **V kartě receptů (`frontend/recipe_card.yaml`):**
   * Pokud používáte kartu pro nahlížení do receptů, musíte suroviny přidat i do šablony v této kartě.

---

## 💡 Tip na závěr
Automatizace v balíčku automaticky vymaže ("zresetuje") jídelníček pro aktuální den vždy ve 21:00, aby byl připraven čistý pro další cyklus (za 14 dní).
