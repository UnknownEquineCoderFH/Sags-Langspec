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

### **2. Overall Description**
#### 2.1 User Needs
<p style="font-size: 16;">
The typical user of this app.
</p>

#### 2.2 Assumptions and Dependencies

### **3. Requirements**
#### 3.1 Business Requirements
<ul style="font-size: 16;">
<li> Create a connected user base
<li> Collect knowledge 
<li> Update knowledge about places of interest
<li> Have multiple admins 
<li> Produce reconstructions of historical sights
</ul>

#### 3.2 User Requirements
<ul style="font-size: 16;">
<li> Sign In the app
<li> Keep a collection of favourite places
<li> Interact with QRs in the environment
<li> Share their knowledge and participate in active cache hiding
</ul>

#### 3.3 Functional Features
<ul style="font-size: 16;">
<li> Sign In are implemented with a 2FA protocol in mind (biometric/email link + credentials)
<li> Upon scanning a QR code, virtual reality should be introduced in the scene
<li> App should be multiplatform, preferrably with the same code base
<li> Calls to the database should be handled by a proxy server
<li> Content should be filtrable by tag, location and popularity
<li> Database should be abstracted away from the front-end, a simple rest API from app to server should serve as a middleware, while the server handles different services to gather the data and serving it
<li> The final product should be distributable
<li> AR should be implemented using well known technologies
</ul>

#### 3.4 Nonfunctional Requirements
<ul style="font-size: 16;">
<li> Median TTI should be lower than 1 second
<li> Gameification is key, interactions and feedbacks is as important as the feature itself
<li> Dark Mode and Accessibility are fundamental for a democratic user experience
</ul>

