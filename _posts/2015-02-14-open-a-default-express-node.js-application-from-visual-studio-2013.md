---
layout: post
title: "Open a default Express node.js application from Visual Studio 2013"
date: 2015-02-14 13:30:00
description: How to open and further develop an Express node.js application from Visual Studio 2013
categories: [node.js]
tags: [Express, Visual Studio]
fullview: false
comments: true
shortinfo: 
---

#### node.js and Visual Studio

[node.js][node] is a very popular framework which allows having Javacript executed on the server. This is what everybody reads when navigating on the [official site][node]:
_Node.js® is a platform built on Chrome's JavaScript runtime for easily building fast, scalable network applications. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient, perfect for data-intensive real-time applications that run across distributed devices._

During the last couple of years Microsoft has put a lot of effort to provide a nice experience when we want to develop a node.js application inside Visual Studio. This comes of course in conjunction of supporting node.js hosting on the company's cloud platform [Microsoft Azure][nodeAzure]. We are able to develop any node.js application in Visual Studio because of the [Node.js Tools for Visual Studio][nodetools] awesome open source project. This is an extension that is completely free and anyone who is interested could install it on Visual Studio. After installing the extension we can create various node.js applications as we can see in the following picture.

<div class="row">
   <div class="col-sm-6 col-sm-offset-3 col-md-4 col-md-offset-4">
        <a href="/assets/images/newNodeProject.jpg" class="new node project">
            <img src="/assets/images/newNodeProject.jpg" alt="new node project">      
        </a>
   </div>
</div>

#### Open an existing node application

The most interesting part according to my opinion is the first one, **From existing Node.js code,** as it gives us the opportunity to open an existing node application that was created from a different IDE and maybe on a different platform (linux, OSX). This option gives us tremendous freedom to start contributing in a node.js project that some parts of the team use different IDE and are on different platforms and we can still use Visual Studio without problem. Let me demonstrate how this works and also mention a fix to a minor problem.

#### Create a default Express application

The first step is to create the default Express application. I am not going to explain the prerequisites of doing this as [here][expressCreate] you can find very detailed instructions. After we have installed all the required dependencies and we have created a folder somewhere in our system, we should open a command windows to the newly created folder and just hit:
{% highlight c# %}
express firstExpressApplication
{% endhighlight %}
and after this is finished we have to move the newly created folder and install the referenced node packages. This can be done my hitting:
{% highlight c# %}
cd firstExpressApplication
npm install
{% endhighlight %}
At this point we have a very simple Express application which we can launch by typing in the command window
{% highlight c# %}
set DEBUG=firstExpressApplication & node .\bin\www
{% endhighlight %}
After doing this just open a browser tab and navigate to the url: http://localhost:3000 and you should see the default express application running.

#### Open the Express application from Visual Studio

Now is the most interesting part where we can open this application from visual studio and make a small change. After giving a name in the window that is shown in the picture above we press next and we are presented with a window like the one following where we should choose the folder that contains the application's code.

<div class="row">
   <div class="col-sm-6 col-sm-offset-3 col-md-4 col-md-offset-4">
        <a href="/assets/images/selectforlder.jpg" class="select node folder">
            <img src="/assets/images/selectforlder.jpg" alt="select node folder">      
        </a>
   </div>
</div>

After clicking next a window like the following is shown to us where we can choose which file should be executed when F5 is pressed.

<div class="row">
   <div class="col-sm-6 col-sm-offset-3 col-md-4 col-md-offset-4">
        <a href="/assets/images/selectstartfile.jpg" class="select start file">
            <img src="/assets/images/selectstartfile.jpg" alt="select start file">      
        </a>
   </div>
</div>

Here is the small problem as it doesn't give us the option to choose the bin\www file which contains the initialization logic. We have to manually change this after the Visual Studio project creation is finished. We are leaving the app.js file as selected and click next. The coming window is a great thought as it gives the flexibility of storing the Visual Studio project file in a different place than the original Express application. This means that we could even not add this file to source control and definitely it is not going to bother other people in the team that they don't use Visual Studio.

<div class="row">
   <div class="col-sm-6 col-sm-offset-3 col-md-4 col-md-offset-4">
        <a href="/assets/images/selectprojectlocation.jpg" class="select project location">
            <img src="/assets/images/selectprojectlocation.jpg" alt="select project location">      
        </a>
   </div>
</div>

#### Fixing the problem of initial file

When the importing of the project is finished we can press F5 in order to achieve the same result as previously where we start the project from command line. But if we do this we will experience an error. A normal debugging session is starting and a command window with debugger details is shown but after a couple of seconds the windows is disappeared and no application is present. This is due the starting file selection we made earlier. In order to fix this issue we need to edit the project and change the corresponding setting manually. We have to spot the _<StartupFile>app.js</StartupFile>_** and change it to _<StartupFile>bin\www</StartupFile>_**. After saving the changes, reload the project and pressing F5 everything should be work as expected.

You can find more details for node.js tools for visual studio in the [codeplex project][nodetools]

[node]: http://nodejs.org/
[nodeAzure]: http://azure.microsoft.com/en-us/develop/nodejs/
[nodetools]: https://nodejstools.codeplex.com/
[expressCreate]: http://expressjs.com/starter/generator.html