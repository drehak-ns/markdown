.PHONY: all clean

AUXFILES=*.tmp *.tui *.tuo *.mp *.tuc *.markdown.in *.markdown.out \
  *.markdown.lua *.log *.aux *.dvi *.idv *.lg *.tmp *.xref *.4ct *.4tc \
  latex-pdftex.tex latex-xetex.tex latex-luatex.tex latex-tex4ht.tex \
	example.tex
AUXDIRS=_markdown_*/
LUACLI_OPTIONS=cacheDir=_markdown_example hashEnumerators=true \
  definitionLists=true footnotes=true inlineFootnotes=true \
  smartEllipses=true fencedCode=true contentBlocks=true pipeTables=true \
  tableCaptions=true taskLists=true
OUTPUT=context-mkii.pdf context-mkiv.pdf latex-pdftex.pdf \
  latex-luatex.pdf latex-xetex.pdf latex-tex4ht.html latex-tex4ht.css

# This is the default pseudo-target.
all: $(OUTPUT)
	$(MAKE) clean

# This target typesets the ConTeXt example using the Mark II format.
context-mkii.pdf: context-mkii.tex example.tex
	texexec --passon="--shell-escape --8bit" context-mkii.tex

# This target typesets the ConTeXt example using the Mark IV format.
context-mkiv.pdf: context-mkiv.tex example.tex
	context context-mkiv.tex

# This target typesets the LaTeX example using the pdfTeX engine.
latex-pdftex.pdf: latex.tex example.tex
	cp latex.tex latex-pdftex.tex
	pdflatex --shell-escape latex-pdftex
	pdflatex --shell-escape latex-pdftex

# This target typesets the LaTeX example using the XeTeX engine.
latex-xetex.pdf: latex.tex example.tex
	cp latex.tex latex-xetex.tex
	xelatex --shell-escape --8bit latex-xetex
	xelatex --shell-escape --8bit latex-xetex

# This target typesets the LaTeX example using the LuaTeX engine.
latex-luatex.pdf: latex.tex example.tex
	cp latex.tex latex-luatex.tex
	lualatex latex-luatex
	lualatex latex-luatex

# This target typesets the LaTeX example using TeX4ht.
latex-tex4ht.html latex-tex4ht.css: latex.tex example.tex
	cp latex.tex latex-tex4ht.tex
	# TODO: Replace with `make4ht --shell-escape latex fn-in` in TeX Live 2020.
	htlatex latex-tex4ht "xhtml,fn-in,html5,charset=utf-8" " -cunihtf -utf8" '' -shell-escape
	htlatex latex-tex4ht "xhtml,fn-in,html5,charset=utf-8" " -cunihtf -utf8" '' -shell-escape

# This target converts the markdown example to a plain TeX representation
# using the Lua command-line interface for the Markdown package.
example.tex: example.md
	texlua "`kpsewhich -a markdown-cli.lua | head -n 1`" $(LUACLI_OPTIONS) -- $< $@

# This pseudo-target removes any existing auxiliary files and directories.
clean:
	rm -f $(AUXFILES)
	rm -rf $(AUXDIRS)

# This pseudo-target removes any makeable files.
implode: clean
	rm -f $(OUTPUT)
