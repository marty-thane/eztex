# EZTeX

EZTeX je šablonová nadstavba nad LuaLaTeX/BibLaTex pro tvorbu seminárních, maturitních a jiných prací. Jejím účelem je oddělení procesu tvorby dokumentu od jeho sazby, přičemž o sazbu a plnění tzpografických norem je postaráno automaticky.

Tento návod se věnuje stažení, nastavení a užívání EZTeX pro tvorbu dokumentů. Předpokládá se zde předem úspěšně nainstalovaná distribuce LaTeXu, např. [MikTeX]() nebo [TeX Live](), a základní znalost systému TeX.

## Stažení

EZTeX stáhneme kliknutím na tlačítko **Code** v horní části stránky a poté **Download ZIP**. Archiv rozbalíme na svém zařízení a přesuneme se do nově vzniklého adresáře.

![Jak stáhnout EZTeX](.github/download.png)

## Konfigurace

Veškeré nastavení se provádí v souboru `nastaveni.tex`, který nyní otevřeme. Soubor má dvě části: metadata a moduly.

Metadata nám dovolují specifikovat informace typu autor, název... V souboru je nalezneme v následujícím formátu:
```tex
\def\<klic>{%
    <hodnota>
}
```
Přepsáním výchozích hodnot si dokument přizpůsobíme na míru. Některá metadata u sebe mají poznámku k jejich používání; ty doporučujeme nejdříve přečíst.

Druhou částí jsou moduly, což není nic jiného než kusy kódu, které do našeho dokumentu zavádí nějakou funkcionalitu, např. podporu pro obrázky. microtyping... V souboru je poznáme podle tvaru:
```tex
\input{moduly/<nazev>}
}
```
Všechny moduly jsou ve výchozím nastavení povoleny. Toto doporučujeme neměnit, pokud nevíte, co děláte. Každý modul je v souboru okomentovaný a vysvětlený.
