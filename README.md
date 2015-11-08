**CPEN 221 / Fall 2015: Challenge Task 2**
Crawling the Web
===

## Introduction
A **web crawler** is an internet agent (bot) that systematically browses the World Wide Web ([Wikipedia Article](https://en.wikipedia.org/wiki/Web_crawler)). Its purpose is to collect web content to be processed, indexed and used later. The web crawler is one of the major components of *search engines*. It is sometimes called a web spider, or ant.

In the most basic scenario, the web crawler starts at a *root* page, and looks for all the links in the page. The crawler validates the links and then proceeds to visit the links in some order, collecting the links in each visited page, and so on. 

Upon arriving at a page, the crawler should

1. Search if the page contains the desired content. If it does, it stores
	* The link identifying the page;
	* The whole HTML content of the page, either to be used for later processing, or for caching purposes.
2. Not revisit a page that has been visited before. This is achieved by storing the visited links in a **database**. (look below for instructions on how to setup you database server.)

##The Task: Harvesting Job Opennings
Your task is write a **multithreaded** web crawler in Java *from the scratch* to **collect job offers** posted on the internet. 

Your crawler should start crawling from a set of *seed* pages, spawning a thread for each seed page. Typically the seeds will be company pages, such microsoft.com, qualcomm.com, etc. Your crawler should be able to detect pages that contain job postings. You will do this by using suitable **regular expressions**. *There will be significant creativity in designing your regular expressions*.

Once your crawler detects that a page contains a job posting, it should extract the following information about the job posting:

1. Company/institution offering the job;
2. Date of job posting;
3. Location;
4. Job title;
5. Job Description.

All of this information should be stored in suitable tables in your database.

Of course, there is no standard format in which those pieces of information are written across different web pages; therefore, you will have to manually look at online job postings to determine a common pattern in which job postings are written. Your regular expressions should be general enough to handle the format discrepancies as much as possible, while at the same time be specific enough to minimize misdetections.

**Question:** How would you uniquely identify each job in your database ? 
     
**Note:** You are **not** allowed to use any external crawling libraries, such as crawler4j.

### Selection Policy: Scheduling page visits
There are two things to consider when visiting pages:

1. The Selection Policy: The order in which the links contained in a page are visited next, and
2. Exclusion of already visited pages.

The selection policy could be any of the well-known graph traversal algorithms, such as BFS or DFS. One of your subtasks is to determine the selection policy that best suits our application.

To prevent your crawler from visiting a link that has already been visited, one way is to add a flag field in your table of visited links in the database (you may call it IS_VISITED), and lookup this field *if the link exists*; i.e., has been added but not visited yet. 

### Synchronization
There will be several threads traversing and indexing pages, and those threads will access the database simultaneously. You will have to synchronize access to your database such that the consistency of the data is preserved. 

Moreover, even if each thread maintains its own graph, say, of links scheduled to be visited or the ones visited already, it might be the case that another thread traverses through links that lead to a page in another thread's graph. In this assignment this is a situation that we do not allow, and we require a page to be *locked* during the time a thread is working on it. In other words, if a thread is working on a page and another thread attempts to visit the same page, then this other thread will be blocked. In this situation, a plausible courses of action is to allow the blocked thread to access another page. **But how would a blocked thread choose another page to visit next? Randomized way ? Or the next page in the BFS queue?**



##Setting up your Environment
You will use a database to handle the storage component of the crawler. You will use **MariaDB** to create a relational database and store the crawled web content in tables.

[MariaDB](https://mariadb.org) is a new replacement for the infamous MySQL. It is open source, and it significantly extends the functionality of MySQL without sacrificing compatibility. The easiest way to install MariaDB is through ApacheFriends' [XAMPP](https://www.apachefriends.org/index.html) installer. Although XAMPP installs other things related to web development, such as Apache server, PHP, etc, we will use it because it also installs phpMyAdmin, which is a graphical interface, through the web browser, that allows you to  access MariaDB and perform all the operations you need, such as database creation, deletion, table creation, etc.

Once you install XAMPP and start the database server (through XAMPP's GUI), you will be ready to create a database.  


##Testing

You should develop testing strategies to ensure at least the following:

1. Proper synchronization of database access; i.e., that no one thread overwrites the data written by another thread, and no two or more threads access the same page or job row at the same time; 
2. Proper synchronization of thread visits of pages;
3. Your crawler extracts   

## Submission

Submit your work by **November 27, 6pm** to a branch called `challenge2` in your Github repository. Then set up a meeting with Bader to discuss your submission.


