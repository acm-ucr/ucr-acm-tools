ucr-acm-tools
=============

Scripts and tools useful to ACM at UCR members.

**If you find any bugs** in any of these scripts, please describe the nature in an email addressed to jsull003@ucr.edu.

ucr_print
---------

Given a file as a command line argument, this script will print that file to one of the lab printers in WCH. Syntax for the command:

    ucr_print FILE_TO_PRINT PRINTER_NAME

If **PRINTER_NAME** is not specified, then **kilop** is used (which is the printer inside of the ACM lab). Below are some example uses of the script.

    > ucr_print essay.pdf
    Attempting to print PDF file... Converting to postscript first.
    > ucr_print "Quick Note.txt" alphap

Notice when printing a PDF file you will get a conversion message. You can safely ignore that message, but know that the program **pdf2ps** is being used to convert your file to postscript, so if you find that it's not printing out correctly, that program is likely to blame.