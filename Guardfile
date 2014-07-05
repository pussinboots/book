guard :shell do
  watch /.*\.md$/ do |m|
    `softcover build:pdf`

    pages = `pdfinfo ebooks/example.pdf 2>/dev/null | grep Pages | cut -d ":" -f 2 | tr -d ' '`
    msg = "changed #{m[0]} pdf has #{pages} pages"
    n msg, 'LaTeX'
    "-> #{msg}"
  end
end