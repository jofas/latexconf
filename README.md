# latexconf

My LaTeX configuration.

## Tikz to Standalone SVG

This setup is based on [this](https://tex.stackexchange.com/a/51766) answer 
from the TeX stackexchange.
Creating `svg` images from your `tikz` drawings requires some 
configuration. 
Assuming you have installed the dependencies from `install-deps.sh`,
you also need to set the right permissions for the conversion program,
which is `ImageMagick`.
For this you need to open the `policy.xml` file and change the following
policies:

```diff
- <policy domain="module" rights="none" pattern="{PS,PDF,XPS}" />
+ <policy domain="module" rights="read|write" pattern="{PS,PDF,XPS}" />
- <policy domain="coder" rights="write" pattern="PDF" />
+ <policy domain="coder" rights="read|write" pattern="PDF" />
```

This is taken from [this](https://stackoverflow.com/a/52863413/20665825)
Stack Overflow answer.

Once you have set up and configured the dependencies properly, you can
use this tamplate to draw your `tikz` picture:

```latex
\documentclass[tikz,convert={outfile=\jobname.svg}]{standalone}
\usetikzlibrary{
    arrows,
    arrows.meta,
    decorations,
    backgrounds,
    positioning,
    fit,
    petri,
    shadows,
    datavisualization.formats.functions,
    calc,
    shapes,
    shapes.multipart
}
\begin{document}
\begin{tikzpicture}
    % draw picture here
\end{tikzpicture}
\end{document}
```

and compile it with:

```
lualatex -shell-escape $FILE
```

Once I'm finished drawing I manually change the `width` and `height`
settings of the `svg` file to `100%`.
