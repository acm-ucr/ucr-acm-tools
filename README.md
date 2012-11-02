ucr-acm-tools
=============

Scripts and tools useful to ACM at UCR members.

**If you find any bugs** in any of these scripts, please describe the nature in an email addressed to jsull003@ucr.edu.

remote_printing
---------

Given a file as a command line argument, the **ucr_print** bash script will print that file to one of the lab printers in WCH. This script is meant to be used from your own computer. You do not need to be on campus for this to work, you only need to have access to **bell.cs.ucr.edu**.

You need to add the following lines to your ~/.ssh/config file (if you do not have one, make it) on the computer you will be running the script on.

    Host bell
        HostName bell.cs.ucr.edu
        User jsull003

**Make sure to change the user to whatever your cs login is.** Seriously, don't be trying to log in as me. *Note this will allow you to type in ssh bell from now on rather than ssh bla@bell.cs.ucr.edu, which is a useful trick in of itself*

Once you have your SSH config set up, syntax for the command is as follows.

    ucr_print FILE_TO_PRINT PRINTER_NAME

If **PRINTER_NAME** is not specified, then **kilop** is used (which is the printer inside of the ACM lab). Below are some example uses of the script.

    > ucr_print essay.pdf
    Attempting to print PDF file... Converting to postscript first.
    jsull003@bell.cs.ucr.edu's password:
    > ucr_print "Quick Note.txt" alphap
    jsull003@bell.cs.ucr.edu's password:

Notice when printing a PDF file you will get a conversion message. You can safely ignore that message, but know that the program **pdf2ps** is being used to convert your file to postscript, so if you find that it's not printing out correctly, that program is likely to blame. Also note that you will have to enter your password each time you want to print.