---
title: "First time working with frontend developers"
categories: TIL
tag: [Java, Spring, Frontend, React]
toc: true
---

✍️Today I Learned: the post is about I did or learned today.
{: .notice--info}

I worked together with the frontend developers for the first time on the last week's project.
It was a very new experience because I was kind of used to only working with the server.
Of course, I knew that the server won't exist by itself for forever, but I never really put much thought into how I would work with the frontend developers.
Through the collaboration, I learned few lessons that I should keep in mind when working together with the frontend.


## Start as a team, work as a team
This sounds pretty obvious, but I think this is the most important thing to keep in mind when working with the FEs.
For the last few weeks, I have been working alone or just with the backend developers on the assignment.
This means that I had less to consider when designing the api.
I could decide which information receive and which to give back as a response.
For example, when creating a post, I could just give back a string "The post is created" as a response than full information of the post.
When I run it on the Postman and if it gives me back the proper response I wanted, then everything was fine and my work was done.


But when working with the frontend developers, these decisions weren't entirely upto me.
I had to talk with the frontend developer for about an hour discussing what information I need to receive from the client and what response I should return.
If the api design wasn't planned well in the first place, there was a chance that both of us would have to correct things later.
For example, I asked the frontend developer if I can just give back the string "The post is created" as a response for the creation of a post like I used to and the FE agreed. 
However, later we realized that the FE needs all the information of the post, not just the message saying that the post is created.
It wasn't a big deal since it only took me about 10 minutes making the changes.
However, if it was a more complex project, where more developers were involved, the miscommunication from the start would have definitely caused a problem.


## Check the connection as soon as you can
This should be done as soon as a part of the project is ready since you never know what errors can come up just from the connection, especially when it is your first time working with the frontend.
Our team encountered the CORS error, which is a typical error that occurs when connecting the frontend and backend server.
However, at that time no one expected to encounter this error because we had no idea that the frontend developers would use the different port for their server. Actually, the thought of the port number, same-orgin, cross-origin wasn't even on my mind.
Fortunately, we checked on the connection between the frontend server and backend server on the 3rd day of the collaboration.
f we had decided to put our work together on the last day of the assignment, we wouldn't have solved the problem on time.


## Keep on checking the progress
Always check the progress of the team.
This is the part that lacked attention.
After deciding on what and how to build the project, we divided into two smaller groups, FE and BE.
Within the backend developers, we kept track on what we were doing, what features were left to do and the deadlines.
However, we didn't ask the frontend developers much on where they were standing and the deadlines were vague.
I think I kind of thought that their schedule was their problem and because I don't know much about the frontend, I didn't want to be a person who ask them all the time about what they are busy.
But since we are a team, I think we should have communicated more to at least know at what point both BE and FE were at.
We just agreed to do the final feature check about an hour before the assignment hand-in, and it turned out that there was an issue with the frontend server, which we couldn't solve it in time.
If we checked all our progress more often and planned things out more neatly, we could have finished the project a bit earlier and double check on the whole service.

<br>

After all, my first experience with the frontend developers was very interesting and gave me some ideas on what to check during the collaborative work!