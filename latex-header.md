# LaTeX Header
## General-purpose header for LaTeX

```latex
\documentclass[12pt]{article}
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage[urw-garamond]{mathdesign}
\usepackage[margin=1in]{geometry}
\pagenumbering{gobble}
```

Supports Unicode and much better than the lame default of Computer Modern
Roman, also omits page numbering (which is what I prefer. Here is additional
configuration I recommend if hyperlinks are going to be used:

```latex
\usepackage{hyperref}
\usepackage{xcolor}
\hypersetup{
    colorlinks,
    linkcolor={red!50!black},
    citecolor={blue!50!black},
    urlcolor={blue!80!black}
}
```
