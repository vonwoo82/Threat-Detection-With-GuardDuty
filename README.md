# Threat-Detection-With-GuardDuty
Deployed a CloudFormation template that launches an insecure web app (OWASP Juice Shop). The three main components are the web app infrastructure, an S3 bucket and GuardDuty protecting our environment.

The services used was GuardDuty, Cloudformation, S3, and CloudShell. Key concepts I learned include SQL + command injection, using Linux commands like wget, cat and jq, and malware protection!

To set up for this project, I deployed a CloudFormation template that launches an insecure webb app (OWASP Juice Shop). The three main components are. the web app infrastructure, an S3 bucket and GuardDuty protecting our environment

The web app deployed is called OWASP Juice Shop. To practice GuardDuty skills, I will attack the Juice Shop, and then visit the Guard Duty console to detect and analyze it's findings - does it pick up on our attacks to our web app?

GuardDuty is an AI-powered threat detection service, which means it is designed to help us find security attacks or vulnerabilities that affects our AWS resources/environment. Once it detects something unusual, it's up to us to investigate. 

<img width="1129" height="371" alt="aws-security-guardduty_n1o2p3q4" src="https://github.com/user-attachments/assets/eab0d4fd-b5d8-4089-a07e-89a3032f7000" />
