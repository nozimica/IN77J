CN=in77j

TEXNAME=$(CN)
TEXCOMM=xelatex -halt-on-error
#TEXCOMM=pdflatex -halt-on-error

default: $(TEXNAME).pdf

$(TEXNAME).pdf: $(TEXNAME).tex in77j.sty $(TEXNAME)*.tex tex/*.tex
	$(HOME)/.cabal/bin/pandoc -f markdown tex/1.01.md.tex -t beamer -o tex/1.01.tex
	$(TEXCOMM) -no-pdf $(TEXNAME).tex && rm -f $(TEXNAME).xdv
	bibtex $(TEXNAME)
	# $(TEXCOMM) -interaction=batchmode $(TEXNAME).tex
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
