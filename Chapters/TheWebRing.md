[Return](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/README.md) | [The Tolkien Ring](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Chapters/TheTolkienRing.md) | [The Elfen Ring](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Chapters/TheElfenRing.md) | [The Web Ring](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Chapters/TheWebRing.md) | [The Cloud Ring](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Chapters/TheCloudRing.md) | [The Burning Ring of Fire](#suricata) | [Kringlecon](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Chapters/Kringlecon.md)

<h1 id="top">The Web Ring</h1>

#### Table of Contents

- [Boria Artifacts](#boria)
- [Boria Mine Door](#mine)
- [Glamtariel's Fountain](#fountain)

<h3 id="boria">Boria Artifacts</h3>

#### Naughty IP:

Use the artifacts from Alabaster Snowball to analyze this attack on the Boria mines. Most of the traffic to this site is nice, but one IP address is being naughty! Which is it? After doing some digging around, I was able to find a strange IP address that was acting very suspicious. This IP address stuck out more than other IP addresses. The IP address that was standing out more than others was `18.222.86.32`.

![image1](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image1.png "WireShark Packet Capture")

![image2](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image2.jpg "FIN, PSH, ACK")

This was showing a FIN flag on a couple HTTP packets. This IP has been stock in the log in page trying to log in more than once. This shows that the IP was brute forcing their way into the webpage.

![image3](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image3.jpg "18.222.86.32 Traffic with /login.html")

The best login here would be the `18.222.86.32 --[05/OCT/2022 16:46:41] "POST /login.html HTTP/1.1" 302 -`. Once that he has a good log in, he starts to use a web crawler. Looking into the directories related to the website.

#### Credential Mining:

The first attack is a brute force login. What is the first username tried? The first username tried would be username Alice as you see below.

![image4](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image4.jpg "First username found: username=alice")

#### 404 FTW:

The next attack is forced browsing where the naughty one is guessing URLS. What is the first successful URL path in this attack? The first URL path that I found would be `/proc`.

![image5](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image5.jpg "URL path: 'GET /proc HTTP/1.1'")

#### IMDS, XXE, and Other Abbreviations:

The last step in this attack was the use of XXE to get secret keys from the IMDS service. What URL did the attacker force the server to fetch? The last URL the attacker was able to force the server to fetch was `http://169.254.169.254/latest/meta-data/identity-credentials/ec2/security-credentials/ec2-instance`. Also, with this HTTP Follow we can see that he was able to obtain the Secret Access Key Hash and Token Hash as seen below.

![image6](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image6.jpg "Secret Access Key | Token")

<h3 id="mine">Boria Mine Door</h3>

With the locked door code, I was able to unlock the first frame of the lock. Which is found in the source code of the website. This information was under `<div class="iframes">` `/pin1`. From here you can find the rest of the locked pins that coincide with each other. 

![image7](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image7.jpg "DevTools | Website Source Code")

First lock was unlocked using the dev notes within the source code. I was able to see what the developer left behind in his comments tag `<!-- -->`. The first lock used `@&@&&W&&W&&&&`.

![image8](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image8.jpg "PIN1 Unlocked using Dev notes")

For PIN2 I was able to use <SVG> Scalable Vector Graphic. The second PIN I was able to input this SVG.

![image9](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image9.jpg "<svg> script")

With this script PIN2 was able to unlock.

![image10](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image10.jpg "PIN 2 Unlocked using <SVG> square")

For PIN3 I was able to figure out that there was an error with a <!DOCTYPE html> when inputting just <SVG> code. So, I enclosed the <SVG> within the <html> and <body> to if that will take the script within the input of the PIN. The script used was:

![image11](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image11.jpg "<svg> script first attempt")

![image12](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image12.jpg "<!DOCTYPE html> Error in DevTools | Dev Notes Filter out JavaScript from user input")

![image13](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image13.jpg "<svg> script second attempt")

After inputting that information into the input, I was able to unlock PIN3.

![image14](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image14.jpg "PIN3 Unlocked using <SVG> Circle with Enclosed <!DOCTYPE html>")

Next is PIN4 here I was able to use another svg script in order to unlock the pin. The svg script used is:

![image15](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image15.jpg "<svg> imbeded into a <html> header and <body>")

![image16](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image16.jpg "PIN4 Unlocked using <SVG> two rectangles with Enclosed <!DOCTYPE html>")

For PIN5 I would have to insert `/</</` first in order to submit any code after. This is because of the input.value = content within the script of the PIN. For example `.replace(/"/gi, ' ')` would take any character with the " and will be removed from the input. With html it uses a lot of ", <, >, and ' characters. Any character that has those will be stripped from the input. I was able to break the input using a bunch of `/</</` first then input my code after. The svg code used is:

![image17](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image17.jpg "Websource <script> for PIN4")

![image18](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image18.jpg "<svg> script using polygons")

![image19](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image19.jpg "PIN5 Unlocked | Bypassing special characters and <SVG> polygons")

For PIN6 I was able to manipulate the svg script to match to corresponding colored pins on either side. The only way I was able to do this was to tweet the polygon integers to match the pins on either side. This is the script that was used on the input.

![image20](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image20.jpg "<svg> script using polygons")

![image21](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image21.jpg "PIN6 Unlocked | Using <SVG> Polygons")

<h3 id="fountain">Glamtariel's Fountain</h3>

![image22](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image22.jpg "Glamtariel's Fountain webAPP")

While looking at the source code of the website, I noticed something different about this line of code.

![image23](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image23.jpg "<div class=visit> has a draggable='false' that was changed to draggable='true'")

![image24](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image24.jpg "Draggable Icons")

![image25](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image25.jpg "Changed the draggable='false' to draggable='true'")

Once you change the draggable from false to true you are able to drag the little characters on the top right-hand corner on to the Princess or Fountain. With each one responding about each item. When dragging the icons on the Fountain or Princess you received some POST requests to .png files. For example, `2022_glamtariel_2022.png`, `2022_icefountain_2022.png`, `stage2ring-eyecu_2022.png` and `grinchum-supersecret_9364274`. The `grinchum-supersecret_9364274` would only pop up with you messed with any of the cookies of the Requests. I moved back and forth between Burp Suite and DevTools to solve this puzzle. After reading all the dialog and moving the icons between the two characters I was able to figure out the keywords.

> Keywords that pop-up: PATH, APP, TAMPER, RINGLIST, TYPE, SIMPLE FORMAT
>
> TAMPER - Content-Type:
>
> [<PATH "APP/TYPE/SIMPLE FORMAT/RINGLIST">]

I was able to come up with a XML snippet from OWASP XML Injections. I also had to convert one of the GET responses from JSON to XML in order to respond to either character.

![image26](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image26.jpg "Test XXE Injection")

After posting a GET request, I would get this response back.

![image27](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image27.jpg "Response back | 'I love rings of all colors!'")

Now that we know that the XXE Injection works we can work on figuring out what to input for the GET request. First, we would need to change the `Content-Type: application/json to Content-Type: application/xml`. If we change anything else in this header, will we get a response back about modifying cookies and would need to reset the webapp. The season will expire and will need to do it all over again. 

![image28](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image28.jpg "POST header: Content-Type changed from application/json to application/xml")

Once that was changed, we would need to update the file path for the XML Injection. The file path would be `app/static/images/ringlist.txt`. The xml script would look like this.

![image29](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image29.jpg "OWASP XML Injection Script | RINGLIST")

After posting the GET request with the added xml script we would get a response like this.

![image30](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image30.jpg "Response 'You found my ring list!' with a visit:static/images/pholder-morethantopsupersecret63842.png")

With this information we can take that URL directory and see what can be obtained from it. So, we will add this to the URL `http://glamtarielsfountain.com/static/images/pholder-morethantopsupersecret63842.png`. We should get an image once we put this in.

![image31](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image31.png "An image of the directory and two files | bluering.txt & redring.txt")

Now that we have the information we need, we can modify the xml code to match the file path and see what we get back. This is what was modified in the xml code.

![image32](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image32.jpg "OWASP XML Injection | redring.txt")

Now we send another GET request and see what information is sent back to us.

![image33](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image33.jpg "Response back from XML GET request | redring.txt")

That was a dead end, so let's move to the bluering.txt and see what we get back. This is the modified code.

![image34](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image34.jpg "OWASP XML Injection | bluering.txt")

Now let's do a GET request and see what we can get with the blue ring.

![image35](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image35.jpg "Response back from the XML GET request | bluering.txt")

After some dead end's I thought to myself maybe I should try other colors rings and see what I can get back in response. The only rings I can think of was the silver ring and maybe a green ring. I do remember some of the Princess's responses talking about silver rings are her favorite. This is the xml's modified code.

![image36](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image36.jpg "OWASP XML Injection | silverring.txt")

After posting a GET request, I was able to get a response back about the silver ring.

![image37](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image37.jpg "Response back from the XML GET request | silverring.txt | redring-supersupersecret928164.png")

From this response I was able to get another file path to add to the URL `http://glamtarielsfountain.com/static/images/x_phial_pholder_2022/redring-supersupersecret928164.png`. This is the file that I got back.

![image38](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image38.png "Red Ring with a directory | goldring_to_be_deleted.txt")

This was interesting to find an image with a file directory to check out. We will need to add the file path to the xml code. But before I go any further, I wanted to check out if there was any greenring.txt. Here is the modified XML code.

![image39](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image39.jpg "OWASP XML Injection | greenring.txt")

After post a GET request, this is what response we got back.

![image40](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image40.jpg "Response back from the XML GET request | greenring.txt | tomb2022-tommyeasteregg3847516894.png")

From this response I was able to get another file path to add to the URL `http://glamtarielsfountain.com/static/images/x_phial_pholder_2022/tomb2022-tommyeasteregg3847516894.png`. This is what we got back.

![image41](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image41.jpg "tomb2022-tommyeasteregg3847516894.png")

OH, look at that I got myself a little easter egg rhyme.

Ok, back to the `goldenring_to_be_deleted.txt` and see what response we will get back from this. The modified xml code.

![image42](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image42.jpg "OWASP XML Injection | goldenring_to_be_deleted.txt")

After posting the GET request this is what was sent back in response.

![image43](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image43.jpg "Response stating bold REQest and secret TYPE of tongue")

Here we see that we would have to change to REQ to a different TYPE. The only thing I can think of would be moving the `&xxe;` from imgDROP to reqTYPE and see if it will help with changing the GET request. Also, I would need to add a proper imgDROP from the old JSON post request, so it knows what I am looking for which is the silver ring. The modified XML code.

![image44](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image44.jpg "OWASP XML Injection | goldenring_to_be_deleted.txt")

After posting the GET request this is what was sent back in response.

![image45](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image45.jpg "Response back from the XML GET request | goldring-morethansupertopsecret76394734.png")

From here I would need to add this file path to the URL `http://glamtarielsfountain.com/static/images/x_phial_pholder_2022/goldring-morethansupertopsecret76394734.png` and see what we get back.

![image46](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheWebRingImages/image46.png "The prized Golden Ring")

I have finally discovered to prized Golden Ring! I stare into Glamariel's fountain and was presented a file name `goldring-morethansupertopsecret76394734.png`.

[Top](#top)
