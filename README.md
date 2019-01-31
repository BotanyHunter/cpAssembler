# cpAssembler
Software to assemble plastomes from Illumina reads. 
<b>Currently only works for Windows</b>

<b>Getting started</b>

<ol>
<li>The Illumina files should be placed in a directory, either locally or on an external hard drive</li>
<li>The files should be unzipped. No need to change their names.  If you do, however, please leave the fastq file extension.</li>
<li>Start the cpAssembler program typically double-clicking on cpAssembler.exe</li>
<li>Adding a new accession:
<ol>
  <li>Add a new file set. From the menu click <b><i>file/new fileset</i></b>. Give a name to the fileset.
  I prefer something with a unique numeric ID plus the species name (e.g. 25678_L_erinus). The
  fileset name can include spaces and any other legal character for file names.</li>
  <li><b>One-by-one</b> add the paired-end fastq files to the fileset. From the menu click <b><i>file/add to fileset</i></b>.
    Browse to the first file to be added and click open.  If there is more than one file associated
    with the accession, click again on file/add to fileset. Browse to the second file to be added and click open.
    Continue until all files associated with the accession have been added.
  <li>If there are more than two files, all forward reads must be added first, then all reverse reads should follow.
    The program expects the the paired end reads to be in the same order - the forward starting at record 1 and
    the reverse starting at record N/2 and continuing until the end, where N is the total number of reads.  
    Of course, forward and reverse do not mean anything, so they can be swapped, but all from one direction should 
    come first and all from the other should follow.
    </li>
</ol>
</li>
<li>Once all input files have been added to the fileset, click <b><i>Read</i></b> on the menu.  
    This will start the time consuming read process.  A message will appear on the bottom information line
  when the process has completed.  Depending on the computer, it could take several hours for large files.</li>
<li>From the menu, click <b><i>Assemble / Find genes</i></b>.  This will search for reads that match
    templates stored in the program for the 120 chloroplast coding regions (tRNA's, genes, etc.). These are
  then combined to form the genes for the current accession.</i>
<li>When this completes, click <b><i>Assemble / Assemble genes</i></b>.  This will take the genes found
  above and use them as seeds to build contigs that include the gene and its flanking regions.
  Then the contigs are compared pairwise to find those that can be linked.  This process continues until
  no contig can be extended nor linked.</li>
 <li>If you have a closely related accession with a fasta file of the complete plastome, 
     then you can use this related accession as a guide to map the contigs of the new accession to
     the guide plastome:
  <ul><li>From the menu, click <b><i>File / Import plastome (.fasta)</i></b>.  Browse and select the fasta
    file for the guide plastome.  A message will shortly appear on the bottom information line saying 
    "finished read and indexing..."</li>
    <li>Click on <b><i>Assemble / Map contigs</i></b>. This will take a minute or two while the program
      scans each contig from the assembly process and looks for a closely matching region of the
      guide plastome.</li></ul>
</ol>

<b>Next steps:</b>

The prior steps required a lot of computer time, but very little human time.
If the "map contigs" step was run, then a file is created with the extension ".contigmap". This file
lists the details of the mappings that were found.  Each line shows the start position on the guide plastome,
the length of the contig, the number of the contig, the direction of the contig, and finally, the contig sequence.
If any contigs were not mapped both the forward and reverse complement are listed at the end of the file.

If the "map contigs" step was not run, the assembly step created a file with the extension ".assembly".
This file simply lists each contig (one contig per line) from longest to shortest.

