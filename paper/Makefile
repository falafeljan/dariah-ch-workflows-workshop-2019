pdf:
	latexmk -pdf paper.tex

clean:
	latexmk -C

test:
	pdfx paper.pdf -c

stats:
	wc -w paper.md

.PHONY: pdf clean test stats
