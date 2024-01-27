<h1>LLMNR Poisoning</h1>

 <h2>Description</h2>
Project consists of performing a LLMNR poisoning attack, a type of man-in-the-middle technique used to obtain password hashes, on a vulnerable Windows home lab.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Responder</b> 
- <b>Hashcat</b>

<h2>Environments Used </h2>

- <b>Kali Linux</b>

<h2>Project walk-through:</h2>

<p align="center">
LLMNR Poisoning 
<br />
<br />
We are going to use a tool called Responder to attempt to capture these hashes on our lab network. Run the following commands to start the tool. Change out eth0 with your interface name if different: <br />
<img src="https://i.imgur.com/fj3ppH9.png" height="80%" width="80%" alt="LLMNRpoison"/>
<br />
<br />
Responder will begin to listen for events on the network generating traffic. Once it intercepts some traffic it will respond back with poisoned info and capture the hashes.  <br/>
<img src="https://i.imgur.com/FVC6BK7.png" height="60%" width="60%" alt="LLMNRpoison"/>
<br />
<br />
We can now take those hashes, save them to a text file and send them to a cracking tool to perform further attacks. <br />
To crack the password hash we obtained from responder we are going to use the tool hashcat. Since this is a NTLMv2 hash we will set are module in hashcat to 5600, set our hash file and then a wordlist to use to crack the hash file.  <br/>
<img src="https://i.imgur.com/Sk7Sz06.png" height="80%" width="80%" alt="LLMNRpoison"/>
<br />
<br />
Hashcat will run and begin the cracking process. If the password is cracked it will display the password in clear text at the end of the hash we provided.  <br/>
<img src="https://i.imgur.com/JBfIHtu.png" height="60%" width="60%" alt="LLMNRpoison"/>
<br />
<br />
We have now obtained authenticated credentials for the pcuser2 account.  <br/>
<br />
<br />
</p>
<p align="left">
Mitigation/Remediation Strategies <br />
1. Create a GPO to Disable LLMNR: Computer Policies > Computer Configuration > Admin Templates > Network > DNS Client > Turn off multicast name resolution. <br />
2. Disable NetBIOS on the local machine: Network connections > Network adapter properties > TCP/IPv4 > Advanced > WINS > Disable NetBIOS over TCP/IP. <br />
3. Having strong password complexity rules in place will also help to mitigate passwords being cracked so easily by an attacker.
<br />
<br />
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
