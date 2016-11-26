Metro (0.6)

What is Metro?
=============
Metro is a library of components to support rapid development of applications that use ColdSpring and Transfer ORM. 

Impetus
=======
While developing projects with Transfer over the course of the past year, I've noticed a repetition 
in the application model code that led me to adopt some basic conventions thereby actively generating
much of the code I would have created with passive code generation.  Convention based code 
generation will only get you so far, there are nuances to an application model that are difficult to 
achieve with code generation.  To hedge this, Metro makes it easy to define concrete components 
(services or gateways) that extend the core Metro components, so one can write custom code to override
and/or augment the actively generated code.

Conventions
===========
The over-reaching convention for metro is the concept of packaging related object so that they are managed 
by a single service.  As an example, Metro includes a security package with simple User, Role and Permission
objects that are managed by a single UserService composed with a gateway for each object.  To achieve this,
Metro parses the transfer XML configuration into a simplified config structure.   

API
===
A service created by the Metro ServiceFactory provides get(), new(), list(), save() and delete() methods for objects
under a given package.  For example, the security package included in metro contains three objects: User, Role and
Permission.  One can use get("objectName") or get{objectName}(), etc. for each object managed by the service. The
syntactic sugar of get{objectName}() is achieved through onMissingMethod.

Setup
=====
Metro is setup using ColdSpring and Transfer.  You'll find a sample Coldspring bean definitions file in the tests/config
folder.  The Metro ServiceFactory accepts 5 constructor arguments.

1. TransferConfig (required) - The transfer configuration object.
2. BeanInjector (required) - The beanInjector found in the metro.lib package.
3. componentPath (optional) - The base component path in your application where each package can be found.
4. libPath (optional) - The base component path in your application where each package can be found.
5. afterCreateMethod (optional) - A method to call on Services or Gateways created by the ServiceFactory


Requirements
============
- Transfer (tested against 1.1)
- ColdSpring (tested against 1.2)

Installation and Testing
========================
To see Metro in action, follow the directions below.

1. place metro in web root
2. create a database and run the database schema files located in /metro/docs/sql/ (choose either mssql or mysql)
3. create a datasource "metro-security" pointing to the database
4. run mxunit tests under metro/tests

Acknowledgments
===============
A big thanks to Mark Mandel (http://www.compoundtheory.com), Bob Silverberg (http://www.silverwareconsulting.com) and
Matt Quackenbush (http://www.quackfuzed.com) for advice and guidance, and to Brian Kotek (http://www.briankotek.com/blog/)
for approving the inclusion of his BeanInjector and TDOBeanInjectorObserver components in the library.

