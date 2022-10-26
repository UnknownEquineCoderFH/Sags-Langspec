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

#### 1.5 Definitions and Acronyms
! TODO (FILL OR REMOVE)


---


### **2. Overview**

#### 2.1 User Needs
<p style="font-size: 16;">
The typical user of this app.
! TODO (FILL OR REMOVE)
</p>

#### 2.2 Assumptions and Dependencies
Dinu, prolly is shit
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
<li> Sign In the app.
<li> Keep a collection of favourite places.
<li> Interact with QRs in the environment.
<li> Share their knowledge and participate in active cache hiding.
</ul>

#### 3.3 Functional Features
<ul style="font-size: 16;">
<li> Sign In are implemented with a 2FA protocol in mind (biometric/email link + credentials).
<li> Upon scanning a QR code, virtual reality should be introduced in the scene.
<li> App should be multiplatform, preferrably with the same code base.
<li> Calls to the database should be handled by a proxy server.
<li> Content should be filtrable by tag, location and popularity.
<li> Database should be abstracted away from the front-end, a simple rest API from app to server should serve as a middleware, while the server handles different services to gather the data and serving it.
<li> The final product should be distributable.
<li> AR should be implemented using well known technologies.
</ul>

#### 3.4 Nonfunctional Requirements
<ul style="font-size: 16;">
<li> Median TTI should be lower than 1 second.
<li> Gameification is key, interactions and feedbacks is as important as the feature itself.
<li> Dark Mode and Accessibility are fundamental for a democratic user experience.
</ul>


---


### **4. Workload and Responsibilities**

#### 4.1 Components built in-house
! TODO (FILL OR REMOVE)

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

