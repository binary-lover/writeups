---
description: Here is the easy peesy walk through
icon: vector-square
---

# Invite Only

You are an SOC analyst on the SOC team at Managed Server Provider TrySecureMe. Today, you are supporting an L3 analyst in investigating flagged IPs, hashes, URLs, or domains as part of IR activities. One of the L1 analysts flagged two suspicious findings early in the morning and escalated them. Your task is to analyse these findings further and distil the information into usable threat intelligence.

Flagged IP: **101\[.]99\[.]76\[.]120**\
Flagged SHA256 hash: **5d0509f68a9b7c415a726be75a078180e3f02e59866f193b0a99eee8e39c874f**

We recently purchased a new threat intelligence search application called TryDetectThis2.0. You can use this application to gather information on the indicators above.



## Solution

#### Q1: What is the name of the file identified with the flagged SHA256 hash?

Head to the VirusTotal and we will get the Answer.

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>



#### Q2: What is the file type associated with the flagged SHA256 hash?

Head over to Details you will get the answer.

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

#### Q3: What are the execution parents of the flagged hash? List the names chronologically, using a comma as a separator. Note down the hashes for later use.

Go to Relation tab and scroll down a bit you will find&#x20;

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

#### Q4: What is the name of the file being dropped? Note down the hash value for later use.

on the same page down a little you will see the name

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

#### Q5: Research the second hash in question 3 and list the four malicious dropped files in the order they appear (from up to down), separated by commas

click on the 2nd file, then go to relation tab and see the list of dropped files names

<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

#### Q6: Analyse the files related to the flagged IP. What is the malware family that links these files?

i go through virus total but its not so direct so i search for google if any report is there like mention in the very next question,  And i found this helpful site

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

On this site i search for the ip `101.99.76.120` and we got the family of malware  &#x20;

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

#### Q7: Research the second hash in question 3 and list the four malicious dropped files in the order they appear (from up to down), separated by commas.

Luckily we are on the same original report just need to copy paste the title of report

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

#### Q8: Which tool did the attackers use to steal cookies from the Google Chrome browser?

I start reading the Key Takeaways and i found the tool name

<figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

#### Q9: Which phishing technique did the attackers use? Use the report to answer the question.

on same view we can see the phishing techniquee

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

#### Q10: What is the name of the platform that was used to redirect a user to malicious servers?

scroll a bit and we can see the platform name

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

Congratulations We solved the lab successfully&#x20;

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

<h2 align="center">Thanks</h2>
