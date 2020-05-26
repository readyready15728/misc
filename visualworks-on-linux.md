# VisualWorks on Linux
## Making the venerable commercial Smalltalk implementation not hideous

First of all, I needed to find the email linking to the download. This wasn't
in my spam folder as the website suggested, but in "Promos".

After getting the ISO, this sums it up:

http://www.cincomsmalltalk.com/main/questions/question/how-do-i-install-cincom-smalltalk-on-linux/

Basically:

1. Make sure that the appropriate VM is selected during installation and
2. Go through the launcher menu System → Load Parcels Named... and load "Xft"
   and "Xft-Integration". It has to be done through the launcher like this
specifically because I found some other way of loading parcels and I got some
message about how the format was invalid.
3. Save the image and restart.

What you will see is an enormous improvement over the jagged eyesore that is
core font rendering in the X Window System.
