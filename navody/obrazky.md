# Obrázky

Ujistěte se, že máte povolený modul `moduly/obrazky.tex`.

Zmíněný modul poskytuje podporu pro grafiku a příkaz `\img`, kterým lze obrázky vkládat. Povinnými parametry jsou popisek a cesta k souboru, volitelně lze potom specifikovat výšku, resp. velikost.
```tex
\img[<vyska>]{<popisek>}{<soubor>}
```

Pokud se nám nelíbí, kam LaTeX obrázek umisťuje, můžeme mu vnutit námi zvolenou pozici v textu pomocí alternativního příkazu `\img*` (s hvězdičkou).

Na obrázky se v zásadě odkazujeme ne podle jejich pozice (viz obr. výše), ale podle čísla (viz obr. 1). To se dělá pomocí příkazu `\ref`. Identifikátor obrázku je shodný s jeho souborovým názvem. Příklad:
```tex
\img{Obrázek psa}{pes.png}
Jak je vidět na obrázku \ref{pes.png},
psi jsou roztomilá zvířata.
```
