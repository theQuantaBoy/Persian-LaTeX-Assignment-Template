# LaTeX Assignment & Report Template (Persian)

A ready‑to‑use **XeLaTeX** template for Persian assignments and lab reports at **Sharif University of Technology** (and easily adaptable elsewhere).  
It supports **RTL/LTR** mixing, two document modes (`assignment` / `report`), pre‑included Persian fonts, code listings, Persian list environments (`ابجد`, `الفبا`), and automatic title generation.

[![MIT License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![XeLaTeX](https://img.shields.io/badge/XeLaTeX-required-green.svg)](https://tug.org/xetex/)

---

## 🚀 Quick Start

### 1. Choose your mode
Open `main.tex` and set:

```latex
\doctype{assignment}   % for problem sets
% or
\doctype{report}       % for lab/project reports
```

### 2. Fill in the metadata
All fields are already present in `main.tex`. Replace the placeholders with your own information.

**Assignment mode** uses:

```latex
\coursetitle{COURSE_TITLE}
\semester{SEMESTER}
\prof{INSTRUCTOR_NAME}
\studentname{YOUR_NAME}
\studentid{YOUR_STUDENT_ID}
\assignmenttype{ASSIGNMENT_TYPE}      % e.g., "تمرین شماره 1"
\assignmenttitle{ASSIGNMENT_TITLE}    % optional
```

**Report mode** uses:

```latex
\reportcoursename{COURSE_NAME}
\reportsemester{SEMESTER}
\reportprof{INSTRUCTOR_NAME}
\reportTS{TEACHING_ASSISTANT}         % optional
\reportgroupmembers{MEMBER1 \\ MEMBER2}
\reporttitle{REPORT_TITLE}
\reportsubtitle{SUBTITLE}             % optional (e.g., "گزارش پروژه:")
\reportdepartment{DEPARTMENT_NAME}
\reportuniversity{UNIVERSITY_NAME}
\reportenglishtitle{ENGLISH_TITLE}    % optional
```
> You can safely leave the unused block as‑is – only the active mode’s fields are used.

### 3. Write your answers
Put each answer in a separate `.tex` file inside the `answers/` folder.  
Then list them inside `main.tex` using the `\answers{}` command:

```latex
\answers{file1,file2,file3}
```

Each file will be inserted on a new page (except the first).  
Use `\question{...}` or `\question[number]{...}` to start numbered questions.

### 4. Compile

**Local compilation** (requires a full TeX distribution – TeX Live or MikTeX):
```bash
latexmk -xelatex main.tex
```

**If you enable the `minted` option** (see below), you must add `-shell-escape`:
```bash
latexmk -xelatex -shell-escape main.tex
```

> For **online editors** (Overleaf, Sharif LaTeX, etc.), make sure the compiler is set to **XeLaTeX**.

> **Need a complete TeX distribution?**  
> - TeX Live: `sudo apt install texlive-full` (Linux) or install from [tug.org/texlive](https://tug.org/texlive)  
> - MikTeX: [miktex.org](https://miktex.org) (Windows)  
> If you don’t need all packages, you can remove unused `\RequirePackage` lines from `style.sty` – but the template works best with a full distribution.

---

## 🎨 Code Listings: `listings` (default) vs `minted`

The package `style.sty` supports **two backends** for code blocks.

### Option 1: `listings` (default – no extra tools)
- Works without `-shell-escape`
- Available on all LaTeX installations
- To use: simply do nothing (the package defaults to `listings`)

### Option 2: `minted` (more syntax highlighting)
Add the `[minted]` option when loading the package in `main.tex`:
```latex
\usepackage[minted]{commons/style}
```
Then compile with:
```bash
latexmk -xelatex -shell-escape main.tex
```
**Requirements**:
- Python installed
- Pygments: `pip install pygments`
- `-shell-escape` enabled

> We recommend `listings` for simplicity unless you need the extra highlighting capabilities of `minted`.

---

## 💻 VS Code + LaTeX Workshop Setup

Add the following **LaTeX‑related** settings to your `settings.json` (the rest of your regular VS Code settings can stay).

```json
{
    "latex-workshop.latex.tools": [
        {
            "name": "xelatexmk",
            "command": "latexmk",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-xelatex",
                "-shell-escape",
                "-outdir=%OUTDIR%",
                "%DOC%"
            ]
        }
    ],
    "latex-workshop.latex.recipes": [
        {
            "name": "xelatex ➞ build",
            "tools": ["xelatexmk"]
        }
    ],
    "latex-workshop.latex.outDir": "./build"
}
```

**Explanation**:
- `xelatexmk` uses `latexmk` with XeLaTeX and allows `-shell-escape` (required for `minted`).
- Output directory is set to `./build` to keep your project clean.
- The recipe `xelatex ➞ build` will appear in the LaTeX Workshop sidebar.

---

## 🏫 Use Online

You can use this template directly in the Sharif University online LaTeX editor [here](https://latex.sharif.edu/read/qdhgndghvrsv).  
Make sure the compiler is set to **XeLaTeX**.

---

## 📝 Template Features

- **Two modes** – assignment (single student) and report (group members, course info).
- **Automatic title generation** – call `\MakeFrontMatter` after filling metadata.
- **RTL/LTR support** – use `\lr{...}` for inline Latin text.
- **Custom Persian lists** – `\begin{ابجد} ... \end{ابجد}` and `\begin{الفبا} ... \end{الفبا}`.
- **Question command** – `\question{...}` steps a counter; reset with `\resetquestions`.
- **Math shortcuts** – `\IN`, `\IR`, `\set{...}`, `\floor{...}`, `\ceil{...}`, etc.
- **Missing image placeholder** – if a graphic is not found, a box with the filename is shown (helpful for sharing).
- **Tuned spacing** – for Persian text, displays, and footnotes.

---

## 🙏 Acknowledgements

- Based on the Sharif University of Technology LaTeX template – [direct download link](https://latex.sharif.edu/latex/templates/639854882581e80097d08105/zip)
- Inspired by repositories by [MoeeinAali](https://github.com/MoeeinAali)
