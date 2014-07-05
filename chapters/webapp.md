#Web Application

This chapter discover the new technologies that are used to implement the project unitcover, frameworks and tools to develop Web Application these days. Here is the web application defintion from wikipedia.
\todo{quotations with latex}
"A web application or web app is any application software that runs in a web browser or is created in a browser-supported programming language (such as the combination of JavaScript, HTML and CSS) and relies on a common web browser to render the application". 
The term Web Application describe for me an application that run and is accessable with a browser. It use a couple of technologies called HTML 5.

The border between Web Applications and Mobile Applications are very fluent and each native Mobile Application could also be implemented as complete HTML 5 Web Application the customer see no differences between them. 

##HTML 5

\todo{quotations}
The short definition from wikipedia "HTML5 is a core technology markup language of the Internet used for structuring and presenting content for the World Wide Web." With the HTML 5 technology the browser become the new what I called BVM (stands for Browser Virtual Machine like the JVM Java Virtual Machine). The modern browsers offer a couple of features to write whole web application with the JavaScript programming language. It offer local storage similar to an Relational Database called WebSQL. You could think of HTML 5 as a GUI framework to develop Graphical User Interfaces that run inside the browser and with the HTML 5 markup language you describe the look and feel of your GUI. And with the JavaScript language you implement the view logic.

##CSS 3

The short definition from wikipedia \todo{quotations} "Cascading Style Sheets (CSS) is a style sheet language used for describing the look and formatting of a document written in a markup language."
I'am not an expert in css development but it is a powerful language to specify the design and the format for the HTML view. There exists a lot of CSS frameworks like [bootstrap](http://getbootstrap.com/) that offer you a complete styled design ready to use and cover also mobile devices. There also a lot of angularjs modules that integrates the boostrap framework to use it very simple with angularjs

##Javascript

The short definition from wikipedia says \todo{quotations} "JavaScript (JS) is a dynamic computer programming language.[5] It is most commonly used as part of web browsers, whose implementations allow client-side scripts to interact with the user, control the browser, communicate asynchronously, and alter the document content that is displayed". JavaScript is a very powerful and underestimated programming language that is \todo{older tha Java ???} older than the Java programming language. With the rehype of the functional programing model JavaScript becomes the language of choice for implementing HTML 5 Web Application that run completly in the browser.

\todo{a little history info}

I guess the need for Web Application that are renderd on the server side is over and waste a lot of resources on the server side. What belongs to the client should be performed on the client side. The tool support for JavaScript is more or less powerful like for Java. They exists package manager, test frameworks, server runtimes, code completion and all what you can imagine and exists for your programming language of choice.

###Package Management

The [bower](http://bower.io/) will come to rescue you. It brings the maven familiar dependency management to Web Applications that use JavaScript in the browser. Define the dependencies in the bower.json file and with the command
```bash
bower install
```
will fetch them and save they it the folder bower_components. The folder can be configured. The download is very fast compared to the maven and sbt downloads. Bower has also a very useful feature that can create the css and javascript ref tags in any html file. That means it not only fetch the dependencies it also can be used to inject the dependencies in the html files. So that it also populate the dependencies for the web application no need to manual insert javascript tags anymore.

##CoffeeScript

The [CoffeeScript](http://coffeescript.org/) is a new programming language on top of JavaScript. It is compiled down to an equivalent JavaScript could be compared with for example MarkDown which is a markup languages that will be compiled to Html. So when the result is still JavaScript than why use this new abstraction. One of the main goal of CoffeeScript is to have better readable code. 

To get a feeling about CoffeeScript look at the next code example which compared an CoffeeScript code with an equivalent hand written javascript code. First the javascript code example it is a angularjs scenario test. It has oonly some few lines and i guess it is still good readable. But compared with the CoffeeScript below
```javascript
'use strict';

describe('overview live test', function() {
  describe('the overview page (index.html#/builds/) the unitcover project should', function() {
    beforeEach(function() {
      browser().navigateTo('index.html#/builds/');
    });

    it('display max 10 builds', function() {
      expect(repeater('li.build').count()).toBe(10);
    }); 
  });
});
```
it could be more readable and less code. CoffeeScript was inspired by python and ruby syntax for example like in python there is no need for brackets {} just use Indentation. It defines some rules like don't use var anymore and some syntactical sugar like -> that define a function callback. 
```coffeescript
"use strict"

describe "overview live test", ->
  describe "the overview page (index.html#/builds/) the unitcover project should", ->
    beforeEach -> browser().navigateTo "index.html#/builds/"

    it "display max 10 builds", ->
      expect(repeater("li.build").count()).toBe 10
```

But how looks the compiled javascript code of the CoffeeScript above. Here it is

```javascript
// Generated by CoffeeScript 1.7.1
(function() {
  "use strict";
  describe("overview live test", function() {
    return describe("the overview page (index.html#/builds/) the unitcover project should", function() {
      beforeEach(function() {
        return browser().navigateTo("index.html#/builds/");
      });
      return it("display max 10 builds", function() {
        return expect(repeater("li.build").count()).toBe(10);
      });
    });
  });

}).call(this);
```

it look similar to the hand written javascript with little differences. It wraps the complete javascript in a anonymous function to keep the namespace clean.
\todo{explain namespace scope coffeescript}
And the return statements are not nessary but coffeescript always set return keyword of the last code line in the CoffeeScript. This can be solved by adding explicit return in the CoffeeScript but this return statements doesn't matter so the test code could the keep clean.

##Web Frameworks

This chapter introduce the web frameworks we will used to implement the web application unitcover. They are a lot of good web frameworks out there so it is more a problem to choose the right one that fit your needs. In the chapter Project we have define the web application architecture and the goal what we want to achieve with the web application.

With the project vision in mind we can start the looking of the right frameworks to realize our vision. The project will have different layers like the View, API, Database. So it possible to use a complete 

\todo{rewrite better english}
Of course every developer has favorite frameworks and programming languages that he is familiar with. To get on speed during the development i decided to use angularjs for the view, because i had some experience with it and it make it very simple to render web pages based on json data. It has a wide community that is amazing. They are more or less exists support and integration for a lot of thinks like build management integration with bower or plugins to integrate google plus sign with just one line. 

For the API and backend layer i decided to use the play framework

###angularjs

So if you plan to integrate third party services or javascript frameworks look first on the [ngmodules](http://ngmodules.org/) site 
if exists a module integration for it. 

Thanks to the great modularity of angularjs you can easily extends the angularjs framework. You can write interceptors to extends the ajax functionality of angularjs or with directive you can even extends the html markup with your own tags and so on. If you write a module than keep in mind to implement it with the right abstraction from your app. Maybe if you wish than populate it as open source and offer it for other developers. It is very is to bundle a angularjs module and make it available for other developers. First submit a module description to the ngmodule site so that it can be found. The code of your module should be hosted by github than the ngmodule entry can link to it. 

For an example of an own implemented angularjs modul you can look at the  

AngularJs fits perfectly in a HTML 5 web application because they are exists a lot of modules that brings HTML 5 features like local storage to

###play framework