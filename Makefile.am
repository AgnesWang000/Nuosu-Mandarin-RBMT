###############################################################################
## Makefile for Sichuan Yi--Chinese
###############################################################################

LANG1=iii
L1SCRIPT1=Lat
L1SCRIPT2=Yi
LANG2=zho
LANG1SCRIPT1=$(LANG1)@$(L1SCRIPT1)
LANG1SCRIPT2=$(LANG1)@$(L1SCRIPT2)
PREFIX1=$(LANG1)-$(LANG2)
PREFIX2=$(LANG2)-$(LANG1)

BASENAME=apertium-$(PREFIX1)

TARGETS_COMMON =		\
	$(PREFIX1).automorf.bin	\
	$(PREFIX1).prob		\
	$(PREFIX1).rlx.bin	\
	$(PREFIX1).autobil.bin	\
	$(PREFIX1).autolex.bin	\
	$(PREFIX1).autogen.bin	\
	$(PREFIX1).autopgen.bin	\
	$(PREFIX1).rtx.bin	\
	$(PREFIX2).automorf.bin	\
	$(PREFIX2).prob		\
	$(PREFIX2).rlx.bin	\
	$(PREFIX2).autobil.bin	\
	$(PREFIX2).autolex.bin	\
	$(PREFIX2).autogen.bin	\
	$(PREFIX2).autopgen.bin	\
	$(PREFIX2).rtx.bin \
	$(LANG1SCRIPT2)-$(LANG2).autotok.hfst

# This include defines goals for install-modes, .deps/.d, autobil.prefixes and .mode files:
@ap_include@

###############################################################################
## Monolingual transducers
###############################################################################



# -------------------
# Sichuan Yi analysis:
# -------------------

.deps/$(PREFIX1).autobil.prefixes: $(PREFIX1).autobil.bin .deps/.d
	lt-print $(PREFIX1).autobil.bin | sed 's/ /@_SPACE_@/g' > .deps/$(PREFIX1).autobil.att
	hfst-txt2fst -e ε <  .deps/$(PREFIX1).autobil.att > .deps/$(PREFIX1).autobil.hfst
	hfst-project -p upper .deps/$(PREFIX1).autobil.hfst > .deps/$(PREFIX1).autobil.upper
	echo " ?* " | hfst-regexp2fst > .deps/any-symbol.hfst
	hfst-concatenate -1 .deps/$(PREFIX1).autobil.upper -2 .deps/any-symbol.hfst -o .deps/$(PREFIX1).autobil.prefixes

.deps/$(LANG1).automorf.hfst: $(AP_SRC1)/$(LANG1).automorf.att.gz .deps/.d
	$(ZCAT) $< | hfst-txt2fst > $@

.deps/$(LANG1).automorf.bin: $(AP_SRC1)/$(LANG1).automorf.att.gz .deps/.d
	@$(ZCAT) $< > $@.att
	lt-comp lr $@.att $@
	@rm $@.att

$(PREFIX1).automorf.bin: .deps/$(LANG1).automorf.hfst .deps/$(PREFIX1).autobil.prefixes
	hfst-compose-intersect -1 .deps/$(LANG1).automorf.hfst -2 .deps/$(PREFIX1).autobil.prefixes -o .deps/$(PREFIX1).automorf.trimmed
	hfst-fst2txt -i .deps/$(PREFIX1).automorf.trimmed -o .deps/$(PREFIX1).automorf.trimmed.att
	lt-comp lr .deps/$(PREFIX1).automorf.trimmed.att $@

# get tokenizer transducer for tokenizer script

$(LANG1SCRIPT2)-$(LANG2).autotok.hfst : $(AP_SRC1)/$(LANG1SCRIPT2).autotok.hfst
	cp $< $@

# -------------------
# Sichuan Yi generation:
# ---------------------

# This takes SCRIPT1 (Lat) as the target for translation to LANG1 (Yi)
# This can be changed
# Alternatively, multiple targets can be created
$(PREFIX2).autogen.hfst: $(AP_SRC1)/$(LANG1SCRIPT1).autogen.hfst
	cp $< $@


$(PREFIX2).autogen.bin: $(AP_SRC1)/$(LANG1SCRIPT1).autogen.bin
	cp $< $@

# -------------------
# Chinese analysis:
# -------------------

.deps/$(PREFIX2).autobil.prefixes: $(PREFIX2).autobil.bin .deps/.d
	lt-print $(PREFIX2).autobil.bin | sed 's/ /@_SPACE_@/g' > .deps/$(PREFIX2).autobil.att
	hfst-txt2fst -e ε <  .deps/$(PREFIX2).autobil.att > .deps/$(PREFIX2).autobil.hfst
	hfst-project -p upper .deps/$(PREFIX2).autobil.hfst > .deps/$(PREFIX2).autobil.upper
	echo " ?* " | hfst-regexp2fst > .deps/any-symbol.hfst
	hfst-concatenate -1 .deps/$(PREFIX2).autobil.upper -2 .deps/any-symbol.hfst -o .deps/$(PREFIX2).autobil.prefixes

.deps/$(LANG2).automorf.hfst: $(AP_SRC2)/$(LANG2).automorf.att.gz .deps/.d
	$(ZCAT) $< | hfst-txt2fst > $@

.deps/$(LANG2).automorf.bin: $(AP_SRC2)/$(LANG2).automorf.att.gz .deps/.d
	@$(ZCAT) $< > $@.att
	lt-comp lr $@.att $@
	@rm $@.att

$(PREFIX2).automorf.bin: .deps/$(LANG2).automorf.hfst .deps/$(PREFIX2).autobil.prefixes
	hfst-compose-intersect -1 .deps/$(LANG2).automorf.hfst -2 .deps/$(PREFIX2).autobil.prefixes -o .deps/$(PREFIX2).automorf.trimmed
	hfst-fst2txt -i .deps/$(PREFIX2).automorf.trimmed -o .deps/$(PREFIX2).automorf.trimmed.att
	lt-comp lr .deps/$(PREFIX2).automorf.trimmed.att $@

# -------------------
# Chinese generation:
# ---------------------

$(PREFIX1).autogen.hfst: $(AP_SRC2)/$(LANG2).autogen.hfst
	cp $< $@


$(PREFIX1).autogen.bin: $(AP_SRC2)/$(LANG2).autogen.bin
	cp $< $@

###############################################################################
## Tagger models
###############################################################################

$(PREFIX1).prob: $(AP_SRC1)/$(LANG1).prob
	cp $< $@

$(PREFIX2).prob: $(AP_SRC2)/$(LANG2).prob
	cp $< $@

###############################################################################
## Disambiguation rules
###############################################################################


$(PREFIX1).rlx.bin: $(AP_SRC1)/apertium-$(LANG1).$(LANG1).rlx
	cg-comp $< $@


$(PREFIX2).rlx.bin: $(AP_SRC2)/apertium-$(LANG2).$(LANG2).rlx
	cg-comp $< $@

###############################################################################
## Bilingual dictionaries
###############################################################################

$(PREFIX1).autobil.bin: $(BASENAME).$(PREFIX1).dix
	apertium-validate-dictionary $<
	lt-comp lr $< $@

$(PREFIX2).autobil.bin: $(BASENAME).$(PREFIX1).dix
	apertium-validate-dictionary $<
	lt-comp rl $< $@

###############################################################################
## Lexical selection rules
###############################################################################

$(PREFIX1).autolex.bin: $(BASENAME).$(PREFIX1).lrx
	lrx-comp $< $@

$(PREFIX2).autolex.bin: $(BASENAME).$(PREFIX2).lrx
	lrx-comp $< $@


###############################################################################
## Structural transfer rules
###############################################################################


$(PREFIX1).rtx.bin: $(BASENAME).$(PREFIX1).rtx
	rtx-comp $< $@

$(PREFIX2).rtx.bin: $(BASENAME).$(PREFIX2).rtx
	rtx-comp $< $@

###############################################################################
## Postgeneration dictionaries
###############################################################################

$(PREFIX1).autopgen.bin: $(AP_SRC2)/$(LANG2).autopgen.bin
	cp $< $@

$(PREFIX2).autopgen.bin: $(AP_SRC1)/$(LANG1).autopgen.bin
	cp $< $@

###############################################################################
## Distribution
###############################################################################

EXTRA_DIST=					\
		$(BASENAME).$(PREFIX1).lrx	\
		$(BASENAME).$(PREFIX1).dix	\
		$(BASENAME).$(PREFIX2).lrx	\
		$(BASENAME).$(PREFIX1).rtx	\
		$(BASENAME).$(PREFIX2).rtx	\
		modes.xml

###############################################################################
## Installation
###############################################################################

apertium_iii_zhodir=$(prefix)/share/apertium/$(BASENAME)/

# Files which should be installed to $(prefix)/share/apertium/$(BASENAME)/:
apertium_iii_zho_DATA=	\
	$(TARGETS_COMMON)


# All modes are created by the same goal, listing several will just give problems with make -j2
noinst_DATA=modes/$(PREFIX1).mode \
	.deps/$(LANG1).automorf.bin \
	.deps/$(LANG2).automorf.bin

install-data-local: install-modes
uninstall-local: uninstall-modes

###############################################################################
## Cleanup
###############################################################################

CLEANFILES = $(TARGETS_COMMON)
clean-local:
	-rm -rf .deps modes

###############################################################################
## Test
###############################################################################

test: all
	apertium-regtest test
