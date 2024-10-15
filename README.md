# EZTeX

**UPOZORNĚNÍ: Toto je work-in-progress, projekt se bude v budoucnu rozvíjet. Pravidelně aktualizujte svoji instalaci.**

EZTeX je šablonová nadstavba nad LuaLaTeX/BibLaTex pro tvorbu seminárních, maturitních a jiných prací. Jejím účelem je oddělení procesu tvorby dokumentu od jeho sazby, přičemž o sazbu a plnění tzpografických norem je postaráno automaticky.

Tento návod se věnuje stažení, nastavení a užívání EZTeX pro tvorbu dokumentů. Předpokládá se zde předem úspěšně nainstalovaná distribuce LaTeXu, např. [MikTeX](https://miktex.org/) nebo [TeX Live](https://www.tug.org/texlive/), a základní znalost systému TeX.

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
```
Všechny moduly jsou ve výchozím nastavení povoleny. Toto doporučujeme neměnit, pokud nevíte, co děláte. Každý modul je v souboru okomentovaný a vysvětlený.

## Užívání

Po provedení konfigurace je možné začít psát náš dokument. Otevřeme TeXWorks (či jiný editor pro LaTeX) a v něm soubor `obsah.tex`. Další postup už je shodný s normální tvorbou. Soubor má předpřipravenou strukturu.

Před kompilací se ujistíme, že máme jako kompilátor zvolený **LuaLaTeX** (V TeXWorks v levém rohu horní lišty.)

![Jak zvolit kompilátor](.github/texworks.png)

V následující sekci se dozvíte o zvláštnostech a specifikách EZTeXu a jakým způsobem řešit některé úkony.

## Jak na...

### Nadpisy

Většina nadpisů prvního řádu (jako je obsah, reference apod.), nejsou číslované, toto je proto zobecněno na všechny nadpisy prvního řádu (jako je úvod, praktická část apod.). EZTeX toto z technických důvodů řeší vlastním příkazem `\nsection{}`. Ten užívejte místo klasického `\section{}`

### Obrázky

Ujistěte se, že máte povolený modul `obrazky.tex`, pokud jste v minulosti měnili jejich nastavení.

Zmíněný modul poskytuje příkaz `\img[<vyska>]{<popisek>}{<soubor>}` pro pohodlné vkládání obrázků. Povinnými parametry jsou popisek a cesta, volitelně lze potom specifikovat výšku, tedy velikost.

Pokud se nám nelíbí, kam LuaLaTeX obrázek umisťuje, můžeme mu vnutit námi zvolenou pozici v textu pomocí alternativy `\img*`.

Na obrázky se lze v textu odkazovat přes název souboru pomocí `\ref{}`:
```tex
\img{Obrázek psa}{pes.png}

Jak je vidět na obrázku \ref{pes.png}, psi jsou roztomilá zvířata.
```
### Citace

EZTeX využívá systém BibLaTeX. Ten sprošťuje uživatele nutnosti formátovat citace ručně; místo toho si zavádíme jednotnou citační databázi, na kterou se v textu odkazujeme.

Před pokračováním se ujistíme, že máme povolený modul `citace.tex`, pokud jsme v minulosti měnili jejich nastavení.

Citační databázi nejlépe vytvoříme pomocí nějakého portálu ([Scribbr](https://scribbr.com)), popřípadě je lze vytvářet ručně. Po vytvoření klikneme na tři tečky v pravém horním rohu a vybereme **Export to LaTeX**. Ujistíme se, že stahovaná databáze je ve formátu **BibTeX** a ne **BibLaTeX**.

![Stažení citační databáze](.github/scribbr.png)

Soubor ukládáme jako `reference.bib` do adresáře se zbytkem dokumentu. Pokud tak neučiníme, další kroky nebudou fungovat.

Příkladem položky v databázi může být:

```bib
@book{darwin-1900,
	author = {Darwin, Charles},
	title = {{The origin of species, by Charles Darwin.}},
	year = {1900},
	doi = {10.5962/bhl.title.46292},
}
```

V textu se na tuto knihu budeme odkazovat jejím identifikátorem, což je vždy první položka (zde tedy `darwin-1990`). V textu se odkazujeme pomocí příkazu `\cite{<identifikator>}`. Pokud je po nás vyžadováno citování v poznámce pod čarou, použijeme místo toho `\footfullcite{}`
