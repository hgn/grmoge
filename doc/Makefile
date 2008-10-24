# $Id: Makefile 7 2007-01-17 22:57:49Z pfeifer $
# Copyright 2005
# Distributed under the terms of the GNU General Public License v2


OBJ = grmoge

LANG = en

OBJ_SRC = $(addsuffix .tex,$(OBJ))
OBJ_PDF = $(addsuffix .pdf,$(OBJ))
OBJ_PS  = $(addsuffix .ps,$(OBJ))
OBJ_DVI = $(addsuffix .dvi,$(OBJ))
OBJ_AUX = $(addsuffix .aux,$(OBJ))
OBJ_GLO = $(addsuffix .glo,$(OBJ))
OBJ_GLS = $(addsuffix .gls,$(OBJ))

all: $(OBJ_PDF)
pdf: $(OBJ_PDF)
ps:  $(OBJ_PS)
dvi: $(OBJ_DVI)

$(OBJ_DVI): $(OBJ_SRC) $(STYL)
	make -f figures/Makefile all
	latex $(OBJ_SRC)
	bibtex $(OBJ_AUX) || true
	latex $(OBJ_SRC)
	latex $(OBJ_SRC)

$(OBJ_PS): $(OBJ_DVI)
	dvips -o${OBJ_PS} $(OBJ_DVI)

$(OBJ_PDF): $(OBJ_SRC) $(STYL)
	make -f figures/Makefile all
	pdflatex -shell-escape -file-line-error $(OBJ_SRC)
	bibtex $(OBJ_AUX) || true
	pdflatex -shell-escape -file-line-error $(OBJ_SRC)
	pdflatex -shell-escape -file-line-error $(OBJ_SRC)

preview: $(OBJ_PDF)
	xpdf -fullscreen -papercolor white -bg black \
		 $(OBJ_PDF) 1>/dev/null 2>&1 &

spellcheck: $(OBJ_SRC)
	aspell --mode=tex --ignore=3 --lang=$(LANG) -c chapter/*.tex

clean:
	make -f figures/Makefile clean
	rm -f *.aux *.idx *.log *.out *.toc *.bbl *.blg \
		  *.dvi *.ps *.lot *.pdf *.tmp *.bak *~

.PHONY: all clean


# vim600: fdm=marker tw=120 sw=4 ts=4 sts=4 ff=unix noet:
