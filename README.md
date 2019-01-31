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

The prior steps required a lot of computer time, but very little human time.  The next steps take more human time.

If the "map contigs" step was run, then a file is created with the extension ".contigmap". This file
lists the details of the mappings that were found.  Each line shows the start position on the guide plastome,
the length of the contig, the number of the contig, the direction of the contig, and finally, the contig sequence.
If any contigs were not mapped both the forward and reverse complement are listed at the end of the file.

If the "map contigs" step was not run, the assembly step created a file with the extension ".assembly".
This file simply lists each contig (one contig per line) from longest to shortest.

In my experience, after practice, an assembly that results in less than 10 contigs that includes a contig map
can procede to a complete plastome in under an hour.  More time will be needed for first time users, accessions
without a closely related guide plastome, and accessions with more than 10 contigs.

The method to proceed from a contig map to a complete plastome is intuitive: from the contig map, we know where a contig ends and
where the next contig starts - we simply need to bridge the gap.  The program that built the contigs terminates
extending the contig because it found something wrong - usually as simple as an error in sequencing, but it could also be a 
polymorphic site, the boundary between a repeat section and a single copy section, or possibly a gap where no (or a single) read
spans the gap.

<b>Some details:</b>

<ul><li>The first step is to get a starting point, typically the start of the large single-copy region.
  From the guide plastome, grab the first 30-ish base pairs and search for these in cpAssembler.
  (in other words, copy the base pairs to the Windows clip-board - i.e. in the text editor, highlight and hit ctrl^c.).
  In cpAssembler, click on the rectangular box in the menu bar. This opens up a window for searching the reads
  for base pair strings.  Paste the copied base pairs into the window and click ok. Hopefully you will see a
  list of reads that match the search string.
  
Next, to confirm that the new accession has the same boundaries as the guide, in cpAssembler, highlight 30-ish base pairs
to the left of the search string 
(to highlight, left mouse down at the start of the desired string, drag, and left mouse up at the end of the desired string).
This automatically places the highlighted string on the clip-board.  Open up the search string box again
and paste the new string and hit ok to search.  Hopefully the new results will show the search string followed
by two alternatives each represented about 50-50.  You are looking at one end of the inverted repeat followed by
the start of the LSC and the end of the LSC. If this has gone smoothly, once again copy the first 30-ish base pairs
from the LSC and paste into a new sequence in Geneious.  You now have a starting point.</li>

<li>Next step, find if this starting point is part of a contig.  In Geneious, copy the 30-ish base pairs of the
  starting point and search for it in the .contigmap file.  
  If found, highlight (in the contigmap) the search string and all base pairs to the right.
  Replace the search string in Geneious file with the longer string from contig map.</li>
  
  <li>At this point, you are now at a gap. 
  To span gaps,I usually have open in Geneious my new, growing plastome as well as the guide plastome.
  In Geneious, grab the last 30-ish bps of the new plastome and find them in the guide plastome. Note the positions
  of the ends in both plastomes. From the contig map, find the position where the next contig is expected to
  start. You now know how many base pairs need to be spanned.
  To set a target extend length, click <b><i>Search / Extend parameters</i></b> and the target length.
  In Geneious, copy the last 30-ish base pairs
  of the new, growing plastome and paste into cpAssembler's search box.
  Hopefully you will find many matches, but there will be polymorphism in the base pairs following the search string.
  <ul>
    <li>If there is a clear dominant base pair with one (or few) minor base pairs, this probably is a sequencing error
      and the dominant base pair is the correct base pair.  Click on the search box and add the desired, correct
      base pair to the end of the search string and click ok.  
      Then to extend the string click <b><i>Search / Extend</i></b>.  After extension, the result is automatically
      placed on the clip-board, so return to Geneious and replace the search string (from the new plastome) with the
      extension.  
    </li>
    <li>If there is only a single match...
  </ul>
  </ul>
  
  <b>Still writing...</b>
