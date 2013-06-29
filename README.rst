========
README
========

install
========

sprai requres

* zlib
* `blast+ ver. 2.2.27 or newer <ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/>`_
* `Celera Assembler <http://sourceforge.net/apps/mediawiki/wgs-assembler/index.php?title=Main_Page>`_ (if you assemble)


When you install Celera Assembler, you need to change one line. In AS_global.h in the src directory of Celera Assembler, change from ::

#define AS_READ_MAX_NORMAL_LEN_BITS 11

to ::

#define AS_READ_MAX_NORMAL_LEN_BITS 15

For details, please read `pacbiotoca wiki <http://sourceforge.net/apps/mediawiki/wgs-assembler/index.php?title=PacBioToCA>`_

After the requirements are satisfied, ::

   cd sprai
   ./waf configure [--prefix=/some/dir/]
   ./waf build
   ./waf install

If you specify --prefix=/some/dir/, sprai will be installed in /some/dir/bin/ directory. If you don't, it will be installed in /usr/local/bin.

uninstall
================
::

   cd sprai
   ./waf uninstall

run sprai
================
::

   mkdir tmp
   cd tmp
   ln -s target_CLRs.fastq all.fq
   cp /path/to/sprai/asm.spec .
   cp /path/to/sprai/ec.spec .

one node mode
--------------

Open *ec.spec* by an editor and specify a *ca_path* parameter the directory in which you put wgs-assembler binaries.

.. Then,
.. ::

..    fs2ctg_v4.pl ec.spec asm.spec -n

.. You can confirm what will happen by using fs2ctg_v4.pl with '-n' option.
You **must** change *estimated_genome_size*.
If you cannot estimate the length of your target genome, give a large number (ex. 1e+12).

Modify other parameters in ec.spec for your needs following instructions in the file.
Then,
::

   fs2ctg_v4.pl ec.spec asm.spec > fs2ctg_v4.log 2>&1 &

This will do error correction and make contigs.

If you use error corrected reads and does not assemble, do

.. ::

..   fs2ctg_v4.pl ec.spec asm.spec -n -ec_only

::

   fs2ctg_v4.pl ec.spec asm.spec -ec_only > fs2ctg_v4.log 2>&1 &

many node mode
--------------

If you would like to use SGE to correct errors of CLRs and assemble, specify *blast_path* and *sprai_path* in ec.spec, and do
::

   ezez4qsub_v6.pl ec.spec asm.spec > ezez4qsub_v6.log 2>&1 &

.. \or
.. ::

..    ezez4makefile.pl ec.spec asm.spec > ezez4makefile.log 2>&1 && make &

If you use error corrected reads and does not assemble, do
::

   ezez4qsub_v6.pl ec.spec asm.spec -ec_only > ezez4qsub_v6.log 2>&1 &

.. \or
.. ::

..    ezez4makefile.pl ec.spec asm.spec > ezez4makefile.log 2>&1 && make ec_only &

many node mode 2
------------------

If you use `TGEW <https://github.com/mkasa/TGEW>`_, 
::

    ezez4makefile.pl ec.spec asm.spec > ezez4makefile.log 2>&1
    tge_make > tge_make.log 2>&1 &

\or
::

    ezez4makefile.pl ec.spec asm.spec > ezez4makefile.log 2>&1
    tge_make > tge_make.log 2>&1 &

.. results
.. ========
.. We used sprai v0.2.1. We evaluated the results by using `the validation script of PacBioToCA <ftp://ftp.cbcb.umd.edu/pub/data/PBcR/validationScripts.tar.gz>`_, which is a variation of the `GAGE <http://gage.cbcb.umd.edu/>`_ method.

.. +------------------------+
   | assembly results       |
   +========================+

.. .. csv-table:: assembly results
   :header: "organism", "SMRT cells", "ref size", "raw que size", "corrected que size", "raw contig count", "corrected contig count", "raw contig n50", "corrected contig n50", "qv", "misassemblies (gap>5bp, inversions, relocations, translocations)"

..    "*E. coli* K12",  "2", "4,639,675", "4,692,608", "4,646,758", "14", "15", "3,429,516", "__572,346", "30", "6"
..    "*P. heparinus*", "2", "5,167,383", "5,181,012", "5,175,158", "_5", "_4", "2,927,100", "1,658,237", "33", "2"
..    "*M. ruber*",     "1", "3,097,457", "3,099,149", "3,106,899", "_1", "_4", "3,099,149", "__962,346", "35", "4"

..
  ================ =========== ========== ============ ================== =========================== ====================== ============== ==================== == =================================================================
  organism         SMRT cells  ref size   raw que size corrected que size raw contig count            corrected contig count raw contig n50 corrected contig n50 qv misassemblies (gap>5bp, inversions, relocations, translocations)
  ================ =========== ========== ============ ================== =========================== ====================== ============== ==================== == =================================================================
  *E. coli* K12    2           4,639,675  4,692,608    4,646,758          14                          15                     3,429,516       572,346             30 6 
  *P. heparinus*   2           5,167,383  5,181,012    5,175,158          5                            4                     2,927,100      1,658,237            33 2 
  *M. ruber*       1           3,097,457  3,099,149    3,106,899          1                            4                     3,099,149       962,346             35 4 
  ================ =========== ========== ============ ================== =========================== ====================== ============== ==================== == =================================================================

..  test
  ======

  +---------+-----+
  |foo      |bar  |
  +=========+=====+
  | \ 4     | 15  |
  +---------+-----+

.. (under construction)
.. ==============================

