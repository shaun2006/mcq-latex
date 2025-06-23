# <img src="images/icons/icon.png" width="36" alt="latex Icon">  MCQ in LateX

### 📌 Description

This project is a LaTeX-based template for creating multiple-choice questions (MCQs). It includes a main compilation file, a settings file for customizing the question format, and example output in PDF form. Additionally, screenshots are provided for visual reference.

## 🔧 Pre-Requrements

1. any latex compiler
2. On windows you can use [MikTeX](https://miktex.org/)
3. On linux you can use [LateX](https://www.latex-project.org/get/)

## 🛠️ code for mcq settings    
you can copy and paste this code into a file called setting.tex and then input that file in your main.tex  
Example is shown below after this code
``` tex
\newbox\allanswers
\setbox\allanswers=\vbox{}

\newenvironment{answer}
{%
    \global\setbox\allanswers=\vbox\bgroup
    \unvbox\allanswers
}%
{%
    \bigbreak
    \egroup
}

\newcommand{\showallanswers}{\par\unvbox\allanswers}
% End answer

\newcommand*{\getanswer}[5]{%
    \ifthenelse{\equal{#5}{a}}
    {\begin{answer}\thequestion. (a)~#1\end{answer}}
    {\ifthenelse{\equal{#5}{b}}
        {\begin{answer}\thequestion. (b)~#2\end{answer}}
        {\ifthenelse{\equal{#5}{c}}
            {\begin{answer}\thequestion. (c)~#3\end{answer}}
            {\ifthenelse{\equal{#5}{d}}
                {\begin{answer}\thequestion. (d)~#4\end{answer}}
                {\begin{answer}\textbf{\thequestion. (#5)~Invalid answer choice.}\end{answer}}}}}
}

\setlength\parindent{0pt}
%usage \choice{ }{ }{ }{ }
%(A)(B)(C)(D)
\newcommand{\fourch}[5]{
    \par
    \begin{tabular}{*{4}{@{}p{0.23\textwidth}}}
        (a)~#1 & (b)~#2 & (c)~#3 & (d)~#4
    \end{tabular}
    \getanswer{#1}{#2}{#3}{#4}{#5}
}

%(A)(B)
%(C)(D)
\newcommand{\twoch}[5]{
    \par
    \begin{tabular}{*{2}{@{}p{0.46\textwidth}}}
        (a)~#1 & (b)~#2
    \end{tabular}
    \par
    \begin{tabular}{*{2}{@{}p{0.46\textwidth}}}
        (c)~#3 & (d)~#4
    \end{tabular}
    \getanswer{#1}{#2}{#3}{#4}{#5}
}

%(A)
%(B)
%(C)
%(D)
\newcommand{\onech}[5]{
    \par
    (a)~#1 \par (b)~#2 \par (c)~#3 \par (d)~#4
    \getanswer{#1}{#2}{#3}{#4}{#5}
}


\newlength\widthcha
\newlength\widthchb
\newlength\widthchc
\newlength\widthchd
\newlength\widthch
\newlength\tabmaxwidth

\setlength\tabmaxwidth{0.96\textwidth}
\newlength\fourthtabwidth
\setlength\fourthtabwidth{0.25\textwidth}
\newlength\halftabwidth
\setlength\halftabwidth{0.5\textwidth}

\newcommand{\choice}[5]{%
\settowidth\widthcha{AM.#1}\setlength{\widthch}{\widthcha}%
\settowidth\widthchb{BM.#2}%
\ifdim\widthch<\widthchb\relax\setlength{\widthch}{\widthchb}\fi%
    \settowidth\widthchb{CM.#3}%
\ifdim\widthch<\widthchb\relax\setlength{\widthch}{\widthchb}\fi%
    \settowidth\widthchb{DM.#4}%
\ifdim\widthch<\widthchb\relax\setlength{\widthch}{\widthchb}\fi%

% Allows for the \onech option.
\ifdim\widthch>\halftabwidth
    \onech{#1}{#2}{#3}{#4}{#5}
\else\ifdim\widthch<\halftabwidth
\ifdim\widthch>\fourthtabwidth
    \twoch{#1}{#2}{#3}{#4}{#5}
\else
    \fourch{#1}{#2}{#3}{#4}{#5}
\fi\fi\fi}
```

Here is how to include this code in your latex file  
Note:- 
1. Here latex refers to your working directory 
2. Here mcq-settings.tex refers to the file where the above code should be pasted.


```bash
cd latex-floder
tocuh mcq-settings.tex
gedit mcq-settings.tex
```


## 🛠️ code for main.tex
This is an example code for mcq typing in LateX

**Import points to remember**
1. **\input{mcq-setting.tex}** is the metod that allows you to add the mcq-seeting.tex file into your main latex file where you write/type all the mcq questions or other things.
2. mcq-setting.tex is the file name of my choice you can rename it to anything you want but remember to change the name also in \input{} field.
3. The below code is just for example purpose and the document settings are a4paper, Time New Roman font size:- 12pt. 

```latex
\documentclass[a4paper,12pt]{exam}  % paper is set to a4 and font size is set to 12pt
\usepackage{mathptmx} % set font family to time-new-roman

\input{mcq-setting.tex}


% The document starts here....
\begin{document}

\begin{flushleft}
Q1. \textbf{Multiple Choice questions}\hspace*{\fill} \textbf{(10 Points)}
\end{flushleft}

% mcq questions start here...
\begin{questions}
\question What is the capital city of Canada?
\choice{Toronto}{Vancouver}{Ottawa}{Montreal}{c}

\question Which planet is known as the Red Planet?
\choice{Jupiter}{Mars}{Venus}{Mercury}{b}

\question Who wrote the play Romeo and Juliet?
\choice{William Shakespeare}{Charles Dickens}{Jane Austen}{Leo Tolstoy}{a}

\question  What is the chemical symbol for gold?
\choice{Ag}{Go}{Gd}{Au}{d}

\question In computing, what does CPU stand for?
\choice{Central Process Unit}{Computer Processing Unit}{Central Processing Unit}{Core Processing Utility}{c}
\end{questions}

\newpage

% comment the line bellow for not to show answers
\showallanswers

\end{document}

```


## How to run main.tex
1. open terminal or cmd on linux or windows respectively depends on where you have saved your main.tex *in that floder (directory)*

2. you can compile **main.tex**  easly with below command if you have installed the latex compiler correctly.

```latex
pdflatex main.tex
```

3. A file called **main.pdf** will be created, if pdflatex compiled everything withou any erros. you can open main.pdf with and pdf reader

### 📸 Screenshots
Here are some screenshots of the example pdf

1. Pdf page 1
[![screenshort](https://github.com/shaun2006/mcq-latex/blob/main/images/image1.png?raw=true)](https://github.com/shaun2006/mcq-latex/blob/main/main.pdf)

2. Pdf page 2
[![screenshort](https://github.com/shaun2006/mcq-latex/blob/main/images/image2.png?raw=true)](https://github.com/shaun2006/mcq-latex/blob/main/main.pdf)

## 🧪 Clone and Build 

```bash
git clone https://github.com/shaun2006/mcq-latex.git
cd mcq-latex
pdflatex main.tex
```
## 📄 The pdf file
[📄 Click to View the PDF](https://github.com/shaun2006/mcq-latex/blob/main/main.pdf)

## 📂 Files Structure
``` bash
├── mcq-setting.tex # LaTeX definitions and macros for MCQ formatting
├── main.tex # Main LaTeX document that includes questions
├── main.pdf # Compiled output (viewable PDF)
├── screen-shorts/ # Folder containing example screenshots
│ ├── image1.png
│ └── image2.png
│ └── icons/
│   └── image1.png
```

