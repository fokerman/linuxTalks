# EL MAKEFILE DE SVG QUE MAKEFILEA A TODOS LOS MAKEFILES DE SVG QUE EXISTAN!
# Este makefile esta preparado para la version 0.92.4 de inkscape. Si usas una
# version mas nueva o mas vieja los nombres de los comandos de consola cambian
# Todos los svg seran convertidos a pdf, si el svg contiene capas, estas seran
# convertidas en archivos pdf distintos, indicadas por el id de la capa.
# Ademas, si hay archivos dentro de una carpeta especial denominada RECURSOS
# estos no seran convertidos a svg.

SOURCES := $(shell find . -name '*.svg' | grep -v RECURSOS)

OUTPUT := $(SOURCES:%.svg=%.pdf)
RMOUTPUT := $(SOURCES:%.svg=%*.pdf)

all: $(OUTPUT)

%.pdf: %.svg
	@if [ $$(inkscape --query-all $< | grep layer | wc -l ) = 1 ] ;\
	then \
	echo "(1) $@" ;\
		inkscape $< --without-gui --export-plain-svg=$$(basename $< .svg)-plain.svg ;\
		inkscape $$(basename $< .svg)-plain.svg --without-gui --export-pdf=$$(basename $< .svg).pdf ;\
		rm $$(basename $< .svg)-plain.svg ;\
	else \
	echo "(n) $@" ;\
		for i in $$(inkscape --query-all $< | grep layer | awk -F, '{print $$1}') ;\
		do \
		inkscape $< -jC -i $$i --without-gui --export-plain-svg=$$(basename $< .svg)-$$i.svg ;\
		inkscape $$(basename $< .svg)-$$i.svg --without-gui --export-pdf=$$(basename $< .svg)-$$i.pdf ;\
		rm $$(basename $< .svg)-$$i.svg ;\
		done ;\
		cp $$(basename $< .svg)-layer1.pdf $$(basename $< .svg).pdf ;\
	fi

clean:
	rm -f $(RMOUTPUT)
