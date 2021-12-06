---
layout: post
title: "How to add nomenclature in research article using Latex"
categories: Latex
tag: 
  - Latex
---

In a researchers life it is very important to have an efficient tool for article writing. We use Latex for the same. Latex is used for the production of high quality technical and scientific documentation.

But this time I had to add nomenclature for my article and I was facing difficulty to do the same in sublime text editor. So I searched for an alternative and found TeXmaker as a solution to my problem.  

I am documenting the step by step procedure I have used :

- Use the following packages in the preamble section of the Latex document. 

```latex
\usepackage{framed} % Framing content

\usepackage{multicol} % Multiple columns environment

\usepackage{nomencl} % Nomenclature package

\makenomenclature

\renewcommand*\nompreamble{\begin{multicols}{2}}

\renewcommand*\nompostamble{\end{multicols}}

```

-    Add the following lines in the body of the latex document. 

```latex
\begin{framed}
    \nomenclature{$\partial \Gamma_D$}{Dirichlet boundaries}
    \nomenclature{$\stresst$}{stress tensor}
    \nomenclature{$\disp(x)$}{displacement field}
    \nomenclature{$\alpha$}{multiplication factor}
    \nomenclature{\mbox{}}{}
    \printnomenclature
\end{framed}
```

- Next step is to Go to 

  ​						texmaker --- Preferences --- Commands --- Latexmk 

  ​	Then copy paste this command 

  ```latex
  "latexmk" -e "$pdflatex=q/pdflatex -synctex=1 -interaction=nonstopmode/" -pdf %.tex ; makeindex name.nlo -s nomencl.ist -o name.nls 
  ```

-  Next step is to Go to 

  ​						Tools --- open Terminal

  And run 

  ```latex
   makeindex name.nlo -s nomencl.ist -o name.nls 
  ```

- Last step is to build the pdf. Go to Quick Build. 

  

  That's it friends you are goood to go now. 

  All the best :)

  ​		

