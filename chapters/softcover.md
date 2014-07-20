# This Book

This chapter introduce the reason and motivation behind this book. This book is about how to develop a full functional Web Application with Continous 
Testing and Continous Integration. The generic term would be full Automated Development Workflow aka ADW. It is a self created term 
\todo{clearify the term ADW}. The different process or topics of ADW will be explained chapter by chapter. 
This book will be practical guide to setup Web Application Automated Development Workflow. In the practical part we will devlop a little full 
functional Web Application that use JavaScript for the view layer and Scala for the Backend. 

I will try to keep the concept and approaches of AWD programming language independent where it is possible. But this is not alwasy possible 
for example implements unit tests for the backend will be use the Scala programming language because the backend itself is implemented in. 
Íf you plan or already have Web Application written in an other programming language than you will implement the unit test in that language of course. 
The topic End2End Testing of Web Application is for example programing language independent because it is a black box tests so. I will emphasize the 
parts they are programming independant. 

The main focus is to keep things short and easy not quick and dirty this is often missunderstood. So the main principal is to reuse tools and frameworks 
they are already out there and if they miss a feature than develop it and share it with the community of course. Open source lives from the willing 
to give back. 

They are a lot of tools and services out there they can be combined to get a Automated Development Workflow from the project concept to the shipped 
product. That could also be achieved with a lot of closed source products out there maybe even faster. But i promise with the combination of the 
introducing tools you will get even close sometime even closer to what you can achieve with the commercial products.

##Chapters
\todo{chapter overview}

Chapter by chapter will introduce the different processes they are part of the Automated Development Workflow and each will concentrating of one 
aspect at a time. 

The chapter Development Workflow decribe the different processes that are part of that entire Workflow. The focus for this chapter is to give 
theoretical overview what all belongs to the complete Development Workflow. What can be achieved with each process from a overall perspective. 
\todo{maybe also explaint different roles like developer, tester here but not my focus}

The chapter GitHub

The Project chapter
We start with an idea we want to implement a little test report service that collect test results from different projects and display them in 
a nice and readable way. The phase from the idea to an project is cover in the \todo{link to it} Project chapter. What it covers.

* motivation behind the project (the vision)
* first draft of the architecture 

The chapter Web Application give a little overview about technology we will use to implement the project.

* html related technologies (css, javascript)
* main frameworks we use
* capabilities of testing a web app
* tools to increase productivity and quality

The chapter Database

The chapter Development 

To illustrate the setup of a complete Development Process we will go from the project concept phase to a shipped product.  we will implement a little 
test report service. For the moment let name it unitcover. For more explanation look into the \todo{link to it} Project chapter.

The chapter Testing

The chapter Build Management

The chapter Deployment

The chapter Continous

The chapter Conclusion

##Continous Writing

This chapter illustrate the journey of writing a technical book that self use Continous Integration. So why not adapt the Software Development paradigms 
not also to the Development of a whole book. Both is about handling content and building a high quality product. So they are not so much differences 
between software and books. 

The following chapters are familiar to developers but i guess not so to book writers even technical book writers. My skills to write books are not so 
good at the moment but i guess it is like discover a new programming language. Like Aristolte said \todo{reference book here} "For the things we have 
to learn before we can do them, we learn by doing them.”. But I have some experience to write code and also by using a lot of tools that support me 
to get things done faster and even better. 


###Github

Github could not only be used to host source code it coul dbe used to host any kind of content preferred ascii based onced. This book starts as a 
local softcover project but after a while of writing i came to this situation where i want to keep writing on that book but not from my personal computer. So the book content should be available over the internet. Hey I start to think about i used GitHub for my source code why not using it also for the book content. I've found also a lot of people they host her latex based thesis on GitHub.

It could not be wrong to doing this. Then i realized that means the complete book raw content is public available but maybe the time where books and even the raw content should be private are over. At the moment I'am not planning to sell the book but even If i do for example with the purchase capabilities of the softcover platform than i belief that a lot of readers are willing to pay the price and not download the public latex content and build her own version without paying. 

To use GitHub has also a lot of advantages for example when comes to collaboration and community. I can imagine by writing a book also commit Pull Request with text fixes or complete new chapters from everybody how wants do collaborate. 

###Softcover

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
on how the chapter look like or the whole book it is not possible only with Github. So I setup a Github project called 
[book](https://github.com/pussinboots/book) that i used to write directly in github or if you prefer use a online ide like 
[Codio](https://codio.com) it is so much possible if you use Github to host your content. When the book source is at Github why not use 
a Build Server like Travis CI to build the actual version of your book with softcover and publish it to them.

###Travis

With the following .travis.yml file it was possible to setup a automated build and publishing of that book after i commit changes to Github.
\todo{link to content not embed}
\begin{codelisting}
\codecaption{.travis yml for that book}
\label{code:.travis.yml}
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
\end{codelisting}
The build will take more than 10 minutes that is to long for fast feedback but could be reduced in the future. It takes so long
because it has to install the complete texlive latex distribution, then softcover and its dependencies for every build.
\todo{reduce build time or give a hint}
But what we have achieved so far is that after a commit to github rather than ten minutes (or less more) you have a new published version of pdf, mobi and epub ready for reading online on the [softcover](https://www.softcover.io) plattform.

###Softcover Service

The automated build of books with Travis Ci has allure but takes to long. So i started the [Softcover Service Project](https://github.com/pussinboots/heroku-softcover) that offer a simple Rest Api to build softcover books by checkout the book project from github and perform softcover build. A pdf version of this book can simple be build by open the following [url](http://nnamretti.ddns.net/api/build/pdf/pussinboots/book). It is hosted on an Amazon Web Service EC2 micro instance that can handle some load but it is still an prototyp as proof of concept. Completely implements as nodejs server. If you are intressting in that project than look on the github project page. Contribution is of course welcomed.  

###Guard

The [Guard](https://github.com/guard/guard) is a command line tool to handle file changes. With that tool you can setup very easily a complete pdf latex build that use the softcover tool to generate every time you save changes on that book a new version of the resulting pdf document.

But first lets install the Guard tool. It is written in the ruby programming language and published as [RubyGem](https://rubygems.org). We need a installed version oof RubyGem for an instruction see here [RubyGem](https://rubygems.org).

After the installation of RubyGem you can install Guard with the following command
```bash
gem install guard
gem install guard-shell
```
We also install the [guard-shell](https://github.com/guard/guard-shell) plugin to execute shell commands for file changes. After that Save the following ruby code snippet in a file called Guardfile
```ruby
guard :shell do
  watch /.*\.md$/ do |m|
    `softcover build:pdf`
    pages = `pdfinfo ebooks/example.pdf 2>/dev/null | grep Pages | cut -d ":" -f 2 | tr -d ' '`
    msg = "changed #{m[0]} pdf has #{pages} pages"
    n msg, 'LaTeX'
    "-> #{msg}"
  end
end
```
And now everytime you changed some of the markdown book pages it will execute
```bash
	softcover build:pdf`
```
that produce a pdf that contains the changes you did before. The following lines 
```ruby
 	pages = `pdfinfo ebooks/example.pdf 2>/dev/null | grep Pages | cut -d ":" -f 2 | tr -d ' '`
    msg = "changed #{m[0]} pdf has #{pages} pages"
    n msg, 'LaTeX'
    "-> #{msg}"
```
print out a little message that contains the filename that was changed and the page count of the new generated pdf document. I added the page count info to see the growth of the book during writing. It was a little motivation trick to see how the book growth give me a good feeling and kept me writing. I put little goals for me like today I will write two 2 new pages in chapter what ever and so i get a fast feedback if i achieve that goal.

The last thing to do is to start the Guard tool with the following command
```bash
	guard start
```
now it watch for changes you did on the markdown files of the book.

###Codio

For example the [codio](https://codio.com/) website which offer a complete online Web IDE that is free for open source development. It supports a lot of frameworks and programming languages for example the play framework with Scala. Thats right you can coding a Scala project directly in the browser which no need to install the Scala language stack on your local development. And not only coding is possible you could also run your integration or even end 2 end tests directly in the browser it is amazing for a detail explanation look into the \todo{link to Codio chapter} Codio chapter.
