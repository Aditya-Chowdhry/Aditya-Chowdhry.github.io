---
title: "Interview Tips And Suggestions"
layout: post
date: 2016-02-24 22:48
image: /assets/images/job.jpg
headerImage: false
tag:
- interviews
- computerscience
- programming
category: blog
author: adityachowdhry
description: Land and ace coding interviews
# jemoji: '<img class="emoji" title=":ramen:" alt=":ramen:" src="https://assets.github.com/images/icons/emoji/unicode/1f35c.png" height="20" width="20" align="absmiddle">'
---

## Introduction

The following tips and suggestions are combination of my experience and different sources. This post includes all the relevant material that can help you in landing job oppurtunities and acing them.

Note: This post is only for students looking to crack tech interviews and was written specifically for my college but can be usefull in general. 

## Tips for pre-application-stage 

Working on the following factors can help you land interview oppurtunities:

1. **Resume** - A resume should be well formatted, simple and concise(one page only). The resume should be such, that it can be parsed by automated tools. [CareerCup Resume](https://www.careercup.com/resume) is a great resource for building a resume. To get a detailed feedback for your resume, you can use [Vmock](https://www.vmock.com/). VMock is a free, online instant resume feedback application.
2. **LinkedIn profile** ­- An updated LinkedIn profile acts as an online resume and a platform where you can get opportunities. Online presence ­ Online presence includes links such as Github, Behance etc, live working
3. **Online presence** ­- Online presence includes links to websites such as Github, Behance etc and your live working projects, blog and personal website. This gives an edge to your application.
4. **Projects** - Projects play an important role in short listing of resumes and interview process. Projects show your creativity and ability to apply.
    - Library/hospital/hotel/etc management system as a project immediately gives a red flag. Avoid doing these.
    - Searching for a unique idea is a tough work. If you are not able to get a unique idea, research an already implemented project/product and try to implement it yourself. This link [Project Ideas](https://github.com/Aditya-Chowdhry/Projects) contains a list of projects that one can implement.
    - Making a website? Host it online! There are numerous companies providing free hosting for students. Like Heroku, Open Shift, Amazon web services etc. Make use of student discounts, tools etc like Github Student Developer pack. For mobile applications, make a group and split the cost. Publish your applications to the store.
5. **Trainings** ­- A certificate in six weeks Java/.Net/C/C++ course from <institute_name> institute is of no use if you are doing it just to include in your resume. Do these courses for your own learning and betterment. Try to implement projects. Projects are a proof that you know a particular technology.
6. **Internships** -­ Internships are an important and the best way to learn how things work in a real world. There are many startups offering flexible work. Search for internship opportunities on Letsintern, Internshala, AngelCo, Greymeter, posting on groups like Delhi Startups or directly apply to startup websites. GSOC(Google Summer of Code) : Google Summer of Code is a global program that offers students stipends to write code for open source projects. For more information ­[Google Summer Of Code](https://summerofcode.withgoogle.com/)
7. **Competitions** - 
    - Hackathons are one of the best way to learn, develop and make awesome projects in just a day. Interacting with other fellow developers will make you learn many things. Rule: Complete your project and give the presentation even if your project is half completed.
    - Coding Contests are also an effective way to make your skills sharper. Winning and participating in good coding contests like ACM ICPC, Facebook Hacker Cup and Google code jam can even land you direct interviews with different companies. Google also hold Google APAC for final year students, good performance in this the contest will fetch direct interview with Google.

##  Ways to apply for interviews
1. **Direct** - Directly applying to different company websites. Google, Facebook and Amazon have dedicated careers page for applying. And yes don’t hesitate to apply to these ,if your resume is good they do respond. Don’t restrict yourself to India only. Apply to open positions in different countries. There is basically a false notion among students that companies/startups do not respond to online applications or emails if you don’t have any reference but if your resume is strong they do.
2. **Hiring based Coding Contests & Online Challenges** - This is one of the shortest way to land interviews with some of the best product based companies. Some of the websites that hold coding contests are HackerEarth, HackerRank.
    - Websites like HackerEarth, StockRoomIO, Venturesity etc have also started project/hackathon based hiring. In project/hackathon based hiring a problem statement or theme is given on which a participant has to develop a working project and submit in 1­4 days (Change with different companies). After the submission of the projects, they are evaluated and selected candidates are further called for interviews.
3.  **Internship/Trial week** -­ Sometimes Internships leads to full time jobs. Also startup like Zomato holds Trial week every month in which selected candidates work on different projects. The work done by candidates are evaluated for a week and at the end of week good performing candidates are given job offers.
4. **Startup Jobs** -­ There are many websites that lists different startup jobs like AngelCo, Jobspire etc.
5. **References** -­ One of the most effective way to land interview opportunity. Ask your Relatives/Seniors/FriendsOfFriends/LinkedinConnections for a reference.
6. **Exams** - Exams such as Amcat, Elitmus, Cocubes etc. They have a big pool of companies and if your score is good in these exams you can land many opportunities. Visit each website and see the list of companies.

## Interview Gyaan

##### Interview Rounds
Generally, there are 3­-5 rounds in an interview with a product based company. These rounds are purely technical. If there are 4 rounds then 2 rounds are coding interviews, 3rd would be project based and system design round. Last round will be with HR/CTO/CEO. The format of interview change with company to company.

##### Preparation
Coding interviews are a basic test of your language, data structures and algorithmic knowledge. You can code in any language you want but languages like C, C++, Java or Python should be preferred.

1. **Language** - Choose the language you know well(Avoid using C because of lack of STL). You should know the basic things about the language like
    - In C++ we use set, map etc, what are basic underlying data structures for these?
    - In Java we use Array.sort(), what is the underlying algorithm for sorting?
2. **Data Structures** ­- Knowing about Arrays, Stacks, Queues, Linked Lists, Trees and Graphs doesn’t mean that you know data structures. Data Structures is about application. In what condition you will use Queues and not the arrays? In what conditions will the Trees be more efficient? Example: Consider a list of numbers (1,2,3,4,5,6). Now you have to store it in some data structure. But there are some conditions:
    - Any number can be removed and order should remain the same.
    - Any number can be added at any position.
    - Ex: If I remove 2 then the numbers should be in same order i.e (1,3,4,5,6). I can add any number at any position i.e adding 99 at 3rd position (1,3,99,4,5,6).
    - So what will be the best data structure for this problem?
    - Consider Array: Array stores values in continuous form i.e if 2 is removed then all elements after 2 shall be needed to shift left side. Thus, every time any number is added or removed it will involve shifting of numbers before or after it. So clearly here Array is not an efficient choice.
    - What can perform better in this case? Think Linked List.
    - Likewise, a question might be taken up and modified based on any condition.
3. **Algorithms and Time/Space Complexity** - Knowledge and application of different algorithms is important especially for big product based companies along with time/space complexity. Which sorting technique is better MergeSort or QuickSort? In which cases you will use Merge over Quick and vice versa?Hashing, Binary Search, Bit Manipulation, BackTracking, Greedy, Dynamic Programming etc.

##### Resources for practice
To keep it simple for interview preparations I found these three resources best and enough to crack interviews.
1. **InterviewBit** -­ Keep this as your main website for preparation. Start doing this at least 4 months before interviews. Solve questions daily and don’t skip questions. If you are not able to do questions read about the concepts. You can get solutions to the problems on LeetCode and GeeksForGeeks. But keep this as the last step. Read questions on Quora for more depth insight: https://www.quora.com/topic/InterviewBit
2. **LeetCode** ­- Keep it as a secondary website. InterviewBit and Leetcode have mostly similar questions.
3. **Cracking the Coding interview­ by Gayle McDowell** - A good book with complete solutions and step by step solutions with proper time and complexity analysis. Read the book along with preparation.
4. **Competitive Coding** - Competitive Coders are more easily able to adjust to these online platforms as they are constantly exposed to coding contests. But don’t do competitive coding
just for the sake of getting a job. If you are enjoying it, then do it. It looks difficult at first but you start enjoying afterwards.

##### System Design Interview Preparation
System design interview questions are open-ended questions and are asked to test your application ability. You are good in theory but you should know how things are applied. For example, a very common system design interview question is “How will you design a URL shortener?”. This is a very good video that explains this: [system­design](http://www.hiredintech.com/system­design) 

Project based questions are very common. So be prepared and go through your projects before an interview. Interviewers ask specific questions to your projects.

##### Presentation Skills and Overcoming nervousness of a F2F interview
Presenting yourself properly and conveying your thoughts clearly is one of the key points which leads to a successful interview. Clarity of your ideas, confidence and good communication is important.

One of the problems many students face including me is that during interviews mind gets stuck or blank!

**How to overcome this?**
One of the best way to overcome this is giving many mock interviews. Mock interviews are very important to overcome your fear. Take help from your seniors, friends. Make them take your interviews(Technical Interviews). You and your friends can take interviews of each other. This is very helpful.

There is a website that allows Mock interviews for free. I gave and took around 4-­5 mock interviews from this site: [Pramp](https://www.pramp.com/)

##### Note: There can be other ways to crack interviews too. The above post is the summary of me and my friends experiences.
<center>Keep Coding ✌</center>
<center>All the best!!</center>
