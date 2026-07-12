While this isn't suppose to be a HUGE database class, as that is suppose to be another class's job, we need to have a concept of why we need a database in the first place.

It's not very smart to just directly store data in a server as a variable, there's no persistence of the data over time, as it's just stored in memory.

So... whenever we close the server, or modify it's code, or when it crashes, all the data is gone from memory.

![[Screenshot 2026-07-05 at 9.56.33 AM.png|300]]
![[Screenshot 2026-07-05 at 9.56.47 AM.png|300]]


So... just store it in some text file instead? We have some hard-drive which stores the data for whatever we put there, and then load it when needed, and write to it when needed.

![[Screenshot 2026-07-05 at 9.58.17 AM.png|400]]

![[Screenshot 2026-07-05 at 9.58.52 AM.png|500]]

But that's not a good solution!
- Write Speed: Saves every story/comment whenever someone posts
- Memory Usage: Still keeps all stories/comments in RAM
- Query Speed: To find story with a particular id, we linear search through all stories
- Single Point of Failure: What if your laptop hard drive breaks?
- Concurrency Issues: What if two users post at the exact same time?


Obviously, people before us came to the same issue, if I can't just store all the data in memory as that can easily fail, and I can't just store all the data in a hard drive as there's many problems to that as well, how can we mix and match this in a smart engineering solution?

Well, we're not actually here to give the answer to that. That's a whole different research topic on its own. We're just going to sweep those questions under the rug and assume that something called 'databases' is going to solve all of that for us.

In other words... it's just:
- data.txt but better
- read/write data from file functions but better

![[Screenshot 2026-07-05 at 10.02.27 AM.png|500]]

---
## Databases

Now, there are 2 types of databases, relational databases, and non relational databases.

**Relational (SQL):** data in tables with fixed columns, linked by keys.

- Pros: strict structure catches bad data, powerful queries
- Cons: hard to scale and has rigid relationship schemas

**Non-relational (NoSQL):** flexible records, often JSON-like documents.

- Pros: any shape of data that scales horizontally easily
- Cons: weaker consistency and  no schema enforcement

![[Pasted image 20260705103008.png]]

It's just... you are either using some form of SQL (relational database) or not (non-relational database).

You either entangle yourself in strict relationships, or untangle yourself in wild data.


We won't go into the details of SQL databases here, but the idea of non-SQL data bases look similar to this instead, just JSON files!

Each JSON item we call an 'object', each object’s properties are kept in one document, so it can be easily referenced in one place. Also note that documents can contain different information, which allows for more flexibility.

![[Screenshot 2026-07-05 at 10.36.26 AM.png|300]]

![[Screenshot 2026-07-05 at 10.37.46 AM.png|300]]


However, later on, we will see that a document structure called a Schema might be desirable.
- just enforcing most data looks the same way...

Now that MongoDB (an implementation of a no SQL database) is what we are using, it fixes most of our problems!
- Write Speed: Optimized!
- Memory Usage: Optimized!
- Query Speed: Optimized!
- Concurrency Issues: Solved!


Except 1 problem, points of failure, right now if your device that you are running the backend and database on fails, it still dies, so we can instead run this on a cloud.

- Guys, so called 'cloud computing' really is just you computing on another computer... this is a whole other branch of tech we aren't going into detail here.


For the class's example, they used ATLAs cloud (by AWS, amazon), the idea is that the backend process on a computer connects to servers over the network, and there's fail safe systems behind the scene to make sure your data isn't lost.

How? Don't know, this is another like 'sweep under the rug for now kids' type of question, but we can take a simple guess.


The simplest way is have duplicates of systems, like having a primary MongoDB hard disk, and then it makes copies over to other secondary disks, then whenever a disk goes down, another duplicate backup could be referenced.

![[Screenshot 2026-07-05 at 11.02.46 AM.png|400]]

![[Screenshot 2026-07-05 at 11.03.05 AM.png|400]]

---
## Reading & Writing to Databases