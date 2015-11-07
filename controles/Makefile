CN=02

TEXNAME=e$(CN)
TEXCOMM=pdflatex -halt-on-error

default: $(TEXNAME).pdf

$(TEXNAME).pdf: clean $(TEXNAME).tex in77j.exercise.sty
	echo '\\answerstrue' > flags.tex
	$(TEXCOMM) -no-pdf $(TEXNAME).tex && rm -f $(TEXNAME).xdv
	$(TEXCOMM) $(TEXNAME).tex
	$(TEXCOMM) $(TEXNAME).tex
	mv $(TEXNAME).pdf $(TEXNAME).pauta.pdf
	> flags.tex
	$(TEXCOMM) $(TEXNAME).tex
	$(TEXCOMM) $(TEXNAME).tex
	$(MAKE) reduce

clean:
	rm -f *.aux *.blg *.log *.toc *.lot *.lof *.bbl *.nav *.out *.snm *.vrb *.xdv

complete: clean
	$(TEXCOMM) $(TEXNAME).tex
	$(TEXCOMM) $(TEXNAME).tex

reduce:
	gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dNOPAUSE -dQUIET -dBATCH \
		-sOutputFile=$(TEXNAME)-reduc.pdf $(TEXNAME).pdf
	gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dNOPAUSE -dQUIET -dBATCH \
		-sOutputFile=$(TEXNAME).pauta-reduc.pdf $(TEXNAME).pauta.pdf

runEditor:
	@test -s ~/.local/bin/when-changed && xterm -e ~/.local/bin/when-changed $(TEXNAME).tex -c make &
	vim $(TEXNAME).tex

compileLive:
	@test -s ~/.local/bin/when-changed && ~/.local/bin/when-changed $(TEXNAME).tex -c make
