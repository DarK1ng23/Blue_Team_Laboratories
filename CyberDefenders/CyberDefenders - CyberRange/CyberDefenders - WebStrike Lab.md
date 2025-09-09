# [CyberDefenders - WebStrike Lab](https://cyberdefenders.org/blueteam-ctf-challenges/webstrike/)
Created: 08/09/2025 06:00 pm
Last Updated: 08/09/2024 06:00 pm
* * *
>**Category**: Network Forensics
>**Tags**: Wireshark, PCAP, Exfiltration
* * *
**Scenario**: An anomaly was discovered within our company's intranet as our Development team found an unusual file on one of our web servers. Suspecting potential malicious activity, the network team has prepared a pcap file with critical network traffic for analysis for the security team, and you have been tasked with analyzing the pcap.

**Tools**: Wireshark
* * *
## Questions
> Q1: Understanding the geographical origin of the attack aids in geo-blocking measures and threat intelligence analysis. What city did the attack originate from?

![WebStrikeLab1.png](../../_resources/CyberDefenders/WebStrikeLab1.png)
![WebStrikeLab2.png](../../resources/CyberDefenders/WebStrikeLab2.png)
After taking a look at pcap file, There are only 2 IP addresses were captured.
Which `117.11.88.124` is probably the client (attacker) and `24.49.63.79` is a web server
![WebStrikeLab3.png](../../_resources/CyberDefenders/WebStrikeLab3.png)
![WebStrikeLab4.png](../../_resources/CyberDefenders/WebStrikeLab4.png)
I used [iplocation](https://www.iplocation.net/ip-lookup) to find both of IP addresses, attack was from the China and the web server was on the US so the answer is
<details>
  <summary>Answer</summary>
<pre><code>Tianjin</code></pre>
</details>

> Q2: Knowing the attacker's user-agent assists in creating robust filtering rules. What's the attacker's user agent?

![WebStrikeLab5.png](../../_resources/CyberDefenders/WebStrikeLab5.png)
Follow HTTP or TCP stream of HTTP traffic, here is the user-agent of the attacker

<details>
  <summary>Answer</summary>
<pre><code>Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0</code></pre>
</details>

> Q3: We need to identify if there were potential vulnerabilities exploited. What's the name of the malicious web shell uploaded?

![WebStrikeLab6.png](../../_resources/CyberDefenders/WebStrikeLab6.png)
After browsing the website, the attacker found the upload page and used POST method to upload php reverse shell to the server which was a successful attempt.

<details>
  <summary>Answer</summary>
<pre><code>image.jpg.php</code></pre>
</details>

> Q4: Knowing the directory where files uploaded are stored is important for reinforcing defenses against unauthorized access. Which directory is used by the website to store the uploaded files?

![WebStrikeLab7.png](../../_resources/CyberDefenders/WebStrikeLab7.png)
The php reverse shell was uploaded to this directory as a link

<details>
  <summary>Answer</summary>
<pre><code>/reviews/uploads/</code></pre>
</details>

> Q5: Identifying the port utilized by the web shell helps improve firewall configurations for blocking unauthorized outbound traffic. What port was used by the malicious web shell?

Look at the content of php reverse shell, The port that was used is

<details>
  <summary>Answer</summary>
<pre><code>8080</code></pre>
</details>

![WebStrikeLab8.png](../../_resources/CyberDefenders/WebStrikeLab8.png)
Which the attacker successfully gained the reverse shell from the server.

> Q6: Understanding the value of compromised data assists in prioritizing incident response actions. What file was the attacker trying to exfiltrate?

![WebStrikeLab9.png](../../_resources/CyberDefenders/WebStrikeLab9.png)
<details>
  <summary>Answer</summary>
<pre><code>passwd</code></pre>
</details>

* * *
