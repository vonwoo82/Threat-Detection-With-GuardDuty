# Threat-Detection-With-GuardDuty
Deployed a CloudFormation template that launches an insecure web app (OWASP Juice Shop). The three main components are the web app infrastructure, an S3 bucket and GuardDuty protecting our environment.

The services used was GuardDuty, Cloudformation, S3, and CloudShell. Key concepts I learned include SQL + command injection, using Linux commands like wget, cat and jq, and malware protection!

To set up for this project, I deployed a CloudFormation template that launches an insecure webb app (OWASP Juice Shop). The three main components are. the web app infrastructure, an S3 bucket and GuardDuty protecting our environment

The web app deployed is called OWASP Juice Shop. To practice GuardDuty skills, I will attack the Juice Shop, and then visit the Guard Duty console to detect and analyze it's findings - does it pick up on our attacks to our web app?

GuardDuty is an AI-powered threat detection service, which means it is designed to help us find security attacks or vulnerabilities that affects our AWS resources/environment. Once it detects something unusual, it's up to us to investigate. 

<img width="1129" height="371" alt="aws-security-guardduty_n1o2p3q4" src="https://github.com/user-attachments/assets/eab0d4fd-b5d8-4089-a07e-89a3032f7000" />

SQL Injection
The first attack I performed on the web app is SQL injection, which means injecting malicious SQL code that manipulates a result from our web app. SQL injection is a security risk because it can let attackers bypass logins, or delete/edit data. 

My SQL injection attack involved entering the code '' or 1=1;--' into the email field of the web app's login page. This means the login query will always evaluate to true (i.e. our database is manipulated into telling our web app this line exists). 

<img width="1412" height="571" alt="aws-security-guardduty_h1i2j3k4" src="https://github.com/user-attachments/assets/c5c895c9-2974-45c1-bd11-437f81e261da" />

Command Injection
Next, I used command injection, which is a technique that manipulates the web app's web server to run code that has been entered e.g. in a form. The Juice Shop web app is vulnerable to this because it does not sanitize user inputs i.e. does not block scripts. 

To run command injection, I entered JavaScript code in the username field of the web app's admin console.  The script will tell our web server to expose the server's IAM credentials and save them in a publicly accessible JSON file. 
