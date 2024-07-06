.. foo documentation master file, created by
   sphinx-quickstart on Mon Mar 18 15:10:12 2013.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

sprai = single pass read accuracy improver
==============================================================

Contents
============

.. toctree::
   :maxdepth: 2

   README
   Example
   Download
   FAQ
   Contact

Changelogs
=============
2017.2.12 v0.9.9.23: dumbbell_filter.pl: use the longest subread per molecule. ec.spec: use_one_subread is 1 by default.

2017.1.14 v0.9.9.22: Contact page was updated.

2016.10.19 v0.9.9.21 check_circularity.pl: a bug was fixed. The bug is that check_circularity.pl shows circular regardless of linear when param_max_overlap_hang_len is big and start and end of a contig have a reverse overlap. (Thanks to Si for a report and code modification)

2016.10.19 v0.9.9.20 ezez4makefile_v4.pl: an error message was modified. (Thanks to Yuuki Kobayashi for a report and Tomoaki Nishiyama for code modification)

2016.8.5 v0.9.9.19: ezez_vx1.pl: use the blast_path parameter. (Thanks to Rajanikanth Govindarajulu for a report)

2016.6.19 v0.9.9.18: myrealgner.c: initial colsize was changed. (Thanks to Takahiro Bino for a report)

2016.6.3 v0.9.9.17: use_one_subread option in ec.spec: if not 0, use one subread per one molecule. (Thanks to Tomoaki Nishiyama for advice)

2016.6.1 v0.9.9.16: ezez_vx1.pl & ezez4qsub_vx1.pl: set -o pipefail was added. 

2016.5.31 v0.9.9.15: ezez4makefile_v4.pl was added. You can use Makefile when execute Sprai. See README. (Thanks to Tomoaki Nishiyama for code modifications)

2016.4.15: v0.9.9.14: -ec_only mode can be run without a spec file of Celera Assembler. (Thanks to Afif Elghraoui for a report)

2016.4.13: v0.9.9.13: myrealigner.c: dynamic memory allocation for element & col pools. (Thanks to Tomoaki Nishiyama for code modifications)

2016.4.12: v0.9.9.12: Sprai is released under MIT license. See LICENSE.txt .

2015.10.20: v0.9.9.11: nss2v_v3.c: variable max read length. (Thanks to Tomoaki Nishiyama for code modifications)

2015.10.16: v0.9.9.10: bfmt72s.c: variable max read length. bfmt72s.c & nss2v.c: refactored (Thanks to Tomoaki Nishiyama for code modifications)

2015.10.14: v0.9.9.9: bfmt72s.c: max read length 65536 -> 131072 (Thanks to Tomoaki Nishiyama for a report)

2015.9.7: v0.9.9.8: blastn -max_target_seqs 100: use less memory (Thanks to Adrian Platts for a report)

2015.7.14: v0.9.9.7: ezez_vx1.pl & ezez4qsub_vx1.pl: zcat -> gzip -d -c (Thanks to Hikoyu Suzuki for a report)

2015.7.1: v0.9.9.6: ezez_vx1.pl: around line 325, a problem that the file dfq2fq_v2.pl was being referred to without a path was fixed. (Thanks to Adrian Platts & Jeff Xing for a report)

2015.5.5: v0.9.9.5: ca_ikki_v5.pl: can be executed without uuidgen (Thanks to Adithi for a report)

2015.4.29: v0.9.9.4: ezez_vx1.pl and ezez4qsub_vx1.pl: can be executed without uuidgen (Thanks to Adithi for a report)

2015.4.28: v0.9.9.3: ezez_vx1.pl: can be executed by dash (Thanks to Peter Szovenyi for a report)

2015.2.17: v0.9.9.2: reduced the load on the SGE master daemon

2014.11.4: v0.9.9.1: adapted to P6/C4 chemistry

2014.8.31: v0.9.9: released

2014.7.26: v0.9.5.1.6 : ezez4qsub_v8.pl doesn't stop Celera Assembler on SGE. 

2014.7.7: v0.9.5.1.5 : sprai (ezez_v7.pl and ezez4qsub_v8.pl) adapt to Celera Assembler version 8.1. (Thanks to Hiroaki Sakai for a report)

2013.10.12: v0.9.5.1.3 bug fix: ezez_v7.pl does not stop after error correction and run Celera Assembler. (Thanks to Tomoko F. Shibata for a bug report)

2013.09.09: v0.9.5.1 bug fix: We replaced '\|&' with '\|' (Thanks to Kazutoshi Yoshitake for a bug report).

2013.09.02: v0.9.5 was released.

2013.07.08: Example was added to this document.

2013.06.29: v0.9.1 was released.
