[Return](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/README.md)

<h1 id="top">The Tolkien Ring</h3>

#### Table of Contents

- [Wireshark Phishing](#wireshark)
- [Windows Event Logs](#windows)
- [Suricata Regatta](#suricata)

<br><br>

<h3 id="wireshark">Wireshark Phishing</h3>

This all started when I clicked on a link in my email. Can you help me? Yes, I would be able to help you with this situation.
<br>
There are objects in the PCAP file that can be exported by Wireshark. What type of object can be exported from this PCAP? You will need to go to `File > Export Object > HTTP`

![image1](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheTolkienRing/image1.jpg "Exported files that can be analyzed further")

What is the file name of the largest file we can export? This would be the 808kB app.php file
<br>
What packet number starts that app.php file? This packet would be #687

![Image2](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheTolkienRing/image2.jpg "Application that was downloaded to host")

What is the IP of the Apache server? Clicking on Packet#687 directed me to the IP address of 192.185.57.242

![Image3](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheTolkienRing/image3.jpg "The IP Address to the Apache Server")

What file is saved to the infected host? When you open the saved app.php in VBCode you will be able to see the file name at the end of the script. This file would be Ref_Sept24-2022.zip

![Image4](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheTolkienRing/image4.jpg "app.php script | File: Ref_Sept.24-2020.zip")

Attackers used bad TLS certificates in the traffic. Which countries where they registered to? To find this answer you would need to do a little digging on how to get the set of TLS certificates which is a handshake with the server. The [SSL/TLS handshake | Packet Analysis with Wireshark](https://subscription.packtpub.com/book/cloud-and-networking/9781785887819/4/ch04lvl1sec27/the-ssl-tls-handshake) and find the server certificate for a Wireshark filter. I used this filter in Wireshark `ssl.handshake.type == 11`

![Image5](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheTolkienRing/image5.jpg "Wireshark Packet Analysis")

After some digging, I was able to find the country code. It was reference under `Transport Layer Security > TLSv1.2 Record Layer: Handshake Protocol > Handshake Protocol: Certificate > Certificate: ASCII Hash > signedCertificate > subject: rdnSequence (0) > rndSequence: > RDNSequence Item: with CounryName = [IE, IL, SS, US]`

To find the Country Codes I referenced the ISO3166 to convert the codes to an actual name of the Country that it references to: [Online Browsing Plateform (OBP) ISO.org](https://www.iso.org/obp/ui/#search) The countries that corresponds to the RDNSequence Country Names: [IE = Ireland, IL = Israel, SS = South Sudan, US = United States]

Is the host infected? This would definitely be a Yes, that the host is infected.

<br><br>

<h3 id="windows">Windows Event Logs</h3>

Grinchum successfully downloaded his keylogger and has gathered the `admin credent[0/0]`. We think he used PowerShell to find the Lembanh recipe and steal our secret ingredient. Luckily, we enabled PowerShell auditing and have exported the Windows PowerShell logs to a flat text file. Please help me analyze this file and answer my questions. Ready to being the epic quest? I am always ready to solve questions that need to be answered.

What month/day/year did the attack take place? This would be around 12/24/2022 where there was a suspicious Remote Execution Command.

![Image6](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheTolkienRing/image6.jpg "Windows Event Logs | Execute a Remote Command | Event ID 4104")

An attacker got a secret from a file. What was the original files' name? The command used to find this was grep recipe `powershell.evtx.log` which returned with the file name `recipe_update.txt`.

![Image7](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheTolkienRing/image7.jpg "Command: grep recipe powershell.evtx.log | recipe_update.txt")

The contents of the previous file where retrieved, changed, and stored to a variable by the attacker. This was done multiple times. Submit the last full PowerShell line that performed only these actions. The command used to search for this was `grep -E "Get-Content|Set-Content" powershell.evtx.log` which inturn gave me this `$foo = Get-Content .\Recipe|% {$_-replace 'honey', 'fish oil'} $foo | Add-Content -Path 'recipe_updated.txt'`.

![Image8](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheTolkienRing/image8.jpg "The returned grep command for Get-Content|Set-Content")

After storing the altered file contents into the variable, the attacker used the variable to run a separate command that wrote the modified data to a file. This was done multiple times. Submit the last full PowerShell line that performed only this action. After doing some more grep commands I was able to find the last performed action. `grep -E "recipe_update|foo" powershell.evtx.log`.

![Image9](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheTolkienRing/image9.jpg "Command: grep -E 'recipe_update | foo' powershell.evtx.log")

The attacker ran the previous command against a file multiple time. What is the name of this file. This file that was run multiple times would be the Recipe.txt file.

![Image10](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheTolkienRing/image10.jpg "File: Recipe.txt")

![Image11](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheTolkienRing/image11.jpg "Deleted Files")

Was the original file deleted? No, it was not deleted, but modified by the attacker.

What is the Event ID of the log that shows the actual command line used to delete the file? This was `[Event 4104]`

What is the secret ingredient? The secret ingredient was Honey before it was modified and turned to Fish Oil.

<br><br>

<h3 id="suricata">Suricata Regatta</h3>

Use your investigative analysis skills and the suspicious.pcap file to help develop Suricata rules for the Elves! There is a breif list of rules started in suricata.rules in your home directory. First off, the STINC (Santa's Team of Intelligent Naughty Catchers) has a lead for us. They have some Dridex indicators of compromise to check out. First, please create a Suricata rule to catch DNS lookups for adv.epostoday.uk. Whenever there is a match, the alert message (msg) should read Known bad DNS lookup, possible Dridex Infection. Good luck, and thanks for helping save the North Pole!

This was the first attempt at creating rules. I was able to create the first alert event while referencing the link provided. [6.1.Rules Format - Suricata 6.0.0 Documentation](https://docs.suricata.io/en/suricata-6.0.0/rules/intro.html).

```Rule 1: alert dns $HOME_NET any -> any any (msg:"Known bad DNS lookup, possible Dridex Infection."; dns_query; content:"adv.epostoday.uk";)```

![Image12](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheTolkienRing/image12.jpg "Command: ./rule_checker against First Rule")

STINC thanks you for you work with the DNS record! In this PCAP, it points to `192.185.57.242`. Develop a Suricata rule that alerts whenever the infected IP address communicates with internal systems over HTTP. When there is a match, the message (msg) should read Investigate suspicious connections, possible Dridex Infection. This is what I was able to come up with for my second rule for HTTP traffic with the referenced IP address.

```Rule 2: alert http 192.185.57.242 any <> any any (msg:"Investigate suspicious connections, possible Dridex Infection."; sid:19; rev:1;)```

![Image13](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheTolkienRing/image13.jpg "Command: ./rule_checker against Second Rule")

We heard that some naughty actors are using TLS certificates with a specific CN. Develop a Suricata rule to match and alert on an SSL certificate for heardbellith.icanwepeh.nagoya. When your rule matches, the message (msg) should read Investigate bad certificates, possible Dridex Infection. For the third rule was able to solve for the TLS certificate.

```Rule 3: alert tls any any -> any any (msg:"Investigate bad certificates, possible Dridex Infection."; tls.subject:"CN=heardbellith.icanwepeh.nagoya"; sid:200012;)```

![Image14](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheTolkienRing/image14.jpg "Command: ./rule_checker against Third Rule")

Ok, one more to rule them all and in the darkness find them. Let's watch for one line from the JavaScript: `let byteCharacters = atob` oh, and that string might be GZIP compressed - I hope that's Ok! Just in case they try this again, please alert on that HTTP data with the message Suspicious JavaScript function, possible Dridex Infection. The fourth one I was having a hard time trying to come up with a good rule. That after doing some more research on how to decompress a file in a rule. I was able to come up with this set rule.

```Rule 4: alert http any any -> any any (msg:"Suspicious JavaScript function, possible Dridex Infection."; http.response_body; content:"let byteCharacters = atob"; sid:10054;)```

[Top](#top)
