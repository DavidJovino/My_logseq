- # Introduction
  collapsed:: true
	- In order to target APIs, you must first be able to find them. In this
	   module, we will learn how to uncover the API attack surface of a target
	   using passive and active reconnaissance techniques.
	  
	  How an API is meant to be consumed will determine how easily it can 
	  be found. Public APIs are meant to be easily found and used by 
	  end-users. Public APIs may be entirely public without authentication or 
	  be meant for use by authenticated users. Authentication for a public API
	   primarily depends on the sensitivity of the data that is handled. If a 
	  public API only handles public information then there is no need for 
	  authentication, in most other instances authentication will be 
	  required. Public APIs are meant to be consumed by end-users. In order to
	   facilitate this, API providers share documentation that serves as an 
	  instruction manual for a given API. This documentation should be 
	  end-user friendly and relatively straightforward to find.
	  
	  **Partner APIs** are intended to be used exclusively by 
	  partners of the provider. These might be harder to find if you are not a
	   partner. Partner APIs may be documented, but documentation is often 
	  limited to the partner.
	  
	  **Private APIs** are intended for use, privately, within
	   an organization. These APIs are often documented less than partner 
	  APIS, if at all, and if any documentation exists it is even harder to 
	  find. 
	  
	  In all instances where API documentation is unavailable, you will 
	  need to know how to reverse engineer API requests. We will cover reverse
	   engineering in a follow-up module. For now, we will focus on detecting 
	  APIs and using them as described within discovered documentation.
- ## Web API Indicators
  collapsed:: true
	- APIs meant for consumer use are meant to be easily discovered. 
	  Typically, the API provider will market their API to developers who want
	   to be consumers. So, it will often be very easy to find APIs, just by 
	  using a web application as an end-user. The goal here is to find APIs to
	   attack and this can be accomplished by discovering the API itself or 
	  the API documentation. If you can find the target's API and 
	  documentation as an end-user then mission accomplished, you have 
	  successfully discovered an API.
	  
	  Another way to find an API provided by a target is to look around the
	   target's landing page. Look through a landing page for links to API or 
	  development portal. When searching for APIs there are several signs that
	   will indicate that you have discovered the existence of a web API. Be 
	  on the lookout for obvious URL naming schemes:
	  
	  [https://target-name.com/api/v1](https://target-name.com/api/v1) 
	  
	  [https://api.target-name.com/v1](https://api.target-name.com/v1) 
	  
	  [https://target-name.com/docs](https://target-name.com/v1)
	  
	  [https://dev.target-name.com/rest](https://target-name.com/v1)
	  
	  Look for API indicators within directory names like:
	  */api, /api/v1, /v1, /v2, /v3, /rest, /swagger, /swagger.json, /doc, /docs, /graphql, /graphiql, /altair, /playground*
	  
	  Also, subdomains can also be indicators of web APIs:
	  
	  **api**.target-name.com
	  
	  **uat**.target-name.com
	  
	  **dev**.target-name.com
	  
	  **developer**.target-name.com
	  
	  **test**.target-name.com
	  
	  
	  
	  Another indicator of web APIs is the HTTP request and response 
	  headers. The use of JSON or XML can be a good indicator that you have 
	  discovered an API. 
	  
	  *HTTP Request and Response Headers containing "Content-Type: application/json, application/xml"*
	  
	  
	  
	  *Also, watch for HTTP Responses that include statements like:
	  {"message": "Missing Authorization token"}*
	  
	  
	  
	  One of the most obvious indicators of an API would be through 
	  information gathered using third-Party Sources like Github and API 
	  directories.
	  
	  Gitub: [https://github.com/](https://github.com/) 
	  
	  Postman Explore: [https://www.postman.com/explore/apis](https://www.postman.com/explore/apis)
	  
	  ProgrammableWeb API Directory: [https://www.programmableweb.com/apis/directory](https://www.programmableweb.com/apis/directory) 
	  
	  APIs Guru: [https://apis.guru/](https://apis.guru/) 
	  
	  Public APIs Github Project: [https://github.com/public-apis/public-apis](https://github.com/public-apis/public-apis) 
	  
	  RapidAPI Hub: [https://rapidapi.com/search/](https://rapidapi.com/search/) 
	  
	  
	  
	  When searching for a target's APIs use a target's web application as 
	  it was designed. Use a browser go to the web application and see if an 
	  API is advertised. Once you have an idea of how the web app functions, 
	  dig deeper by deploying passive and active reconnaissance techniques.
-
- # **Passive Reconnaissance** #API_Passive_Reconnaissance
	- ## **Introduction**
	  collapsed:: true
		- Passive API Reconnaissance **is the act of obtaining 
		  information about a target without directly interacting with the 
		  target’s systems. When you take this approach, your goal is to find and 
		  document public information about your target’s attack surface. 
		  
		  Typically, passive reconnaissance leverages open-source intelligence 
		  (OSINT), which is data collected from publicly available sources. You 
		  will be on the hunt for API endpoints, exposed credentials, version 
		  information, API documentation, and information about the API’s business
		   purpose. Any discovered API endpoints will become your targets later, 
		  during active reconnaissance. Credential-related information will help 
		  you test as an authenticated user or, better, as an administrator. 
		  Version information will help inform you about potential improper assets
		   and other past vulnerabilities. API documentation will tell you exactly
		   how to test the target API. Finally, discovering the API’s business 
		  purpose can provide you with insight into potential business logic 
		  flaws.
		  
		  As you are collecting OSINT, it is entirely possible you will stumble
		   upon a critical data exposure, such as API keys, credentials, JSON Web 
		  Tokens (JWT), and other secrets that would lead to an instant win. Other
		   high-risk findings would include leaked PII or sensitive user data such
		   as SSN, full names, email addresses, and credit card information. These
		   sorts of findings should be documented and reported immediately because
		   they present a valid critical weakness.
		  
		  Now we will check out a few passive reconnaissance techniques that 
		  can be leveraged to discover APIs. Including Google Dorking, Git 
		  Dorking, API Repositories, the Way Back Machine, and Shodan.
	-
	- ## **Google Dorking** #Google_Dorking
	  collapsed:: true
		- Even without any Dorking techniques, finding an API as an end-user could be as easy as a quick search.
		  
		  ![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/3QiE3ZaXRLWKOYwRfCre_redditapisearch.png)
		  
		  *Google Search for Reddit's API.*
		  
		  However, sometimes you may not get the exact results you were hoping 
		  for. If you are getting too many irrelevant results then you could 
		  deploy some Google Dorking techniques to more effectively discover APIs.
		  
		  ![image.png](../assets/image_1678827182835_0.png)
	- ## **GitDorking** #GitDorking
	  collapsed:: true
		- Regardless of whether your target performs its own development, it’s worth checking GitHub (www.github.com)
		   for sensitive information disclosure. Developers use GitHub to 
		  collaborate on software projects. Searching GitHub for OSINT could 
		  reveal your target’s API capabilities, documentation, and secrets, such 
		  as API keys, passwords, and tokens, which could prove useful during an 
		  attack. Similar to Google Dorking, with GitHub, you can specify 
		  parameters like:
		  
		  **filename**:swagger.json
		  
		  **extension**: .json
		  
		  Begin by searching GitHub for your target organization’s name paired 
		  with potentially sensitive types of information, such as “api key,” "api
		   keys", "apikey", "authorization: Bearer", "access_token", "secret", or 
		  “token.” Then investigate the various GitHub repository tabs to discover
		   API endpoints and potential weaknesses. Analyze the source code in the 
		  Code tab, find bugs in the Issues tab, and review proposed changes in 
		  the Pull requests tab.
		  
		  ![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/vJHflsacRw6gsCDkbd2c_GithubExposed.png)
		  
		  Code contains the current source code, readme files, and other files.
		   This tab will provide you with the name of the last developer who 
		  committed to the given file, when that commit happened, contributors, 
		  and the actual source code. 
		  
		  ![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/Dn6kLSBGmQ2mI5S484Ao_GithubCode.png)
		  
		  Using the Code tab, you can review the code in its current form or use ctrl-F
		   to search for terms that may interest you (such as API, key, and 
		  secret). Additionally, view historical commits to the code by using the 
		  History button found near the top-right corner of the above image.  If 
		  you came across an issue or comment that led you to believe there were 
		  once vulnerabilities associated with the code, you can look for 
		  historical commits to see if the vulnerabilities are still viewable.
		  
		  
		  
		  When looking at a commit, use the Split button to see a side-by-side 
		  comparison of the file versions to find the exact place where a change 
		  to the code was made.![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/I7Zza4TSRgG0dQ5NFdQg_GithubHistory.png)The
		   Split button (top right of the above image) allows you to separate the 
		  previous code (left) and the updated code (right). Here, you can see a 
		  commit to an application that removed the Google Maps API key from the 
		  code, revealing both the key and the API endpoint it was used for.
		  
		  The Issues tab is a space where developers can track bugs, tasks, and
		   feature requests. If an issue is open, there is a good chance that the 
		  vulnerability is still live within the code (see Figure 6-9).
		  
		  ![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/S0xHhF3QWyPOOVFIewWQ_GithubIssue.png)
		  
		  This is an example, of an open GitHub issue that provides the exact 
		  location of an exposed API key in the code of an application. If the 
		  issue is closed, note the date of the issue and then search the commit 
		  history for any changes around that time. 
		  
		  The Pull requests tab is a place that allows developers to 
		  collaborate on changes to the code. If you review these proposed 
		  changes, you might sometimes get lucky and find an API exposure that is 
		  in the process of being resolved. As this change has not yet been merged
		   with the code, we can easily see that the API key is still exposed 
		  under the Files changed tab. The Files changed tab reveals the section 
		  of code the developer is attempting to change. 
		  
		  If you don’t find weaknesses in a GitHub repository, use it instead 
		  to develop the profile of your target. Take note of programming 
		  languages in use, API endpoint information, and usage documentation, all
		   of which will prove useful moving forward.
	- ## **TruffleHog**  #TruffleHog
	  collapsed:: true
		- TruffleHog is a great tool for automatically discovering exposed 
		  secrets. You can simply use the following Docker run to initiate a 
		  TruffleHog scan of your target's Github.
		  
		   $ sudo docker run -it -v "$PWD:/pwd" trufflesecurity/trufflehog:latest github --org=target-name
		  
		  ![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/01s4gYuoQmq9GgdZg4oG_TruffleHogv3.png)
		  
		  In the above example, you can see that the org that was targeted was 
		  Venmo and the results of the scan indicate URLs that should be 
		  investigated for potentially leaked secrets. In addition to searching 
		  Github, TruffleHog can also be used to search for secrets in other 
		  sources like Git, Gitlab, Amazon S3, filesystem, and Syslog. To explore 
		  these other options use the "-h" flag. For additional information check 
		  out [https://github.com/trufflesecurity/trufflehog](https://github.com/trufflesecurity/trufflehog).
	- ## **API Directories** #API_Directories
	  collapsed:: true
		- Programmableweb.com is a go-to source for API-related information ([https://www.programmableweb.com/apis/directory](https://www.programmableweb.com/apis/directory)).
		   To learn about APIs, you can use their API University. To gather 
		  information about your target, use the API Directory, a searchable 
		  database of over 23,000 APIs. Expect to find API endpoints, version 
		  information, business logic information, the status of the API, source 
		  code, SDKs, articles, API documentation, and a changelog.
		  
		  ![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/Pl5zVW8Rde4fCFd32jz3_twilioapidirectory.png)
		  
		  *Twilio API page on programmableweb.com.*
		  
		  Click through the various tabs in the directory listing 
		  and note the information you find. To see the API endpoint location, 
		  portal location, and authentication model. To see information about the 
		  APIs version history, select a specific version listed under the 
		  Versions tab. In this case, both the portal and endpoint links lead to 
		  API documentation as well. In the case of Twilio, you can see all the specs related to the current version of the REST API.
		  
		  ![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/8Zn6Z9PIRse67JCxJz8s_twilioapidirectory2.png)
		  
		  *The Twilio specs page on programmableweb.com.*
		  
		  On the Twilio specs page, you can learn all sorts of 
		  useful information about the API. For instance, the API endpoint URL is 
		  listed, the forum for the API, the developer support URL, the 
		  authentication model, and more are all listed on this page. At the 
		  bottom of the Specs page, you can also see articles related to the API 
		  and developers of the API, all of which could prove useful when 
		  attacking the API.
	- ## **Shodan** #Shodan
	  collapsed:: true
		- Shodan is the go-to search engine for devices accessible from the 
		  internet. Shodan regularly scans the entire IPv4 address space for 
		  systems with open ports and makes their collected information public on https://shodan.io.
		   You can use Shodan to discover external-facing APIs and get information
		   about your target’s open ports, making it useful if you have only an IP
		   address or organization’s name to work from. Like with Google dorks, 
		  you can search Shodan casually by entering your target’s domain name or 
		  IP addresses; alternatively, you can use search parameters like you 
		  would when writing Google queries. The following table shows some useful
		   Shodan queries.
		  
		  ![image.png](../assets/image_1678827326586_0.png)
	- ## **The Wayback Machine** #The_Wayback_Machine
	  collapsed:: true
		- The Wayback Machine is an archive of various web pages over time. 
		  This is great for passive API reconnaissance because this allows you to 
		  check out historical changes to your target. If, for example, the target
		   once advertised a partner API on their landing page, but now hides it 
		  behind an authenticated portal, then you might be able to spot that 
		  change using the Wayback Machine. Another use case would be to see 
		  changes to existing API documentation. If the API has not been managed 
		  well over time, then there is a chance that you could find retired 
		  endpoints that still exist even though the API provider believes them to
		   be retired. These are known as Zombie APIs. Zombie APIs fall under the 
		  Improper Assets Management vulnerability on the OWASP API Security Top 
		  10 list. Finding and comparing historical snapshots of API documentation
		   can simplify testing for Improper Assets Management.  ![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/FGPF2fPT8ysfQHtTHQbk_Wayback1.PNG)
		  
		  Check for differences between the API documentation. Later, when you 
		  are actively testing the API, make sure to test using old endpoints,
-
	- ## **Conclusion**
	  collapsed:: true
		- In this module, we covered some basic techniques that can be deployed
		   to gather about your target's API attack surface. The first step to 
		  hacking a target's APIs is to uncover as much information about them as 
		  possible. Using these reconnaissance techniques can not only help you 
		  discover the existence of APIs, but can also lead to critical 
		  vulnerability findings. Next we will focus on active recon techniques.
-
-
-
- # **Active API Reconnaissance** #API_Active_Reconnaissance
	- ## **Introduction**
	  collapsed:: true
		- Active reconnaissance is the process 
		  of interacting directly with the target primarily through the use of 
		  scanning. We will use our recon to search for our target's APIs and any 
		  useful information.
		  
		  During this process you will be 
		  scanning systems, enumerating open ports, and finding ports that have 
		  services using HTTP. Once you have found systems hosting HTTP, you can 
		  open a web browser and investigate the web application. You could find 
		  an API being advertised to end users or you may have to dig deeper. 
		  Finally, you can scan the web app for API-related directories. 
		  Essentially, you will be building out the target's API attack surface. 
		  During active recon we will use tools like: nmap, OWASP Amass, gobuster,
		   kiterunner, and DevTools.
	-
	- ## **Nmap** #Nmap
	  collapsed:: true
		- Nmap is a powerful tool for scanning ports, searching for 
		  vulnerabilities, enumerating services, and discovering live hosts. For 
		  API discovery, you should run two Nmap scans in particular: general 
		  detection and all port. The Nmap general detection scan uses default 
		  scripts (-sC) and service enumeration (-sV) against a target and then 
		  saves the output in three formats for later review (-oX for XML, -oN for Nmap, -oG for greppable, or -oA for all three):
		  
		  $ nmap -sC -sV [target address or network range] -oA nameofoutput
		  
		  The Nmap all-port scan will quickly check all 65,535 TCP ports for 
		  running services, application versions, and host operating system in 
		  use:
		  
		  $ nmap -p- [target address] -oA allportscan
		  
		  As soon as the general detection scan begins returning results, kick 
		  off the all-port scan. Then begin your hands-on analysis of the results.
		   You’ll most likely discover APIs by looking at the results related to 
		  HTTP traffic and other indications of web servers. Typically, you’ll 
		  find these running on ports 80 and 443, but an API can be hosted on all 
		  sorts of different ports. Once you discover a web server, you can 
		  perform HTTP enumeration using a Nmap NSE script (use -p to specify 
		  which ports you'd like to test).
		  
		  ```
		  **$ nmap -sV --script=http-enum <target> -p 80,443,8000,8080**
		  ```
	- ## **OWASP Amass** #OWASP_Amass
	  collapsed:: true
		- OWASP Amass is a command-line tool that can map a target’s external 
		  network by collecting OSINT from over 55 different sources. You can set 
		  it to perform passive or active scans. If you choose the active option, 
		  Amass will collect information directly from the target by requesting 
		  its certificate information. Otherwise, it collects data from search 
		  engines (such as Google, Bing, and HackerOne), SSL certificate sources 
		  (such as GoogleCT, Censys, and FacebookCT), search APIs (such as Shodan,
		   AlienVault, Cloudflare, and GitHub), and the web archive Wayback.
		- ### Making the most of Amass with API Keys
		  
		  Before diving into using Amass, we should make the most of it by 
		  adding API keys to it. Let's obtain a few free API keys to enhance our 
		  Amass scans.
		  
		  First, we can see which data sources are available for Amass (paid and free) by running:
		  $ amass enum -list 
		  ![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/eex0psZsSx2Zyd9ekGIl_ActiveDiscovery1.PNG)
		  
		  Next, we will need to create a config file to add our API keys to.
		  
		  **`$ sudo curl https://raw.githubusercontent.com/OWASP/Amass/master/examples/config.ini >~/.config/amass/config.ini`**
		  
		  Now we can update the config.ini. I will demonstrate the process for adding API keys with Censys. Simply visit [https://censys.io/register](https://censys.io/register) and
		   register for a free account. Make sure to use a valid email because you
		   will have to verify for access to your free account.
		  
		  ![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/ZMWysMVxSPp9CREpENjU_ActiveDiscovery2.PNG)
		  
		  Once you have obtained your API ID and Secret, edit the config.ini file and add the credentials to the file.
		  
		  **`$ sudo nano ~/.config/amass/config.ini`**
		  
		  ![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/XYQwwA4JTwWOF7CH0d3T_ActiveDiscovery3.PNG)
		  
		  Also, as with any credentials make sure not to share them like I just
		   did. If you did share them then simply use the "Reset My API Secret" 
		  button back on Censys.io. You can repeat this process with many free 
		  accounts and API keys, then you will make OWASP Amass into a powerhouse 
		  for API reconnaissance.
		  
		  **`$ amass enum -active -d target-name.com |grep api`**
		  
		  legacy-api.target-name.com
		  
		  api1-backup.target-name.com
		  
		  api3-backup.target-name.com
		  
		  
		  
		  This scan could reveal many unique API subdomains, including legacy-api.target-name.com. An API endpoint named legacy could be of particular interest because it seems to indicate an improper asset management vulnerability.
		  
		  Amass has several useful command-line options. Use the intel command
		   to collect SSL certificates, search reverse Whois records, and find ASN
		   IDs associated with your target. Start by providing the command with 
		  target IP addresses
		  
		  $ amass intel -addr [target IP addresses]
		  
		  If this scan is successful, it will provide you with domain names. These domains can then be passed to intel with the whois option to perform a reverse Whois lookup:
		  
		  $ amass intel -d [target domain] –whois
		  
		  This could give you a ton of results. Focus on the interesting 
		  results that relate to your target organization. Once you have a list of
		   interesting domains, upgrade to the enum subcommand to begin enumerating subdomains. If you specify the **-**passive option, Amass will refrain from directly interacting with your target:
		  
		  $ amass enum -passive -d [target domain]
		  
		  The active enum scan will 
		  perform much of the same scan as the passive one, but it will add domain
		   name resolution, attempt DNS zone transfers, and grab SSL certificate 
		  information:
		  
		  $ amass enum -active -d [target domain]
		  
		  To up your game, add the -brute option to brute-force subdomains, -w to specify the API_superlist wordlist, and then the -dir option to send the output to the directory of your choice:
		  
		  $ amass enum -active -brute -w /usr/share/wordlists/API_superlist -d [target domain] -dir [directory name]
	- ## **Directory Brute-force with Gobuster** #Gobuster
	  collapsed:: true
		- Gobuster can be used to brute-force URIs and DNS subdomains from the 
		  command line. (If you prefer a graphical user interface, check out 
		  OWASP’s Dirbuster.) In Gobuster, you can use wordlists for common 
		  directories and subdomains to automatically request every item in the 
		  wordlist and send them to a web server and filter the interesting server
		   responses. The results generated from Gobuster will provide you with 
		  the URL path and the HTTP status response codes. (While you can 
		  brute-force URIs with Burp Suite’s Intruder, Burp Community Edition is 
		  much slower than Gobuster.)
		  
		  Whenever you’re using a brute-force tool, you’ll have to balance the 
		  size of the wordlist and the length of time needed to achieve results. 
		  Kali has directory wordlists stored under /usr/share/wordlists/dirbuster that
		   are thorough but will take some time to complete. Instead, you can use 
		  an API-related wordlist, which will speed up your Gobuster scans since 
		  the wordlist is relatively short and only contains directories related 
		  to APIs.
		  
		  The following example uses an API-specific wordlist to find the directories on an IP address:
		  
		  $ gobuster dir -u target-name.com:8000 -w /home/hapihacker/api/wordlists/common_apis_160
		  
		  ========================================================
		  
		  Gobuster
		  
		  by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
		  
		  ========================================================
		  
		  [+] Url:                     http://192.168.195.132:8000
		  
		  [+] Method:                  GET
		  
		  [+] Threads:                 10
		  
		  [+] Wordlist:                /home/hapihacker/api/wordlists/common_apis_160
		  
		  [+] Negative Status codes:   404
		  
		  [+] User Agent:              gobuster
		  
		  [+] Timeout:                 10s
		  
		  ========================================================
		  
		  09:40:11 Starting gobuster in directory enumeration mode
		  
		  ========================================================
		  
		  /api                (Status: 200) [Size: 253]
		  
		  /admin                (Status: 500) [Size: 1179]
		  
		  /admins               (Status: 500) [Size: 1179]
		  
		  /login                (Status: 200) [Size: 2833]
		  
		  /register             (Status: 200) [Size: 2846]
		  
		  Once you find API directories like the /api directory
		   shown in this output, either by crawling or brute force, you can use 
		  Burp to investigate them further. Gobuster has additional options, and 
		  you can list them using the -h option:
		  
		  $ gobuster dir -h
		  
		  If you would like to ignore certain response status codes, use the option -b. If you would like to see additional status codes, use -x. You could enhance a Gobuster search with the following:
		  
		  $ gobuster dir -u
		  
		  ://targetaddress/ -w /usr/share/wordlists/api_list/common_apis_160 -x 200,202,301 -b 302
		  
		  Gobuster provides a quick way to enumerate active URLs find API paths.
	- ## **Kiterunner** #Kiterunner
	  collapsed:: true
		- Kiterunner is an excellent tool that was developed and released by 
		  Assetnote. Kiterunner is currently the best tool available for 
		  discovering API endpoints and resources. While directory brute force 
		  tools like Gobuster/Dirbuster/ work to discover URL paths, it typically 
		  relies on standard HTTP GET requests. Kiterunner will not only use all 
		  HTTP request methods common with APIs (GET, POST, PUT, and DELETE) but 
		  also mimic common API path structures. In other words, instead of 
		  requesting GET /api/v1/user/create, Kiterunner will try POST /api/v1/user/create, mimicking a more realistic request.
		  
		  You can perform a quick scan of your target’s URL or IP address like this:
		  
		  $ kr scan HTTP://127.0.0.1 -w ~/api/wordlists/data/kiterunner/routes-large.kite
		  
		  ![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/nXzTsPZ8R6C79ghxe2DO_ActiveDiscovery10.PNG)
		  
		   As you can see, Kiterunner will provide you with a list of 
		  interesting paths. The fact that the server is responding uniquely to 
		  requests to certain /api/ paths indicates that the API exists.
		  
		  Note that we conducted this scan without any authorization headers, 
		  which the target API likely requires. I will demonstrate how to use 
		  Kiterunner with authorization headers in Chapter 7.
		  
		  If you want to use a text wordlist rather than a .kite file, use the brute option with the text file of your choice:
		  
		  $ kr brute <target> -w ~/api/wordlists/data/automated/nameofwordlist.txt
		  
		  If you have many targets, you can save a list of line-separated 
		  targets as a text file and use that file as the target. You can use any 
		  of the following line-separated URI formats as input:
		  
		  Test.com
		  
		  Test2.com:443
		  
		  http://test3.com
		  
		  http://test4.com
		  
		  http://test5.com:8888/api
		  
		  One of the coolest Kiterunner features is the ability to replay 
		  requests. Thus, not only will you have an interesting result to 
		  investigate, you will also be able to dissect exactly why that request 
		  is interesting. In order to replay a request, copy the entire line of 
		  content into Kiterunner, paste it using the kb replay option, and include the wordlist you used:
		  
		  $ kr kb replay "GET     414 [    183,    7,   8]
		  
		  ://192.168.50.35:8888/api/privatisations/count 0cf6841b1e7ac8badc6e237ab300a90ca873d571" -w
		  
		  ~/api/wordlists/data/kiterunner/routes-large.kite
		  
		  Running this will replay the request and provide you with the HTTP 
		  response. You can then review the contents to see if there is anything 
		  worthy of investigation. I normally review interesting results and then 
		  pivot to testing them using Postman and Burp Suite.
	- ## **DevTools** #DevTools
	  collapsed:: true
		- DevTools contains some highly underrated web application hacking 
		  tools. The following steps will help you easily and systematically 
		  filter through thousands of lines of code in order to find sensitive 
		  information in page sources. Begin by opening your target page, and then
		   open DevTools with F12 or ctr-shift-I.
		   Adjust the DevTools window until you have enough space to work with. 
		  Select the Network tab and then refresh the page (CTRL+r).
		  
		  ![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/KAIntko1RBud1q6MVwBQ_ActiveDiscovery5.PNG)
		  
		  You can use the filter tool to search for any term you would like, 
		  such as "API", "v1", or "graphql". This is a quick way to find API 
		  endpoints in use. You can also leave the Devtools Network tab open while
		   you perform actions on the web page. For example, let's check out what 
		  happens if we leave the DevTools open while we authenticate to crAPI. 
		  You should see a new request pop up. At this point, you can dive deeper 
		  into the request by right-clicking on one of the requests and selecting 
		  "Edit and Resend".
		  
		  ![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/JHIANpvkSDONA1eM3T0S_ActiveDiscovery7.PNG)
		  
		  This will allow you to check out the request in the browser, edit the
		   headers/request body, and send it back to the API provider. Although 
		  this is a great DevTools feature, you may want to move into a browser 
		  that was meant for interacting with APIs. You can use DevTools to 
		  migrate individual requests over to Postman using cURL.
		  
		  ![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/dKkYPAvmRTM4i4y825GQ_ActiveDiscovery7-5.PNG)
		  
		  Once you have copied the desired request, open Postman. Select Import
		   and click on the "Raw text" tab. Paste in the cURL request and select 
		  import.
		  
		  ![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/NPybx1iQaeK63RN9bsTz_ActiveDiscovery8.PNG)
		  
		   Once the request has been imported it will have all of the necessary
		   headers and the request body necessary to make additional requests in 
		  Postman. This is a great way to quickly interact with an API and 
		  interact with a single API request. To automatically build out a more 
		  complete Postman Collection check out the next module which is on 
		  Reverse Engineering an API.
		  
		  Reconnaissance is extremely important when testing APIs. Discovering 
		  API endpoints is a necessary first step when attacking APIs. Good recon 
		  also has the added benefit of potentially providing you with the keys to
		   the castle in the form of API keys, passwords, tokens, and other useful
		   information disclosures.