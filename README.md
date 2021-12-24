# M.A.R.S - Mars Active Response System
Group project by Frédéric Goosens, Lenn Crochart, Caspar Nuël, Jorge David Garcia Prada and Stef Wauters

[TOC]

## General information
### History
The Mars Corporate War began when rival mega-corps used their finances and military muscle to fight over buying out a company and its vital resources. 

In early 2040, AquaMars, a mega-corp that specialized in underwater shipping and tech, went bankrupt, which lead to two rival aqua corps, Nestle and Red Bull, 
squaring off for a hostile takeover of AquaMars's remaining assets. 

At first, both corporations engaged in the typical opening rounds of corporate battle; stock manipulations and economic warfare, but as the conflict grew out of hand, it was only a matter of time before true fighting broke out.

### Concept
The potentially hazardous environment of business operations in a dark dystopian Mars, and The Mars Corporate War established there means that emergency management and response planning are critical to the health and safety of the workers of any company.

We are M.A.R.S. (Mars Active Response System). Our domain is based on IoT and Industrial Security solutions. We provide 24/7 emergency aerial vehicle dispatch with a reflex always-ready pilot, armed safety experts, and military-trained paramedics.

A client's health is monitored by a device we put on them, and if a client takes a turn for the worse, an aerial vehicle squad receives their GPS signal and arrives on the scene in minutes. Reaction time and additional perks are dependent on the client's insurance package.

## Proof Of Concept (POC)

Our proof of concept focuses on the employee side. Our clients that are subscribed to our service are monitored by a bio-sensor. When their vitals spike or flat lined, we send a team to their location to extract them and bring them to the nearest hospital. The action of sending a team to a client will be done through a map, with clients, domes and vehicles on it. To extract a client, you'll have to click on a client's dot and assign a vehicle to it. Once those 2 are connected, the closest hospital is determined and the route will be automatically set. We also made dashboards for the employees, so when they're running our website on their 2 monitors they can have a dashboard open and their map open. 
We did develop a small amount of the client's view as well. This includes our community aspect feature, the display of the dangerzones for people who are and aren't subscribed to our service.

## API Specifications
### Clients

Our API has 4 endpoints to get our clients and apply specific filters on our clients. 
- /api/clients      
This endpoint gives all clients we have/had in our business. This includes clients who do not have an active subscription any or clients who cancelled their subscription
- /api/clients/subscribed       
This endpoint returns all the clients of our company who have an active subscription. People who have a running subscription but are not reimbursed are also shown with this endpoint.
- /api/clients/{clientId}       
This endpoint returns the client's information given a valid MARS-ID. (ex: MARS-ID-001).
- /api/clients/location/{clientId}/{latitude}/{longitude}       
This endpoint is used to change the location of a user. This endpoint will be used to update their location when picked up by an ambulance on their way to the hospital. Another use case is to have their live location correctly displayed.

The use cases of these endpoints are to show our clients on our client's dashboard, show them on our map and to move them on our map.

### Vehicles
Our API also has 4 endpoints to give and change information about our vehicles.
- /api/vehicles             
This endpoint gives back all vehicles with their current locations, whether they're occupied and their identifiers.
- /api/vehicles/{vehicleId}         
This endpoint is used to search for a specific vehicle and return their location, occupation status and their identifier.
- /api/vehicles/location/{vehicleId}/{latitude}/{longitude}     
The point of this endpoint is to move a specific vehicle to another location. The 2 use cases of this endpoint is to display their current location and to see the progress from a client to the nearest hospital when they're saving a client.
- /api/vehicles/status/{vehicleId}/{status}     
This endpoint will be used together with the one mentioned above to quickly change the status (occupation) of a vehicle.

The use cases of these endpoints are to display and move vehicles on the employees' map.

### Subscriptions

This endpoint has one use case, and it's to display every subscription type we have with their name, price and description.

### Dangerzones

This endpoint will be used to show the clients' map the dangerzones. These zones are marked because there are a lot of people being saved there meaning could be a conflict over there.

### Domes

Our API has 2 endpoints for domes
- /api/domes        
This endpoint returns all domes that are on Mars with their  identifiers, locations and sizes.
- /api/domes/{domeId}       
This endpoint returns the specific dome you want with their respective identifier, location and size.

The use case of both these endpoints is to display the domes on the map for the employees.

### Overview

Overview is a bundle of vehicles, clients, domes and dispatches. The use case of this endpoint is to quickly get all the information needed to display on our employees' map.

### Dispatches

Our API has 4 endpoints for dispatches.

- /api/dispatches       
This endpoint shows every dispatch. A dispatch has an identifier, source details and destination details. A source can be a client or a vehicle and a destination can be a dome of client.
- /api/dispatches/{identifier} **GET**         
This endpoint returns a specific dispatch with their respective identifier, source details and destination details.
- /api/dispatches/{identifier} **DELETE**             
This endpoint simply deletes the specific dispatch.
- /api/dispatches/create        
This endpoint expects a specific body as explained in the yaml file to create a new dispatch.

The use cases of these endpoints are to display every dispatch at the dashboards for the employees as well to show/delete/create new dispatches on the employee map.

