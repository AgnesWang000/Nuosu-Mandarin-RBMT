Sichuan Yi and Chinese: `apertium-iii-zho`
===============================================================================

This is an Apertium language pair for translating between Sichuan Yi and
Chinese. What you can use this language package for:

* Translating between Sichuan Yi and Chinese
* Morphological analysis of Sichuan Yi and Chinese
* Part-of-speech tagging of Sichuan Yi and Chinese

For information on the latter two points, see subheading "For more
information" below.

Requirements
-------------------------------------------------------------------------------

You will need the following software installed:

* autoconf
* automake
* pkg-config
* lttoolbox (>= 3.5.1)
* apertium (>= 3.6.1)
* vislcg3 (>= 1.3.1)
* hfst (>= 3.15.1)
* apertium-iii
* apertium-zho

If this does not make any sense, we recommend you look at: apertium.org.

Compiling
-------------------------------------------------------------------------------

Given the requirements being installed, you should be able to just run:

```console
$ autoreconf -fvi
$ ./configure
$ make
# make install
```

You can use `./autogen.sh` instead of `autoreconf` and `./configure` in case you're compiling
from source. If you installed any prerequisite language packages using a
`--prefix` with `./configure`, make sure to use the same `--prefix` when running
`./configure` here.

If any of this doesn't make sense or doesn't work, see https://wiki.apertium.org/wiki/Install_language_data_by_compiling

Testing
-------------------------------------------------------------------------------

If you are in the source directory after running make, the following
commands should work:

```console
$ echo "TODO test sentence 1" | apertium -d . iii-zho
TODO test translated sentence 1

$ echo "TODO test sentence 2" | apertium -d . zho-iii
TODO test translated sentence 2
```

After installing somewhere in `$PATH`, you should be able to do e.g.

```console
$ echo "TODO test sentence 1" | apertium iii-zho
TODO test translated sentence 1
```

Files and data
-------------------------------------------------------------------------------

* [`apertium-iii-zho.iii-zho.dix`](apertium-iii-zho.iii-zho.dix) - Bilingual dictionary
* [`apertium-iii-zho.iii-zho.rtx`](apertium-iii-zho.iii-zho.rtx) - Structural transfer rules for translating into Chinese
* [`apertium-iii-zho.zho-iii.rtx`](apertium-iii-zho.zho-iii.rtx) - Structural transfer rules for translating into Sichuan Yi
* [`apertium-iii-zho.iii-zho.lrx`](apertium-iii-zho.iii-zho.lrx) - Lexical selection rules for translating into Chinese
* [`apertium-iii-zho.zho-iii.lrx`](apertium-iii-zho.zho-iii.lrx) - Lexical selection rules for translating into Sichuan Yi
* [`modes.xml`](modes.xml) - Translation modes

For more information
-------------------------------------------------------------------------------

* https://wiki.apertium.org/wiki/Installation
* https://wiki.apertium.org/wiki/apertium-iii-zho
* https://wiki.apertium.org/wiki/Using_an_lttoolbox_dictionary

Help and support
-------------------------------------------------------------------------------

If you need help using this language pair or data, you can contact:

* Mailing list: apertium-stuff@lists.sourceforge.net
* IRC: `#apertium` on irc.oftc.net (irc://irc.oftc.net/#apertium)

See also the file [`AUTHORS`](AUTHORS), included in this distribution.

More documentations
-------------------------------------------------------------------------------
Refer to our wiki page for more detailed documentations

Nuosu-Mandarin Main Page

https://wikis.swarthmore.edu/ling073/Nuosu_and_Mandarin

Lexical Selection

https://wikis.swarthmore.edu/ling073/Nuosu_and_Mandarin/Lexical_selection

Contrastive Grammar

https://wikis.swarthmore.edu/ling073/Nuosu_and_Mandarin/Contrastive_grammar

Structural Transfer

https://wikis.swarthmore.edu/ling073/Nuosu_and_Mandarin/Structural_transfer

Final Updates & Evaluation

https://wikis.swarthmore.edu/ling073/Nuosu_and_Mandarin/Final_Project
