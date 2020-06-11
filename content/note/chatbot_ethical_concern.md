---
title: "Chatbot Ethical Concern"
date: 2019-05-09T22:45:08-05:00
---

I have been making a Facebook Fan Page Chatbot using Dexter, a platform people can create automated conversation. The purpose of this robot is to help to answer questions from Taiwanese Students who study at the University of Illinois. It especially targets the frequent ask questions from Taiwanese Student Association Facebook Fan Page. 

There are two common approaches to build a chatbot. Some use **natural language processing** systems, others use **rule-based** pattern matching from a database.

Thus, before I started writing the content of this robot, I decided to download the facebook page message history. One of my friends told me that it can be illegal. I discussed it with my Information Science Professors, Professor Emily Knox, and Professor Judith Pintar. Both of them told me this can be an ethical issue. 

It’s not illegal because it’s mentioned in [Facebook’s Terms of Service]( https://www.facebook.com/full_data_use_policy)
Yet, even though Facebook Privacy Term mentions that Facebook is collecting the data. Generally, the users might feel bad finding out we analyzed it without their approvals. 

In the big data era, computer scientist, mathematicians, sociologists, and other scholars are looking for access to the massive quantities of information produced by and about people, things,
and their interactions. **Danah Boyd & Kate Crawford** points out that **"Just because it is accessible does not make it ethical"**. They gave an example of a Harvard-based research group research in 2006. In this research, they gather the profiles of 1700 college-based Facebook users to study how their interests and friendships changed over time(Lewis et al. 2008). Some other researchers found out that none of the students were aware that their data were being collected (Zimmer 2008). 

To download Facebook Fan Page Message, I used Facebook Graph API and a [python script-FB page chat download](https://github.com/eisenjulian/fb-page-chat-download) that I found on GitHub.

- Go to https://developers.facebook.com/tools/explorer and click 'Get User Access Token'
- Make sure to check 'manage_pages' and 'read_page_mailboxes'
- Switch to a page that you want to scrape
- Get the page_id and the access token to pass as parameters to the script

![img1](/fb-permission.png)

Normally, when we start to use a new APP on Facebook, it asks for users permission 'X would like to  ____ and ____' or 'X will receive ____'.

![img2](/fb-permission2.png)

It's not the case for an "in development App". It does not limit our access to the data without asking users' permission. 

### Why it mattered?

There is a link to a private policy for each Facebook Fan Page,. 

![img3](/privacy-policy.png)

When we deploy an APP on facebook, it requires us to prepare a private policy. 
In section [4. Collection of Data on Pages, Groups, and Events](https://www.facebook.com/policies/pages_groups_events/): Collecting Data From Users pages, groups, event of Facebook Policies, Facebook states: "If you collect content and information directly from users, your Page, Group or Event must make it clear that you (and not Facebook) are collecting it, and must provide notice about and obtain user consent for your use of the content and information that you collect."

When we request information from users through Facebook, this action triggers several laws aiming at protecting personal information. One of those is the General Data Protection Regulation (GDPR). This applies to all of the EU member states. 

Laws related to privacy that I can think of in America are the Computer Fraud and Abuse Act (“CFAA”) and the California Consumer Protection Act (CCPA).

California Consumer Protection Act, which will take effect in 2020, limits companies’ use of customer data and require businesses to give consumers more control over it. Maybe other states will follow up or federal privacy will be legislated. 

CFAA punishes who "intentionally accesses a computer without authorization or exceeds authorized access, and thereby obtains…information from any protected computer.” One of the cases about CFAA is "hiQ Labs, Inc vs. LinkedIn Corporation”. HiQ Labs is a business that relies on data-scraping on LinkedIn public data. 

I am not sure how many people notice this issue when downloading Facebook data. At least from the instruction in the python script I found, it did not point out anything related to ethical or policy regarding the data scraping. 

If you are interested in my process of the chatbot project, you can find it here: https://portfolio.ajoy.me/project/chatbot/

### Reference:

- Lewis, K., Kaufman, J., Gonzalez, M., Wimmer, A. & Christakis, N. (2008)‘Tastes, ties, and time: a new social network dataset using Facebook.com’,*Social Networks*, vol. 30, no. 4, pp. 330–342.
- Zimmer, M. (2008) ‘More on the “Anonymity” of the Facebook dataset – it’s Harvard College’, *MichaelZimmer.org Blog*, [Online](http://www.michaelzimmer.org/2008/01/03/more-on-the-anonymity-of-the-facebook-dataset-its-harvard-college/) (20 June 2011).
- boyd, d. & Crawford, K. (2012). Critical questions for big data: Provocations for a cultural, technological, and scholarly phenomenon. *Information, Communication & Society, 15*(5), 662–679.
- “Privacy Policy URL for Facebook App.” TermsFeed, 29 Oct. 2018, www.termsfeed.com/blog/privacy-policy-url-facebook-app/.