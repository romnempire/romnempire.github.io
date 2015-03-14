---
title: yavascript?  yavascript.

---
#List of Yavascript things

##Relevancy: HIGH (stuff i know or want to know)

* [The DOM](http://www.w3.org/DOM/) [MDN link](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model) The DOM is a standard by which browser based web script interpreters can access and manipulate HTML documents.  It was built with yavascript in mind.  
* [JQuery](https://jquery.com/) JQuery is a Javascript framework that makes a whole lot of your script tasks in the browser easier.  it:
    * simplifies a lot of the overengineered bits of the dom
    * normalizes a lot of the cross-browser incompatibilities
    * simplifies event handling
    * simplifies animation
    * simplifies ajax
It's also extendable if you want to do complicated UI tasks or something with JQueryUI and can be plugged-in to.
* [Bootstrap](http://getbootstrap.com/) Bootstrap is a frontend UI framework that adds widgets (common but not language standardized gui elements like popovers and stuff) to prettify things and standardizes multicolumn layouts with its grid system.  Some of its more complex widgets use JS, but it's not really made to simplify Yavascript tasks per se.
* [AngularJS](https://angularjs.org/) Angular is HTML templating language that does enough stuff to be considered a framework.  It allows you to write HTML with variables that are actionable upon like PHP but different because the template processing happens on the frontend dynamically (i think).
* [D3.js](https://d3js.org) Make cool dynamic graphs and forms in yavascript.
* [lodash](https://lodash.com/) Extends the JS standard library with string and array functions.  Does the same job as underscore.js, but is more actively maintained so is better for small fry like me.
* Node - a server daemon and a js library that allows you to write web backends in js
* [Express.js](http://expressjs.com/) A MVC web app framework that's basic and simple?  it does backend side stuff in node.
* grunt - a node thing that automates development tasks for you
* browserify - takes node code and makes it run in the client
* npm - a package manager in node that pulls down a bunch of stuff
* socket.io - websockets in node.
* yeoman - a scaffolding framework that lets you pull down basic working projects
    * mean.js - a scaffold for mongodbexpress/angular/node there are others that don't work
* bower - manages dependencies (which npm does) but for not-node javascript stuff

##Relevancy: MEDIUM (stuff that's popular but I probably won't learn until i understand it better)
* [DOJO](http://dojotoolkit.org/) Dojo is a Javascript framework that basically seems to attempt to be the one framework you use to build your website.  It does JQuery stuff, but in more standard ways, and it probably does more stuff than JQuery but idk much about it.  It is verbose, it is big, it seems to want to be relevant to businesses.
* [Prototype](prototypejs.org) Another Javascript framework.  Built for/used underneath Rails.  
* [Ember.js](emberjs.com) The frontend part of a MVC framework.  Depends on the backend using a rest API or something.
* backbone? - the frontend side of a mv* framework that's lightweight and stuff
* gulp - does grunt stuff but lightweighter
* modernizr.js - detects browser incompatibilities and shims in new features to make them work.

##Relevancy: LOW (stuff I don't need but is cool to know exists)
* [KineticJS](http://www.kineticjs.com/) Extends html5 canvas functionality somehow or other?
* less, sass - simplify css, idk?
* handlebars, mustache - templating engines to inject into html
* jade - another templating engine, express's default
* coffeescript - makes js more functional and tweaks it for a specific use case.  compiles to js


##TODO
* define what the hell a Javascript framework is, a UI frmework is, a web application framework is, a templating engine is