* The following makes it possible to view XZ-compressed PDF files in Midnight
Commander:

    ```
    # .xz-compressed PDF
    shell/.pdf.xz
      Open=/usr/lib/mc/ext.d/doc.sh open pdf
      View=%view{ascii} /usr/lib/mc/ext.d/doc.sh view pdf
    ```
   
    Note that it is not necessary to pass along `%f` or the like; the filename
    appears to be handled by environment variables set by Midnight Commander
    itself.

* It is possible to launch Windows executables from, for example, games from
GOG installed on Wine, like so:

    ```
    # Windows executables
    shell/i/.exe
      Open=wine %f
    
    shell/i/.lnk
      Open=wine start /unix %f
    ```

    Note that these instances are case-insensitive. Note also that the `/unix`
    switch is necessary for `wine start`; it tends to choke without it.

* A user-defined listing mode for both panels with `size:4` not only saves a
little more of the limited screen real estate of the file manager than would
otherwise be the case, but also makes sizes display in ways that are more
readily comprehensible with familiar suffixes.
