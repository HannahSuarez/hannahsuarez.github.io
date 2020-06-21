---
layout: post
title: "From the 2015 archive: Introduction to the different types of mining"
description: Introduction to the different types of mining
comments: true
keywords: "data, threat hunting"
---

> Below is an essay submitted on 8 May 2015 and re-written for this website.


## Introduction to the different types of mining

Due to the large swathes of data, it is important to note the different types of mining and what is involved in mining for data, metadata, text, web and social. However these areas tend to overlap over each other but each has its own distinctions.

While these areas overlap there are some differences. It is also important to note that for all types of data the following questions should be asked:

* What is the data retention strategy?
* What data warehouse will this go?
* Who pays for my data?
* Will I have control of my data?
* What is the company's thread model if there is a breach of my data?

## Metadata Mining

Metadata is a set of ‘hidden’ data that provides further information about a certain piece of data. For example, image exif data can contain metadata such as geolocation, camera hardware used and time. While metadata has existed, the term has entered into the wider public consciousness due to the NSA metadata gathering and storing thanks to the Snowden documents and further revelations from news media ranging from The Intercept to The Guardian. Metadata types includes descriptive, structural, and administrative (National Information Standards Organization, 2014).

Metadata provides a record of online actions online whether it is the websites visited, the geolocation searches being made, the email activity and some parts of the email content and event the account passwords. There are concerns, raised by the Guardian (Ball, J. 2013) that “this can be used to build a detailed picture of an individual's life.” The other item to note is that metadata collection can also take place beyond the web browser and into other channels and platforms such as phone metadata (Schneier, B. 2015).

Metadata mining has its applications within the banking and financial services sector ranging from database search right through to digital forensics to obtain evidence of a potential corporate espionage act. There is a chance that metadata is among the more useful types of data for these types of applications and has the ability to feed into further business intelligence applications as already seen in financial institutions such as banking.

## Text Mining

Text mining involves focusing on the mining of textual objects and information. Prior to the advent of the Internet and multimedia content are large volumes of text- and text-based works that are both offline (such as print, manuscripts), or converted into text (such as oral histories, translations). While other forms of mining involves text, such as web, metadata and social, text mining primarily involves these types of humanities related content in which the results are designed to be human readable straight away such as database searches. An example is the Text Encoding Initiative which is a project designed to develop guidelines for textual information such as “novels, plays and poetry” (National Information Standards Organization, 2014) and has a focus on the humanities.

Beyond the humanities, it is being recognised that text mining has uses within the business intelligence applications. For example, the Bank of Canada has published the paper using text mining techniques to determine whether their communications had an “impact on the Canadian interest rates over and above the effect of the monetary policy” (Hendry, S. Madeley, A., 2010).

## Web Mining

Web mining encompasses a variety of other types of mining such as social, image and text. Due to the specific features of each type of mining it is a good idea to consider these separately. According to Wikipedia, “Web mining - is the application of data mining techniques to discover patterns from the Web” (Wikipedia, 2015). It is also further divided into three types – “Web usage mining, Web content mining and Web structure mining.” (Wikipedia, 2015). Web mining has a number of business intelligence applications such as the analysis of web pages to detect e-banking phishing scam websites (Aburrous, M., Hossain, M. A., Dahal, K., Thabatah, F., 2009) or to detect the structure of the web content to determine if the search engine optimization strategy of a financial product is black hat in nature.

## Social Mining

Social mining involves the social web and with it unique components as well as technologies and techniques. Social mining encompasses the main platforms such as Twitter, Facebook, YouTube, Vimeo, conversation technologies such as Disqus and LiveFyre, as well as the separate clusters of blogs and discussions forums. The unique components that separates social mining from the rest is its association with human metrics – its influence, reach, audience, activity type, networks (online/social), the emotions involves (such as positive, neutral and negative).

Business applications involving social mining has been widely adopted due to the availability of tools, including popular ones like Klout, the explosion of social media use and its evangelism within the tech and business community such as digital strategists and online marketers. In banking, it is reported that banks do mine social media sites for data including customer insights (Peppers & Rogers Group, 2014) and is then merged into data retrieved via offline channels.

## Image and Multimedia (Video/Audio) Mining

Similar to the metadata example involved Exif metadata within an image, there is also the practice of image and video mining. In images themselves are different types of metadata – IPTC-IIM, IPTC Core & Extension, PLUS, XMP, Dublin Core and the more well-known Exif type (PhotoMetaData.org, year unknown). Thanks to technological innovations in natural language processing and other artificial intelligence techniques, image mining will become more ‘smart’ as seen by facial recognition in Windows 10 (Steele, B. 2015) in which the content is submitted, processed and stored in Microsoft servers.

For multimedia, there is the MPEG-7, Multimedia Content Description Interface (ISO/IEC 15938), and MPEG-21, Multimedia Framework (ISO/IEC 21000) which are the standards concerning metadata (National Information Standards Organization, 2014). This covers a number of metadata elements “including still pictures, graphics, 3D models, music, audio, speech, video, or multimedia collections” (National Information Standards Organization, 2014).

Just like other forms of mining, image/multimedia mining is transferrable across other types of data being mined such as the extraction and mining of satellite imagery from the Google Maps Engine (Bernabe, S., Plaza, A., 2010).

# Types of mining and their relevance to the field of Business Intelligence

## Web Mining

Web mining will have a continued business intelligence relevance especially as websites continue to be the first point of contact. For example, the insights gained from user activities via logs and analytics are useful for retail banks in gaining insights and to optimise the online experience for further actions within the user conversion tunnel such as a purchase or a download. One of the potential downfalls of this type of mining is in user privacy.  For example, a security researcher has developed a persistent ‘zombie cookie’ which is intentionally difficult to delete (Kamkar, 2010). Another security researcher has dubbed the ‘perma-cookie’ which inserts a UIDH that allows advertisers to identify individuals on the web (White, 2014) – this modification is seen as untrusted as it allows a profile to be built up of the user based on internet habits.  

## Social Mining

Social media is a continued force and may soon play a higher strategic role on the Internet following Facebook’s involvement in larger scale initiatives such as Internet.org (Levy, J., 2015). Therefore social mining may soon eclipse as the more strategic focus in overall data mining operations as the Internet-enabled population increases. Mining operations in this field should therefore be a continued focus for business intelligence applications that wish to remain relevant in the future – instead of being a case of “pro” and “con” it will be more of a “must-have”.

## Image and Multimedia (Audio/Video) Mining

As the consumer attention online becomes more competitive, other forms of content such as image and multimedia are being preferred especially in the shift from social media to visual social media (Moritz, D., 2012). Including this type of mining is a pro for consumer-facing business intelligence applications, especially in relation to social web, where in one minute “Instagram users post nearly 220,000 new photos (and) YouTube users upload 72 hours of new video content” (Gunelius, S., 2014). An obvious con for this type of mining work will involve copyright issues due to the content, privacy issues of the individuals involved, capital requirements for data warehousing activities as well as the continued evolution of technologies such as natural language processing in image recognition to a text (ie searchable) format.

# Text and Data Mining

Overall, data mining has the following main negatives:

The infrastructure requirements in handling the amount of data that needs to be stored, processed, analysed will grow over time and over use. With these requirements there are also capital requirements that need to be covered by the business. The limitations of infrastructure would mean limitations on ability, including dealing with unstructured data. Infrastructure tech companies such as Dell recognise this (Dell, 2013).
In terms of handling existing requirements, also in future requirements since data can only increase, there is the issue of requiring technical expertise. This expertise tends to be developed in-house or contracted externally so it is not a big issue.
Integration of unstructured text into a structured environment (aka 'garbage in, garbage out') is also another issue. An example is web-extracted data which is mostly unstructured data and this area still requires further research.
In this case it's good to have guiding principles such as making fact- or evidence-based decisions regarding data. However the negatives are mainly seen as challenges to be addressed in a data-rich and eventually data-driven world.

# Notable uses or applications of each type of mining

## Data Mining

KYC (Know Your Customer)/AML (anti money laundering) initiatives use data mining within the financial services. Data mining assists in the core of transaction monitoring, pattern recognition, and through using techniques in statistical model building, clustering, link analysis and visualisation (PricewaterhouseCoopers, 2005).

Data mining to help mitigate (either as prevention or as part of incidence response) corporate, economic and industrial espionage has obvious business intelligence application. For example, ICS/SCADA systems is one such area under threat. An attacker can penetrate the network and steal IP – this type of attack could potentially be detected via data mining and data analysis approaches to intrusion detection which was identified in research such as the Detection of Novel Network Attacks Using Data Mining.

## Social Mining

Social Content Mining can help build up a customer profile based on data that is already available on the social web. Posting on social networks has also become a major activity online by consumers. This type of mining does not encompass large amounts of data compared to previous example but the data involved is of a high importance due to the exclusive nature as being associated with an individual. Other related sectors could include luxury but the other obvious application is in customer-oriented companies.

Due to the prevalent nature of social web, and also because it is part of an area known as “open source intelligence” social mining is a rich source of data included in data analysis software applications such as Maltego. In another sector, it is used by different groups to build up and create a target profile or a ‘social networking special ops’ (Sumner, C., 2010) based on a social media Tony Hawk campaign.

## Web Mining

A recent application was in Selerity’s web crawler which picked up Twitter’s Investor Relations website news prior to the official launch from Twitter which thus affected the stock price. Selerity’s main selling point of the product is in utilising ‘real-time data’ (Selerity, 2015). In order for the Selerity web crawler to be efficient, it required utilizing data mining techniques including predicting the URL address ‘template’ or to “automatically identify the URL of a company's earnings statement before that URL is shared publicly” (Selerity, 2015).

## Metadata Mining

Metadata is also mined in business application such as robo-advisers that utilise this minig to make recommendations for clients. An example is the use of CRM data to advise clients on making portfolio withdrawals (Graham, P. 2014). The signal-to-noise ratio found in metadata, a negative, will require human intelligence and intervention for it to be applicable in situations such as the robo-adviser example.

## Image / Multimedia (Audio, Video) Mining

One such example that can be gleaned out of this is the reverse search by Image on Google Search which uses a Content Based Image Retrieval (CBIR) query system (Chitu, A., 2013) . CIBR efficiency is improved via Data mining using machine learning algorithms whereby images can be categorised and clustered based on their features (Iskander, A., Thom, J., Tahaghoghi, S., 2008). This is an example where innovations in data mining can help play a role in improving systems that rely on this technologies alongside others. Image mining as a sole discipline it itself which can also further encompass further specializations. The author believes that this is another high value area especially in assisting further innovations and can build upon innovations from the past, such as check image archives.

# On data and business analytics

There are a number of different types of data analytics including predictive analytics which is one of the main differentiators from regular analytics.

For example of the analytics types, ANN, has many uses, including pattern recognition, forecasting, prediction and classification. This is useful in terms of being able to recognise behavioural patterns according to previous histories, classify these behaviour patterns, then forecast and predict possible future actions. An example is in the JP Morgan algorithm to help detect potential rogue employees (Son, H., 2015). Cybersecurity and data analytics has helped mitigate cases of corporate and industrial espionage or at least deal with concerns regarding companies. Within financial services, data mining techniques has aided in KYC (Know Your Customer)/AML (anti money laundering) initiatives.  LBA (location based analytics) is in use from banking to gauge potential fraud use. For example, if you are using an ATM in London, and that is your ‘usual’ ATM based on past history, but the next instance is an ATM in Singapore it may potentially alert the bank of potential fraud. Geo-location analytics is part of their arsenal of safeguards to protect customers of potential fraudulent activityOne of the concerns lies in privacy as for these to work requires a number of different and also qualified data points. Some of these data points will be via external sources from online (such as social networks) to offline (such as traffic history reports, police reports).

## On social analytics

Social analytics involves analysing the influence, reach, and other human-computer interactions (such as metrics in user interaction) on social-centred online platforms like social networks. As consumer-centred approaches become more important in certain business sectors, this is turning into an important business topic.

As mentioned previously, Maltego is one of example of an open source tool used to do social network analysis as part of open source intelligence gathering. The metrics it utilises includes not only the number of networks and connections but also the relationships between connections, any potential topics of interest and so on. A practical use of Maltego is in creating a list of security researchers on Twitter that are being monitored by GCHQ (Maltego, 2015).

# Conclusion notes

Overall, users are willing to take part providing their data when it serves their needs – from security to social. We should also look into the data collection, retention plans, policies and technologies around us. The reality here is that users, for the most part, are unaware as to how much data they are not only broadcasting and providing deliberately, but are also leaking. This short essay provides an overview in the types of data mining involved which can be used for business intelligence applications as well as used in conjunction with other types of analysis that can help build a user profile.

# References

Aburrous, M., Hossain, M. A., Dahal, K., Thabatah, F. (2009). Modelling Intelligent Phishing Detection System for e-Banking using Fuzzy Data Mining. Retrieved fromhttp://www.researchgate.net/profile/Keshav_Dahal/p...

Ball, J. (2013). NSA stores metadata of millions of web users for up to a year, secret files show. Retrieved from http://www.theguardian.com/world/2013/sep/30/nsa-a...

Bernabe, S., Plaza, A. (2010). A New Tool for Information Extraction and Mining from Satellite Imagery Available from Google Maps Engine. Retrieved fromhttp://www.umbc.edu/rssipl/people/aplaza/Papers/Co...

Chitu, A. (2013). How Google's Image Recognition Works. http://googlesystem.blogspot.in/2013/06/how-google...

Dell. (2013). Managing unstructured data. Retrieved from http://www.dell.com/learn/us/en/555/smb/cat3q13-20...

Ertoz, L., Eilertson, E., Lazarevic, A., Tan. P., Dokas, P., et al. (2003). Detection of Novel Network Attacks Using Data Mining. Retrieved fromhttp://www.researchgate.net/profile/Vipin_Kumar26/...

Graham, P. (2014). Wealth Adviser: Beating Robo-Advisers at Their Own Game. Retrieved from http://blogs.wsj.com/totalreturn/2014/08/04/wealth...

Gunelius, S. (2014). The Data Explosion in 2014 Minute by Minute – Infographic. Retrieved from http://aci.info/2014/07/12/the-data-explosion-in-2...

Hendry, S. Madeley, A. (2010). Text Mining and the Information Content of Bank of Canada Communications. Retrieved from http://www.bankofcanada.ca/wp-content/uploads/2010...

Iskander, A., Thom, J., Tahaghoghi, S. (2008). Content-based Image Retrieval Using Image Regions as Query Examples. Retrieved fromhttp://crpit.scem.uws.edu.au/confpapers/CRPITV75Aw...

Kamkar, S. (2010). Evercookie. Retrieved from samy.pl/evercookie/

Levy, J. (2015). Opinion: Facebook’s Internet.org isn’t the Internet, it’s Facebooknet. Retrieved from http://www.wired.com/2015/05/opinion-internet-org-...

Maltego. (2015). Building your own LovelyHorse monitoring system with Maltego (even the free version) - it's easy! Retrieved fromhttp://maltego.blogspot.com.au/2015/02/building-yo...

Moritz, D. (2012). The Shift to Visual Social Media – 6 Tips for Business [Infographic]. Retrieved from http://sociallysorted.com.au/shift-to-visual-socia...

National Information Standards Organization. (2014). Understanding Metadata. Retrieved from http://www.niso.org/publications/press/Understandi...

Peppers & Rogers Group. (2014). Mining for Social Customer Gold in Retail Banking. Retrieved from http://www.peppersandrogersgroup.com/view.aspx?doc...

PhotoMetaData.org. Types of Metadata. Retrieved from http://www.photometadata.org/meta-101-metadata-typ...

PricewaterhouseCoopers. (2005). Anti-Money Laundering. Retrieved from http://www.pwc.com/en_GX/gx/financial-services/pdf...

Selerity. (2015). Selerity. Retrieved from http://www.seleritycorp.com/


Schneier, B. (2015). Another Example of Cell Phone Metadata Forensic Surveillance. Retrieved from https://www.schneier.com/blog/archives/2015/05/ano...

Son, H. (2015). JPMorgan Algorithm Knows You’re a Rogue Employee Before You Do. Retrieved from http://www.bloomberg.com/news/articles/2015-04-08/...

Steele, B. (2015). Microsoft thinks it can guess your age using facial recognition. Retrieved from http://www.engadget.com/2015/04/30/microsoft-azure...

Sumner, C. (2010). Social Networking Special Ops: Extending data visualization tools for faster pwnage. Retrieved from https://media.blackhat.com/bh-us-10/whitepapers/Su...

Wagner, K. (2015). Twitter Stock Tanks on Revenue Miss, Weak Guidance. Retrieved from http://recode.net/2015/04/28/wall-street-halts-twi...

White, K. (2014). Checking known AT&T, Verizon, Sprint, Bell Canada & Vodacom Unique Identifier beacons. Retrieved from http://lessonslearned.org/sniff

Wikipedia. (2015). Web mining. Retrieved from http://en.wikipedia.org/wiki/Web_mining
