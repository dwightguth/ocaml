CFLAGS=-g -O

all: texquote2 transf htmlquote htmlgen dvi2txt caml-tex2

dvi2txt:
	cd dvi_to_txt; ${MAKE}

transf: transf.cmo htmltransf.cmo transfmain.cmo
	ocamlc -o transf -g transf.cmo htmltransf.cmo transfmain.cmo

transf.ml: transf.mll
	ocamllex transf.mll

htmltransf.ml: htmltransf.mll
	ocamllex htmltransf.mll

htmlgen: latexmacros.cmo latexscan.cmo latexmain.cmo
	ocamlc -o htmlgen -g latexmacros.cmo latexscan.cmo latexmain.cmo

latexscan.ml: latexscan.mll
	ocamllex latexscan.mll

caml-tex2: caml_tex2.cmo
	ocamlc -o caml-tex2 str.cma unix.cma caml_tex2.cmo
#	ocamlc -custom -o caml-tex2 str.cma unix.cma caml-tex2.cmo \
#		-cclib -lunix -cclib -lstr

.SUFFIXES:
.SUFFIXES: .ml .cmo .mli .cmi .c

.ml.cmo:
	ocamlc -c $<

.mli.cmi:
	ocamlc -c $<

.c:
	$(CC) $(CFLAGS) -o $@ $<

clean:
	rm -f transf.ml latexscan.ml htmltransf.ml
	rm -f texquote2 transf htmlquote htmlgen dvi2txt
	rm -f transf.ml latex.ml
	rm -f *.o *.cm? *.cmxa
	rm -f *~ #*#
	cd dvi_to_txt; ${MAKE} clean

latexmacros.cmo: latexmacros.cmi 
latexmain.cmo: latexscan.cmo 
latexscan.cmo: latexmacros.cmi 
transfmain.cmo: transf.cmo htmltransf.cmo 
