---
title: "Instagram clone coding troubleshooting"
categories: Project:Instagram-Cloning
tag: [Java, Spring, Troubleshooting, Clone project]
toc: true
---


## Creating a post

### Problem 1 : SQLIntegrityConstraintViolationException: Column 'user_id' cannot be null

When I ran the application after finishing the basic **@PostMapping method**, it kept on giving me the following error saying the **user_Id** was null.


```
2022-08-24 16:36:33.715  WARN 16508 --- [nio-8080-exec-6] o.h.engine.jdbc.spi.SqlExceptionHelper   : SQL Error: 1048, SQLState: 23000
2022-08-24 16:36:33.715 ERROR 16508 --- [nio-8080-exec-6] o.h.engine.jdbc.spi.SqlExceptionHelper   : Column 'user_id' cannot be null
2022-08-24 16:36:33.727 ERROR 16508 --- [nio-8080-exec-6] o.a.c.c.C.[.[.[/].[dispatcherServlet]    : Servlet.service() for servlet [dispatcherServlet] in context with path [] threw exception [Request processing failed; nested exception is org.springframework.dao.DataIntegrityViolationException: could not execute statement; SQL [n/a]; constraint [null]; nested exception is org.hibernate.exception.ConstraintViolationException: could not execute statement] with root cause

java.sql.SQLIntegrityConstraintViolationException: Column 'user_id' cannot be null
```

### 🌧Cause

I checked the problem using the debugger.
It turned out that the annotation **@AuthenticationPrincipal** I used to get the user details of the logged in user couldn't fetch the correct information.

![userDetails returning null](https://i.imgur.com/xeBbQLr.png)


### 🌈Solution

Googled the issue, but couldn't find the exact reason why this happens. So I decided to take away the annotation and call the user details directly from the **tokenProvider**.

![userDetails received](https://i.imgur.com/N5JcKeZ.png)


<br>


### Problem 2 : AnnotationException: Associations marked as mappedBy must not define database mappings like @JoinTable or @JoinColumn

After creating the **Image** entity, I used **@ManytoOne** and **@OnetoMany** annotation to the **Image** and the **Post** entity respectively. I tried running the app and it gave me the following error message.

```
Caused by: org.hibernate.AnnotationException: Associations marked as mappedBy must not define database mappings like @JoinTable or @JoinColumn:
```

### 🌧Cause

The problem was becaused I used the **@OnetoMany(mappedby="post")** and **@JoinColumn** together in the **Post** entity.

![@JoinColumn used with mappedby](https://i.imgur.com/jPw0b2R.png)


However, **@JoinColumn** should be used from the owning side, in this case, the **Image** entity. The **mappedby** attribute is used from the referencing side to define the relationship.

[For read: Difference between joincoulum and mappedby](https://www.baeldung.com/jpa-joincolumn-vs-mappedby)

### 🌈Solution

Problem solved by removing **@JoinColumn** from the **Post** entity.

![remove @JoinColumn](https://i.imgur.com/ncaGeVg.png)

<br>

### Problem 3 : foreign key stays null in the database

When I wrote the code, what I thought was that the **Image** entity would fetch the **post_Id** as a foreign key. However, when I checked the database of **Image** after uploading the file, the **post_Id** column of the **Image** entity turned out to be null.


### 🌧Cause

The order of the code was the problem here. I had uploaded the file to the S3 bucket as soon as the file came into the **PostService**. This created a row in **Image** database. But because the **post** wasn't saved to the **Post** database yet, the **post_Id** wasn't created yet, which means that there is no **post_Id** to be saved together to the **Image** entity when uploading the image.

![image saved before saving post](https://i.imgur.com/XtiAZT3.png)


### 🌈Solution

I changed the logic and saved the post first after uploading the image to the S3 bucket.Then I converted the **List<String>** to **<List>Image**. Before, I didn't create the **Image repository**, because the images were already saved in the database even though I didn't create one. But this time I created the repository to make sure that the imageURl is saved with the post_id in the **Image** database.

![saving the List<Image> to image repository](https://i.imgur.com/3bKCqiY.png)

### ⚡Better way to solve?
There was something called a convenience method which is used to set the relationship between the two entities. 
    
[reference: convenience method](https://peace-log.tistory.com/entry/%EC%97%B0%EA%B4%80-%EA%B4%80%EA%B3%84-%ED%8E%B8%EC%9D%98-%EB%A9%94%EC%84%9C%EB%93%9C%E2%9D%93)
    
    
<br>
    
## Getting a Post/all Posts
### Problem 1 : LazyInitializationException: could not initialize proxy
    
After correcting the Dtos, I ran the application again and it threw me a different error, but it was related to the proxy problem as well.
    
```
2022-08-25 10:06:35.012 ERROR 11720 --- [nio-8080-exec-2] o.a.c.c.C.[.[.[/].[dispatcherServlet]    : Servlet.service() for servlet [dispatcherServlet] in context with path [] threw exception [Request processing failed; nested exception is org.hibernate.LazyInitializationException: could not initialize proxy [com.clonecode.inssagram.domain.User#1] - no Session] with root cause

org.hibernate.LazyInitializationException: could not initialize proxy [com.clonecode.inssagram.domain.User#1] - no Session
	at org.hibernate.proxy.AbstractLazyInitializer.initialize(AbstractLazyInitializer.java:176) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
	at org.hibernate.proxy.AbstractLazyInitializer.getImplementation(AbstractLazyInitializer.java:322) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
	at org.hibernate.proxy.pojo.bytebuddy.ByteBuddyInterceptor.intercept(ByteBuddyInterceptor.java:45) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
	at org.hibernate.proxy.ProxyConfiguration$InterceptorDispatcher.intercept(ProxyConfiguration.java:95) ~[hibernate-core-5.6.10.Final.jar:5.6.10.Final]
```

### 🌧Cause
    
I set **@OnetoMany** relationship with **fetchType.LAZY** and the error occurred because the session was gone when proxy tried to bring the lazily fetched object. I googled the solution and one of the solution I found was to change the FetchType as EAGER, but it didn't work. Also it said that using **fetchType.EAGER** is not a good way to solve the problem.

![Without @Transactional](https://i.imgur.com/EeSxo44.png)


### 🌈Solution

I added the **@Transactional** annotation on top of the get method to keep the transaction going.
    
![Add @Transactional](https://i.imgur.com/h7LudOK.png)

### ⚡Better way to solve?
There are different ways to solve the problem but using **Join Fetch** directive is the best way.
    
[reference: Different solutions for LazyInitializationException](https://www.baeldung.com/hibernate-initialize-proxy-exception)
    
    
<br>    
   
    
### Problem 2 : HttpMessageNotWritableException: Could not write JSON: could not initialize proxy

앱 실행을 했을 때 dto를 참조하는 proxy 오류가 났다.
There were several issue messages regarding the initialization of proxy when running the application and all of them were pointing to the **ResponseDto**s. 
    
```
WARN 14236 --- [nio-8080-exec-9] .w.s.m.s.DefaultHandlerExceptionResolver : Resolved [org.springframework.http.converter.HttpMessageNotWritableException: Could not write JSON: could not initialize proxy [com.clonecode.inssagram.domain.User#1] - no Session; nested exception is com.fasterxml.jackson.databind.JsonMappingException: could not initialize proxy [com.clonecode.inssagram.domain.User#1] - no Session (through reference chain: com.clonecode.inssagram.dto.response.ResponseDto["data"]->java.util.ArrayList[0]->com.clonecode.inssagram.dto.response.PostAllResponseDto["user"]->com.clonecode.inssagram.domain.User$HibernateProxy$3WV4xhH2["createdAt"])]
```     
    
### 🌧Cause

The reason that caused the error were the entities called directly to the **ResponseDto**. When the response is returned as an entity, there can be a Json parser error.

![Dto including the entity as a attribute](https://i.imgur.com/O0jt2ud.png)


### 🌈Solution
Make another dto for the entities called directly into the "ResponseDto". The below is the example of the newly created **UserProfileDto**.

![UserDto](https://i.imgur.com/xf2VL7f.png)

You can see below that the **UserProfileDto** is used to replace the **User** entity that was called directly into the **PostAllResponseDto**.
    
![User replaced by UserDto](https://i.imgur.com/MWbguAA.png)
    
    
<br>
    

## Viewing photos in AWS S3 bucket
### Problem 1 : XML Access Denied

When viewing the urls from the frontend server, the imageUrls didn't show the photos, saying that the access is denied.
    
![Access Denial](https://i.imgur.com/61idAmO.png)

```
<Error>
<Code>AccessDenied</Code>
<Message>Access Denied</Message>
<RequestId>2M0MEN0GTBW1E993</RequestId>
<HostId>QTZrLa+/D+M7RpGdTxg1bqpQFhO9i7vmyG9n7dPv8z+dfZkHwuNqIfgb+Wl9EUCDSQaT8nNuO3E=</HostId>
</Error>
```

### 🌧Cause
The S3 bucket returns the above error for anonymous requests to objects that aren't public.
    

### 🌈Solution
    
From the bucket, I change the **Permissions** settings.

I turned off the 'Block public access' settings and let the public access the files in my bucket.
    
![Public access allowed](https://i.imgur.com/WNbCfzx.png)

Then I added the bucket policy that allows anonymous user to read the images in the bucket.

![Bucket policy added](https://i.imgur.com/GQVsERT.png)

    
[To check other bucket policies : Bucket policy example](https://docs.aws.amazon.com/AmazonS3/latest/userguide/example-bucket-policies.html)