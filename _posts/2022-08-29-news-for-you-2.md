---
title: "News for you 1: Planning a new project"
categories: Project:News-for-you
tag: [Java, Spring, Troubleshooting]
toc: true
---

💻 This series is to record my work through a 6-weeks Spring project at the coding bootcamp.
{: .notice--success}


Since we now had a project plan, we moved on to the next step.


## Where to get the data
One of the teammates shared the link of [Big Kinds](https://www.bigkinds.or.kr/), a website mostly used for statistics purposes.
The site offers the organized lists of news articles in Excel files, so we decided to use those data for our search system.

## How much data to get
The website kindly shows the total number of news articles they have been collecting.
There were around 76 million when we checked.
We set our minimum data as 10 million, target data as 76 million, and maximum data as 100 million.
We decided to find a way and see if we could include foreign articles in our db, once we are done with putting all the data from Big Kind to our db.

## What database to use
We all agreed that when thinking about the amount of data we are going to deal with, the best choice for us was using NoSQL(RDBMS).
However, we decided to see if we could work with SQL first. In this way, we can check how different the performance can be between the two.

## ER Diagram design
We designed the ER diagram based on the table of the Excel file we downloaded.

![img.png](assets/images/2022-08-29-yournews-erdiagram.png)

## Create Entity
Based on the er-diagram, I made the entity files.


### Troubleshooting 1 - no resources directory(folder)
But when I tried to run the program to see if everything was right, there was no 'resources' directory.

![img.png](assets/images/2022-08-29-yournews-files.png)

This never happened before, so I googled the problem.
I think the issue was when I cloned the remote repo to my local, there was no application.properties file uploaded due to the security issue.
I made a new directory where it should have been and marked the directory as a 'resources' root.


### Troubleshooting 2 - MappingException

After creating the application.yml file and setting the database, I ran the app but it gave me the following error message.
```
org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'entityManagerFactory' defined in class path resource [org/springframework/boot/autoconfigure/orm/jpa/HibernateJpaConfiguration.class]: Invocation of init method failed; nested exception is javax.persistence.PersistenceException: [PersistenceUnit: default] Unable to build Hibernate SessionFactory; nested exception is org.hibernate.MappingException: Repeated column in mapping for entity: com.trip.butler.model.Group column: group_id (should be mapped with insert="false" update="false")
```
The error message was quite directly telling me what the reason was, so I checked the Group entity again.

![img.png](assets/images/2022-08-29-yournews-entity.png)

I found out that I mapped the same column twice in where I had to map the parent entity "Division".
So I corrected the @JoinColumn annotation as follows;

![img_1.png](assets/images/2022-08-29-yournews-entity-edit.png)