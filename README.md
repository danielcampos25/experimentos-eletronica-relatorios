# Tutorial: configurando o LaTeX Localmente

As duas principais libs para compilar latex são:

- [MikTEX](https://miktex.org/download)
- [TEXLive](https://www.tug.org/texlive/)

## Linux

### 1. Instale o LaTeX Live

Em distribuições baseadas em Debian/Ubuntu:

```bash
sudo apt update
sudo apt install texlive-latex-extra texlive-lang-portuguese texlive-fonts-extra latexmk texlive-publishers texlive-science
```

### 2. Verifique a instalação

Execute:

```bash
pdflatex --version
```

Se o comando retornar informações sobre a versão instalada, o LaTeX está configurado corretamente.

### 3. Compile um documento

Crie um arquivo chamado `exemplo.tex`:

```latex
\documentclass{article}

\begin{document}

Olá, mundo!

\end{document}
```

Depois, execute:

```bash
pdflatex exemplo.tex
```

Isso produzirá o arquivo `exemplo.pdf`.

---

## Windows

### 1. Instale o MiKTeX ou LaTeX Live

No Windows, o **MiKTeX** é uma alternativa bastante comum ao LaTeX Live. Caso queira especificamente o LaTeX Live, baixe o instalador [oficial](https://tug.org/texlive/windows.html#install) e siga as instruções de instalação.

Durante a instalação, mantenha a opção de adicionar os executáveis ao `PATH` quando ela estiver disponível.

### 2. Verifique a instalação

Abra o **PowerShell** ou o **Prompt de Comando** e execute:

```powershell
pdflatex --version
```

Se a versão for exibida, a instalação está funcionando.

### 3. Compile um documento

Crie `exemplo.tex` com:

```latex
\documentclass{article}

\begin{document}

Olá, mundo!

\end{document}
```

No terminal, entre na pasta do arquivo e execute:

```powershell
pdflatex exemplo.tex
```

O arquivo `exemplo.pdf` será gerado na mesma pasta.

## Editor

Para editar documentos LaTeX, você pode usar editores como:

* **Visual Studio Code**, com extensões para LaTeX (LaTEX Workshop);
* **TeXstudio**;
* **Overleaf**, caso prefira trabalhar diretamente no navegador.

## Dica

No Visual Studio Code, você pode configurar `Ctrl+Enter` para compilar arquivos
LaTeX com a extensão **LaTeX Workshop**, semelhante ao overleaf. Abra `Ctrl+Shift+P`, escolha
**Preferences: Open Keyboard Shortcuts (JSON)** e adicione:

```json
{
	"key": "ctrl+enter",
	"command": "latex-workshop.build",
	"when": "editorLangId == 'latex'"
}
```

