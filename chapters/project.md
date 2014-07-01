#Project

To illustrate the concepts and approaches of Continous Integration and Deployment we will develop a Web Application. This
example Web Application is a full functional one that i develop in my spare time. The idea to write this book rise during 
my development of the [unitcover](https://github.com/pussinboots/unitcover) project. And what is more obviouslly to take
that project to demonstrate the complete development process from a project concept to a launched product.

\todo{say something more about the begining phase of the unitcover project \ldots}

##Why

From my work as a Java Developer i'am really familiar with Continous Integration Systems like Cruisecontrol from the older days
where [Ant](http://ant.apache.org/) was the most popular Build System for Java projects or Hudson now known as Jenkins. I found
a very good alternative for Open Source Projects there are hosted by Github called [Travis CI](https://travis-ci.org/). It is very
good at building project of different languages with very few configuration needed. For a detailed explanation for Travis See Chapter Build Management. In a comparisson with Jenkins Travis CI miss some report capabilities like a page contains test reports for every build.

##What is it about

Continous Integration is not only to build a project and has maybe at the end a an artifcats its also about to collect quality data of the build like test reports, test coverage, code quality analyse reports and so on. This report data are generated during a Travis CI build but not display there. For test coverage i found a really good project called [coveralls.io](http://coveralls.io) that store and display the test coverage for every Travis build. But for test reports i found no similar projects so brave new open source world than develop one. And here it is the unitcover project store and display test results for all running tests during the Travis CI build.

The general idea behind the unitcover project is to make test results public and accessable via the web and also collect historical data like test report trends since the last x builds.  

##Next steps

After having a idea is just the beginning of a project. Than i collect some features and group them by priority of needed and nice. So start with that they are needed follow the nice once. 

\missingfigure{Add a scrennshot of the unitcover trello board here.}

##Architecture

\missingfigure{Add simple architectural overview contains the layer upload, frontend and backend and also the used languages and frameworks.}

###Upload

###Frontend

###Backend
