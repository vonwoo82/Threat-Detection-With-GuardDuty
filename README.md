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

<img width="570" height="599" alt="aws-security-guardduty_t3u4v5w6" src="https://github.com/user-attachments/assets/38008b85-9125-44fc-91a6-bfb66336ca40" />


Attack Verification

To verify the attack's success, we visited the publicly exposed credentials file (i.e credentials.json). This page showed us access keys that can represent our EC2 instances's access to the developers AWS environments.  We can use those keys to get the same level of access


Using CloudShell for Advanced Attacks

The attack continues in CloudShell, because this is a Command-line  tool we can use to run AWS commands that uses the credentials I've stolen. CloudShell is now our medium for doing suspicious things like stealing data from an S3 Bucket. 

In CloudShell, I used wget to download the exposed credentials file into our CloudShell environment. Next, we ran a command using cat and jq to read the downloaded file and format it nicely so the credentials (in JSON) are easy to understand. 

I then set up a new profile using all of the stolen credentials. I had to create a new profile because the hacker doesn't inherently have access to the victim's AWS environment. They'll need to use the profile to switch permission settings. 

<img width="1406" height="254" alt="aws-security-guardduty_j9k0l1m2" src="https://github.com/user-attachments/assets/69ec16f9-3e9f-47ef-9923-1606c31e359d" />

GuardDuty's Findings

After performing the attack, GuardDuty reported the finding within 15 minutes. Findings are notifications from GuardDuty that something suspicious has happened, and they give you additional details about the who/what/when of the attack. 

GuardDuty's finding was called UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration.InsideAWS, which means credentials belonging to an EC2 instance  were being used in another account. Anomaly detection was used because this was unusual behavior. 

GuardDuty's detailed finding reported that an S3 bucket was affected; the action that was done using the stolen credentials (GetObject); and the EC2 instance whose credentials were leaked. The IP address + location of the actor was also available. 

<img width="831" height="638" alt="aws-security-guardduty_v1w2x3y4" src="https://github.com/user-attachments/assets/b336bec1-c9ea-4c21-86a0-20d766be2141" />

Malware Protection

For the project extentions, I enabled Malware protection for S3. Malware is file that contains threat e.g. opening the file will cause a data breach or deletion of resources. 

To test Malware Protection, I've uploaded and EICAR test file into a protected bucket. The uploaded file won't actually cause damage because the test file is only designed to alert antivirus software. 

Once we uploaded the malware, GuardDuty instantly triggered a finding called Object:S3/MaliciousFile. This verified that GuardDuty could successfully detect malware. It also mentioned that the threat type is EICAR-Test-File (Which means its not a virus). 

<img width="776" height="878" alt="aws-security-guardduty_sm42x3y4" src="https://github.com/user-attachments/assets/a532c4e3-78e2-496d-a25b-e54ae4fbea99" />

