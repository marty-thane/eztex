# EZTeX

**UPOZORNĚNÍ: Toto je work-in-progress, projekt se bude v budoucnu rozvíjet. Pravidelně aktualizujte svoji instalaci.**

EZTeX je šablonová nadstavba nad LuaLaTeX/BibLaTeX pro tvorbu seminárních, maturitních a jiných prací. Jejím účelem je oddělení procesu tvorby dokumentu od jeho sazby, přičemž o sazbu a plnění typografických norem je postaráno automaticky.

Tento návod se věnuje stažení, nastavení a užívání EZTeX pro tvorbu dokumentů. Předpokládá se zde předem úspěšně nainstalovaná distribuce LaTeXu, např. [MikTeX](https://miktex.org/) nebo [TeX Live](https://www.tug.org/texlive/), a základní znalost systému TeX.

## Stažení

EZTeX stáhneme kliknutím na tlačítko **Code** v horní části této stránky a poté **Download ZIP**. Archiv rozbalíme a přesuneme se do nově vzniklého adresáře.

![Jak stáhnout EZTeX](.github/download.png)

## Nastavení

Veškerá nastavení se provádí v souboru `nastaveni.tex`. Ten má dvě části: metadata a moduly.

Metadata nám dovolují specifikovat informace typu autor, název apod. V souboru je poznáme podle následujícího formátu:
```tex
\def\<klic>{%
<hodnota>
}
```
Přepsáním výchozích hodnot si dokument přizpůsobíme na míru. Některá metadata u sebe mají poznámku k jejich používání.

Druhou částí jsou moduly, což není nic jiného než kusy kódu, které do našeho dokumentu zavádí nějakou funkcionalitu. Příkladem může být podpora obrázků, microtyping... V souboru je poznáme podle tvaru:
```tex
\input{moduly/<nazev>}
```
Všechny moduly jsou ve výchozím nastavení povoleny. Toto doporučujeme neměnit, pokud nevíte, co děláte.

## Užívání

Po provedení konfigurace je možné začít psát náš dokument. Otevřeme [TeXworks](https://www.tug.org/texworks/) (či jiný editor) a v něm soubor `obsah.tex`. Další postup už je shodný s normální tvorbou v systému LaTeX.

Před kompilací se ujistíme, že máme jako kompilátor zvolený **LuaLaTeX** (V TeXworks v levém rohu horní lišty.)

![Jak zvolit kompilátor](.github/texworks.png)

V následující sekci se dozvíte o zvláštnostech a specifikách EZTeXu a jakým způsobem řešit některé úkony.

## Zvláštnosti

### Nadpisy

Nadpisy prvního řádu nejsou číslované. Toto je převzato z výchozího nastavení některých objektů (obsah, odkazy). Z technických důvodů má EZTeX svůj vlastní příkaz `\nsection{}`. Používejte ho místo klasického `\section{}`

### Obrázky

Ujistěte se, že máte povolený modul `obrazky.tex`. Ten poskytuje podporu pro grafiku a příkaz `\img` pro pohodlné vkládání obrázků. Povinnými parametry jsou popisek a cesta k souboru, volitelně lze potom specifikovat výšku, tedy velikost.
```tex
\img[<vyska>]{<popisek>}{<soubor>}
```

Pokud se nám nelíbí, kam LuaLaTeX obrázek umisťuje, můžeme mu vnutit námi zvolenou pozici v textu pomocí alternativy `\img*`.

Na obrázky se lze v textu odkazovat přes název souboru pomocí `\ref{}`:
```tex
\img{Obrázek psa}{pes.png}
Jak je vidět na obrázku \ref{pes.png},
psi jsou roztomilá zvířata.
```
### Citace

EZTeX využívá systém BibLaTeX. Ten sprošťuje uživatele nutnosti formátovat citace ručně; místo toho si zavádíme jednotnou citační databázi, na kterou se v textu odkazujeme. EZTeX při citování dodržuje normu [ČSN ISO 690](https://www.iso690.zcu.cz/).

Citační databázi vytvoříme pomocí webové služby [Scribbr](https://www.scribbr.com/citation/generator/). Po vytvoření klikneme na tři tečky v pravém horním rohu a vybereme **Export to LaTeX**. Ujistíme se, že stahovaná databáze je ve formátu **BibTeX** a ne **BibLaTeX**.

![Stažení citační databáze](.github/scribbr.png)

Soubor ukládáme jako `reference.bib` do adresáře se zbytkem dokumentu. Pokud tak neučiníme přesně, další kroky nebudou fungovat.

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
