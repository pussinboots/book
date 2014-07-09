guard :shell do
  watch /chapters\/.*\.md$/ do |m|
    n "file #{m[0]} rebuild pdf", 'LaTeX'
    "-> file #{m[0]} rebuild pdf"
    `softcover build:pdf -n`

    pages = `pdfinfo ebooks/example.pdf 2>/dev/null | grep Pages | cut -d ":" -f 2 | tr -d ' '`
    msg = "changed #{m[0]} pdf has #{pages} pages"
    n msg, 'LaTeX'
    "-> #{msg}"
  end
end