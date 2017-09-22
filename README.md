## Welcome to CISC 5950 - Big Data Programming!

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
