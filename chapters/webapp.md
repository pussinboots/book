#Web Application

This chapter discover the new technologies, frameworks and tools to develop Web Application these days. Here is the web application defintion from wikipedia.
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

I guess the need for Web Application that are renderd on the server side is over and waste a lot of resources on the server side. What belongs to the client should be performed on the client side. The tool support for JavaScript is more or less powerful like for Java. They are package manager, test frameworks, server runtimes, code completion and all what you can imagine and exists for your programming language of choice. 

##Frameworks

###angularjs

###play framework

##Database

###slick

####Lessons learned with play and c3p0

I had big trouble to get the ClearDB SSL communication to work with play 2 and scala. So here my solution.

First of all you have to deal with keystore and truststore related topics
#####KeyStore and TrustStore

#####Definition
What i've learned is keystore and trustore are more or less based on the same file but for different purpose.
Here a simple summary what both means.
* trustore is used to validate server certificates 
* keystore is to validate client authentication

There a lot of good articles about the difference below are some of them

* [Stackoverflow discussion about](http://stackoverflow.com/questions/318441/truststore-and-keystore-definitions)
* [Java realted discussion](http://javarevisited.blogspot.de/2012/09/difference-between-truststore-vs-keyStore-Java-SSL.html)

#####Usage

There are also a lot off tutorials how to setup custom keystore and truststore and here is my for the Java 7 JDK from oracle it could not work with openjdk i don't try it.

First of all i had a special purpose for the truststore because it was used for different things the first one
is to get the ssl communication working with cleardb hosted mysql and second also web service requests from the play controller
to a external https endpoint. To get only the first thing to work you can build your own truststore contains only the cleardb server certificate.

But to get also the second thing to work you should copy the java standard truststore and import the cleardb server certificate to them.

Require the cleardb pem certifcates download at [ClearDB Dashboard](https://www.cleardb.com/dashboard). This certificate i guess are app specific so download it for your app you want to enable ssl communication for.

You need the two following files
* ClearDB CA Certificate
* Client Certificate

Store it in the same directory where you want to put your truststore and keystore file


* first step locate your java truststore called cacerts it should be found at [your jdk folder]/jre/lib/security/cacerts
for example on my ubuntu 14.04 system i found it at /usr/lib/jvm/java-7-oracle/jre/lib/security/cacerts
* second make a copy of it
\begin{codelisting}
\codecaption{copy cacerts}
\label{code:cacerts}
```sh
cp /usr/lib/jvm/java-7-oracle/jre/lib/security/cacerts ./
```
\end{codelisting}
* third import the ClearDB CA Certificate to the cacerts truststore you copied. The first command list the existing certificates the should be round 80 entries could be more or less but to check that the import was successful it should contains one more after the import was done. The cacerts password is changeit (was it by my jdk 7 oracle). There will also propmt a question trust that certificate answer it with yes
\begin{codelisting}
\codecaption{import truststore}
\label{code:truststore}
```bash
keytool -list -keystore cacerts
keytool -import -alias clearDBCACert -file cleardb-ca.pem -keystore cacerts 
keytool -list -keystore cacerts 
```
\end{codelisting}
* fourth import the Client Certificate in a new keystore file (the file name of the ClearDB Client Certificate depends on your app so for me it was bfa19bff3390d4-cert.pem) with the list command you could verify that the keystore contains only your Client Certificate An password input will prompt so set a password of your choice but you will need it later so remeber or store it in a text file for later use.
\begin{codelisting}
\codecaption{import keystore}
\label{code:keystore}
```sh
keytool -import -file bfa19bff3390d4-cert.pem -keystore keystore -alias clearDBClientCertificate
keytool -list -keystore keystore
```
\end{codelisting}

More or less that was it with the creation of your truststore and keystore.

#####Play 2 and c3p0

######Better c3p0 logging to simply debug what the hell was the problem with ssl
Before we use the created truststore and keystore i would suggest to activate better logging of c3p0 in a play 2 runtime.
You could ask why it is specified as -D parameter that was the only working way i found. My first approach was System.setProperties but it didn't work and it should not be used in production it is only to debug if the ssl cleardb database connection is working and when not get a detailed exception why not. The why not part is import without the c3p0 logging i get only play 2 exception with there was a problem wis the the underlying database so you don't now what was the problem the truststore was not configured proberly or the password was wrong and so on.

* activate c3p0 logging in play 2
\begin{codelisting}
\codecaption{activate c3p0 logging}
\label{code:c3p0 logging}
```bash
play -Dcom.mchange.v2.log.MLog=com.mchange.v2.log.FallbackMLog -Dom.mchange.v2.log.FallbackMLog.DEFAULT_CUTOFF_LEVEL=ALL run
```
\end{codelisting}

play -Dcom.mchange.v2.log.MLog=com.mchange.v2.log.FallbackMLog -Dom.mchange.v2.log.FallbackMLog.DEFAULT_CUTOFF_LEVEL=ALL run

######Activate your keystore and truststore

Require your cleardb jdbc url you can get it with the heroku command like below or get it from your application settings from the heroku dashboard.
\begin{codelisting}
\codecaption{heroku config}
\label{code:heroku config}
```bash
heroku config
```
\end{codelisting}

With the next command you start your play app with your custom keystore and truststore and communicat with your live cleardb database over ssl hopefully.

```bash
play -Djavax.net.ssl.keyStore=keystore -Djavax.net.ssl.keyStorePassword=<you remember your keystore password than insert here> -Djavax.net.ssl.trustStore=cacerts -Djavax.net.ssl.trustStorePassword=changeit -DCLEARDB_DATABASE_URL=<insert your cleardb jdbc url here> -Dcom.mchange.v2.log.MLog=com.mchange.v2.log.FallbackMLog -Dom.mchange.v2.log.FallbackMLog.DEFAULT_CUTOFF_LEVEL=ALL run
```

Hopefully everything work like expected otherwise show in the next comming exception section what goes wrong by my first try and learn from it. (Missing at the moment) Next i put a code example how you could set all the play 2 stuff above with code.

######TODO add some potential exception they could get here and what they mean and how to fix it


######Play 2 Code Example enable SSL truststore and c3p0 logging

You could find more or less the same code in this project look into the following files.

* [Global](https://github.com/pussinboots/bankapp/blob/master/app/HTTPSRedirectFilter.scala)
* [DB](https://github.com/pussinboots/bankapp/blob/master/app/model/DB.scala)
* [application.conf](https://github.com/pussinboots/bankapp/blob/master/conf/application.conf)

First implements a [Play 2 Global object](http://www.playframework.com/documentation/2.0/ScalaGlobal) that register the system properties for your truststore and keystore and also for the c3p0 logging. I had a proplem with a [controller test](https://github.com/pussinboots/bankapp/blob/master/test/integration/GoogleControllerSpec.scala) that test an external web service call that i mocked with the great [Betamax](http://freeside.co/betamax/) tool and this tool had some problem by mocking https calls with my custom truststore and keystore so i decided to make it configurable within the application.conf and disable it in that test above. The import line is
```
FakeApplication(additionalConfiguration=Map("enableDBSSL" -> "false")
```
but it doesn't matter here. One my first approach i set the system properties in my database intialize code outside the Global object but that had no effect so i guess it was to late because the SSLEngine initialization was done before so do it in the Global implementation or on the command line.

```scala
import play.api._
import play.api.mvc._

object Global extends GlobalSettings
{
    override def onStart(app: Application) {
      val enableDBSSL = app.configuration.getBoolean("enableDBSSL").getOrElse(true)
      val enablePoolLogging = app.configuration.getBoolean("enablePoolLogging").getOrElse(false)
      if(enableDBSSL) {
        Logger.info("set custom truststore for cleardb mysql ssl connections")
        WithSSL()
      }
      if(enablePoolLogging) {
        WithPoolLogging()
      }
      Logger.info("Application has started")
    }
    override def onStop(app: Application) {
      Logger.info("Application shutdown...")
    }
    def WithPoolLogging() {
     System.setProperty("com.mchange.v2.log.MLog","com.mchange.v2.log.FallbackMLog")
     System.setProperty("com.mchange.v2.log.FallbackMLog.DEFAULT_CUTOFF_LEVEL","ALL")
    }
    def WithSSL() {
      System.setProperty("javax.net.ssl.keyStore", "keystore")
      System.setProperty("javax.net.ssl.keyStorePassword", Properties.envOrElse("SSLPW", ""))
      System.setProperty("javax.net.ssl.trustStore", "cacerts")
      System.setProperty("javax.net.ssl.trustStorePassword", Properties.envOrElse("SSLPW2", ""))
    }
}
```

Activate it in your application.conf with the following or remove the if statements.

```
enableDBSSL=true
enablePoolLogging=true
```

So here was the complete Global implementation and the important lines are
```scala
def WithSSL() {
      System.setProperty("javax.net.ssl.keyStore", "keystore")
      System.setProperty("javax.net.ssl.keyStorePassword", Properties.envOrElse("SSLPW", ""))
      System.setProperty("javax.net.ssl.trustStore", "cacerts")
      System.setProperty("javax.net.ssl.trustStorePassword", Properties.envOrElse("SSLPW2", ""))
    }
```
That set your custom truststore and keystore the files has to be on the project root folder but can also be placed everywhere in the project adapt the relative path here.
```scala
Properties.envOrElse("SSLPW", "")
```
This line prepare it for a deployment on [heroku](http://www.heroku.com) for example so that the keystore and truststore password are not stored in the git repository. But if you want to run your play 2 app locally than you have to specify them in a special way. And don't forget to configure it as environment variable on heroku with the command line tool or the dashboard. For example
```bash
heroku heroku config:add SSLPW2=changeit
```

To run it locally start play with the following commands.
```bash
export SSLPW=<your keystore password here>
export SSLPW2=changeit
play run
```
Ask me not why it is so but there is a big difference between system properties and environment variables. And heroku works with environment variables not with system properties so feel free to use -D and System.getProperty in your code but that will not work on heroku.
```bash
play -DSSLPW=<your keystore password here> -DSSLPW2=changeit run
```
Will not work with Properties.envOrElse() !!!!!! cost me some headache to find this out
