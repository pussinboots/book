#Project

This chapter illustrate the project idea that will be implemented using the newest html 5 technologies to illustrate the concepts and approaches of Continous Integration and Deployment. The Web Application we will develop is a full functional one. The idea to write this book rise during my development of the [unitcover](https://github.com/pussinboots/unitcover)project. And what is more obviouslly to take that project to demonstrate the complete development process from a project concept to a launched product.

\todo{say something more about the begining phase of the unitcover project \ldots}

##Why

From my work as a Java Developer i'am really familiar with Continous Integration Systems like Cruisecontrol from the older days
where [Ant](http://ant.apache.org/) was the most popular Build System for Java projects or Hudson now known as Jenkins. I found
a very good alternative for Open Source Projects there are hosted by Github called [Travis CI](https://travis-ci.org/). It is very
good at building project of different languages with very few configuration needed. For a detailed explanation for Travis See Chapter Build Management. In a comparisson with Jenkins Travis CI miss some report capabilities like a page contains test reports for every build.

The new offered feature named badge of services like Travis CI, coveralls, david-dm and a lot more see Build Management Chapter. The idea of a test badge was born so i discover the [shields.io](http://shields.io) service. With that service it can easily realized to implement little nice and informative badges. This bagdes can be used in the README.md on Github to display build qualitive metrics in a very compact and actual way directly in the project documentation. That was the ground idea for develop this project display a badge that show the test report of the latest build in a very compact way in the README.MD file on Github.

##What is it about

Continous Integration is not only to build a project and has maybe at the end a an artifcats its also about to collect quality data of the build like test reports, test coverage, code quality analyse reports and so on. This report data are generated during a Travis CI build but not display there. For test coverage i found a really good project called [coveralls.io](http://coveralls.io) that store and display the test coverage for every Travis build. But for test reports i found no similar projects so brave new open source world than develop one. And here it is the unitcover project store and display test results for all running tests during the Travis CI build.

The general idea behind the unitcover project is to make test results public and accessable via the web and also collect historical data like test report trends since the last x builds. To build this project a lot of great Open Source Services and Software will be used. First the great and reliable Github Source Management is used and it offers a lot os services around SM like issue tracking, markdown for documentation files and a lot more.      

##Next steps

After having a idea is just the beginning of a project. Than i collect some features and group them by priority of needed and nice. So start with that they are needed follow the nice once or changed between them to keep the self motivation high. If write some lines of code and more or less you see the results and the new upcoming possible features that keep you in flow. 

\missingfigure{Add a scrennshot of the unitcover trello board here.}

So the goal to achieve is to display test report badges in the manner of for example Tests passed 45 or in the failure/error case Tests failed/errored 5 to get a quick information of the test quality of the latest build. With that defined goal in mind we sketch the first architecure draft. 

What will be the best choice of the framework and language to use to achieve the goal and that also very quick. I had some experience with angularjs and Play framework (the scala version) and found both will be good to achieve the goal very quick. With angularjs and his very big community it is very simple to implement a HTML 5 web application based on an Rest API for backend communication. The good [bootstrap](http://getbootstrap.com/) integration is also a big plus for angularjs. The Play framework is also good designed to build a complete web application but we will use it as Rest framework because with it route approach it is very easy to map url calls to method invocations and the json and xml support is also wonderfull.

The consequence of the choosen frameworks is that the unitcover project will be a multi programming language project. That could have some disadvantage for building and development it could become much complex. But after a while of development i discover that this disadvantage will be more or less rather an advantage. The used programming language will be JavaScript and Scala and both have a great build and development tool support and both cover very well what is needed for the their layer. 

The JavaScript eco system besides angularjs cover all aspects of developing a web application from package management, testing, coverage, debugger and so on. For example with the [bower](http://bower.io/) project there exist a really great package management tool it cover all needs and offer new features directly for html, css and JavaScript files. The use of the angularjs framework ships the view layer completly to were it belongs to the web application files. And bower brings what we loved about package management like versionized dependency management and publishing to the HTML 5 web applications. Like with maven or for Scala sbt define the dependencies and bower will fetch them for you. But here come the glue it not only fetch it for you it also inject javascript and css reference tags directly in your html file. Gone the time where you have to put script tags in your html files by hand for new javascript dependencies or to change the url of a script tag to update the used version. For a detail explanation of bower look into the build management chapter.
\todo{short description of karma, jasmine and istanbul for testing purpose of javascript code \ldots}

The scala eco system can be compared with the java eco system there is sbt as package management and a lot of good testing frameworks for example [spec2](http://etorreborre.github.io/specs2/) and the play framwork it self has some very good features for quick development like class reloading, wonderful test capabilities and big community with extensions. That make the scala language very productive and quick to code something.

Next to the decision of the core frameworks and programming languages to use we will got to the Architecture draft of the unitcover project. Next chapter Architequre.

\todo{maybe add summary box here and think of it general use}

[sample-footnode] The term web application files means all files that are common for HTML 5 web applications like html of course, css, javascript, coffee, less and so on.

##Architecture

\missingfigure{Add simple architectural overview contains the layer upload, frontend and backend and also the used languages and frameworks.}

###Upload

###Frontend

###API

###Backend
