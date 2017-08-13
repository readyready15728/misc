# Recompressing PDFs with GhostScript

Often, large PDFs can be cut down to size with the following:

```bash
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/ebook -dNOPAUSE -dBATCH -sOutputFile=output.pdf input.pdf
```

Sometimes, even further reductions can be gained by converting the PDF to a
DJVU like so:

```bash
pdf2djvu output.pdf > output.djvu
```
