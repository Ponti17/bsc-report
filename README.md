# Welcome to the Large Latex Document Template

## Guide
The main.tex serves 1 purpose:

That is to "activate" the individual sections in the correct order.

git gud

## Useful things
### Keybinds (keybinds.json):
```
[
//------------ Latex related commands: -------------
    { // Bold highlighted text
        "key": "ctrl+b b",
        "command": "editor.action.insertSnippet",
        "when": "editorLangId == 'latex'",
        "args": {
            "snippet": "\\textbf{$TM_SELECTED_TEXT}",
        }
    },
    { // Begin figur
        "key": "ctrl+b f",
        "command": "editor.action.insertSnippet",
        "when": "editorLangId == 'latex'",
        "args": {
            "snippet": "\\begin{figure}[htp]\n\\centering\n\\includegraphics[width=3cm]{$ImagePath}\n\\end{figure}"
        }
    },
    { //Begin bulleted list
        "key": "ctrl+b i",
        "command": "editor.action.insertSnippet",
        "when": "editorLangId == 'latex'",
        "args": {
            "snippet": "\\begin{itemize}\n\\item \n\\end{itemize}"
        }
    },
    { //Begin numbered list
        "key": "ctrl+b n",
        "command": "editor.action.insertSnippet",
        "when": "editorLangId == 'latex'",
        "args": {
            "snippet": "\\begin{enumerate}\n\\item \n\\end{enumerate}"
        }
    },
    { //Begin code snippet
        "key": "ctrl+b c",
        "command": "editor.action.insertSnippet",
        "when": "editorLangId == 'latex'",
        "args": {
            "snippet": "\\noindent JSON formatted body:\n\\begin{lstlisting}[language=json,firstnumber=1]\n$code\n\\end{lstlisting}"
        }
    },
    { //Begin table
        "key": "ctrl+b t",
        "command": "editor.action.insertSnippet",
        "when": "editorLangId == 'latex'",
        "args": {
            "snippet": "\\begin{center}\n\\begin{tabularx}{1\\textwidth} {\n| >{\\centering\\arraybackslash}X\n| >{\\centering\\arraybackslash}X\n| >{\\centering\\arraybackslash}X\n| }\n\\hline\n\\bf{$Item1} & \\bf{$Item2} & \\bf{$Item3}\\\\\\\n\\hline\nText1 & Text2 & Text3\\\\\\\n\\hline\n\\end{tabularx}\n\\end{center}"
        }
    },
    { // Emphazise 
        "key": "ctrl+b e",
        "command": "editor.action.insertSnippet",
        "when": "editorLangId == 'latex'",
        "args": {
            "snippet": "\\emph{$TM_SELECTED_TEXT}"
        }
    },
    { // Emphasize highlighted text
        "key": "ctrl+n i",
        "command": "editor.action.insertSnippet",
        "when": "editorLangId == 'latex'",
        "args": {
            "snippet": "\\noindent "
        }
    },
    { // Begin double underlined
        "key": "ctrl+b u",
        "command": "editor.action.insertSnippet",
        "when": "editorLangId == 'latex'",
        "args": {
            "snippet": "\\uline{\\uline{$TM_SELECTED_TEXT}}"
        }
    },
    { // Begin URL (deprecated)
        "key": "ctrl+r u",
        "command": "editor.action.insertSnippet",
        "when": "editorLangId == 'latex'",
        "args": {
            "snippet": "\\noindent \\textbf{Request URL:}<API-URL>/{$Text1}\\\\\\"
        }
    },
    { // Begin indexed dagger symbol (deprecated)
        "key": "ctrl+b d",
        "command": "editor.action.insertSnippet",
        "when": "editorLangId == 'latex'",
        "args": {
            "snippet": "$\\dagger_{$Index}$"
        }
    },
    { // Insert equation
        "key": "ctrl+b m",
        "command": "editor.action.insertSnippet",
        "when": "editorLangId == 'latex'",
        "args": {
            "snippet": "\\begin{equation}\\label{$LabelName} \n$insert_equation_here\n\\end{equation}"
        }
    },
    { // Build latex file if editor lang is latex
        "key": "ctrl+enter",
        "command": "latex-workshop.build",
        "when": "editorLangId == 'latex'"
    },
    { // Find location on pdf
        "key": "ctrl+shift+enter",
        "command": "latex-workshop.synctex",
        "when": "editorLangId == 'latex'"
    }
]
```
### Settings (settings.json)
```
//Point auxiliary files to a build folder:
"latex-workshop.latex.outDir": "%WORKSPACE_FOLDER%\\Build",

//Added support for minted latex.
"latex-workshop.latex.tools": [
  {
    "name": "latexmk",
    "command": "latexmk",
    "args": [
      "-shell-escape",
      "-synctex=1",
      "-interaction=nonstopmode",
      "-file-line-error",
      "-pdf",
      "-outdir=%OUTDIR%",
      "%DOC%"
    ],
    "env": {}
  }
],
```

### User snippets (latex.json)
```
{
// Begin circuitikz template
"circuit": {
		"prefix": "circuit",
		"body": [
			"\\begin{center}",
			"	\\begin{circuitikz}",
			"		%\\draw (0,0) to[american controlled current source, invert, l=label] ++(0,2);",
			"		%\\draw (0,0) node[anchor=center, circle, draw, inner sep=2pt, fill=white](){};",
			"		%\\draw (0,0) to[R, i^>=i, v_>=v] ++(2,0);",
			"		%\\draw (0,0) to[short, i=i] ++(2,2);",
			"		\\ctikzset{tripoles/pmos style/nocircle}",
			"		\\ctikzset{tripoles/mos style/arrows}",
			"	",
			"		\\draw (0, 0)",
			"		$1",
			"		node[anchor=center, circle, draw, inner sep=2pt, fill=white](){}",
			"		;",
			"	\\end{circuitikz}",
			"\\end{center}"
		],
		"description": "Insert a circuit"
	},
  // Wire connector
	"wire":{
		"prefix": "short",
		"body": [
			"to[short]"
		],
	},

  // American style source, parameters can be changed.
	"american source":{
		"prefix": "american source",
		"body": [
			"to[american controlled current source, invert, l=label]"
		],
	},

  // Creates a small white filled circle
	"circle":{
		"prefix": "circle",
		"body": [
			"node[anchor=center, circle, draw, inner sep=2pt, fill=white](){}"
		],
	},

  // Nmos transistor
	"nmos":{
		"prefix": "nmos transistor",
		"body": [
			"node[nmos](){}"
		],
	},

  // Pmos transistor
	"pmos":{
		"prefix": "pmos transistor",
		"body": [
			"node[pmos](){}"
		],
	},

  // Ground symbol
	"ground":{
		"prefix": "ground",
		"body": [
			"node[ground](){}"
		],
	},

  // Resistor
	"resistor":{
		"prefix": "resistor",
		"body": [
			"to[R]"
		],
	},

  // Capacitor
	"capacitor":{
		"prefix": "capacitor",
		"body": [
			"to[C]"
		],
	},

  // Inductor
	"inductor":{
		"prefix": "inductor",
		"body": [
			"to[L]"
		],
	},

  // Vdd symbol (flat bar)
	"Vdd": {
		"prefix": "Vdd",
		"body": [
			"node[rground, rotate=180](){}"
		],
	},

  // Wire jump, creates a semi-circle that resembles a wire jump.
	"jump right":
	{
		"prefix": "jump right",
		"body": [
			"arc (180:0:2pt) % go left -0.072"
		],
	},

  // Wire jump, creates a semi-circle that resembles a wire jump.
	"jump left":
	{
		"prefix": "jump left",
		"body": [
			"arc (0:180:2pt) % go right +0.072"
		],
	},

  // Wire jump, creates a semi-circle that resembles a wire jump.
	"jump down":
	{
		"prefix": "jump down",
		"body": [
			"arc (90:-90:2pt) % go up +0.072"
		],
	},

  // Wire jump, creates a semi-circle that resembles a wire jump.
	"jump up":
	{
		"prefix": "jump up",
		"body": [
			"arc (-90:90:2pt) % go down -0.072"
		],
	},

  // Resize a component
	"resize components":
	{
		"prefix": "size",
		"body": [
			"/tikz/circuitikz/bipoles/length=0.5cm"
		],
	},
}
```

## kNOwN isSuES
### Build from main.tex fails

Sometimes building the root file from the main.tex will fail.

Solution: Go to one of the section pages and [ctrl]+[enter] select "Default root file".

### Minted Latex

The Python script _pygments_ that is used together with _minted_ for syntax highlighting
cannot look inside the Build folder by default - which means that it will fail.

Solution: Change the output build directory to the same folder as the workspace.
