WebFramework
============

A specification for a generalized full-stack web framework.

Introduction
============

The web development ecosystem is in a state of rapid evolution. Its evolution is chaotic and decentralized, lending to the development of frameworks, libraries, tools, and best practices that are at best de facto standards. As is often the case with software, a set of solutions to common problems often appear simultaneously. Eventually some solutions fade in to obscurity, and community-driven standards drive the success of a few (or only one) solution.

The purpose of this document is to outline the minimal set of "solutions" required in a full-stack web development framework. A "solution-set" may be defined as either a monolithic multi-purpose solution or a curated set of micro-libraries that each fulfill a specific purpose.

The goal of this outline is to attempt to weed out unnecessary components and determine core functionality for a successful full-stack web architecture. To limit the scope of this document, particular focus is placed on solutions that remain in active production code--build tools, etc. shall not be included.

Overview
========

Several web architectures exist, all of which currently involve a client-server arrangement with either HTTP and/or websocket communication. This document focuses on a "thick client" in which a full offline-capable webapp is delivered to the client. Note that the "thin" vs. "thick" client terminology traditionally refers to hardware on a network, in this case it is being applied only to the application software. The client-side app communicates with a server using RESTful techniques. The server-side app mostly handles composition and delivery of the initial client app, authentication, and an interface to a database.

While thin-client webapps tend to be more popular, a thick client implementation has the following advantages:

1. Significant reduction of server-side resource use
2. Reduction of bandwidth use when taking advantage of "appcacheing" to store the app on the client device
3. Quicker load times of the application after initial appcache
4. Greater responsiveness when switching application state
5. Complete or partial persistence when a connection to the server is lost

Some disadvantages of a thick client architecture:

1. Slower initial load times
2. Increased use of client-side resources

Slower initial load times may be partially overcome or masked by loading a pre-rendered document prior to loading the application code, and reducing the application payload size. Reducing the application payload often requires reducing the use of third-party libraries that carry unused functionality, instead opting for micro-libraries that perform one or very few functions. The increased use of client-side resources is inherent in the architecture, but in many cases represents a negligible impact on the user experience.

Client Architecture
===================

Ideally, the client-side application is delivered as a single file containing all necessary functionality. Third-party libraries and all application components should be included in this file as part of a build step. While a variety of features and libraries may be included, the following core components should be included in a complete framework:

1. Client-side URL routing
2. Asynchronous HTTP and/or websocket communication client
3. Data indexing/storage
4. Data-to-hypertext rendering (e.g. templating)
5. Functional compartmentalization (controllers, modules, etc.)

Many features that are often included in frameworks, such as DOM manipulation or a coherent model-view-controller system are not listed as core requirements. The architectural core is only concerned with maintaining application state, sending/receiving/storing data, rendering data as HTML, and providing a "sandbox" for application code. DOM manipulation as well as abstract model handling, etc. lie within the application code so are not considered "core" functionality.
