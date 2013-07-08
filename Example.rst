=====================================
Example: assemble phage genome
=====================================

After installing Sprai, assemble a small genome.

For example, we showed how to assemble the phage genome.

Prepare data
=======================
Go to `pacbiotoca wiki <http://sourceforge.net/apps/mediawiki/wgs-assembler/index.php?title=PacBioToCA>`_ and download phage data ( http://www.cbcb.umd.edu/software/PBcR/data/sampleData.tar.gz ).

::

   mkdir tmp
   cd tmp
   wget http://www.cbcb.umd.edu/software/PBcR/data/sampleData.tar.gz
   tar xvzf sampleData.tar.gz

Convert fasta to fastq. You can use a fa2fq.pl script in Sprai.
::

   fa2fq.pl sampleData/pacbio.filtered_subreads.fasta > pacbio.filtered_subreads.fq

Prepare Sprai
==========================================

::

   mkdir tmp2
   cd tmp2
   ln -s ../pacbio.filtered_subreads.fq all.fq
   cp /your/sprai/directory/asm.spec .
   cp /your/sprai/directory/ec.spec .

Open ec.spec and change values.
::

   #>- params -<#
   input_fastq all.fq
   estimated_genome_size 50000
   partition 12
   evalue 1e-50
   trim 42
   ca_path /path/to/your/wgs/Linux-amd64/bin/
   word_size 11
   #>- params -<#

*input_fastq* is your input file name.

*estimated_genome_size* is the number of nucleotides of your target.
If you do not know it, set large number. For example, set 1e+12.

*partition* is the number of processors Sprai uses.

*evalue* is used by blastn.

*trim* is the number of nucleotides Sprai cut from both sides of alignments.

*word_size* is used by blastn.

Correct errors & assemble
==============================
::

   fs2ctg_v4.pl ec.spec asm.spec > log.txt 2>&1 &

Sprai gives ID to each read in all.fq and outputs c00.idfq.gz.

Sprai partitions all.fq to c00_00xx.fa.

c00.nin, c00.nhr and c00.nsq are output by makeblastdb.

Sprai aligns c00_00xx.fa to c00.nxx database by using blastn, correct errors and output c00_00xx.dfq.gz.
dfq format contains the IDs of reads, bases, aligned depths and quality values.
(Current Sprai outputs dummy quality values.)

Sprai cut low depth regions of each read, delete '-' characters to convert to FASTQ format and outputs corrected reads in c00.fin.idfq.gz.

Sprai extracts longest 20X reads of the *estimated_genome_size* from c00.fin.idfq.gz.
And feed them to Celera Assembler.

Celera Assembler outputs files into c01.fin.top20x directory.

Find contigs
===================
You will find contigs in a *c01.fin.top20x/9-terminator/c01.fin.top20x.ctg.fasta* file.
Files in *c01.fin.top20x* are produced by the wgs-assembler (Celera Assembler).
Read `the wgs-assembler document <http://sourceforge.net/apps/mediawiki/wgs-assembler/index.php?title=Main_Page>`_ for details. 

Get N50 value
================
If you install Statistics::Descriptive module to a directory Celera Assembler can see, Celera Assembler outputs N50 value and so on in a do_c01.fin.top20x.log file.
You will find lines in the file like below:
::

   [Contigs]
   TotalContigsInScaffolds         1         
   TotalBasesInScaffolds           50618     
   TotalVarRecords                 0         
   MeanContigLength                50618
   MinContigLength                 50618     
   MaxContigLength                 50618     
   N25ContigBases                  50618
   N50ContigBases                  50618
   N75ContigBases                  50618

These are the statistics of contigs of the assembly.
