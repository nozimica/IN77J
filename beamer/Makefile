CN=in77j

# export TEXINPUTS:=.:./texmf:~/texmf:${TEXINPUTS}
export TEXMFHOME:=.:./texmf:~/texmf:${TEXMFHOME}

TEXNAME=$(CN)
TEXCOMM=xelatex -halt-on-error
#TEXCOMM=pdflatex -halt-on-error
PANDOC=$(HOME)/.cabal/bin/pandoc -f markdown --slide-level=3

default: $(TEXNAME).pdf

$(TEXNAME).pdf: $(TEXNAME).tex in77j.sty $(TEXNAME)*.tex tex/*.tex
	$(PANDOC) tex/1.01.md.tex -t beamer -o tex/1.01.tex
	$(PANDOC) tex/1.02.md.tex -t beamer -o tex/1.02.tex
	$(PANDOC) tex/1.03.md.tex -t beamer -o tex/1.03.tex
	$(TEXCOMM) -no-pdf $(TEXNAME).tex && rm -f $(TEXNAME).xdv
	bibtex $(TEXNAME)
	$(TEXCOMM) -interaction=batchmode $(TEXNAME).tex
	$(TEXCOMM) $(TEXNAME).tex

clean:
	rm -f *.aux *.blg *.log *.toc *.lot *.lof *.bbl *.nav *.out *.snm *.vrb *.xdv

complete: clean
	$(TEXCOMM) $(TEXNAME).tex
	$(TEXCOMM) $(TEXNAME).tex

handout:
	cp -f $(TEXNAME).tex $(TEXNAME)-handout.tex
	sed -i 's:documentclass\[\(.*\)\]{beamer}:documentclass[\1,handout]{beamer}:' $(TEXNAME)-handout.tex
	$(TEXCOMM) $(TEXNAME)-handout.tex
	$(TEXCOMM) $(TEXNAME)-handout.tex
	$(TEXCOMM) $(TEXNAME)-handout.tex
	gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dNOPAUSE -dQUIET -dBATCH \
		-sOutputFile=$(TEXNAME)-handout-reduc.pdf $(TEXNAME)-handout.pdf
	#mv -f $(TEXNAME)-handout-reduc.pdf $(TEXNAME)-handout.pdf

reduce:
	gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dNOPAUSE -dQUIET -dBATCH \
		-sOutputFile=$(TEXNAME)-reduc.pdf $(TEXNAME).pdf

compileLive:
	~/.local/bin/when-changed tex/1.01.md.tex tex/1.02.md.tex tex/1.03.md.tex in77j.tex -c make

getOldPgf:
	mkdir -p texmf/tex
	rm -rf tmptikz && mkdir -p tmptikz
	wget -P tmptikz ftp://tug.org/historic/systems/texlive/2013/tlnet-final/archive/pgf.tar.xz
	tar Jxf tmptikz/pgf.tar.xz --directory tmptikz
	mv tmptikz/tex/* texmf/tex
	rm -rf tmptikz
