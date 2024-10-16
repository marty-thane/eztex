# Citace

EZTeX využívá systém BibLaTeX. Ten sprošťuje uživatele nutnosti formátovat citace ručně; místo toho si zavádíme jednotnou citační databázi, na kterou se v textu odkazujeme. .

Citační databázi vytvoříme pomocí webové služby [Scribbr](https://www.scribbr.com/citation/generator/). Po vytvoření klikneme na tři tečky v pravém horním rohu a vybereme **Export to LaTeX**. Ujistíme se, že stahovaná databáze je ve formátu **BibTeX** a ne **BibLaTeX**.

![Stažení citační databáze](../.screenshots/scribbr.png)

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

Pokud chceme kompilovat s referencemi, musíme zvolit posloupnost LuaLatex -> BibTeX -> LuaLatex -> LuaLatex (v nabídce překladačů). Překládat dokument čtyřikrát je krkolomné, toto proto neděláme tak často.
