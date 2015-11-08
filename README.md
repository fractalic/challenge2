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
2. Not revisit a page that has been visited before. This is achieved by storing the visited links in a **database**. 

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


     
You are **not** allowed to use any external crawling libraries, such as crawler4j.




##Setting up your Environment
You will use a database to handle the storage component of the crawler. You will use **MariaDB** to create a relational database and store the crawled web content in tables.

[MariaDB](https://mariadb.org) is a new replacement for the infamous MySQL. It is open source, and it significantly extends the functionality of MySQL without sacrificing compatibility. The easiest way to install MariaDB is through the [XAMPP](https://www.apachefriends.org/index.html) installer. Although XAMPP installs other things related to web development, such as Apache server, PHP, etc, we will use it because it also installs phpMyAdmin, which is a graphical interface, through the web browser, that allows you to  access MariaDB and perform all the operations you need, such as database creation, deletion, table creation, etc.

Once you install XAMPP and start the database server (through XAMPP's GUI), you will be ready to create a database.  