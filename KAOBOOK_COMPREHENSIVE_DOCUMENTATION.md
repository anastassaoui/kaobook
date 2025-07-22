# KaoBook Template: Complete Documentation Guide

## Table of Contents
1. [Introduction](#introduction)
2. [Installation and Setup](#installation-and-setup)
3. [Basic Usage](#basic-usage)
4. [Document Structure](#document-structure)
5. [Class Files and Packages](#class-files-and-packages)
6. [Document Layout System](#document-layout-system)
7. [Chapter and Section Styling](#chapter-and-section-styling)
8. [Text and Typography](#text-and-typography)
9. [Margin Content System](#margin-content-system)
10. [Figures and Tables](#figures-and-tables)
11. [Mathematical Environments](#mathematical-environments)
12. [Bibliography and Citations](#bibliography-and-citations)
13. [Cross-Referencing System](#cross-referencing-system)
14. [Customization Guide](#customization-guide)
15. [Compilation Instructions](#compilation-instructions)
16. [Troubleshooting](#troubleshooting)
17. [Complete Command Reference](#complete-command-reference)
18. [Examples and Templates](#examples-and-templates)

---

## Introduction

KaoBook is a LaTeX document class inspired by the Tufte-LaTeX design philosophy and Ken Arroyo Ohori's doctoral thesis layout. It provides a distinctive 1.5-column layout with wide margins for sidenotes, marginnotes, small figures, and tables, creating an elegant and readable document format ideal for academic books, textbooks, and technical documentation.

### Key Features
- **Wide Margin Design**: Generous margins (47.7mm) for extensive margin content
- **Flexible Chapter Styles**: Four distinct chapter heading styles (kao, bar, lines, plain)
- **Rich Margin Content**: Support for sidenotes, marginnotes, figures, tables, and code listings
- **Advanced Typography**: Based on KOMA-Script with careful attention to spacing and readability
- **Integrated Bibliography**: Margin citations with full bibliography integration
- **Mathematical Environments**: Colorful theorem boxes and mathematical typesetting
- **Hyperlinks**: Full hyperref integration with customizable link colors
- **Multi-language Support**: Built-in support for English, Italian, and Danish

### Design Philosophy
The layout follows Edward Tufte's principles of information design:
1. **Integration of text and graphics**: Figures and tables can appear both in the main text and margins
2. **High information density**: Efficient use of page real estate
3. **Multiple information layers**: Main text complemented by margin annotations
4. **Quality typography**: Professional typesetting with careful attention to detail

---

## Installation and Setup

### Requirements
- **LaTeX Distribution**: TeX Live 2020+ or MikTeX 2.9+
- **Compilation Engine**: pdfLaTeX, XeLaTeX, or LuaLaTeX
- **Bibliography**: Biber (not BibTeX)
- **Additional Tools**: makeindex, makeglossaries (for nomenclature and glossaries)

### File Structure
```
project/
├── kaobook.cls          # Main book class
├── kaohandt.cls         # Report/handout class (if available)
├── kao.sty              # Core definitions
├── kaobiblio.sty        # Bibliography handling
├── kaotheorems.sty      # Mathematical environments
├── kaorefs.sty          # Cross-referencing commands
├── main.tex             # Your document
├── main.bib             # Bibliography database
├── glossary.tex         # Glossary definitions
├── chapters/            # Chapter files
│   ├── chapter1.tex
│   ├── chapter2.tex
│   └── ...
└── images/              # Image directory
    ├── figure1.jpg
    └── ...
```

### Installation Methods

#### Method 1: Project-Local Installation (Recommended)
1. Download the kaobook repository
2. Place all `.cls` and `.sty` files in your project directory
3. Create your `main.tex` file in the same directory

#### Method 2: System-Wide Installation
1. Locate your local texmf tree: `kpsewhich -var-value=TEXMFHOME`
2. Create directory: `$TEXMFHOME/tex/latex/kaobook/`
3. Copy all `.cls` and `.sty` files to this directory
4. Run `texhash` or `mktexlsr` to update the filename database

#### Method 3: Overleaf
1. Visit the [LaTeX Templates page](https://www.latextemplates.com/template/kaobook)
2. Open in Overleaf directly
3. Start editing the template

---

## Basic Usage

### Minimal Document Structure
```latex
\documentclass[
    a4paper,           % Paper size
    fontsize=10pt,     % Base font size
    twoside=true,      % Two-sided layout
]{kaobook}

% Essential packages
\usepackage{kaobiblio}    % Bibliography
\usepackage{kaotheorems}  % Theorem environments
\usepackage{kaorefs}      % Cross-referencing

\addbibresource{main.bib} % Bibliography file

\begin{document}

\frontmatter
\maketitle
\tableofcontents

\mainmatter
\chapter{Introduction}
Your content here...

\backmatter
\printbibliography

\end{document}
```

### Document Class Options
```latex
\documentclass[
    % Paper options
    a4paper,              % Default paper size
    a5paper,              % Smaller format
    letterpaper,          % US letter size
    
    % Font options
    fontsize=9pt,         % Small font (9-12pt supported)
    fontsize=10pt,        % Default font size
    fontsize=11pt,        % Large font
    
    % Layout options
    twoside=true,         % Two-sided (book-style)
    oneside,              % One-sided layout
    open=right,           % Chapters start on right pages
    open=any,             % Chapters can start on any page
    
    % TOC options
    chapterentrydots=true, % Dots in chapter TOC entries
    numbers=noenddot,      % No dots after chapter numbers
    
    % Section numbering
    secnumdepth=2,        % Number down to subsections
]{kaobook}
```

---

## Document Structure

### Front Matter, Main Matter, and Back Matter
KaoBook automatically adjusts layouts for different document parts:

```latex
\frontmatter  % Roman page numbers, plain style
% Title page, preface, TOC, LOF, LOT

\mainmatter   % Arabic page numbers, fancy headers, margin layout
% Chapters, sections, main content

\appendix     % Appendices (still main matter)
% Appendix chapters

\backmatter   % Plain style, wide layout
% Bibliography, index, glossary
```

### Page Layout Modes
KaoBook provides three distinct page layouts:

#### 1. Margin Layout (Default for Main Matter)
```latex
\pagelayout{margin}
```
- Text width: 107mm
- Margin width: 47.7mm  
- Margin separation: 6.2mm
- Used for: Main content with margin annotations

#### 2. Wide Layout (Default for Front/Back Matter)
```latex
\pagelayout{wide}
```
- Full page width with symmetric margins
- Used for: Title pages, TOC, bibliography

#### 3. Full Width Layout
```latex
\pagelayout{fullwidth}
```
- Complete page coverage
- Used for: Special pages, large figures

### Chapter Organization
```latex
% Organize content with parts
\pagelayout{wide}
\addpart{Part Title}
\pagelayout{margin}

% Regular chapters
\chapter{Chapter Title}
\input{chapters/chapter1.tex}

% Appendix chapters
\appendix
\chapter{Appendix Title}
```

---

## Class Files and Packages

### Core Components

#### 1. kaobook.cls
The main document class file that:
- Inherits from KOMA-Script's `scrbook` class
- Defines chapter heading styles (kao, bar, lines, plain)
- Sets up front/main/back matter behavior
- Configures default fonts and spacing

#### 2. kao.sty  
The core style file containing:
- **Page Layout System**: Margin, wide, and fullwidth layouts
- **Typography Settings**: Font configurations, paragraph formatting
- **Color Definitions**: Link colors, theorem colors
- **Margin Content**: Sidenotes, marginnotes, margin floats
- **Figure/Table Setup**: Caption positioning, float behavior
- **TOC Customization**: Multi-level table of contents
- **Hyperlink Configuration**: PDF bookmarks, link colors

#### 3. kaobiblio.sty
Bibliography management:
- **Citation Commands**: `\sidecite`, `\sidetextcite`, `\sideparencite`
- **Margin Citations**: Automatic margin citation formatting
- **Biblatex Integration**: Modern bibliography processing
- **Language Support**: Multilingual bibliography strings
- **Citation Styling**: Numeric or author-year styles

#### 4. kaotheorems.sty
Mathematical environments:
- **Theorem Types**: theorem, proposition, lemma, corollary
- **Definition Types**: definition, assumption
- **Informal Types**: remark, example, exercise
- **Styling Options**: Framed or plain theorem styles
- **Color Customization**: Background colors for each type

#### 5. kaorefs.sty
Cross-referencing system:
- **Labeling Commands**: `\labch{}`, `\labsec{}`, `\labfig{}`, etc.
- **Reference Commands**: `\refch{}`, `\vrefch{}`, `\nrefch{}`, `\frefch{}`
- **Smart References**: Integration with varioref and cleveref
- **Multilingual Support**: Language-specific reference names

---

## Document Layout System

### Layout Mechanics

#### Margin Layout Dimensions
```latex
% Calculated for A4 paper (210×297mm)
\newgeometry{
    top=27.4mm,           % Top margin
    bottom=27.4mm,        % Bottom margin
    inner=24.8mm,         % Inner margin
    textwidth=107mm,      % Main text width
    marginparsep=6.2mm,   % Separation between text and margin
    marginparwidth=47.7mm,% Margin width for content
}
```

#### Scaling System
KaoBook uses a scaling system for different paper sizes:
```latex
% Scaling factors
\newlength{\hscale} % Horizontal scale
\newlength{\vscale} % Vertical scale

% A4 paper (base)
\setlength{\hscale}{1mm}
\setlength{\vscale}{1mm}

% A5 paper
\setlength{\hscale}{0.704mm}
\setlength{\vscale}{0.704mm}
```

### Headers and Footers
KaoBook uses KOMA-Script's `scrlayer-scrpage` for sophisticated headers:

#### Main Style (`scrheadings`)
- **Left pages**: Page number | Rule | Section title
- **Right pages**: Chapter title | Rule | Page number  
- **Rule**: Vertical line separating elements

#### Plain Style (`plain.scrheadings`)
- **All pages**: No headers or footers
- **Used for**: Title pages, chapter openings

### Creating Custom Layouts
```latex
% Define custom layout command
\newcommand{\customlayout}{%
    \newgeometry{
        top=25mm,
        bottom=25mm,
        inner=20mm,
        textwidth=120mm,
        marginparsep=5mm,
        marginparwidth=40mm,
    }%
    \recalchead% Recalculate header dimensions
}

% Use custom layout
\customlayout
```

---

## Chapter and Section Styling

### Chapter Styles

#### 1. Kao Style (Default)
```latex
\setchapterstyle{kao}
```
- Large chapter number (2.85× scale) in margin
- Chapter title in main text area
- Vertical rule connecting number and title
- Different positioning for odd/even pages

#### 2. Bar Style  
```latex
\setchapterstyle{bar}
```
- Gray background bar spanning full width
- Chapter number and title within the bar
- Modern, clean appearance

#### 3. Lines Style
```latex
\setchapterstyle{lines}
```
- Horizontal rules above and below chapter title
- Large chapter number (3.5× scale)
- Spans full text width plus margin

#### 4. Plain Style
```latex
\setchapterstyle{plain}
```
- Standard KOMA-Script chapter style
- Simple, minimal appearance

### Chapter Images
Add decorative images to chapter headers:
```latex
% Set chapter image
\setchapterimage[55mm]{images/chapter-header.jpg}
\chapter{Chapter with Image}

% Image specifications
% - Width: Full paper width
% - Height: Adjustable (default 55mm)
% - Maintains aspect ratio: false (stretches to fit)
```

### Chapter Preambles
Add content before chapter title:
```latex
\setchapterpreamble[u]{\margintoc}      % Margin TOC
\setchapterpreamble[o]{%                % Custom content
    \vspace*{-20mm}%
    \includegraphics[width=\paperwidth]{image.jpg}%
}
\chapter{Chapter Title}
```

### Section Numbering Control
```latex
% Set numbering depth (0=chapter, 1=section, 2=subsection, etc.)
\setcounter{secnumdepth}{2}

% Show sections and subsections in TOC
\setcounter{tocdepth}{2}
```

### Customizing Section Fonts
```latex
% Customize KOMA fonts
\addtokomafont{chapter}{\color{darkblue}}
\addtokomafont{section}{\scshape}
\addtokomafont{subsection}{\itshape}
```

---

## Text and Typography

### Font Configuration
KaoBook supports both traditional LaTeX engines and modern Unicode engines:

#### pdfLaTeX Configuration
```latex
% Palatino-based font setup
\RequirePackage[scaled=.97,helvratio=.93,p,theoremfont]{newpxtext}
\RequirePackage[vvarbb,smallerops,bigdelims]{newpxmath}
\RequirePackage[scaled=.85]{beramono}
```

#### XeLaTeX/LuaLaTeX Configuration  
```latex
% Libertinus font family
\setromanfont[Scale=1.04]{Libertinus Serif}
\setsansfont[Scale=1]{Libertinus Sans}
\setmonofont[Scale=.89]{Liberation Mono}
\setmathfont{Libertinus Math}
```

### Typography Settings
```latex
% Line spacing
\linespread{1.07} % Slightly increased for Palatino

% Paragraph settings
\setlength{\parskip}{0.5\baselineskip} % Space between paragraphs
\setlength{\parindent}{0pt}            % No paragraph indentation

% Microtype improvements
\RequirePackage{microtype}
```

### Special Text Commands
KaoBook provides semantic markup commands:

#### Code and Technical Terms
```latex
\Command{includegraphics}    % LaTeX commands
\Environment{theorem}        % Environment names  
\Package{amsmath}           % Package names
\Class{article}             % Document classes
\Option{twoside}            % Class options
\Path{/home/user/file.tex}  % File paths
```

#### Latin Phrases and Abbreviations
```latex
\ie    % i.e. (that is)
\eg    % e.g. (for example)
\etal  % et al. (and others)
\etc   % etc. (and so forth)
\vs    % vs (versus)
\adhoc % ad hoc
```

### Lists and Itemization
```latex
% Customized list symbols
\renewcommand{\labelitemi}{\small$\blacktriangleright$}
\renewcommand{\labelitemii}{\textbullet}

% Compact list spacing
\setlist[itemize]{noitemsep}
\setlist[enumerate]{noitemsep}
\setlist[description]{noitemsep}
```

---

## Margin Content System

### Sidenotes
Sidenotes are numbered notes that appear in the margin:

#### Basic Sidenotes
```latex
This is main text\sidenote{This is a sidenote}.

% With custom mark
Text\sidenote[†]{Custom symbol sidenote}.

% With vertical offset
Text\sidenote[][2mm]{Sidenote moved down 2mm}.
Text\sidenote[][*-2]{Sidenote moved up 2 baselineskips}.
```

#### Advanced Sidenotes
```latex
% Manual mark and text
\sidenotemark[5]
\sidenotetext[5][3mm]{Sidenote text with offset}

% Counter management
\setcounter{sidenote}{0}                    % Reset counter
\counterwithin{sidenote}{chapter}           % Reset per chapter
\counterwithout{sidenote}{chapter}          % Continuous numbering
```

### Marginnotes
Unnumbered notes in the margin:

#### Basic Usage
```latex
Text with note\marginnote{Margin comment}.

% With offset
Text\marginnote[5mm]{Note moved down 5mm}.
Text\marginnote[*3]{Note moved down 3 baselineskips}.
```

#### Positioning
```latex
% Positive values: move down
\marginnote[10mm]{Move down 10mm}

% Negative values: move up  
\marginnote[-5mm]{Move up 5mm}

% Baselineskip multiples
\marginnote[*2]{Move down 2 lines}
\marginnote[*-1.5]{Move up 1.5 lines}
```

### Margin Figures
```latex
\begin{marginfigure}[offset]
    \includegraphics[width=\linewidth]{image.jpg}
    \caption{Figure caption}
    \labfig{margin-figure}
\end{marginfigure}
```

### Margin Tables
```latex
\begin{margintable}[offset]
    \centering
    \begin{tabular}{cc}
        A & B \\
        C & D \\
    \end{tabular}
    \caption{Table caption}
    \labtab{margin-table}
\end{margintable}
```

### Margin Listings
```latex
\begin{marginlisting}[offset]
    \begin{lstlisting}[language=Python]
def hello_world():
    print("Hello, World!")
    \end{lstlisting}
    \caption{Python code}
\end{marginlisting}
```

### Margin Table of Contents
```latex
% Basic margin TOC
\margintoc

% With custom offset
\margintoc[-5mm]

% In chapter preamble
\setchapterpreamble[u]{\margintoc}
\chapter{Chapter with Margin TOC}

% Custom depth
\setcounter{margintocdepth}{1} % Only sections, not subsections
```

### Managing Margin Content
```latex
% Spacing around margin floats
\setlength{\kaomarginskipabove}{3mm plus 2pt minus 2pt}
\setlength{\kaomarginskipbelow}{3mm plus 2pt minus 2pt}

% Force float placement
\FloatBarrier % Process all pending floats

% Margin content formatting
\renewcommand*{\marginfont}{\footnotesize\sffamily}
```

---

## Figures and Tables

### Standard Figures
```latex
\begin{figure}[htbp]
    \centering
    \includegraphics[width=0.8\textwidth]{image.jpg}
    \caption{Standard figure caption}
    \labfig{standard-figure}
\end{figure}
```

### Wide Figures
Figures spanning the full page width:
```latex
\begin{figure*}[htbp]
    \centering  
    \includegraphics[width=\textwidth]{wide-image.jpg}
    \caption{Wide figure spanning text and margin}
    \labfig{wide-figure}
\end{figure*}
```

### Margin Figures
Small figures in the margin:
```latex
\begin{marginfigure}[-2cm]
    \includegraphics[width=\linewidth]{small-image.jpg}
    \caption{Small margin figure}
    \labfig{margin-fig}
\end{marginfigure}
```

### Table Variations

#### Standard Tables
```latex
\begin{table}[htbp]
    \centering
    \caption{Standard table}
    \begin{tabular}{lcc}
        \toprule
        Item & Value 1 & Value 2 \\
        \midrule
        A & 1 & 2 \\
        B & 3 & 4 \\
        \bottomrule
    \end{tabular}
    \labtab{standard-table}
\end{table}
```

#### Wide Tables
```latex
\begin{table*}[htbp]
    \centering
    \caption{Wide table spanning full width}
    \begin{tabular}{lccccc}
        \toprule
        Item & Col1 & Col2 & Col3 & Col4 & Col5 \\
        \midrule
        Data & 1 & 2 & 3 & 4 & 5 \\
        \bottomrule
    \end{tabular}
    \labtab{wide-table}
\end{table*}
```

#### Long Tables
For tables spanning multiple pages:
```latex
\begin{longtable}{lcc}
    \caption{Long table with page breaks} \\
    \toprule
    Column 1 & Column 2 & Column 3 \\
    \midrule
    \endfirsthead
    
    \multicolumn{3}{c}{\tablename\ \thetable{} -- continued} \\
    \toprule
    Column 1 & Column 2 & Column 3 \\
    \midrule
    \endhead
    
    \midrule
    \multicolumn{3}{r}{Continued on next page} \\
    \endfoot
    
    \bottomrule
    \endlastfoot
    
    Row 1 & Data 1 & Data 2 \\
    Row 2 & Data 3 & Data 4 \\
    % ... many more rows
\end{longtable}
```

#### Margin Tables
```latex
\begin{margintable}
    \centering
    \caption{Compact margin table}
    \begin{tabular}{cc}
        \toprule
        A & B \\
        \midrule
        1 & 2 \\
        3 & 4 \\
        \bottomrule
    \end{tabular}
    \labtab{margin-table}
\end{margintable}
```

### Figure and Table Customization

#### Caption Positioning
```latex
% Figures: captions in margin
% Tables: captions in margin (above table)
% Wide figures/tables: captions below/above

% Custom caption format for margin content
\DeclareCaptionFormat{margin}{\@margin@par #1#2#3}
```

#### Float Behavior
```latex
% Improve float placement
\renewcommand{\topfraction}{.9}
\renewcommand{\textfraction}{0.35}  
\renewcommand{\floatpagefraction}{0.8}

% Force float processing
\FloatBarrier

% Continue figure/table numbering
\ContinuedFloat
```

### Image Handling
```latex
% Set image search paths
\graphicspath{{images/}{figures/}{pics/}}

% Default image settings
\setkeys{Gin}{
    width=\linewidth,
    totalheight=\textheight,
    keepaspectratio
}

% Include with specific size
\includegraphics[width=0.5\textwidth]{image.jpg}
\includegraphics[height=3cm]{image.jpg}
\includegraphics[scale=0.8]{image.jpg}
```

---

## Mathematical Environments

### Theorem-Like Environments
KaoBook provides beautifully styled mathematical environments:

#### Basic Theorem Types
```latex
\begin{theorem}[Optional Name]
    Every vector space has a basis.
    \labthm{basis-theorem}
\end{theorem}

\begin{proposition}[Optional Name]
    This follows from the theorem.
    \labprop{corollary-prop}
\end{proposition}

\begin{lemma}[Optional Name]  
    A useful intermediate result.
    \lablemma{useful-lemma}
\end{lemma}

\begin{corollary}[Optional Name]
    An immediate consequence.
\end{corollary}
```

#### Definition and Assumptions
```latex
\begin{definition}[Vector Space]
    A vector space over a field $F$ is a set $V$ together with...
    \labdef{vector-space}
\end{definition}

\begin{assumption}[Linearity]
    We assume all functions are linear.
    \labassum{linearity}
\end{assumption}
```

#### Informal Environments
```latex
\begin{remark}
    This is worth noting.
    \labremark{important-note}
\end{remark}

\begin{example}[Euclidean Space]
    Consider $\mathbb{R}^3$ with the standard inner product.
    \labexample{euclidean}
\end{example}

\begin{exercise}
    Prove that every finite-dimensional vector space has a basis.
    \labexercise{basis-exercise}
\end{exercise}
```

### Theorem Styling Options

#### Framed Theorems (Default)
```latex
\usepackage[framed=true]{kaotheorems}
```
- Colored background boxes
- Customizable colors per environment type
- Professional appearance

#### Plain Theorems
```latex
\usepackage[framed=false]{kaotheorems}
```
- Simple italic text
- Minimal visual styling
- Traditional LaTeX appearance

#### Color Customization
```latex
\usepackage[
    framed=true,
    background=blue!10,              % Default background
    theorembackground=red!20,        % Theorem color
    definitionbackground=green!15,   % Definition color
    examplebackground=yellow!10,     % Example color
]{kaotheorems}
```

### Proofs
```latex
\begin{proof}[Proof of Theorem~\ref{thm:basis-theorem}]
    Let $V$ be a vector space. Consider the collection...
    
    Therefore, every vector space has a basis.
\end{proof}

% Proof with custom QED symbol
\begin{proof}
    The proof follows directly.
    \qedhere
\end{proof}
```

### Mathematical Displays
```latex
% Inline math
The equation $E = mc^2$ is famous.

% Display math
\begin{equation}
    \int_{-\infty}^{\infty} e^{-x^2} dx = \sqrt{\pi}
    \labeq{gaussian-integral}
\end{equation}

% Wide equations spanning text and margin
\begin{wideequation}
    \sum_{n=1}^{\infty} \frac{1}{n^2} = \frac{\pi^2}{6}
    \labeq{basel-problem}
\end{wideequation}

% Aligned equations
\begin{align}
    x &= a + b \\
    y &= c + d
\end{align}
```

### Integration with Margin Content
```latex
\begin{theorem}
    This is an important theorem.
    \marginnote{Historical context about this theorem.}
\end{theorem}

\begin{definition}
    A group is a set with an operation...
\end{definition}
\sidenote{Groups are fundamental algebraic structures.}
```

---

## Bibliography and Citations

### Bibliography Setup
KaoBook uses Biblatex with Biber for modern bibliography management:

```latex
% In preamble
\usepackage{kaobiblio}
\addbibresource{main.bib}      % Bibliography file
\addbibresource{extra.bib}     % Additional files

% Choose citation style
\usepackage[
    style=numeric-comp,         % Numeric citations [1,2,3]
    sorting=none,              % Order by appearance
    backend=biber,             % Use biber backend
    hyperref=true,             % Hyperlinked citations
    backref=true,              % Back references
]{biblatex}
```

### Citation Commands

#### Standard Citations
```latex
% Basic citations
\cite{key}                  % [1]
\cite{key1,key2,key3}      % [1,2,3]
\cite[p.~123]{key}         % [1, p. 123]
\cite[See][p.~123]{key}    % [See 1, p. 123]

% Textual citations
\textcite{key}             % Author (Year) or Author [1]
\parencite{key}            % (Author Year) or [1]
```

#### Margin Citations (KaoBook Special Feature)
```latex
% Citation with margin annotation
\sidecite{key}             % Citation number + margin info
\sidecite[p.~45]{key}      % With page reference
\sidecite[][*2]{key}       % With vertical offset

% Text citation with margin
\sidetextcite{key}         % Textual citation + margin
\sideparencite{key}        % Parenthetical citation + margin

% Margin citation formatting
\formatmargincitation{key}  % Customize margin appearance
```

#### Multiple Citations
```latex
% Multiple references in margin
\sidecite{key1,key2,key3}

% Complex citation with pre/post notes
\sidecite[See][for details]{key}
```

### Bibliography Database (main.bib)
```bibtex
@article{einstein1905,
    author = {Einstein, Albert},
    title = {Zur Elektrodynamik bewegter K{\"o}rper},
    journal = {Annalen der Physik},
    volume = {17},
    number = {10},
    pages = {891--921},
    year = {1905},
    doi = {10.1002/andp.19053221004}
}

@book{knuth1984,
    author = {Knuth, Donald E.},
    title = {The {\TeX}book},
    publisher = {Addison-Wesley},
    year = {1984},
    isbn = {0-201-13447-0}
}

@incollection{chapter2020,
    author = {Smith, John},
    title = {Modern Techniques},
    booktitle = {Handbook of Advanced Methods},
    editor = {Johnson, Mary},
    publisher = {Academic Press},
    year = {2020},
    pages = {123--156}
}
```

### Bibliography Output
```latex
% Print bibliography
\printbibliography[heading=bibintoc,title=Bibliography]

% With custom note
\defbibnote{bibnote}{The following sources were consulted.}
\printbibliography[heading=bibintoc,prenote=bibnote]

% Filtered bibliography
\printbibliography[type=article,title=Journal Articles]
\printbibliography[type=book,title=Books]
```

### Citation Style Customization
```latex
% Numeric style
\usepackage[style=numeric-comp]{biblatex}

% Author-year style  
\usepackage[style=authoryear-comp]{biblatex}

% Custom citation format
\DeclareFieldFormat{postnote}{#1}
\DeclareFieldFormat{multipostnote}{#1}
```

### Advanced Bibliography Features

#### Back References
```latex
% Show where items were cited
\usepackage[backref=true]{biblatex}

% Custom back-reference text
\DefineBibliographyStrings{english}{
    backrefpage = {cited on page},
    backrefpages = {cited on pages}
}
```

#### Field Filtering
```latex
% Remove unwanted fields from bibliography
\AtEveryBibitem{
    \clearfield{issn}
    \clearfield{isbn}
    \clearfield{doi}
    \clearfield{url}
}
```

---

## Cross-Referencing System

KaoBook provides a comprehensive cross-referencing system through `kaorefs.sty`:

### Labeling Commands
Systematic labeling with prefixes:

```latex
% Structural elements
\labpage{intro}          % \label{page:intro}
\labpart{fundamentals}   % \label{part:fundamentals}
\labch{introduction}     % \label{ch:introduction}
\labsec{methods}         % \label{sec:methods}
\labsubsec{analysis}     % \label{subsec:analysis}

% Floats
\labfig{results-plot}    % \label{fig:results-plot}
\labtab{data-summary}    % \label{tab:data-summary}
\labeq{main-equation}    % \label{eq:main-equation}

% Mathematical environments
\labdef{vector-space}    % \label{def:vector-space}
\labthm{main-theorem}    % \label{thm:main-theorem}
\labprop{useful-prop}    % \label{prop:useful-prop}
\lablemma{key-lemma}     % \label{lemma:key-lemma}
\labremark{important}    % \label{remark:important}
\labexample{simple}      % \label{example:simple}
```

### Reference Commands
Multiple reference styles for each element type:

#### Chapters
```latex
\refch{introduction}        % Chapter 1
\vrefch{introduction}       % Chapter 1 on page 15
\nrefch{introduction}       % Chapter 1 (Introduction)
\frefch{introduction}       % Chapter 1 (Introduction) on page 15
\refchshort{introduction}   % Chap. 1
```

#### Sections
```latex
\refsec{methods}           % Section 2.1
\vrefsec{methods}          % Section 2.1 on page 25
\nrefsec{methods}          % Section 2.1 (Methods)
\frefsec{methods}          % Section 2.1 (Methods) on page 25
\refsecshort{methods}      % Sec. 2.1
```

#### Figures and Tables
```latex
\reffig{results-plot}      % Figure 3.2
\vreffig{results-plot}     % Figure 3.2 on page 45
\reffigshort{results-plot} % Fig. 3.2

\reftab{data-summary}      % Table 2.1
\vreftab{data-summary}     % Table 2.1 on page 30
```

#### Equations
```latex
\refeq{main-equation}      % Equation 4.1
\vrefeq{main-equation}     % Equation 4.1 on page 67
\refeqshort{main-equation} % Eq. 4.1
```

#### Mathematical Environments
```latex
\refdef{vector-space}      % Definition 1.1
\vrefdef{vector-space}     % Definition 1.1 on page 12

\refthm{main-theorem}      % Theorem 2.3
\vrefthm{main-theorem}     % Theorem 2.3 on page 34

\refprop{useful-prop}      % Proposition 2.4
\reflemma{key-lemma}       % Lemma 2.5
\refremark{important}      % Remark 2.1
\refexample{simple}        % Example 2.2
```

### Smart Reference Behavior

#### Varioref Integration
The `vref` commands provide context-aware references:
```latex
\vrefch{intro}
% Output depends on distance:
% - Same page: "Chapter 1"
% - Next page: "Chapter 1 on the following page"  
% - Specific page: "Chapter 1 on page 15"
```

#### Cleveref Integration
Automatic determination of reference type:
```latex
\cref{eq:main-equation}    % Equation (1.1)
\Cref{fig:plot}           % Figure 1.2 (capitalized)
\cref{thm:main,prop:help} % Theorem 2.1 and Proposition 2.2
```

### Multilingual Support
Reference names adapt to document language:

#### English
```latex
\addto\captionsenglish{
    \renewcommand{\chapternameshort}{Chap.}
    \renewcommand{\sectionname}{Section}
    \renewcommand{\figurenameshort}{Fig.}
    % ... more definitions
}
```

#### Other Languages (Italian, Danish)
The package includes predefined strings for multiple languages.

### Hyperlink Integration
All reference commands are fully hyperlinked:
```latex
% Customize link colors
\hypersetup{
    linkcolor=blue,      % Internal links
    citecolor=green,     % Citations
    urlcolor=red,        % URLs
}
```

### Custom Reference Styles
```latex
% Define custom reference command
\newcommand{\myrefch}[1]{%
    \hyperref[ch:#1]{Chapter~\ref{ch:#1}: ``\nameref{ch:#1}''}%
}

% Usage
\myrefch{introduction} % Chapter 1: "Introduction"
```

---

## Customization Guide

### Color Schemes

#### Link Colors
```latex
\hypersetup{
    linkcolor=Blue,        % Internal links (default)
    citecolor=OliveGreen,  % Citations (default)
    urlcolor=OliveGreen,   % URLs (default)
    colorlinks=true,       % Enable colored links
}

% Custom color definitions
\definecolor{customblue}{RGB}{0,100,200}
\hypersetup{linkcolor=customblue}
```

#### Theorem Colors
```latex
\usepackage[
    framed=true,
    theorembackground=blue!15,
    definitionbackground=green!10,
    propositionbackground=orange!10,
    lemmabackground=yellow!15,
    corollarybackground=purple!10,
    remarkbackground=gray!10,
    examplebackground=cyan!10,
    exercisebackground=red!10,
]{kaotheorems}
```

#### Heading Colors
```latex
% Colored headings
\addtokomafont{title}{\color{Maroon}}
\addtokomafont{part}{\color{Maroon}}
\addtokomafont{chapter}{\color{Maroon}}
\addtokomafont{section}{\color{Blue}}
\addtokomafont{subsection}{\color{Blue}}
\addtokomafont{captionlabel}{\color{Blue}}
```

### Typography Customization

#### Font Changes
```latex
% Change main font (requires fontspec for XeLaTeX/LuaLaTeX)
\setmainfont{Times New Roman}
\setsansfont{Arial}
\setmonofont{Courier New}

% Change font sizes
\addtokomafont{chapter}{\Huge}
\addtokomafont{section}{\Large}
\addtokomafont{subsection}{\large}
```

#### Line Spacing
```latex
\linespread{1.1}        % Slightly more spacing
\setstretch{1.2}        % Alternative method

% Localized spacing changes
{\setstretch{1.5}
This paragraph has different line spacing.
}
```

### Layout Modifications

#### Margin Width Adjustment
```latex
% Custom margin layout
\newcommand{\widemarginlayout}{%
    \newgeometry{
        top=25mm,
        bottom=25mm,
        inner=20mm,
        textwidth=100mm,         % Narrower text
        marginparsep=8mm,        % Wider separation
        marginparwidth=55mm,     % Wider margin
    }%
    \recalchead%
}
```

#### Page Dimensions for Different Paper Sizes
```latex
% A5 paper optimization
\documentclass[a5paper,fontsize=9pt]{kaobook}

% US Letter paper
\documentclass[letterpaper]{kaobook}

% Custom paper size
\documentclass{kaobook}
\usepackage[paperwidth=6in,paperheight=9in]{geometry}
```

### Chapter Style Customization

#### Custom Chapter Style
```latex
\DeclareDocumentCommand{\chapterstylecustom}{}{%
    \renewcommand*{\chapterformat}{%
        \textcolor{red}{\scalebox{4}{\thechapter}}%
    }%
    \renewcommand\chapterlinesformat[3]{%
        \parbox{\textwidth}{%
            \centering ##2 \\[1ex]
            \rule{\textwidth}{2pt} \\[1ex]
            ##3
        }%
    }%
    \RedeclareSectionCommand[beforeskip=0pt,afterskip=15mm]{chapter}%
}

% Activate custom style
\setchapterstyle{custom}
```

### Header and Footer Customization

#### Custom Header Style
```latex
\renewpagestyle{scrheadings}{%
    % Left page header
    {\makebox[\textwidth][l]{\thepage\quad|\quad\leftmark}}%
    % Right page header  
    {\makebox[\textwidth][r]{\rightmark\quad|\quad\thepage}}%
    % Plain page header
    {\makebox[\textwidth][c]{\thepage}}%
}{%
    % Footers (empty in this example)
    {}%
    {}%
    {}%
}
```

### Margin Content Customization

#### Sidenote Appearance
```latex
% Customize sidenote formatting
\RenewDocumentCommand\@sidenotes@thesidenotemark{ m }{%
    \textsuperscript{\textcolor{red}{#1}}% Red sidenote marks
}

% Customize margin note font
\renewcommand*{\marginfont}{\small\sffamily\color{blue}}
```

#### Margin TOC Customization
```latex
% Custom margin TOC depth
\setcounter{margintocdepth}{1} % Only show sections

% Custom margin TOC styling
\renewcommand{\margintocstyle}{%
    \footnotesize\sffamily\color{darkgray}%
}
```

### Caption Customization
```latex
% Customize caption format
\captionsetup{
    format=hang,           % Hanging indent
    font=small,            % Smaller font
    labelfont=bf,          % Bold label
    textfont=it,           % Italic text
    justification=justified, % Justified text
    singlelinecheck=false, % Apply to single lines too
}

% Different styles for different floats
\captionsetup[figure]{position=bottom}
\captionsetup[table]{position=top}
```

### Creating Custom Environments

#### Custom Box Environment
```latex
\usepackage[framemethod=TikZ]{mdframed}

\mdfdefinestyle{custombox}{
    linewidth=2pt,
    linecolor=blue,
    backgroundcolor=blue!10,
    roundcorner=5pt,
    innertopmargin=10pt,
    innerbottommargin=10pt,
}

\newmdenv[style=custombox]{custombox}

% Usage
\begin{custombox}
Custom content in a colored box.
\end{custombox}
```

#### Custom Theorem Environment
```latex
\declaretheoremstyle[
    headfont=\normalfont\bfseries\color{red},
    bodyfont=\normalfont,
    mdframed={
        linewidth=2pt,
        rightline=false,
        topline=false,
        bottomline=false,
        linecolor=red,
        backgroundcolor=red!10,
    }
]{redtheorem}

\declaretheorem[
    style=redtheorem,
    name=Important Note,
    numberwithin=section,
]{important}

% Usage
\begin{important}
This is very important information.
\end{important}
```

---

## Compilation Instructions

### Basic Compilation Sequence
The complexity of KaoBook documents requires a specific compilation sequence:

```bash
# Basic sequence
pdflatex main.tex          # First pass
biber main                 # Process bibliography
pdflatex main.tex          # Second pass  
pdflatex main.tex          # Third pass (fix references)
```

### Full Compilation with All Features
```bash
# Complete sequence for all features
pdflatex -interaction=nonstopmode main.tex
makeindex main.nlo -s nomencl.ist -o main.nls    # Nomenclature
makeindex main.idx                                # Index
biber main                                        # Bibliography
pdflatex main.tex
makeglossaries main                               # Glossary
pdflatex main.tex                                # Final pass
```

### Automated Compilation Scripts

#### Bash Script (Unix/macOS/Linux)
```bash
#!/bin/bash
# File: compile.sh

echo "Compiling KaoBook document..."

# First LaTeX pass
echo "First LaTeX pass..."
pdflatex -interaction=nonstopmode main

# Process nomenclature
if [ -f main.nlo ]; then
    echo "Processing nomenclature..."
    makeindex main.nlo -s nomencl.ist -o main.nls
fi

# Process index
if [ -f main.idx ]; then
    echo "Processing index..."
    makeindex main
fi

# Process bibliography
echo "Processing bibliography..."
biber main

# Second LaTeX pass
echo "Second LaTeX pass..."
pdflatex -interaction=nonstopmode main

# Process glossary
if [ -f main.glo ]; then
    echo "Processing glossary..."
    makeglossaries main
fi

# Final LaTeX pass
echo "Final LaTeX pass..."
pdflatex -interaction=nonstopmode main

echo "Compilation complete!"
```

#### PowerShell Script (Windows)
```powershell
# File: compile.ps1

Write-Host "Compiling KaoBook document..." -ForegroundColor Green

# First LaTeX pass
Write-Host "First LaTeX pass..." -ForegroundColor Yellow
pdflatex -interaction=nonstopmode main

# Process nomenclature
if (Test-Path main.nlo) {
    Write-Host "Processing nomenclature..." -ForegroundColor Yellow
    makeindex main.nlo -s nomencl.ist -o main.nls
}

# Process index
if (Test-Path main.idx) {
    Write-Host "Processing index..." -ForegroundColor Yellow
    makeindex main
}

# Process bibliography
Write-Host "Processing bibliography..." -ForegroundColor Yellow
biber main

# Second LaTeX pass
Write-Host "Second LaTeX pass..." -ForegroundColor Yellow
pdflatex -interaction=nonstopmode main

# Process glossary
if (Test-Path main.glo) {
    Write-Host "Processing glossary..." -ForegroundColor Yellow
    makeglossaries main
}

# Final LaTeX pass
Write-Host "Final LaTeX pass..." -ForegroundColor Yellow
pdflatex -interaction=nonstopmode main

Write-Host "Compilation complete!" -ForegroundColor Green
```

### Latexmk Configuration
For automatic compilation dependency tracking:

```perl
# File: .latexmkrc
$pdf_mode = 1;                    # Use pdflatex
$biber = 'biber %O --debug %B';  # Use biber for bibliography
$bibtex_use = 2;                  # Use biber instead of bibtex

# Custom dependency for nomenclature
add_cus_dep('nlo', 'nls', 0, 'nlo2nls');
sub nlo2nls {
    system("makeindex $_[0].nlo -s nomencl.ist -o $_[0].nls");
}

# Custom dependency for glossary
add_cus_dep('glo', 'gls', 0, 'makeglossaries');
add_cus_dep('acn', 'acr', 0, 'makeglossaries');
add_cus_dep('alg', 'glg', 0, 'makeglossaries');
sub makeglossaries {
    my $dir = dirname($_[0]);
    my $base = basename($_[0]);
    if ($dir eq '.') {
        system "makeglossaries $base";
    } else {
        system "makeglossaries -d $dir $base";
    }
}

# Clean up auxiliary files
$clean_ext = "bbl nav out snm";
```

Usage with latexmk:
```bash
latexmk -pdf main.tex       # Compile with dependency tracking
latexmk -pdf -pvc main.tex  # Continuous compilation
latexmk -c                  # Clean auxiliary files
```

### IDE Integration

#### VS Code with LaTeX Workshop
```json
// settings.json
{
    "latex-workshop.latex.tools": [
        {
            "name": "pdflatex",
            "command": "pdflatex",
            "args": [
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOC%"
            ]
        },
        {
            "name": "biber",
            "command": "biber",
            "args": ["%DOCFILE%"]
        },
        {
            "name": "makeglossaries",
            "command": "makeglossaries",
            "args": ["%DOCFILE%"]
        },
        {
            "name": "makeindex",
            "command": "makeindex",
            "args": [
                "%DOCFILE%.nlo",
                "-s", "nomencl.ist",
                "-o", "%DOCFILE%.nls"
            ]
        }
    ],
    "latex-workshop.latex.recipes": [
        {
            "name": "KaoBook Full",
            "tools": [
                "pdflatex",
                "makeindex",
                "biber",
                "pdflatex",
                "makeglossaries", 
                "pdflatex"
            ]
        }
    ]
}
```

#### TeXstudio Configuration
1. Options → Configure TeXstudio
2. Commands → Bibliography: `biber %`
3. Build → User Commands → Add: `makeglossaries %`
4. Build → Default Bibliography Tool: `Biber`

### Troubleshooting Compilation

#### Common Issues and Solutions

**Bibliography not appearing:**
```bash
# Check biber log
biber --debug main

# Common solution: clear cache
biber --cache
rm -rf `biber --cache`
```

**Glossary not appearing:**
```bash
# Check if .glo file exists
ls -la main.glo

# Manual glossary compilation
makeglossaries -d . main
```

**Margin content positioning issues:**
```bash
# Usually fixed with additional LaTeX passes
pdflatex main.tex
pdflatex main.tex
```

**Font warnings with XeLaTeX/LuaLaTeX:**
```latex
% Ensure fonts are installed or use alternatives
\setmainfont{Latin Modern Roman}
\setsansfont{Latin Modern Sans}
\setmonofont{Latin Modern Mono}
```

---

## Troubleshooting

### Common Issues and Solutions

#### Layout and Positioning Problems

**Margin content overlapping main text:**
```latex
% Solution 1: Adjust margin content spacing
\setlength{\kaomarginskipabove}{5mm}
\setlength{\kaomarginskipbelow}{5mm}

% Solution 2: Use FloatBarrier before problematic content
\FloatBarrier
\begin{marginfigure}
    % content
\end{marginfigure}

% Solution 3: Add manual spacing
\marginnote[10mm]{Content with extra spacing}
```

**Chapter styles not displaying correctly:**
```latex
% Ensure TikZ is loaded (required for some styles)
\usepackage{tikz}

% Reset to plain style if issues persist
\setchapterstyle{plain}
```

**Headers extending beyond page margins:**
```latex
% Recalculate header dimensions after layout changes
\recalchead
```

#### Bibliography Issues

**Bibliography not compiling:**
```latex
% Check biber version compatibility
% In terminal: biber --version

% Clear biber cache if needed
% In terminal: 
% biber --cache
% rm -rf [cache directory]

% Ensure correct bibliography backend
\usepackage[backend=biber]{biblatex}
% NOT: \usepackage[backend=bibtex]{biblatex}
```

**Citations not linking:**
```latex
% Ensure hyperref is loaded (usually automatic)
\usepackage{hyperref}

% Check citation key exists in .bib file
% Compile sequence: pdflatex → biber → pdflatex → pdflatex
```

**Margin citations not appearing:**
```latex
% Ensure kaobiblio is loaded
\usepackage{kaobiblio}

% Use correct command syntax
\sidecite{key}           % Correct
\cite{key}               % Wrong for margin citations
```

#### Font and Typography Issues

**Font substitution warnings:**
```latex
% For pdfLaTeX, ensure required fonts are installed
% Alternative: use different font packages
\usepackage{lmodern}     % Latin Modern fonts
\usepackage{charter}     % Charter font

% For XeLaTeX/LuaLaTeX, install required fonts or substitute
\setmainfont{Times New Roman}  % Common alternative
```

**Inconsistent line spacing:**
```latex
% Set consistent line spacing
\linespread{1.07}
\selectfont

% Or use setspace package
\usepackage{setspace}
\setstretch{1.07}
```

#### Cross-Reference Problems

**References showing ?? instead of numbers:**
```latex
% Compile multiple times (references need 2-3 passes)
% Order: pdflatex → pdflatex → pdflatex

% Check label syntax
\labfig{correct}         % Correct
\label{fig:also-works}   % Also works but not recommended
```

**Hyperlinks not working:**
```latex
% Ensure hyperref is loaded after other packages
\usepackage{kaorefs}     % This loads hyperref correctly

% Check for package conflicts
% Load conflicting packages before hyperref/kaorefs
```

#### Compilation Errors

**Package conflicts:**
```latex
% Load packages in correct order
\usepackage{amsmath}     % Before kaotheorems
\usepackage{graphicx}    % Before kao
\usepackage{kaotheorems} 
\usepackage{kaorefs}     % Load last (contains hyperref)
```

**Memory issues with large documents:**
```latex
% Increase LaTeX memory in texmf.cnf
main_memory = 12000000
extra_mem_top = 12000000

% Or split document into smaller files
\include{chapters/chapter1}
\include{chapters/chapter2}
```

**Encoding issues:**
```latex
% Ensure UTF-8 encoding
\usepackage[utf8]{inputenc}  % For pdfLaTeX
% XeLaTeX/LuaLaTeX handle UTF-8 natively

% Check file encoding in your editor
```

### Performance Optimization

#### Faster Compilation
```latex
% Use draft mode for faster compilation during editing
\documentclass[draft]{kaobook}

% Exclude graphics in draft mode
\setkeys{Gin}{draft=true}

% Use \includeonly for selective compilation
\includeonly{chapters/chapter1,chapters/chapter3}
```

#### Memory Management
```latex
% For documents with many floats
\extrafloats{100}

% Clear float queues periodically
\clearpage
\FloatBarrier
```

### Debugging Techniques

#### Verbose Output
```bash
# Get detailed compilation information
pdflatex -interaction=nonstopmode -file-line-error main.tex

# Biber debugging
biber --debug --trace main
```

#### Package Tracing
```latex
% Trace package loading
\listfiles

% Debug specific packages
\usepackage[debug]{kaotheorems}
```

#### Layout Debugging
```latex
% Show page layout boxes
\usepackage{showframe}

% Show margin boundaries
\usepackage{layout}
\layout  % Add this command to see layout

% Debug float placement
\usepackage{afterpage}
\afterpage{\clearpage}
```

### Getting Help

#### Documentation Sources
1. **KaoBook repository**: https://github.com/fmarotta/kaobook
2. **LaTeX Templates page**: https://www.latextemplates.com/template/kaobook
3. **KOMA-Script documentation**: Essential for understanding underlying class
4. **TeX Stack Exchange**: Community Q&A for specific problems

#### Log File Analysis
Always check the .log file for detailed error information:
```bash
# View end of log file for errors
tail -n 50 main.log

# Search for specific errors
grep -i error main.log
grep -i warning main.log
```

---

## Complete Command Reference

### Document Class and Packages
```latex
% Document class
\documentclass[options]{kaobook}

% Essential packages
\usepackage{kaobiblio}     % Bibliography with margin citations
\usepackage{kaotheorems}   % Mathematical environments  
\usepackage{kaorefs}       % Cross-referencing system
```

### Page Layout Commands
```latex
% Layout modes
\pagelayout{margin}        % Main text + margin
\pagelayout{wide}          % Full width, symmetric margins
\pagelayout{fullwidth}     % Complete page coverage

% Matter divisions
\frontmatter               % Roman numerals, plain headers
\mainmatter                % Arabic numbers, fancy headers
\backmatter                % Plain headers, wide layout
\appendix                  % Appendix chapters
```

### Chapter Styling
```latex
% Chapter styles
\setchapterstyle{kao}      % Default with margin number
\setchapterstyle{bar}      % Gray background bar
\setchapterstyle{lines}    % Horizontal rules above/below
\setchapterstyle{plain}    % Simple KOMA-Script style

% Chapter images
\setchapterimage[height]{path}

% Chapter preambles
\setchapterpreamble[position]{content}
```

### Margin Content
```latex
% Sidenotes (numbered)
\sidenote[mark][offset]{text}
\sidenotemark[number]
\sidenotetext[number][offset]{text}

% Margin notes (unnumbered)
\marginnote[offset]{text}

% Margin table of contents
\margintoc[offset]

% Margin floats
\begin{marginfigure}[offset] ... \end{marginfigure}
\begin{margintable}[offset] ... \end{margintable}
\begin{marginlisting}[offset] ... \end{marginlisting}
```

### Text Formatting
```latex
% Semantic markup
\Command{name}             % LaTeX commands
\Environment{name}         % Environment names
\Package{name}            % Package names
\Class{name}              % Document classes
\Option{name}             % Class/package options
\Path{path}               % File paths

% Latin abbreviations
\ie                       % i.e.
\eg                       % e.g.
\etal                     % et al.
\etc                      % etc.
\vs                       % vs
\adhoc                    % ad hoc
```

### Figures and Tables
```latex
% Standard floats
\begin{figure}[position] ... \end{figure}
\begin{table}[position] ... \end{table}

% Wide floats (span text + margin)
\begin{figure*}[position] ... \end{figure*}
\begin{table*}[position] ... \end{table*}

% Long tables
\begin{longtable}{columns} ... \end{longtable}

% Wide paragraphs
\begin{widepar} ... \end{widepar}
\begin{fullwidthpar} ... \end{fullwidthpar}

% Wide equations
\begin{wideequation} ... \end{wideequation}
```

### Mathematical Environments
```latex
% Theorem-like environments
\begin{theorem}[name] ... \end{theorem}
\begin{proposition}[name] ... \end{proposition}
\begin{lemma}[name] ... \end{lemma}
\begin{corollary}[name] ... \end{corollary}

% Definition-like environments
\begin{definition}[name] ... \end{definition}
\begin{assumption}[name] ... \end{assumption}

% Informal environments
\begin{remark} ... \end{remark}
\begin{example}[name] ... \end{example}
\begin{exercise} ... \end{exercise}

% Proof environment
\begin{proof}[name] ... \end{proof}
```

### Custom Boxes
```latex
% Basic colored box
\begin{kaobox}[frametitle=Title] ... \end{kaobox}

% Numbered comment box
\begin{kaocounter} ... \end{kaocounter}
```

### Bibliography and Citations
```latex
% Bibliography setup
\addbibresource{file.bib}
\printbibliography[options]

% Standard citations
\cite[prenote][postnote]{key}
\textcite[prenote][postnote]{key}
\parencite[prenote][postnote]{key}

% Margin citations (KaoBook special)
\sidecite[prenote][postnote]{key}
\sidetextcite[prenote][postnote]{key}
\sideparencite[prenote][postnote]{key}

% Multiple citations
\cite{key1,key2,key3}
\sidecite{key1,key2,key3}
```

### Cross-Referencing
```latex
% Labeling commands
\labpage{key}     \labpart{key}     \labch{key}
\labsec{key}      \labsubsec{key}   \labfig{key}
\labtab{key}      \labeq{key}       \labdef{key}
\labthm{key}      \labprop{key}     \lablemma{key}
\labremark{key}   \labexample{key}

% Reference commands (plain)
\refch{key}       \refsec{key}      \reffig{key}
\reftab{key}      \refeq{key}       \refdef{key}
\refthm{key}      \refprop{key}     \reflemma{key}

% Reference commands (with page)
\vrefch{key}      \vrefsec{key}     \vreffig{key}
\vreftab{key}     \vrefeq{key}      \vrefdef{key}
\vrefthm{key}     \vrefprop{key}    \vreflemma{key}

% Reference commands (with name)
\nrefch{key}      \nrefsec{key}
\frefch{key}      \frefsec{key}     % Full: name + page

% Short forms
\refchshort{key}  \refsecshort{key} \reffigshort{key}
\refeqshort{key}
```

### Glossary and Index
```latex
% Glossary entries (in glossary.tex)
\newglossaryentry{label}{name=name,description=description}
\newacronym{label}{abbrev}{full form}

% Using glossary entries
\gls{label}              % First use: full form, subsequent: abbreviation
\glspl{label}            % Plural form
\Gls{label}              % Capitalized
\acrfull{label}          % Always full form
\acrshort{label}         % Always abbreviation

% Index entries
\index{term}             % Basic index entry
\index{term!subterm}     % Subentry
\index{term|textbf}      % Bold page number
```

### Nomenclature
```latex
% Define nomenclature entries
\nomenclature{$c$}{Speed of light}
\nomenclature{$h$}{Planck constant}

% Print nomenclature
\printnomenclature
```

### Color Customization
```latex
% Hyperlink colors
\hypersetup{
    linkcolor=color,     % Internal links
    citecolor=color,     % Citations  
    urlcolor=color,      % URLs
}

% Theorem colors (kaotheorems options)
theorembackground=color
definitionbackground=color
examplebackground=color
% ... etc for each theorem type

% Heading colors
\addtokomafont{chapter}{\color{color}}
\addtokomafont{section}{\color{color}}
```

### Font Customization
```latex
% KOMA font elements
\addtokomafont{element}{\font-commands}

% Available elements:
% title, part, chapter, section, subsection, subsubsection
% paragraph, captionlabel, pagenumber, etc.

% Font commands:
% \bfseries (bold), \itshape (italic), \scshape (small caps)
% \sffamily (sans serif), \ttfamily (monospace)
% \tiny, \small, \large, \Large, \huge, \Huge
```

### Advanced Customization
```latex
% Custom chapter style
\DeclareDocumentCommand{\setchapterstyle}{m}{...}

% Custom page layout
\newcommand{\customlayout}{%
    \newgeometry{...}%
    \recalchead%
}

% Custom theorem style
\declaretheoremstyle[options]{style-name}
\declaretheorem[style=style-name]{environment-name}

% Custom caption format
\DeclareCaptionFormat{format-name}{formatting}
\captionsetup{format=format-name}
```

---

## Examples and Templates

### Basic Book Template
```latex
\documentclass[
    a4paper,
    fontsize=10pt,
    twoside=true,
    numbers=noenddot,
]{kaobook}

% Load packages
\usepackage[english]{babel}
\usepackage{kaobiblio}
\usepackage[framed=true]{kaotheorems}
\usepackage{kaorefs}

% Bibliography
\addbibresource{main.bib}

% Document metadata
\title{My Book Title}
\author{Author Name}
\date{\today}

\begin{document}

\frontmatter
\maketitle
\tableofcontents

\mainmatter
\setchapterstyle{kao}

\chapter{Introduction}
\labch{intro}

This is the first chapter\sidenote{This is a sidenote}.

\chapter{Main Content}
\labch{main}

\begin{theorem}[Main Result]
This is an important theorem.
\labthm{main-result}
\end{theorem}

\backmatter
\printbibliography

\end{document}
```

### Academic Textbook Template
```latex
\documentclass[
    a4paper,
    fontsize=10pt,
    twoside=true,
    secnumdepth=2,
]{kaobook}

\usepackage[english]{babel}
\usepackage{kaobiblio}
\usepackage[framed=true,theorembackground=blue!10]{kaotheorems}
\usepackage{kaorefs}

% Additional packages for math
\usepackage{amsmath,amsthm,amssymb}
\usepackage{mathtools}

% Graphics and tables
\usepackage{graphicx}
\usepackage{booktabs}
\usepackage{longtabu}

% Bibliography
\addbibresource{references.bib}

% Glossary
\makeglossaries
\input{glossary}

\title{Advanced Mathematics}
\subtitle{A Comprehensive Guide}
\author{Professor Name}
\date{\today}

\begin{document}

\frontmatter
\maketitle

% Copyright page
\makeatletter
\uppertitleback{\@title}
\lowertitleback{
    \textbf{Copyright}\\
    © 2024 Professor Name. All rights reserved.
    
    \medskip
    
    \textbf{Publisher Information}\\
    Published by Academic Press
}
\makeatother

% Table of contents with margin TOC
\setchapterpreamble[u]{\margintoc}
\tableofcontents
\listoffigures
\listoftables

\mainmatter
\setchapterstyle{kao}

\pagelayout{wide}
\addpart{Foundations}
\pagelayout{margin}

\chapter{Basic Concepts}
\labch{basics}

\begin{definition}[Vector Space]
A vector space over a field $F$ is a set $V$ together with two operations...
\labdef{vector-space}
\end{definition}

\sidenote{This definition is fundamental to linear algebra.}

\begin{theorem}[Basis Theorem]
Every vector space has a basis.
\labthm{basis}
\end{theorem}

\begin{proof}
We use Zorn's lemma\sidecite{zorn1935}.
\end{proof}

% Reference the theorem
As shown in \refthm{basis}, every vector space has a basis.

\begin{marginfigure}
\includegraphics[width=\linewidth]{vector-space-diagram.pdf}
\caption{Vector space illustration}
\labfig{vector-diagram}
\end{marginfigure}

\chapter{Advanced Topics}
\labch{advanced}

This chapter builds on \refch{basics}.

\pagelayout{wide}
\addpart{Applications}
\pagelayout{margin}

\chapter{Real-World Applications}

\backmatter
\printbibliography[heading=bibintoc,title=References]
\printglossary[title=Glossary]
\printindex

\end{document}
```

### Technical Report Template
```latex
\documentclass[
    a4paper,
    fontsize=11pt,
    twoside=false,
    open=any,
]{kaobook}

\usepackage[english]{babel}
\usepackage{kaobiblio}
\usepackage{kaotheorems}
\usepackage{kaorefs}

% Code listings
\usepackage{listings}
\lstset{style=kaolst}

% Bibliography
\addbibresource{report.bib}

\title{Technical Report}
\subtitle{Project Analysis and Results}
\author{Research Team}
\date{\today}

\begin{document}

\frontmatter
\maketitle

\begin{abstract}
This report presents the results of our analysis...
\end{abstract}

\tableofcontents

\mainmatter
\setchapterstyle{lines}

\chapter{Introduction}
\labch{intro}

\marginnote{Project started in January 2024}
This project aims to analyze...

\chapter{Methodology}
\labch{methods}

We used the following approach\sidenote{Detailed protocols are in the appendix}:

\begin{enumerate}
\item Data collection
\item Statistical analysis  
\item Validation
\end{enumerate}

\begin{marginfigure}
\includegraphics[width=\linewidth]{methodology-flow.png}
\caption{Analysis workflow}
\labfig{workflow}
\end{marginfigure}

\chapter{Results}
\labch{results}

\reffig{main-results} shows the primary findings.

\begin{figure}[h]
\centering
\includegraphics[width=0.8\textwidth]{results-plot.pdf}
\caption{Main experimental results}
\labfig{main-results}
\end{figure}

\begin{table}[h]
\centering
\caption{Summary statistics}
\begin{tabular}{lcc}
\toprule
Metric & Value & Error \\
\midrule
Accuracy & 94.2\% & ±1.3\% \\
Precision & 91.8\% & ±2.1\% \\
\bottomrule
\end{tabular}
\labtab{stats}
\end{table}

Statistical significance was confirmed\sidecite{statistical-methods-2023}.

\chapter{Discussion}

The results in \refch{results} indicate...

\appendix
\chapter{Detailed Protocols}

\begin{marginlisting}
\begin{lstlisting}[language=Python]
# Data processing script
import pandas as pd
import numpy as np

def process_data(filename):
    data = pd.read_csv(filename)
    return data.groupby('category').mean()
\end{lstlisting}
\caption{Data processing code}
\end{marginlisting}

\backmatter
\printbibliography[heading=bibintoc]

\end{document}
```

### Multilingual Book Template
```latex
\documentclass[
    a4paper,
    fontsize=10pt,
    twoside=true,
]{kaobook}

% Language setup
\usepackage[italian,english]{babel}
\usepackage{kaobiblio}
\usepackage{kaotheorems}
\usepackage{kaorefs}

% Bibliography
\addbibresource{references.bib}

\title{Multilingual Document}
\author{Author Name}

\begin{document}

\frontmatter
\maketitle
\tableofcontents

\mainmatter

\chapter{English Chapter}
This chapter is in English\sidenote{English sidenote}.

\begin{theorem}
This theorem is stated in English.
\end{theorem}

See \refthm{italian-theorem} for the Italian version.

\selectlanguage{italian}
\chapter{Capitolo Italiano}
\labch{capitolo-italiano}

Questo capitolo è in italiano\sidenote{Nota a margine in italiano}.

\begin{theorem}[Teorema Principale]
Questo teorema è enunciato in italiano.
\labthm{italian-theorem}
\end{theorem}

Vedi \refch{capitolo-italiano} per riferimenti.

\selectlanguage{english}

\backmatter
\printbibliography

\end{document}
```

### Customized Layout Template
```latex
\documentclass[a4paper,fontsize=9pt]{kaobook}

\usepackage{kaobiblio}
\usepackage[framed=true,background=yellow!5]{kaotheorems}
\usepackage{kaorefs}

% Custom colors
\usepackage{xcolor}
\definecolor{customblue}{RGB}{0,100,150}
\definecolor{customred}{RGB}{150,50,0}

% Colored headings
\addtokomafont{chapter}{\color{customblue}}
\addtokomafont{section}{\color{customblue}}
\addtokomafont{captionlabel}{\color{customred}}

% Custom hyperlink colors
\hypersetup{
    linkcolor=customblue,
    citecolor=customred,
    urlcolor=customblue,
}

% Custom margin layout
\newcommand{\narrowmarginlayout}{%
    \newgeometry{
        top=25mm,
        bottom=25mm, 
        inner=25mm,
        textwidth=120mm,
        marginparsep=5mm,
        marginparwidth=35mm,
    }%
    \recalchead%
}

% Custom chapter style
\DeclareDocumentCommand{\chapterstylecustom}{}{%
    \renewcommand*{\chapterformat}{%
        \textcolor{customblue}{\scalebox{3}{\thechapter}}%
    }%
    \renewcommand\chapterlinesformat[3]{%
        \makebox[\textwidth][c]{%
            ##2 \quad ##3%
        }%
        \\[1ex]
        \textcolor{customblue}{\rule{\textwidth}{1pt}}%
    }%
}

\title{Customized KaoBook}
\author{Designer}

\begin{document}

\frontmatter
\maketitle
\tableofcontents

\mainmatter
\setchapterstyle{custom}
\narrowmarginlayout

\chapter{Custom Design}

This document demonstrates customization\sidenote{\color{customred}Custom sidenote color}.

\begin{theorem}
Custom theorem with yellow background.
\end{theorem}

\backmatter
\printbibliography

\end{document}
```

These templates provide starting points for different types of documents. Customize them according to your specific needs by:

1. Adjusting class options and package settings
2. Modifying colors and fonts
3. Adding or removing chapters and sections
4. Customizing theorem environments and boxes
5. Adapting the bibliography and citation style
6. Tweaking the page layout and margins

Remember to compile with the full sequence (pdflatex → biber → pdflatex → pdflatex) to ensure all cross-references, citations, and margin content appear correctly.

---

*This documentation covers the complete KaoBook system. For additional help, consult the official repository at https://github.com/fmarotta/kaobook or visit the LaTeX Templates page at https://www.latextemplates.com/template/kaobook.*