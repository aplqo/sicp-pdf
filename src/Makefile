# Contributed by holomorph, 2013.
# Added to by Andres Raba, 2013-2015.

FIG := $(patsubst %.svg,%.pdf,$(wildcard fig/*/*.svg))
DIR := $(shell pwd)

all: sicp-blue.pdf sicp-orig.pdf

sicp-%.pdf: sicp-%.tex exercises.tex figures.tex coverpage.pdf ${FIG}
	latexmk $<;
	mv $@ ..

sicp-%.tex: preamble-%.tex sicp.texi postamble.tex texi-to-latex.pl
	./texi-to-latex.pl -o $@ -p $< sicp.texi

exercises.tex figures.tex: ex-fig-ref.pl
	./ex-fig-ref.pl -e > exercises.tex; \
	./ex-fig-ref.pl -f > figures.tex

%.pdf: %.svg
	inkscape -C -o ${DIR}/$@ ${DIR}/$< # Removed unknown option -A

clean:
	latexmk -CA

clean-all: clean
	${RM} ${FIG} sicp-orig.tex sicp-blue.tex  exercises.tex figures.tex coverpage.pdf

.PHONY: all clean clean-all
