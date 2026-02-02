# 🥗 Home Assistant - Pokročilý Jídelníček & Nákupní seznam

Komplexní "balíček" (package) pro plánování jídel v Home Assistant. Umožňuje plánovat jídla na 14 dní dopředu (lichý/sudý týden), kontrolovat duplicity a jedním kliknutím generovat nákupní seznam rozdělený do kategorií (Pečivo, Maso, Chlaďáky...).

## ✨ Funkce
* **14denní plánování:** Automaticky rozlišuje lichý a sudý týden.
* **Chytrý nákupní košík:** Tlačítko "Do košíku" vezme recept z daného dne a rozháže suroviny do příslušných To-Do seznamů (např. Šunka -> Chlaďáky, Chléb -> Pečivo).
* **Sčítání položek:** Pokud přidáte 2x jídlo s vejci, v seznamu bude "2x Vejce".
* **Detekce duplicit:** Pokud si naplánujete stejný oběd v pondělí i úterý, karta zčervená.
* **Responzivní design:** Na PC zobrazí 4 dny vedle sebe, na mobilu dny pod sebou.

## 🛠 Požadavky

### 1. Frontend doplňky (HACS)
Pro správné zobrazení karet musíte mít nainstalováno:
* [Auto Entities](https://github.com/thomasloven/lovelace-auto-entities)
* [Card Mod](https://github.com/thomasloven/lovelace-card-mod)

### 2. To-Do Seznamy (Nákupní seznamy)
V Home Assistantu (v sekci *To-do list*) si vytvořte následující seznamy. Musí mít přesně tato `entity_id`:

* `todo.nakupni_seznam_pecivo` (Pečivo)
* `todo.nakupni_seznam_ovoce_a_zelenina` (Ovoce a Zelenina)
* `todo.nakupni_seznam_chladaky` (Mléčné výrobky, uzeniny, vejce)
* `todo.nakupni_seznam_maso` (Maso a ryby)
* `todo.nakupni_seznam_mrazene` (Mražené)
* `todo.nakupni_seznam_napoje` (Nápoje)
* `todo.nakupni_seznam_drogerie_a_domacnost` (Drogerie)
* `todo.nakupni_seznam_ostatni` (Trvanlivé a ostatní)

## 🚀 Instalace

1.  Stáhněte soubor `package/meal_planner.yaml`.
2.  Nahrajte ho do složky `/config/packages/` ve vašem HA.
    * *Pokud složku nemáte, vytvořte ji a do `configuration.yaml` přidejte:*
      ```yaml
      homeassistant:
        packages: !include_dir_named packages
      ```
3.  Restartujte Home Assistant.
4.  Vytvořte novou kartu na dashboardu a zkopírujte do ní kód z `frontend/dashboard_card.yaml`.

## 👨‍🍳 Jak přidat vlastní recepty?
Recepty jsou definovány na dvou místech (musíte upravit obě, aby to fungovalo):
1.  **V balíčku (`meal_planner.yaml`):** V sekci `script` -> `variables` -> `recepty`. Zde se definuje, co se má přidat do košíku.
2.  **V kartě (`dashboard_card.yaml`):** Pokud používáte zobrazení receptů na dashboardu.
