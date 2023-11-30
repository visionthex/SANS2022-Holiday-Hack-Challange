[Return](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/SANSHHC.md)

# The Tolkien Ring

#### Table of Contents

- [Wireshark Phishing](#Wireshark)
- [Windows Event Logs](#indent)
- [Suricata Regatta](#center)

## Wireshark Phishing  {#Wireshark}

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
