# EPUB Recompression

Sometimes you'll download an EPUB file and it's just way too big. Often this
can be fixed relatively easily, as you'll see here. Just follow these steps:

1. Copy the offending EPUB into a temporary directory that you are comfortable
with using.

2. `unzip humongous.epub -d huge`, making the obvious substitutions. I
use a single lowercase word from the title for the temporary directory I
unpack the contents into. And yes, really. EPUB files are glorified ZIP
archives.

3. Find out where the images are stored and `cd` into the directory containing
them. (I have only ever come across cases where a single directory holds all
images.) The exact location varies, but finding it should easy as you will see
the paths scrolling by as the contents of the EPUB are extracted. Once you find
it, You might want to run `du -ch` in the directory to get a sense of how large
the images are at this point. Typically, they JPEGs. If they are PNGs, skip to
step 6; otherwise proceed.

4. In my experience, huge EPUB files with JPEG images are a consequence of a
needlessly high compression setting. Everyone hates JPEGs that look like
they've had dirt smeared on them, but it usually really is possible to reduce
the compression without any appreciable loss of quality. So what you want to
do will look like this:

    ```bash
    for img in *.jpg; do convert -quality 70 $img "reduced-$img"; done &
    ```

    This isn't a recipe set in stone. The quality can be changed up or down to
    fit your needs, but I find that 70 is a sensible default. Also, if the
    extension `.jpeg` is being used instead of `.jpg`, make the obvious change.
    When all is said and done, there will be a set of images in the folder
    with names identical to those you started with but for the prefix
    `reduced-`.

5. The reduced images will only take up more space in the archive if they don't
overwrite the ones that are already there. They can replace the original images
in one fell swoop, like so, remembering to do this *after* the last step
runs to completion:

    ```bash
    for img in reduced-*; do mv $img $(echo $img | sed 's/^reduced-//'); done
    ```

    Now go to step 8.

6. If there are PNG images in the image folder, something I have only come
across once, then—at least in the sole instance I came across—converting them
all to JPEGs will result in massive saving of space with no real loss of
quality. In the image folder:

    ```bash
    for img in *.png; do convert -quality 70 $img $(basename $img .png).jpg; done &
    ```

    As before, quality may be adjusted to suit your purposes. *After* the
    background processes run to completion, `rm *.png` to get rid of the PNG
    images.

7. With JPEG recompression, the original filenames will be saved. Not so with
conversion from PNG. Find the directory that contains the text of the EPUB. It
will have a large number of files with the extension `.html` or similar (such
as `.xhtml`). As far as I know, as with images, the text of the EPUB is all
stored in one directory. `cd` into this directory, then run the following,
making any necessary change appropriate for the file suffix used in this
directory:

    ```bash
    for page in *.html; do sed -ri 's/<img(.*?)src="(.*?)\.png"/<img\1src="\2\.jpg"/g' $page; done
    ```

    I believe this regex should be fully appropriate. On the one hand, it will
    prevent instances of `img` tags being discussed in the text from being
    modified, because, in those cases, the angle bracket must be escaped as
    `&lt;`. On the other hand, it is robust enough to account for an `alt`
    attribute or the like intervening between `img` and the `src` attribute.

8. If you followed my advice in step 3, `cd` to the image directory if you are
not already in it and run `du -ch` again to get a sense of how much space
you'll save when the EPUB is recompressed. Of course this figure won't be exact
because it doesn't take compression into account, but it will give you an idea
of how well you did.

9. Now `cd` to the directory that you extracted the EPUB into, in other words,
the directory that followed the `-d` option to `unzip`, and `zip -r
recompressed.epub *`, which will pack everything into a new EPUB file.
Obviously, the name should be altered to fit or changed later. You now have
a fully functioning EPUB!

10. Give your new EPUB the once-over. Is the new EPUB substantially smaller
than the old one? Do the images display properly? Is the image quality
adequate? If so, congratulations on your new, smaller EPUB! If not, try again
with different parameters. If you suspect something is wrong with my procedure,
please inform me and I will see what can be done about it.
