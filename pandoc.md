# Pandoc

If you need to convert files from one markup format into another, [pandoc](https://pandoc.org/index.html) is your swiss-army knife

- Convert from `docx` to github-flavored `markdown` with images: 
  - `pandoc --extract-media=./ -f docx -t gfm file.docx -o output.md`
