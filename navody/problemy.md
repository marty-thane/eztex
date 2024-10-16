# Nejčastější problémy

## Package fontspec Error: The font "Tex Gyre Termes" cannot be found

Tato chyba znamená, že není nainstalován font, který EZTeX používá jako výchozí. Máte tři možnosti:

- Doinstalovat font pomocí správce balíků poskytnutého vaší distribucí.
- Otevřít soubor `moduly/pismo.tex` a nahradit nenalezený font jiným, nejlépe Times New Roman:
```tex
\setmainfont{Times New Roman}
```
- Zakomentovat v `moduly.tex` řádek `\input{moduly/pismo.tex}`. Překladač se vrátí k výchozímu fontu.

## ! Undefined control sequence. l.1 \documentclass [12pt,a4paper,oneside]{article}

Ujistěte se, že máte zvolený správný překladač. EZTeX potřebuje **LuaLaTeX**

## Jsem žena, ale na titulní stránce se mi vytiskává "Vypracoval:"

V souboru `sablona.tex` najděte problematický řádek (pomocí nástroje hledej a nahraď) a nahraďte jej podle potřeby.
