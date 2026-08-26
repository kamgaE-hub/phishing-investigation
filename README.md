<h1>Cloudora - Simulated Phishing Campaign Investigation </h1>

<h2>Description</h2>
I completed a hands-on simulated SOC investigation into a targeted phishing campaign against Cloudora, a fictional organisation.
The investigation started with a reported suspicious payroll/HR-themed email and progressed through email analysis, header investigation, threat intelligence enrichment, campaign scoping and authentication-log analysis.
<br />

<h2>Tools</h2>

- <b>Microsoft data explorer</b> 
- <b>KQL</b>
- <b>Visual studio</b>
- <b>Authentication Logs</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)

<h2>Program walk-through:</h2>

<h3> Email investigation:</h3>
I reviewed the email headers of the suspicious messages and compared their authentication results with a genuine Cloudora email.

The comparison showed that the phishing emails used different methods. One failed the email authentication checks, while another passed because it was authenticated using the attacker's lookalike domain. The genuine Cloudora email passed authentication using the real cloudora.io domain.
This helped me confirm that the sender domain and authentication results needed to be checked together when deciding whether an email was legitimate.

<br />
<img src="https://github.com/kamgaE-hub/phishing-investigation/blob/main/email-analysis.png"/>

*Figure 1 – Message trace analysis showing campaign, sender, authentication and delivery results* 
<br />

<h3> Email Delivery & Authentication Analysis:</h3>

After uploading the data into Azure Data Explorer, I used KQL to analyse the message-trace data in order to understand how the phishing campaign was distributed and how the different email variants were handled by the
mail system.
The investigation compared the sender addresses, sender IPs, SPF, DKIM and
DMARC results and delivery actions. 

The results showed differences between
the phishing variants, including messages that were delivered and others
that were quarantined.
The analysis also identified a second campaign variant using a different
sender domain, which required further investigation to determine whether
the message was legitimate or malicious.

<img src="https://github.com/kamgaE-hub/phishing-investigation/blob/main/evidence/email-delivery-authentication.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

*Figure 2 – Message trace analysis showing campaign, sender, authentication and delivery results*

<h3>Phishing Link and Credentials Submissiom:</h3>

I checked the click activity from the phishing emails to see which users followed the links and whether they submitted their credentials.

The results showed six users who clicked the phishing links. Two of them — Ryan Boyd and Freya Lynn — also submitted their credentials. The results also showed that the emails came from two different phishing variants and used different URLs.

<img src="https://github.com/kamgaE-hub/phishing-investigation/blob/main/evidence/Phishing-Link-credential-submission.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

*Figure 3 - KQL results showing users who clicked the phishing links and whether credentials were submitted*

<h3> Credential Submission - Sign-In Investigation:</h3>

I used KQL to find the users who submitted their credentials through the phishing emails and then checked their successful sign-ins.

The results showed activity for Freya Lynn and Ryan Boyd from 198.18.7.200 in Amsterdam, Netherlands. I also found sign-ins from other locations and devices for comparison.

This helped me identify the sign-ins that needed further investigation.

<img src="https://github.com/kamgaE-hub/phishing-investigation/blob/main/evidence/Credentials%20%26%20Sig-In%20Investigation.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

*Figure 4 – KQL results showing successful sign-ins for users who submitted their credentials*

<h3> Sign-In Investigation:</h3>

I used KQL to look for successful sign-ins from the IP range associated with the suspicious activity. The results showed sign-ins for two Cloudora users from the Netherlands.

I reviewed the users, IP address, location, time of activity and applications used. This gave me information to compare with the users' normal sign-in activity and investigate whether the accounts had been accessed using stolen credentials.

<img src="https://github.com/kamgaE-hub/phishing-investigation/blob/main/evidence/Suspicious-sign-in-investigation.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

*Figure 5 – KQL results showing successful sign-ins from suspicious IP range*



Select the disk:  <br/>
<img src="https://i.imgur.com/tcTyMUE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Enter the number of passes: <br/>
<img src="https://i.imgur.com/nCIbXbg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Confirm your selection:  <br/>
<img src="https://i.imgur.com/cdFHBiU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Wait for process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/JL945Ga.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/K71yaM2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Diskpart</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)

<h2>Program walk-through:</h2>

<p align="center">
Launch the utility: <br/>
<img src="https://i.imgur.com/62TgaWL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Select the disk:  <br/>
<img src="https://i.imgur.com/tcTyMUE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Enter the number of passes: <br/>
<img src="https://i.imgur.com/nCIbXbg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Confirm your selection:  <br/>
<img src="https://i.imgur.com/cdFHBiU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Wait for process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/JL945Ga.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/K71yaM2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
