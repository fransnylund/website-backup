# Introduction to Latex

Latex is a program for writing articles, books, documents, presentations and more. You have probably used Microsoft Word, which is a very popular word processor where you can write articles and books. Latex is very different in the way it makes and formats text, but both Latex and Word share the same purpose: To make formatted, nice text. Latex is common in academia and scientific documents, and is great for writing math and physics equations and symbols, for example. Latex is free and open-source software and is available on a host of different platforms. Latex is extremely customizable and you can do a lot with it, but it does have a somewhat high learning curve compared to something like Word.

Latex does offer some benefits over Microsoft Word:

- Free(both as in freedom and price)
- Support for a host of math symbols and older languages.
- Labels and references.
- Easily convertable to different formats.
- You can use any editor you want.

Start by installing Latex. If you are on Linux, just install it with your package manager. If you are on Windows or Mac ...
The good thing with Latex is that you can use any editor you want. I use vim, for example. It works fine for me.


## The Preamble

![The picture](./img/preamble-env.png)

Every Latex document is divided into two main parts. The top part is where you're going to specify what document you are going to write, what packages to include and more. This section is called preamble.

To specify what type of document you're going to use, use the `\documentclass` command. These are the most common ones:

For articles:

`\documentclass{article}`

For books:

`\documentclass{book}`

For presentations:

`\documentclass[beamer]`


What are packages then? Packages include extra functionality and commands that you can use in Latex, these allow you to get huge fonts, embed pictures and use math symbols and more.

For example, to adjust the margins of your document, include the geometry package:

`\usepackage{geometry}`

To use bigger fonts than 10pt, 11pt or 12pt, include the extsizes package:

`\usepackage{extsizes}`

To embed graphics, like pictures, include the graphicx package:

`\usepackage{graphicx}`

I will have a small list of packages and their uses in the end of this tutorial.


## Document Environment

Remember when I said that Latex documents are divided into two parts? This is the second part, the meat of the document. The document environment is the part where you type the actual text. It starts with `\begin{document}` and ends with `\end{document}`

`\begin{document}
  Hello, world!
  This is some text.
\end{document}`

![](./img/environment.png) \
![](./img/environment2.png)

## Arguments

`\documentclass[]{}`

In Latex, the required arguments go inside the {  } while optional arguments go into [].

For example, you can set the font size of the document by giving the documentclass an argument in the square brackets:

`\documentclass[12pt]{}`



## Fonts

![](./img/font-sizes.png)


The default font size in Latex is 10pt. If you wish to have larger font sizes than 12pt, you have to include the extsizes package.

There are premade font sizes like `\tiny \large \Large \LARGE \huge` and `\Huge`.

Hello big, beautiful, `{\Large large}` world.


### Font families

![](./img/font-family2.png) \
![](./img/font-family.png) 

The three basic font families are Roman text, Sans serif text and typewriter text. The default is Roman.

`\textrm{Default (Roman) text}
\textsf{Sans serif text}
\texttt{Typewriter text}`

You can switch your whole document to one of these with the following command:

![](./img/serif.png) \
![](./img/serif2.png)

Changes your whole document to a serif font
`\renewcommand{\familydefault}{\rmdefault}`

As you can see, the Roman looks like what we had before. That's because it is the default.

Changes your whole document to a sans serif font
`\renewcommand{\familydefault}{\sfdefault}`

Changes your whole document to a typewriter(monospace) font
`\renewcommand{\familydefault}{\ttdefault}`


Typewriter(monospace) text is text where every letter has the same width.


### Changing the font typeface

This can be done by first including a package that includes the font and then choosing between the serif, sans serif or monospace.

This changes the typeface of the entire document to Helvetica:

`\usepackage{helvet}
\renewcommand{\familydefault}{\sfdefault}`


![](.img/helvet.png) \
![](.img/helvet2.png)



### Font styles

Normal text

`\textbf{I'm bold!}`

`\textit{I'm italicized!}`

`\underline{I'm underlined!}`


You can also use more than one modifier at the same time like so:

`\textbf{\textit{I'm bold and italicized!}}`
`\textbf{\underline{I'm bold and underlined!}}`


Make sure you close the curly brackets, otherwise Latex will go crazy and refuse to compile.


The \emph is used to add emphasis to a word or phrase. It will look different depending on the situation you use it in, but usually it looks similar to italics.

`\emph{I'm emphasized}`


![](./img/font-style5.png) \
![](./img/font-style6.png)


You can also use strike through text by including the ulem package:

`\usepackage{ulem}
\sout{I'm strikethrough text!}`


## Changing the sections, chapters and more

You can change how the sections or chapters look like with the titlesec package.

`\usepackage{titlesec}`

The titlesec package includes a couple of useful things, such as `\titleformat`.


`\titleformat{\section}{\huge\bfseries}{\thesection}{1em}{\vspace{2em}}`

The first argument takes what you want to format. I've chosen \section in this case. The next argument takes the actual formatting. I've made the font size huge and bold. You can leave out the 3rd and last argument. The {1em}(or whatever size you want) has to be there. It specifies the space between the section number and the section name.

![](./img/titlesec.png) \
![](./img/titlesec2.png) \
![](./img/titlesec3.png) \
![](./img/titlesec4.png) \
![](./img/titlesec5.png)

## Line spacing

You can add both vertical and horizontal spacing between any text.

This will put some space between the "Hello world!" and "Some random text":

`
Hello world!

\vspace{3em}

Some random text.
`

![](./img/line-spacing.png) \
![](./img/line-spacing2.png) \
![](./img/line-spacing3.png) \
![](./img/line-spacing4.png) \
![](./img/line-spacing5.png) \
![](./img/line-spacing6.png) \
![](./img/line-spacing7.png) \



## Line breaks

Using \\ will make a newline.


Another way of making a newline is by putting two newlines:

Hello

World

![](./img/newline3.png) \
![](./img/newline4.png) \
![](./img/newline6.png) 


## Alignment

You can have left justified, centered, or right justified text in Latex.

`\begin{flushleft}`
Left justified text here.
`\end{flushleft}`

`\begin{center}`
Centered text here.
`\end{center}`

`\begin{flushright}`
Right justified text here.
`\end{flushright}`


![](./img/alignment.png) \
![](./img/alignment2.png) \
![](./img/alignment4.png) \
![](./img/alignment5.png) \
![](./img/alignment6.png) \
![](./img/alignment7.png) 


Don't ask me why it's named "flushleft" and "flushright". I have no idea.



## Indentation

Latex will by default indent every line that starts a new paragraph.

You can change the default behaviour by issuing a `\noindent` before the text.

![](./img/no-indent.png) \
![](./img/no-indent2.png) \
![](./img/no-indent3.png) \

## Tables


Tables can be made by using the tabular environment

`\begin{tabular}{alignment}
  The body of the table.
\end{tabular}`

![](./img/tables.png) \
![](./img/tables2.png)

## Paper size

The two common sizes are A4 and letter size paper. You can also make your own paper size.

You can set which paper size you want in the `\documemntclass` command. 
`\documentclass[ option ]{article}`

You can also make your own paper sizes by giving a couple of arguments when including the geometry package:

`\usepackage[paperwidth=, paperheight= ]{geometry}`

![](./img/paper-sizes.png) \
![](./img/paper-sizes2.png)

## Margins

Just like you can specify what paper size you want, you can specify the margin that you wish to have. There are two ways of doing this:

`\usepackage[margin=size]{geometry}`

Or:

`\usepackage[top=size, bottom=size, left=size, right=size]{geometry}`

![](./img/margins.png) \
![](./img/margins2.png) \
![](./img/margins3.png) \
![](./img/margins4.png) \

## Landscape

In order to change the layout of your document to landscape, you have to include the geometry package and give it the argument "landscape".

`\usepackage[landscape]{geometry}`

`\begin{landscape}
  This should be landscape!
\end{landscape}`

If you are using pdflatex, you have to include the pdflscape instead:

`\usepackage{pdflscape}`


![](./img/landscape.png) \
![](./img/landscape2.png)


## Custom commands

You can create your own custom commands in Latex by using the `\newcommand` command. This is powerful and saves you a ton of typing.

`\newcommand{\nameofcommand}{whattoexecute}`

`\newcommand{\fin}{Finland}`

![](./img/custom-cmds2.png) \
![](./img/custom-cmds.png) 

Make writing bold easier:

`\newcommand{\bo}{\textbf}`

Now you don't have to type \textbf everytime you want bolded text.

![](./img/custom-cmds4.png) \
![](./img/custom-cmds3.png) \


You can also redfine a command in Latex by using `\renewcommand`:

`\renewcommand{\nameofcommand}{whattoexecute}`


![](./img/renewcommand.png) \
![](./img/renewcommand2.png)


## Environments

`\begin{environment}
...
\end{environment}`

We've already talked about the Document Environment, but there are other environments that you can use. An environment just a section that does something with the text.
For example, this environment centers stuff.

`\begin{center} 
...
\end{center}`

![](./img/environment.png) \
![](./img/environment2.png)

A table can be made with the tabular environment:

`\begin{tabular}
...
\end{tabular}`


We've also talked about the flushleft and flushright environments.


## Lists

There are two types of lists in Latex: Unordered and ordered.

To create an unordered list, use the `\begin{itemize}` command:

`\begin{itemize}
\item First item
\item Second Item
\item Third Item
\begin{itemize}
\item First sub-item
\item Secon sub-item
\end{itemize}
\end{itemize}`

![](./img/unorderedlist2.png) \
![](./img/unorderedlist.png)

To create a ordered list, use the `\begin{enumerate}` command:

`\begin{enumerate}
\item First Item
\item Second Item
\begin{enumerate}
\item First Sub-item
\item Second Sub-item
\end{enumerate}
\end{enumerate}`

![](./img/orderedlist2.png) \
![](./img/orderedlist.png)


In the unordered lists, you can specify what kind of list marker you want by giving an argument to the `\item` command, like so:

`\item[$\rightarrow$]`

![](./img/unorderedlist3.png) \
![](./img/unorderedlist4.png)


## Creating a ruler 

`\rule{5pt}{0.75pt}` can be used to create a horizontal ruler. The first argument takes the width of the rule, while the second argument takes the thickness of the ruler.

![](./img/ruler.png) \
![](./img/ruler2.png) \
![](./img/ruler3.png) \
![](./img/ruler4.png)

## Images

Images can be embedded into Latex by including the graphicx package and using the `\includegraphics` command:

`\usepackage{graphicx}`

`\includegraphics{mypicture.png}`

`\includegraphics[width=10cm, height=5cm]{mypicture.png}`

![](./img/image.png) \
![](./img/image2.png)

If you want to center the image, move the `\includegraphics` command inside a `\begin{center}` and `\end{center}` environment.


## Titles

Latex uses the following three commands to make a title, though only the first two are required. 

Note: The date is optional. Latex will automatically put the date in your title.

`\title{The best document on the planet}

\author{Frans}

\date{January 1}`

![](./img/title.png) \
![](./img/title2.png)

In order to tell Latex to make the title, use the `\maketitle` command. Latex will then make a title based on the three commands that we gave(`\title`, `\author` and `\date`).


## Sections

`\section{Section}
\subsection{Subsection}
\subsubsection{Subsubsection}`

![](./img/sections.png) \
![](./img/sections2.png)

The nice thing about Latex is that it will automatically number the section headings for you. You can of course remove the numbering if you prefer to roll without a numbering heading thingy?


## Table of Contents

Table of Contents, or ToC for short, can be done by typing:

`\tableofcontents`

This will create a table of contents. You might have to compile the document twice or thrice in order for it to completely work. Latex has to first compile and count how many chapters you have, and then the second time, it'll complete the toc.

![](./img/toc.png) \
![](./img/toc2.png)

## Labels and References

This is super handy in Latex. Let's say you are referring to a section in your book, and suddenly you make a new section before it. Well, if you referred to the section as Section 4, it is now Section 5. Labels and references solve this nuisance.

"Skills are talked about in Section \ref{skills}."

`\section{Skills\label{skills}}`

Now the `\ref{skills}` will get substituted by whatever section number `\section{Skills}` happen to have, even if it changes.

![](./img/refs.png) \
![](./img/refs2.png) \
![](./img/refs3.png) \
![](./img/refs4.png)

Note: You have to compile your document twice in order for this to work. Latex won't know what \ref{skills} refers to the fist time it compiles, it only knows that the second time it compiles the document.


## Links

More specifically, hyperlinks.

To create hyperlinks, include the hyperref package. This will turn the table of contents into a series of hyperlinks. Also, all the `\ref{}` in the document will get turned into hyperlinks.

`\hyperref[ label ]{ Link text }` can be used to create custom links with custom text.

`\ref*{}` can be used to make a ref and avoid it becoming a link.

The hyperref package also includes a `\href{ url }{text}` command to link to website on the internet.

![](./img/links.png) \
![](./img/links2.png) \
![](./img/links3.png)


## Comments

Comments in Latex are done by using the % sign, like so:

`\begin{center} % Everything in this section will be centered.`

![](./img/comments.png) \
![](./img/comments2.png)

## Packages

There are also other font sizes included in extsizes and anyfontsize packages in case you aren't happy with the default.


You can also use strike through text by including the ulem package:


There are also more packages for creating tables like tabularx, etc.


In order to further customize the lists, you can make use of the enumitem package.


If you wish to customize your table of contents, use the tocloft package.

amsmath for math.

`\usepackage{lastpage}` can be used to get the total number of pages.


## Final word

To wrap it all up, I'll share a couple of tips and tricks that might help you when using Latex.







## The "the" commands

The `\thepage` is used to print the current page number wherever you use it.

`\thesection`

`\thechapter`

`\theauthor`

For `\theauthor` to work, you have to include the titling package.

![](./img/the.png) \
![](./img/the.png) \
![](./img/the.png)


## Page breaks

`\pagebreak`

`\newpage`


- `{\LaTeX}` This writes Latex in the "cool" way.
- Always use {  } when formatting words or sentences. E.g. Hello \textbf{beautiful} world. It is used as a separator to avoid formatting errors like missing whitespace and such.
- Escaping a backslash can be done with `\textbackslash`. Because \\ makes a new line, you can't use it to escape the backslash.
