all: 01_TextProcessing.pdf

01_TextProcessing.pdf: main.tex
	make -C img
	cp main.tex 01_TextProcessing.tex
	pdflatex 01_TextProcessing.tex
	pdflatex 01_TextProcessing.tex
	rm 01_TextProcessing.tex
	
clean:
	rm -f *.aux *.log *.nav *.out *.snm *.toc *.vrb
	rm -f 01_TextProcessing.pdf 01_TextProcessing_hangout.pdf
	
cleanall:
	make clean
	make -C img clean
