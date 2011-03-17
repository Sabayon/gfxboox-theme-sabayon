POFILES	= $(wildcard *.po)
TEXTS	= $(addsuffix .tr,$(basename $(wildcard *.po)))
NLSPACKAGE = bootloader
MSGMERGE = intltool-update -x --gettext-package=$(NLSPACKAGE) --dist

all: text.inc $(TEXTS)


refresh-po:
	catalogs='$(POFILES)'; \
	for cat in $$catalogs; do \
		lang=`basename $$cat .po`; \
		cp $$lang.po $$lang.old.po; \
		if $(MSGMERGE) $$lang ; then \
			rm -f $$lang.old.po ; \
			echo "$(MSGMERGE) of $$lang succeeded" ; \
		else \
			echo "$(MSGMERGE) of $$lang failed" ; \
			mv $$lang.old.po $$lang.po ; \
		fi \
	done

%.tr: %.po text.inc
	bin/po2txt $< >$@

# en.tr uses msgids from bootloader.pot
en.tr text.inc: bootloader.pot
	bin/po2txt $< >en.tr

clean:
	rm -f text.inc *.tr *~
