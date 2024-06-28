# Care2Share
## Overview:

<img src="https://github.com/Pal-96/care2share-finalproject/assets/119008696/a247ade9-ad72-4c80-87bd-5a9352ae96c8" style="border: solid black;" alt="LandingPage">

## Key Features:
 
- **User Authentication & Profiles:** User can register as individual or NGO. Support secure password storing.
- **Surplus Food Postings:** Individuals can post surplus food listings and associated details. NGOs can search for surplus food and place orders.
- **Donation:** Users can make monetary donations to NGOs.
- **Event Management:** NGOs can create events for food distribution. Users can volunteer or donate.
- **Blogging & Awareness Campaigns:** Users can read, write, like, dislike, comment, update or delete blogs.
- **Email Notifications & Map Functionality:** Users receive email notifications after creating Foodposts. NGO users get email notifications after booking the food post with map locations for pickup.

## Steps to set up config.json
This project requires a configuration file (config.json) to store Google Maps Api Key. This file is ignored by Git to ensure the key remains private.
1. Create config.json in the app/src directory of the project (refer the template file).<br/>
<img width="389" alt="config" src="https://github.com/Pal-96/care2share-finalproject/assets/119008696/80504f06-6a2c-4e6d-bab1-31a59dd5dfa8">
<br/>
2. Replace YOUR_API_KEY_HERE with the actual API key.<br/>
3. Save the file.

## Steps to set up .env
This project requires a .env file to store the server port no. and your MongoDB connection parameters. This file is ignored by Git to ensure your connection is private.
1. Create .env file in the service directory of the project (refer the template file).<br/>
<img width="895" alt="env" src="https://github.com/Pal-96/care2share-finalproject/assets/119008696/f40e3345-e6db-4f85-ac84-53ad2a35115a">
<br/>
2. Replace the placeholders with actual data.<br/>
3. Save the file.

## Instructions to execute the project:
1. Clone the repository `git clone https://github.com/Pal-96/care2share.git`
2. Navigate to service directory in local machine and add .env file for MongoDB connection (port: 3000)
3. Execute the command: `cd service`
4. Execute the command: `npm install`
5. Execute the command: `node server.js`
6. Navigate to app directory in local machine and add config.json file
7. Open new terminal on project root directory and execute: `cd app`
8. Execute the command: `npm install`
9. Execute the command: `npm run dev`
10. Open the localhost link on the browser to view the application

## Object Model

```mermaid

---
title: Object Model for Care2Share 
---


classDiagram
  class FoodPost {
    -int fp_id
    -String name
    -int numOfPeople
    -String shelfLife
    -Date timestamp
    -String status
    -String description

    + int getFpId()
    + void setFpId(int fp_id)
    + String getName()
    + void setName(String name)
    + int getNumOfPeople()
    + void setNumOfPeople(int numOfPeople)
    + String getShelfLife()
    + void setShelfLife(String shelfLife)
    + Date getTimestamp()
    + void setTimestamp(Date timestamp)
    + String getStatus()
    + void setStatus(String status)
    + String getDescription()
    + void setDescription(String description)
  }

  class Events {
    -int event_id
    -String eventTitle
    -String description
    -Date timestamp

    + int getEventId()
    + void setEventId(int event_id)
    + String getEventTitle()
    + void setEventTitle(String eventTitle)
    + String getDescription()
    + void setDescription(String description)
    + Date getTimestamp()
    + void setTimestamp(Date timestamp)
  }

  class BlogPost {
    -int blog_id
    -String title
    -String content
    -Date createdDate
    -int likes
    -int dislikes

    + int getBlogId()
    + void setBlogId(int blog_id)
    + String getTitle()
    + void setTitle(String title)
    + String getContent()
    + void setContent(String content)
    + Date getCreatedDate()
    + void setCreatedDate(Date createdDate)
    + int getLikes()
    + void setLike(int likes)
    + int getDislikes()
    + void setDislikes(int dislikes)
  }

  class Donation {
    -int donation_id
    -double amount
    -Date timestamp

    + int getDonationId()
    + void setDonationId(int donation_id)
    + double getAmount()
    + void setAmount(double amount)
    + Date getTimestamp()
    + void setTimestamp(Date timestamp)
  }

  class Comment {
    -int comment_id
    -String content
    -Date createdDate

    + int getCommentId()
    + void setCommentId(int comment_id)
    + String getContent()
    + void setContent(String content)
    + Date getcreatedDate()
    + void setcreatedDate(Date createdDate)
  }

  class User {
    -int user_id
    -String username
    -String email
    -String password
    -String role
    -String contactNo

    + int getUserId()
    + void setUserId(int user_id)
    + String getUsername()
    + void setUsername(String username)
    + String getEmail()
    + void setEmail(String email)
    + String getPassword()
    + void setPassword(String password)
    + String getRole()
    + void setRole(String role)
    + String getContactNo()
    + void setContactNo(String contactNo)
  }

  class Address {
    <<value object>>
    -String line1
    -String line2
    -String city
    -String state
    -String zipCode
    -String country

    + String getLine1()
    + void setLine1(String line1)
    + String getLine2()
    + void setLine2(String line2)
    + String getCity()
    + void setCity(String city)
    + String getState()
    + void setState(String state)
    + String getZipCode()
    + void setZipCode(String zipCode)
    + String getCountry()
    + void setCountry(String country)
  }

  class Person {
    -int person_id
    -String name
    -Date dob

    + int getPersonId()
    + void setPersonId(int person_id)
    + String getName()
    + void setName(String name)
    + Date getDob()
    + void setDob(Date dob)
  }

  class Organization {
    -int organization_id
    -String name
    -String type

    + int getOrganizationId()
    + void setOrganizationId(int organization_id)
    + String getName()
    + void setName(String name)
    + String getType()
    + void setType(String type)
  }

  FoodPost "0..n" *-- "1" User
  BlogPost "0..n" *-- "1" User
  Donation "0..n" *-- "1" User
  Donation "0..n" *-- "1" Organization
  Comment "0..n" *-- "1" User
  User <|-- Person
  User <|-- Organization
  User  o--  Address
  FoodPost "1" *-- "1" Address
  Events "0..n" *-- "1" Organization
  Comment "0..n" *-- "1" BlogPost
```