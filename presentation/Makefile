SRC = presentation.tex
PDF = presentation.pdf
AUX = presentation.aux
TEXC := xelatex
TEXC_OPTS += -shell-escape

.PHONY: clean

all: $(PDF)

$(AUX):
	$(TEXC) $(TEXC_OPTS) $(SRC)

$(PDF): beamerthemem.sty $(AUX) $(SRC)
	$(TEXC) $(TEXC_OPTS) $(SRC)

clean:
	@rm -f $(PDF)
