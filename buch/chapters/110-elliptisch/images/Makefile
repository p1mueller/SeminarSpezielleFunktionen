#
# Makefile -- make images
#
# (c) 2021 Prof Dr Andreas Müller, OST Ostschweizer Fachhochschule
#
all:	lemniskate.pdf ellipsenumfang.pdf unvollstaendig.pdf rechteck.pdf \
	ellipse.pdf pendel.pdf jacobiplots.pdf jacobidef.pdf jacobi12.pdf \
	sncnlimit.pdf slcl.pdf torusschnitt.pdf kegelpara.pdf lemnispara.pdf \
	ellpolnul.pdf ellall.pdf ellselection.pdf

lemniskate.pdf:	lemniskate.tex
	pdflatex lemniskate.tex

ellipsenumfang.pdf:	ellipsenumfang.tex ekplot.tex
	pdflatex ellipsenumfang.tex

ekplot.tex:	ellipsenumfang.m
	octave ellipsenumfang.m

rechteck:	rechteck.cpp
	g++ -O -Wall -g -std=c++11 rechteck.cpp -o rechteck `pkg-config --cflags gsl` `pkg-config --libs gsl`

rechteckpfade.tex:	rechteck
	./rechteck --outfile rechteckpfade.tex

rechteck.pdf:	rechteck.tex rechteckpfade.tex
	pdflatex rechteck.tex

unvollstaendig.pdf:	unvollstaendig.tex unvollpath.tex
	pdflatex unvollstaendig.tex

unvollpath.tex:	unvollstaendig.m
	octave unvollstaendig.m

ellipse.pdf:	ellipse.tex
	pdflatex ellipse.tex

pendel.pdf:	pendel.tex
	pdflatex pendel.tex

jacobi:	jacobi.cpp
	g++ -O -Wall -g -std=c++11 jacobi.cpp -o jacobi `pkg-config --cflags gsl` `pkg-config --libs gsl`

test:	blubb.tex

blubb.tex:	jacobi
	./jacobi --umax=14 --outfile=blubb.tex blubb 0.7

jacobipaths.tex:	jacobi Makefile
	./jacobi --umax=13 --steps=200 --outfile=jacobipaths.tex \
		zero 0.00 \
		one 0.2 \
		two 0.4 \
		three 0.6 \
		four 0.8 \
		five 0.9 \
		six 0.99 \
		seven 0.999 \
		eight 0.9999 \
		nine 0.99999 \
		ten 1.0

jacobiplots.pdf:	jacobiplots.tex jacobipaths.tex
	pdflatex jacobiplots.tex

jacobidef.pdf:	jacobidef.tex
	pdflatex jacobidef.tex

jacobi12.pdf:	jacobi12.tex
	pdflatex jacobi12.tex

sncnlimit.pdf:	sncnlimit.tex
	pdflatex sncnlimit.tex

slcl:	slcl.cpp
	g++ -O -Wall -std=c++11 slcl.cpp -o slcl `pkg-config --cflags gsl` `pkg-config --libs gsl`

slcldata.tex:	slcl
	./slcl --outfile=slcldata.tex --a=0 --b=13.4 --steps=200
slcl.pdf:	slcl.tex slcldata.tex
	pdflatex slcl.tex

KEGELSIZE = -W256 -H256
KEGELSIZE = -W128 -H128
KEGELSIZE = -W1080 -H1080
kegelpara.png:	kegelpara.pov
	povray +A0.1 $(KEGELSIZE) -Okegelpara.png kegelpara.pov

kegelpara.jpg:	kegelpara.png Makefile
	convert -extract 1080x1040+0+0 kegelpara.png \
		-density 300 -units PixelsPerInch kegelpara.jpg

kegelpara.pdf:	kegelpara.tex kegelpara.jpg
	pdflatex kegelpara.tex

torusschnitt.png:	torusschnitt.pov
	povray +A0.1 -W1920 -H1080 -Otorusschnitt.png torusschnitt.pov

torusschnitt.jpg:	torusschnitt.png Makefile
	convert -extract 1640x1080+140+0 torusschnitt.png \
		-density 300 -units PixelsPerInch torusschnitt.jpg

torusschnitt.pdf:	torusschnitt.tex torusschnitt.jpg
	pdflatex torusschnitt.tex

lemnispara:	lemnispara.cpp
	g++ -O2 -Wall -g -o lemnispara `pkg-config --cflags gsl`	\
		lemnispara.cpp `pkg-config --libs gsl`

lemnisparadata.tex:	lemnispara
	./lemnispara

lemnispara.pdf:	lemnispara.tex lemnisparadata.tex
	pdflatex lemnispara.tex

ltest:	lemnispara.pdf

ellpolnul.pdf:	ellpolnul.tex ellcommon.tex
	pdflatex ellpolnul.tex
ellall.pdf:	ellall.tex ellcommon.tex
	pdflatex ellall.tex

rechteckpfade2.tex:	rechteck Makefile
	./rechteck --outfile rechteckpfade2.tex --k 0.87 --vsteps=1
ellselection.pdf:	ellselection.tex rechteckpfade2.tex
	pdflatex ellselection.tex

rechteckpfade3.tex:	rechteck
	./rechteck --outfile rechteckpfade3.tex --k 0.70710678118654752440 \
		--vsteps=4
