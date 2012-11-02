ucr-acm-tools
=============

Scripts and tools useful to ACM at UCR members. Go to the [Downloads](https://github.com/brownhead/ucr-acm-tools/downloads) page to grab a tarball or zipball of this repo.

**If you find any bugs** in any of these scripts, please describe the nature in an email addressed to jsull003@ucr.edu.

remote_printing
---------------

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

cpp_filter
----------

When writing a C++ program, you'll often run into some pretty ugly errors due to templating. For example, if you try to compile the following C++ program, you'll get some pretty ugly errors.

    #include <iostream>

    using namespace std;

    void foo() {
      cout << "I don't return anything.";
    }

    int main() {
      cout << foo();

      return 0;
    }

And here are the errors.

    test.cpp: In function ‘int main()’:
    test.cpp:10: error: no match for ‘operator<<’ in ‘std::cout << foo()’
    /usr/lib/gcc/x86_64-redhat-linux/4.1.2/../../../../include/c++/4.1.2/bits/ostream.tcc:67: note: candidates are: std::basic_ostream<_CharT, _Traits>& std::basic_ostream<_CharT, _Traits>::operator<<(std::basic_ostream<_CharT, _Traits>& (*)(std::basic_ostream<_CharT, _Traits>&)) [with _CharT = char, _Traits = std::char_traits<char>]
    /usr/lib/gcc/x86_64-redhat-linux/4.1.2/../../../../include/c++/4.1.2/bits/ostream.tcc:78: note:                 std::basic_ostream<_CharT, _Traits>& std::basic_ostream<_CharT, _Traits>::operator<<(std::basic_ios<_CharT, _Traits>& (*)(std::basic_ios<_CharT, _Traits>&)) [with _CharT = char, _Traits = std::char_traits<char>]
    /usr/lib/gcc/x86_64-redhat-linux/4.1.2/../../../../include/c++/4.1.2/bits/ostream.tcc:90: note:                 std::basic_ostream<_CharT, _Traits>& std::basic_ostream<_CharT, _Traits>::operator<<(std::ios_base& (*)(std::ios_base&)) [with _CharT = char, _Traits = std::char_traits<char>]
    /usr/lib/gcc/x86_64-redhat-linux/4.1.2/../../../../include/c++/4.1.2/bits/ostream.tcc:241: note:                 std::basic_ostream<_CharT, _Traits>& std::basic_ostream<_CharT, _Traits>::operator<<(long int) [with _CharT = char, _Traits = std::char_traits<char>]
    /usr/lib/gcc/x86_64-redhat-linux/4.1.2/../../../../include/c++/4.1.2/bits/ostream.tcc:264: note:                 std::basic_ostream<_CharT, _Traits>& std::basic_ostream<_CharT, _Traits>::operator<<(long unsigned int) [with _CharT = char, _Traits = std::char_traits<char>]
    /usr/lib/gcc/x86_64-redhat-linux/4.1.2/../../../../include/c++/4.1.2/bits/ostream.tcc:102: note:                 std::basic_ostream<_CharT, _Traits>& std::basic_ostream<_CharT, _Traits>::operator<<(bool) [with _CharT = char, _Traits = std::char_traits<char>]
    /usr/lib/gcc/x86_64-redhat-linux/4.1.2/../../../../include/c++/4.1.2/bits/ostream.tcc:125: note:                 std::basic_ostream<_CharT, _Traits>& std::basic_ostream<_CharT, _Traits>::operator<<(short int) [with _CharT = char, _Traits = std::char_traits<char>]
    /usr/lib/gcc/x86_64-redhat-linux/4.1.2/../../../../include/c++/4.1.2/bits/ostream.tcc:157: note:                 std::basic_ostream<_CharT, _Traits>& std::basic_ostream<_CharT, _Traits>::operator<<(short unsigned int) [with _CharT = char, _Traits = std::char_traits<char>]
    /usr/lib/gcc/x86_64-redhat-linux/4.1.2/../../../../include/c++/4.1.2/bits/ostream.tcc:183: note:                 std::basic_ostream<_CharT, _Traits>& std::basic_ostream<_CharT, _Traits>::operator<<(int) [with _CharT = char, _Traits = std::char_traits<char>]
    /usr/lib/gcc/x86_64-redhat-linux/4.1.2/../../../../include/c++/4.1.2/bits/ostream.tcc:215: note:                 std::basic_ostream<_CharT, _Traits>& std::basic_ostream<_CharT, _Traits>::operator<<(unsigned int) [with _CharT = char, _Traits = std::char_traits<char>]
    /usr/lib/gcc/x86_64-redhat-linux/4.1.2/../../../../include/c++/4.1.2/bits/ostream.tcc:288: note:                 std::basic_ostream<_CharT, _Traits>& std::basic_ostream<_CharT, _Traits>::operator<<(long long int) [with _CharT = char, _Traits = std::char_traits<char>]
    /usr/lib/gcc/x86_64-redhat-linux/4.1.2/../../../../include/c++/4.1.2/bits/ostream.tcc:311: note:                 std::basic_ostream<_CharT, _Traits>& std::basic_ostream<_CharT, _Traits>::operator<<(long long unsigned int) [with _CharT = char, _Traits = std::char_traits<char>]
    /usr/lib/gcc/x86_64-redhat-linux/4.1.2/../../../../include/c++/4.1.2/bits/ostream.tcc:361: note:                 std::basic_ostream<_CharT, _Traits>& std::basic_ostream<_CharT, _Traits>::operator<<(double) [with _CharT = char, _Traits = std::char_traits<char>]
    /usr/lib/gcc/x86_64-redhat-linux/4.1.2/../../../../include/c++/4.1.2/bits/ostream.tcc:335: note:                 std::basic_ostream<_CharT, _Traits>& std::basic_ostream<_CharT, _Traits>::operator<<(float) [with _CharT = char, _Traits = std::char_traits<char>]
    /usr/lib/gcc/x86_64-redhat-linux/4.1.2/../../../../include/c++/4.1.2/bits/ostream.tcc:384: note:                 std::basic_ostream<_CharT, _Traits>& std::basic_ostream<_CharT, _Traits>::operator<<(long double) [with _CharT = char, _Traits = std::char_traits<char>]
    /usr/lib/gcc/x86_64-redhat-linux/4.1.2/../../../../include/c++/4.1.2/bits/ostream.tcc:407: note:                 std::basic_ostream<_CharT, _Traits>& std::basic_ostream<_CharT, _Traits>::operator<<(const void*) [with _CharT = char, _Traits = std::char_traits<char>]
    /usr/lib/gcc/x86_64-redhat-linux/4.1.2/../../../../include/c++/4.1.2/bits/ostream.tcc:430: note:                 std::basic_ostream<_CharT, _Traits>& std::basic_ostream<_CharT, _Traits>::operator<<(std::basic_streambuf<_CharT, _Traits>*) [with _CharT = char, _Traits = std::char_traits<char>]

That's a lot of lines for the error "you can't print out a void value." Wouldn't it be nicer if that error output was a little nicer? Well when I compile that using my setup (which uses the C++ filter I'm about to show you), I get this...

    test.cpp: In function ‘int main()’:
    test.cpp:10: error: no match for ‘operator<<’ in ‘cout << foo()’

It's not "you can't print out a void value" but it does cut down on the ridiculous spam that really isn't any use to me. The reason it shows this rather than the previous error messages, is because when I type in ``g++ some_file`` I'm actually running ``gfilt some_file`` because of some bash aliases I set up, and gfilt is a handy wrapper around the STLFilt program found [here](http://www.bdsoft.com/tools/stlfilt.html).

Enough build up though, to get this working, just copy everything in the cpp_filter directory into your ``~/bin`` directory (make the directory if it doesn't exist). Afterwards, add the following line to your ``~/.bashrc`` file...

    alias g++="~/bin/gfilt -Wall"

And that's it! Now every time you run g++ you'll actually be executing gfilt.

Note that gfilt, by default, displays the results of your compilation through the less program (which means you can scroll up and down if you have long error messages). Hit **q** to exit the less program (you'll know what this means, if you don't already, once you compile something).