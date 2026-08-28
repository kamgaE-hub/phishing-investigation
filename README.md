<h1>Cloudora - Simulated Phishing Campaign Investigation </h1>

<h2>Description</h2>
I completed a hands-on simulated SOC investigation into a targeted phishing campaign against Cloudora, a fictional organisation based in the UK.
The investigation started with a reported suspicious payroll/HR-themed email and progressed through email analysis, header investigation, threat intelligence enrichment, campaign scoping and authentication-log analysis.
<br />

<h2>Tools</h2>

- <b>Microsoft data explorer</b> 
- <b>KQL</b>
- <b>Visual studio</b>
- <b>Authentication Logs</b>

<h2>Environments Used </h2>

- <b>Windows 10</b>

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

<h3>Identify users who received and interacted with the phishing email:</h3>

I used KQL to identify users who clicked the phishing link and then checked whether the phishing email was successfully delivered to those users.
30 users received and clicked the phishing email. I used this list as the starting point for the next stage of the investigation.

<img src="https://github.com/kamgaE-hub/phishing-investigation/blob/main/evidence/Who%20Interacted%20with%20the%20phishing%20email.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

*Figure 3 – Those who interacted with the phishing email*

<h3>Phishing Link and Credentials Submission:</h3>

I checked the click activity from the phishing emails to see which users followed the links and whether they submitted their credentials.

The results showed six users who clicked the phishing links. Two of them — Ryan Boyd and Freya Lynn — also submitted their credentials. The results also showed that the emails came from two different phishing variants and used different URLs.

<img src="https://github.com/kamgaE-hub/phishing-investigation/blob/main/evidence/Phishing-Link-credential-submission.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

*Figure 4 - KQL results showing users who clicked the phishing links and whether credentials were submitted*

<h3> Credential Submission - Sign-In Investigation:</h3>

I used KQL to find the users who submitted their credentials through the phishing emails and then checked their successful sign-ins.

The results showed activity for Freya Lynn and Ryan Boyd from 198.18.7.200 in Amsterdam, Netherlands. I also found sign-ins from other locations and devices for comparison.

This helped me identify the sign-ins that needed further investigation.

<img src="https://github.com/kamgaE-hub/phishing-investigation/blob/main/evidence/Credentials%20%26%20Sig-In%20Investigation.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

*Figure 5 – KQL results showing successful sign-ins for users who submitted their credentials*

<h3> Sign-In Investigation:</h3>

I used KQL to look for successful sign-ins from the IP range associated with the suspicious activity. The results showed sign-ins for two Cloudora users from the Netherlands.

I reviewed the users, IP address, location, time of activity and applications used. This gave me information to compare with the users' normal sign-in activity and investigate whether the accounts had been accessed using stolen credentials.

<img src="https://github.com/kamgaE-hub/phishing-investigation/blob/main/evidence/Suspicious-sign-in-investigation.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

*Figure 6 – KQL results showing successful sign-ins from suspicious IP range*

<h3> Account Sign-In Ivestigation - Ryan Boyd:</h3>

After identifying Ryan Boyd as one of the users who submitted credentials through the phishing email, I went ahead to review his sign-in activity.

Ryan's normal activity was from London, UK, using an iOS device and Safari. Shortly after the phishing interaction, his account was successfully accessed from 198.18.7.200 in Amsterdam, Netherlands, using Windows 11 and Chrome.

The Amsterdam sign-ins were inconsistent with the user's normal activity and occurred after his credentials had been submitted to the phishing page. I therefore identified the Amsterdam activity as malicious sign-in activity resulting from the phishing attack.

<img src="https://github.com/kamgaE-hub/phishing-investigation/blob/main/evidence/Boyd-sign-in-investigation.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

*Figure 7 – Ryan Boyd's sign-in activity showing the suspicious Amsterdam sessions between London activity*

<h3> Account Sign-In Ivestigation - Freya Lynn:</h3>

After identifying Freya Lynn as another user who submitted credentials through the phishing page, I reviewed her sign-in activity.

Freya's normal activity was from Manchester, UK, using an iOS device and Mobile Safari. Her account was then successfully accessed three times from 198.18.7.200 in Amsterdam, Netherlands, using Windows 11 and Chrome.

The Amsterdam activity was inconsistent with her normal sign-in pattern and occurred in the same period as the phishing activity. Based on the credential submission, timing, IP address, location and change in device, I identified these Amsterdam sign-ins as malicious activity resulting from the phishing attack. 

<img src="https://github.com/kamgaE-hub/phishing-investigation/blob/main/evidence/Freya-sign-in-investigation.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

*Figure 8 – Freya Lynn sign-in activity showing the suspicious Amsterdam sessions between London activity*

<h2>Overall Findings:</h2>

The investigation confirmed a phishing campaign targeting Cloudora users.

1. **2 accounts were confirmed compromised:** Both Freya.lynn and Ryan.Boyd clicked and submitted credentials to the phishing page, which later showed suspicious sign-ins from the same Amsterdam IP (198.18.7.200) on Windows 11/Chrome device never seen on their account.

2. **4 users clicked but were not confirmed compromised:** seth.lane, chloe.price, hugo.marsh and dina.said clicked the phishing link, but no credentials were submitted and no suspicious sign-ins were found. Precautionary follow-up was recommended.

3. Thirty delivered-to recipients did not click and form the near-miss list for user communications.  A further four
(emma.hayes, maya.chen, nina.cole, ruth.dean) were targeted but had every copy quarantined by Exchange
Online Protection, so never saw the message.

Overall, the investigation identified 2 confirmed compromises, 4 exposed users requiring follow-up, and no evidence of compromise among the remaining targeted users. 

<h2> Recommended Actions To Take:</h2>

1. Revoked all active sessions and refresh tokens for freya.lynn and ryan.boyd
3. Reset credentials for both compromised accounts and the 4 exposed accounts
4. Required and re-registered MFA on all accounts
5. Blocked infrastructure: 198.18.44.10, 198.18.44.23,198.18.51.7, 198.18.7.200 and cloudora-hr-portal.example (all        subdomains) at mail gateway and web proxy
6. Carry out awareness sessions with the team. 

