=======
FAQ
=======
.. | Q. How many files does sprai create in each cycle?
.. | A. Given P partition in ec.spec, the number of jobs in each cycle is 1 (by makeblastdb)+1 (by partition_fa.pl)+P (by blastn, bfmt72s, nss2v and myrealigner)+ceil(P/CURRENT) (by dfq->fq)+1 (by cat) = P+ceil(P/CURRENT)+3, where CURRENT is 1 in ezez_v3.pl and ezez4make.pl and 12 in ezez4qsub_v4.pl. The number of files created in each cycle is {3 (by makeblastdb)+P (by partition_fa.pl)+P (by blastn, bfmt72s, nss2v and myrealigner)+ceil(P/CURRENT) (by dfq->fq)+1 (by cat)}+2*(# of jobs)(.e and .o files)+2*P(if you specify -pe thet blastn,... will use, and otherwise 0) = {2*P+ceil(P/CURRENT)+4}+2*(P+ceil(P/CURRENT)+3)+(2*P (if -pe) or 0 (otherwise)
