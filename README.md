# Ocgformfields ⚠️This library actually doesn’t work

[![Codacy Badge](https://app.codacy.com/project/badge/Grade/25dae195d0b34eb08b218faab93076ad)](https://app.codacy.com/gh/R0mb0/Ocgformfields/dashboard?utm_source=gh&utm_medium=referral&utm_content=&utm_campaign=Badge_grade)
[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://github.com/R0mb0/Ocgformfields)
[![Open Source Love svg3](https://badges.frapsoft.com/os/v3/open-source.svg?v=103)](https://github.com/R0mb0/Ocgformfields)
[![MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/license/mit)
[![Donate](https://img.shields.io/badge/PayPal-Donate%20to%20Author-blue.svg)](http://paypal.me/R0mb0)

PDF fields (AcroForm) natively associated with OCG (layers) via the `/OC` key in the annotation dictionary, with dynamic toggling of the layer state. Target: pdfLaTeX + Adobe Acrobat/Reader.

## 🧩 Features
- Native binding of fields to layers: adds `/OC <ref>` to the widget dictionary.
- Dynamic layer toggle via `/SetOCGState` action.
- Simple API:
  - `ocgform` (environment): defines the OCG context for fields.
  - `\OCGTextField` (command): text field bound to the current OCG.
  - `\OCGToggle` and `\OCGToggleButton`: link/button to show/hide dynamically.
 
## ✅ Requirements
- Engine: pdfLaTeX
- Viewer: Adobe Acrobat/Reader (other apps may ignore `/OC` on annotations)
- LaTeX packages: `hyperref`, `ocgx2`, `acrotex` (provides `eforms`), `xparse`, `l3packages`

### 💻 `On MiKTeX, install packages via MiKTeX Console (Packages): “acrotex”, “ocgx2”. `

## Installation 🛠️
- Local (same folder as the `.tex`):
  - `\usepackage{./ocgformfields}` (harmless warning about name difference).
- MiKTeX TEXMFHOME (persistent):
  - Create: `C:\Users\<user>\texmf\tex\latex\ocgformfields\ocgformfields.sty`
  - MiKTeX Console → Settings → Directories → Add… add `C:\Users\<user>\texmf`
  - Tasks → Refresh file name database
  - Verify: `kpsewhich ocgformfields.sty`
 
## Quick start 🚀
```latex
\documentclass{article}
\usepackage[a4paper,margin=2.5cm]{geometry}

\usepackage{hyperref}
\usepackage{ocgx2}
\usepackage{eforms}
\usepackage{ocgformfields}

\begin{document}

\OCGToggle{sens}{\textbf{Show/Hide sensitive data}}

\begin{ocgform}{Sensitive Data}{sens}{on}
  Name: \OCGTextField[name=name,width=8cm]{}\\
  Email: \OCGTextField[name=email,width=8cm]{}
\end{ocgform}

\medskip
\OCGToggleButton{sens}{Toggle Sensitive Data}

\end{document}
```
