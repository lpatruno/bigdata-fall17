## Welcome to CISC 5950 - Big Data Programming!

### Lecture 11
---
This week we reviewed the final chapter of the text which reviews the Lamba Architecture. Aside from reviewing each of the batch, serving, and speed layers, the chapter introduces some variations on the basic idea intended at reducing the latency of the batch layer. One variation includes the idea of **partial recomputation** in the batch layer, where recomputation is run only on entities that have changed. By not having the repartition your master dataset, you can reap the benefits of an incremental and recomputation-based approach by only recomputing views for the data that has changed. The second variation involved building multiple batch layers on top of one another. Each layer loosens requirements for the layer above it by reducing the amount of data that layer would have to process. For instance, one batch layer might run a full recomputation over the whole master dataset once-a-month while the next batch layer might take a hybrid incremental approach and run once every 6 hours.

It's important to remember that the Lambda Architecture is just one example of how one may architect a big data system and has its own set of pros and cons. One con, for instance, is the need to have to maintain two separate codebases that perform the same set of computations (a batch version and a streaming version). A student last night brought up another such design, the [Kappa Architecture](http://milinda.pathirage.org/kappa-architecture.com/). The main idea of the Kappa Architecture is to do away with the batch processing system and perform all of your computation in a streaming system. If you're interested in learning more, I would highly recommend reading [this article](https://www.oreilly.com/ideas/questioning-the-lambda-architecture) by Jay Kreps, one of the engineers behind a lot of the online architecture at LinkedIn. In that article, Kreps compares and contrasts the Lambda and Kappa architectures.

I'm looking forward to group presentations next week! Thanks for a great semester!

### Lecture 10
---
This week we discussed the fundamentals of queueing and stream processing - essential elements of asynchronous data processing systems. In particular we noted that queues allow systems to retry events whenever workers processing data fail. Further, they act as a buffer that protect data when the system is hit with a burst in traffic. Single-consumer queues are limited by the fact that the queue is responsible for keeping track of which events have been consumed by worker processes. Multi-consumer queues, such as Apache Kafka, shift the responsiblity of tracking the consumed/unconsumed status of events from the queue to the applications themselves. The queue then provides a service-level agreement guaranteeing that a certain amount of the stream is available.

Stream processing systems are responsible for processing these buffered events and updating the realtime views. These systems provide improvements over the traditional queues-and-workers model which add latency and operational burden to the data processing system. We introduced Apache Storm and discussed the Storm model, which represents the entire stream-processing pipeline as a graph of computation called a *topology*.

Your homework assignment for next class is as follows:

  1. Read chapter 18 **Lambda architecture in depth**. This chapter concludes our study by summarizing the Lambda Architecture and discussing how the views in the serving layer and speed layer are merged together to resolve queries.

### Lecture 9
---
Our discussion this week was focused on the speed layer - the theory and technologies that allow for low latency queries even in the face of petabyte scale data sets. In order to facilitate low latency queries, we need to use specialized forms of databases that allow for random read and random write access and are distributed and scalable. A popular form of databases called NoSQL databases have emerged over the last decade that provide a variety of data models and index types including Apache Cassandra and MongoDB.

Random write access is necessary because we need to update our realtime views in an incremental fashion, meaning that our functions need to take in the most recent data and the previous realtime views and update these views, rather than reconstruct them from scratch. These algorithms are more complex and present challenges when considering the CAP Theorem, which states that when dealing with distributed data systems, you can achieve consistency (where reads incorporate all previous writes) or availability (where every query returns an answer instead of an error) but not both.

Your homework assignment for next class is as follows:

  1. Please reread chapter 14 and read chapter 15. These chapters discuss how to connect the streams of data being generated with the realtime views. You will learn about queuing and stream processing and touch on Apache Kafka and Storm, two massively popular technologies.

### Lecture 8
---
Last week we watched a talk on the [evolution of data processing at Spotify](https://www.youtube.com/watch?v=5JeBiSdyGMY) and discussed the different components of Spotify's big data system. As we saw, Spotify is using many different tools, including the [Google Cloud Big Data](https://cloud.google.com/solutions/big-data/) suite, [Scala](https://www.scala-lang.org/), [Scio](https://github.com/spotify/scio), and [luigi](https://github.com/spotify/luigi). However, these tools are just different solutions to the same issues we've been discussing in class this semester including, batch processing, serialization, serving the results of batch processing, merging/joining big data sets, etc.

The remainder of the class was spent discussing group projects. Kudos to team Spark for a great introduction to their project. I will be asking other groups to give similar short intros in the next few classes. So keep working!

As I mentioned, we will not be having class this week. We will make up this class over a Skype session in the future.

Your homework assignment for next class is as follows:

  1. Please read chapters 12-14. These are our first chapters on the speed layer. You will learn about the CAP theorem, Apache Cassandra, and Storm. We will review all this material in our next class.


### Announcement: Quiz Answers
---
As requested, here are quiz solutions. I'll upload each of them as I complete them.
  * [Quiz 1](https://github.com/lpatruno/bigdata-fall17/blob/master/quiz_1.pdf)
  * [Quiz 2](https://github.com/lpatruno/bigdata-fall17/blob/master/quiz_2.pdf)
  * [Quiz 3](https://github.com/lpatruno/bigdata-fall17/blob/master/quiz_3.pdf)
  * [Makeup Quiz 1](https://github.com/lpatruno/bigdata-fall17/blob/master/makeup_quiz_1.pdf)
  * [Makeup Quiz 2](https://github.com/lpatruno/bigdata-fall17/blob/master/makeup_quiz_2.pdf)

### Announcement: Final Project Groups
---
The final project groups have been formed and are available [here](https://github.com/lpatruno/bigdata-fall17/blob/master/Final_Project_Groups.csv). I wanted to ensure that each student would be able to present on a technology that was in his or her top 3 technologies. In order to do this, I had to make 2 Hadoop groups (they're denoted *Hadoop* and *Hadoop 2* and one of these groups has 5 students. I expect these two groups to talk to one another to ensure they're working on different tutorials for the final project.

If there are any questions, please let me know!

### Lecture 6
---
This week we discussed batch computation in the batch layer. As part of the Lambda Architecture, the batch layer precomputes the master dataset into batch views to be served by the serving layer so that queries can be resolved with low latency. Since the master dataset is constantly growing, these batch views need to be updated - and to do we must choose between recomputation and incremental style algorithms. We also discussed MapReduce, a distributed computing paradigm created at Google that provides a framework for scalable and fault-tolerant batch computation. As a framework, MapReduce abstracts away many of the difficulties of distributed computing, including concurrency, transferring data between machines over a network, and task scheduling, and lets you focus on data processing. Finally, we examined 2 queries - hourly pageview counts and gender inference - and saw how to implement these using MapReduce.

Your homework assignment for next class is as follows:

  1. Please read chapter 8 of the text. Chapter 8 applies the theory we learned about the batch layer to a real world example and walks you through building a batch layer from beginning to end. This chapter marks the end of our study of the batch layer, and with it the end of the first half of the semester. The serving and speed layers are next!
  
  2. Some students had questions about the midterm. In order to address these and similar concerns, I will devote half of the class next week to answering questions about the material for the midterm. That is, if you have questions about material, please bring them to class and we can discuss them as a group. Note that this discussion is dependent on the questions asked; if there are no questions, we will spend the additional time on lecture.
  
I will be posting the answers to the first 3 quizzes and the groups for the final project within the next few days!

### Lecture 5
---
We spent this week discussing how data is physically stored in the batch layer. Namely, we discussed the requirements of the storage layer. These include the ability to handle a large, constantly growing set of data, the ability to compute functions on the whole dataset by reading lots of data at once, and the ability to tune the trade-off between storage cost vs. processing cost. Distributed filesystems, filesystems that scale by adding more machines to a cluster, fit these requirements and the Hadoop Distributed File System is the de facto industry standard for handling the physical storage layer of Big Data Systems.

We spent the remainder of the class discussing libraries that natively handle the operations that we wish to perform (append data to a dataset, enforce a vertical partitioning scheme, and consolidate many small files into larger files). We looked specifically at how the [Pail](https://github.com/nathanmarz/dfs-datastores) library handles these operations. Remember, it's not important to understand how every line of code works - it's much more important to understand **the principles for building out Big Data Systems** rather than how these are implemented in particular libraries. Some students asked questions about serialization, and I think [Wikipedia](https://en.wikipedia.org/wiki/Serialization) does a great job of explaining what serialization is and what it's used for in simple terms. Check it out!

Your homework assignment for next class is as follows:

  1. Please read chapter 6 of the textbook. This chapter discusses computing functions on the batch layer and using MapReduce. Students who are interested in algorithms and data analysis will find this chapter particularly interesting. We will skip the implementation chapter this week in order to really focus on the theory behind batch computation systems.
  
  2. Please read the original [MapReduce](https://static.googleusercontent.com/media/research.google.com/en//archive/mapreduce-osdi04.pdf) paper by Jeffrey Dean and Sanjay Ghemawat of Google. Learn from the masters.
  
  2. Your midterm will take place in-class on October 25th. The test will be a closed-book, essay style examination.
  
See you next week!

### Lecture 4
---
Class cancelled this week. No new reading assignment.

### Lecture 3
---
This week we spent time discussing how to model your master dataset designing a new Big Data System. This is incredibly important as the decisions made about the model determines the kind of analytics you can perform on your data and how you'll consume the data later on. We also worked a bit on coming up with a data model to capture user interactions with a streaming music player service. Kudos to the brave group who presented their work!

Your homework assignment for next class is as follows:

  1. Please read chapters 4 and 5 of the textbook. These chapters focus on how to physically store your master dataset in a distributed filesystem. Please spend a good deal of time going through the code in chapter 5. It's not so important to understand how each line of code works- it's way more important to understand the principles being employed. Please bring any questions you may have to class!
  
  2. Read this primer on [filesystem basics](http://www.porcupine.org/forensics/chapter3.html). It's important to understand the basics before moving on to distributed filesystems!
  
For those students who had questions about normalization last week, check out the [Wikipedia](https://en.wikipedia.org/wiki/Database_normalization) page on database normalization.

See you next week!

### Lecture 2
---
This past week we spent some time discussing the semester final project and reviewing the contents of chapter 1 on the Lambda architecture.

The details of the final project can be found [here](final_project.pdf). I've also added a link to this document in the sidebar for ease of access. Please review this proposal and note any questions you may have. This is a semester long research project that will require a good deal of work; I recommend getting started as early as possible.

Your homework assignment for next class is as follows:

  1. Please read chapters 2 and 3 of the textbook. These chapters focus on designing a data model for a big data system. This foundational material is extremely important as how you choose to model your master dataset determines the kind of analytics that you can perform on your data further downstream. This model must also be extensible because your company's data types will change over time. In chapter 2 you'll learn about the fact-based model, enforceable schemas, and graphical representations. Chapter 3 will introduce Apache Thrift, a data serialization framework. As always, be prepared for a quiz.
  
  2. Part of your assignment last week was to spend time researching the technologies listed in section 1.8.3 of the text. This section includes specific technologies for batch computation systems, serialization frameworks, random-access NoSQL databases, messaging/queuing systems, and realtime computation systems. Research each technology listed in this section and prepare a ranked list of 7 technologies you would like to work on for your final project. I expect students to turn in a document with the student's name, program (either Data Analytics or Computer Science), and a ranking of 7 technologies. Additionally, if there are other technologies that you would like to work on, please email me about these technologies and we can discuss how to incorporate them into the final project.
  
Several students mentioned that they have class during office hours. I invite these students to come to additional office hours on Tuesday evenings from 7:45pm - 8:45 pm in the 3rd floor lounge. Additionally, please email to set up additional office hours.

Please come to class prepared to discuss the material from the chapter. 


### Lecture 1
---

Thank you for a very enjoyable discussion last night! I will be using this site to post resources, links, lecture reviews, and homework assignments.

During our first lecture we spent time discussing the course [syllabus](Syllabus.pdf), including the grading breakdown for the course and the final project, as well as discussing how we might build out a data architecture for capturing user interactions from a Spotify-like music service. As we saw, it will be had to scale to more and more users and features without adding large amounts of complexity to our system. You'll have a chance to read more about these challenges in chapter 1 of the text.


Your homework assignment for next class is as follows:
  
  1. Please purchase the [textbook](https://www.amazon.com/Big-Data-Principles-practices-scalable/dp/1617290343/ref=sr_1_3?s=books&ie=UTF8&qid=1502993183&sr=1-3&keywords=big+data) and read the Preface and Chapter 1. You'll have a chance to read in depth about the topics I covered in lecture last night. The author introduces the Lambda Architecture and discusses how the architecture is advantageous over the traditional relational database model.

  2. Spend time researching the specific technologies listed in section 1.8.3 of the text. Your final project will involve a group presentation of one of these technologies. Next class I will ask you to submit a ranked list of preferences for these technologies. Hence, it is in your best interest to understand them well enough to be able to tell me which you prefer to present on. Feel free to email me about other big data technologies if you have something you really wish to learn.

  3. Read [Part I of Spotify's 3-part blog piece on their Event Delivery system](https://labs.spotify.com/2016/02/25/spotifys-event-delivery-the-road-to-the-cloud-part-i/). This is a great example of cutting edge industry work being done in the field of Big Data systems. In subsequent weeks I will ask you to read parts II and III. We will spend a fair amount of time this semester reading similar blog posts and papers introducing these technologies.

If anyone has any questions, please feel free to email me!
