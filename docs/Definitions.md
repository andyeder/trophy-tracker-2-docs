# Introduction 

This living document is intended to provide guidance to frontend (FE) developers in the construction of code and unit tests to ensure consistence throughout the project. 

This convention comprises a number of rules intended to ensure best practice is followed in terms of sound Software Engineering principles as well as project/technology specific guidance. 

## Frontend Anatomy 

The three core technologies of the web (HTML, CSS and JavaScript) have been designed to provide content authors with the facilities to produce interactive web sites. The web platform has been adopted by the application development community primarily to overcome issues with maintenance and distribution of the user interface. To that ends frameworks have been developed that employ the core technologies (not necessarily as they were originally intended) and apply a development architecture to aid application construction. The primary challenge for such frameworks has been the balance between network efficiency and user experience and consequently the Single Page Application (SPA) approach has become prevalent.  

A SPA provides a single top-level HTML file that load data as and when required as indicated by the user's interaction. In this context the term data includes not just information to be presented to/manipulated by the user but also the artefacts that are combined to make the screen through which the use interacts.  

The composition of a SPA can be described as follows: 

### PAGE: 

The top-level HTML file plus application-wide CSS styling and JavaScript (JS). 

### SCREEN:  

One or more screens that populate a large portion or the entirety of the browsers display. Which screen is presented at a time is defined by routing and controlled by the user as they navigate the application. Whilst some caching can be used it is not unusual for additional requests to be issued to the server to retrieve the files defining the screen as to the user navigates towards it.  

### LAYOUT:  

Also known as templates. Where a number of screens follow a common pattern, especially when Responsive Web Design (RWD) is employed it is often a good policy to define a high-order component to control to presentation.  

### COMPONENTS:  

Discreet functional units that provide specific functionality can be packaged up and provided to the project as components. These may or may not be graphical (GUI) in nature but are intended to aid maintainability and provided consistency between screens. Non-graphics components will often be described as services or helps.  

When the number of components reach a critical point two strategies 

1. Employ a methodology such as Atomic Design to arrange the components 

1. Relocate components to a separate project and provide as a library especially when more than one project needs to make use of them.  

