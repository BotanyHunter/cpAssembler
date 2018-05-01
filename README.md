# cpAssembler
Software to assemble plastomes from Illumina reads. 
<b>Currently only works for Windows</b>

<b>Getting started</b>

<ol>
<li>The Illumina files should be placed in a directory, either locally or on an external hard drive</li>
<li>The files should be unzipped. No need to change their names.  If you do, however, please leave the fastq file extension.</li>
<li>Start the cpAssembler program typically double-clicking on cpAssembler.exe</li>
<li>Adding a new specimen:
<ol>
  <li>Add a new file set. From the menu click <b><i>file/new fileset</i></b>. Give a name to the fileset.
  I prefer something with a unique numeric ID plus the species name (e.g. 25678_L_erinus). The
  fileset name can include spaces and any other legal character for file names.</li>
  <li><b>One-by-one</b> add the paired-end fastq files to the fileset. From the menu click <b><i>file/add to fileset</i></b>.
    Browse to the first file to be added and click open.  If there is more than one file associated
    with the specimen, click again on file/add to fileset. Browse to the second file to be added and click open.
    Continue until all files associated with the specimen have been added.
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
</ol>
