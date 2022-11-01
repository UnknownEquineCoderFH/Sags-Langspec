### **1. Introduction**

#### 1.1 Purpose
<p style="font-size: 16;">
The intent of this document is to specify broad requirements regarding the developement of the ArtCafe project.
</p>

#### 1.2 Intended Audience
<p style="font-size: 16;">
This document was written for stakeholders and functional developers of this project.
</p>

#### 1.3 Intended Use
<p style="font-size: 16;">
The intended use for this document is that of a knowledge base, where all technical and non technical specifications, finds, plans, aspirations and philosophies stay.
</p>

#### 1.4 Scope
<p style="font-size: 16;">
Included in this collection, will be the result of a 3-month research that include documentation reviews, surveys, internal tests and early development prototypes.
It should not and will not include any findings that arose after November the 14th.
</p>

---


### **2. Overview**

#### 2.1 User Needs
<ul style="font-size: 16;">
<li>User needs to be able to login
<li>User must have the ability to scan the QR code using camera
<li>Information must be presented simple and visible so the user will not have any troubles and issues achieving their goal of using the application efficiently
<li>The font being used must be compatible with most of the languages so the user will be able to read everything
<li>Data of the user must be also protected in order to prevent any malicious behavior
<li>User must have the choice to edit the data that is being stored about them, meaning maintainability of the data.
<li>The user shall navigate using an intuitive interface, favouring good colour contrast and simply recognisable icons.
</ul>

#### 2.2 Assumptions and Dependencies
<ul style="font-size: 16;">
<li>We intend to create a cross-platform application.
<li>We expect the application to work for up to 200 users at the same time, with the possibility to upscale the number of users depending on how successful the launch will be. 
<li>We use (The application uses) Python as the main programming language. 
<li>In order to create the cross-platform app we will use the Kivy library.
<li>The database aspect would be delegated to a third party and should be performed using a NoSQL DBMS.
<li>For augmented reality, we are planning on using the OpenCV python library.
</ul>

---


### **3. Requirements**

#### 3.1 Business Requirements
<ul style="font-size: 16;">
<li> Create a connected user base.
<li> Collect knowledge.
<li> Update knowledge about places of interest.
<li> Have multiple admins.
<li> Produce reconstructions of historical sights.
</ul>

#### 3.2 User Requirements
<ul style="font-size: 16;">
<li> The ability to create a personal account within the application and sign into the application using said account.
<li> The ability for a user to keep a collection of favourite locations.
<li> Potentially allowing users to share favourite locations between one another.
<li> Functionality related to scanning the QR Codes and, through the use of Augmented Reality, interpreting them into visualized historical locations within the application.
<li> Functionality that would allow users to chat with each other within the application, giving them a space to discuss locations and exchange any related knowledge.
<li> (Physical cafe) Providing clients with free internet connection.
<li> (Physical cafe) Providing clients with what you would normally find in a cafe (coffee, desserts, snacks, and any other food and drink).
<li> (Physical cafe) Providing clients with restrooms, chairs, tables, and every other requirement in order for the cafe to be FDA-compliant.
</ul>

#### 3.3 Functional Features
<ul style="font-size: 16;">
<li> Registration/Sign In process is to be implemented with a Two-Factor Authentication protocol in mind (usage of an extra login verification step, e.g. biometric, email link + credentials, or even an external authentication app like Google Authenticator).
<li> Upon scanning a QR code, the application should interpret said code and display a location using augmented reality.
<li> The app should be cross-platform, with the same code base and shared database.
<li> Calls to the database should be handled by a proxy server.
<li> If user consent is granted, the application should collect data related to QR code popularity, the amount of times a location has been "favourited", as well as data related to the popularity and the ways that in-app functionality is used.
<li> Content should be filterable by tag, location and popularity.
<li> Database should be abstracted away from the front-end, a simple rest API from app to server should serve as a middleware, while the server handles different services to gather the data and serving it.
<li> The final product should be distributable.
<li> Augmented Reality should be implemented using well known technologies (for example the AugPy Python library).
</ul>

#### 3.4 Nonfunctional Requirements
<ul style="font-size: 16;">
<li> Median Time-To-Interactive (TTI) should be lower than 1 second.
<li> Gameification is key, interactions and feedbacks is as important as the feature itself.
<li> Dark Mode and Accessibility are fundamental for a democratic user experience.
<li> Front-end functionality should be kept simple and intuitive, to prevent as much end user confusion as possible.
</ul>


---


### **4. Workload and Responsibilities**

#### 4.1 Components built in-house
<p style="font-size: 16;">
To be produced in-house by our internal development team:
</p>
<ol style="font-size: 16; list-style-type: upper-roman;">
<li> 
The cross-platform frontend our users interact with. 
<br> Used Frameworks: Kivy library
<br> Bindings will be exported using: Jinja, Py2HTML
<br> HTTP Server will run using: FastAPI + Uvicorn
</li>
<li> 
A notification service 
<br> The specifications are as follows: we should be able to interact with users trough notifications that they allow. 
<br> Preferred notification types are: push and pop. 
<br> It listens for commands from the backend.
<br> Most common use-case: We want the user to use our product more than once so we send a push notification that says: " We have new places to explore! Come and bring your friends!"
</li>
</ol>

#### 4.2 Components to be outsourced
<p style="font-size: 16;">
To be produced outside the scope of our internal development efforts is the following:
</p>
<ol style="font-size: 16; list-style-type: upper-roman;">
<li> 
A cloud hosting solution that will serve to accomodate main database solution and its endpoint handler. 
<br> Accepted hosting services are: AWS and Azure.
</li>
<li> 
A database to be deployed to such host. 
<br> The specifications are as follows: it should be able to easily accomodate for various data files, such as text, unstructured objects, images, videos and 3D object models. 
<br> Preferred architecture is that of Document-based NoSQL databases. 
<br> The amount of data it should hold is in the order of tens to hundreds of TeraBytes.
<br> Most common operations that need to be performed are reads and writes, while updates and deletes will be far less common. Ideally, optimisation should come for the former two.
</li>
<li> 
A microservice that allows simple interfacing with the database.
<br> Such microservice will be accessible via HTTPS, be authentication-aware (only produce data responses from allowed IPs and only with the valid credentials) and capable of handling thousands of requests per second during peak times.
<br> It will have clear and simple routing, especially for most common requests.
</li>
</ol>

