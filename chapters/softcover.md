# Softcover

[Softcover](https://www.softcover.io) is a publishing platform for technical authors. There exists also a very good 
[Manual](http://manual.softcover.io/) about what softcover is and what it does. The idea to write this book was inspired after
i found this lovely tool. For me as a technical guy it is easy to write about stuff that i have done. But to put it in a good
structured and readable book format almost impossible. Thanks to softcover and latex it is possible to concentrate on the content and
not on the book format and design.

The integration between markdown and latex is very brillant and make it so easy to write good formatted text. After a while of writing and 
also coding for that book i discover the possibility to combine  great projects to realize an automated book publishing and
versioning. The supported markdown syntax of softcover make it possible to use github as source management for the book pages, there
is still a drawback the embedded latex commands are not supported by github but use it only where it needed and for the rest markdown. Than 
the book pages are still readable directly in github. And the book source is accessable with only a browser so you could still write
on the book even if you don't have a computer by the hand go to the next internet cafe or use your smartphone and keep writting.

The mentioned preview of book chapters on github is still good enough to look at the content of the book but to get a closer feel
on how look the chapter or the whole book it is not possible only with Github. So I setup a Github project called 
[book](https://github.com/pussinboots/book) that i used to write directly in github or if you prefer use a online ide like 
[Codio](https://codio.com) it is so much possible if you use Github to host your content. When the book source is at Github why not use 
a Build Server like Travis CI to build the actual version of your book with softcover and publish it to them.

With the following .travis.yml file it was possible to setup a automated build and publishing of that book after i commit changes to Github.
\todo{link to content not embed}
```yaml
language: ruby
rvm:
- 1.9.3
script: softcover deploy
install: gem install softcover
before_script:
 - echo api_key":" $SOFTCOVER_API_KEY  > .softcover
after_script:
 - cat .softcover-book
before_install:
 - yes "" | sudo apt-add-repository ppa:texlive-backports/ppa
 - sudo apt-get update -qq
 - sudo apt-get install texlive-xetex texlive-fonts-recommended texlive-latex-recommended texlive-latex-extra
 - sudo apt-get install -qq inkscape
 - sudo python -c "import sys; py3 = sys.version_info[0] > 2; u = __import__('urllib.request' if py3 else 'urllib', fromlist=1); exec(u.urlopen('http://status.calibre-ebook.com/linux_installer').read()); main(install_dir='`echo ~`')"
 - export PATH=$PATH:`echo ~`
 - curl -O -L https://github.com/IDPF/epubcheck/releases/download/v3.0/epubcheck-3.0.zip && unzip epubcheck-3.0.zip -d ~
 - curl -o ~/kindlegen http://softcover-binaries.s3.amazonaws.com/kindlegen && chmod +x ~/kindlegen
```
The build will take more than 10 minutes that is to long for fast feedback but could be reduced in the future. It takes so long
because it has to install the complete texlive latex distribution, then softcover and its dependencies for every build.
\todo{reduce build time or give a hint}
But what we have achieved so far is that after a commit to github rather than ten minutes (or less more) you have a new published version of pdf, 
mobi and epub ready for reading online on the [softcover](https://www.softcover.io) plattform.
