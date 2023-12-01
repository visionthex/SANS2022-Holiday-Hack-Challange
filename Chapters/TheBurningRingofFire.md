[Return](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/README.md) | [The Tolkien Ring](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Chapters/TheTolkienRing.md) | [The Elfen Ring](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Chapters/TheElfenRing.md) | [The Web Ring](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Chapters/TheWebRing.md) | [The Cloud Ring](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Chapters/TheCloudRing.md) | [The Burning Ring of Fire](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Chapters/TheBurningRingofFire.md) | [Kringlecon](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Chapters/Kringlecon.md)

<h1 id="top">The Burning Ring of Fire</h1>

#### Table of Contents

- [Buy a Hat](#hat)
- [Blockchain Divination](#blockchain)
- [Exploit a Smart Contract](#smart)

<h3 id="hat">Buy a Hat</h3>

Travel to the Burning Ring of Fire and purchase a hat from the vending machine with KringleCoin.

![image1](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheBurningRingofFireImages/image1.jpg "Burning Ring of FIre KringleCoin Token Machine")

From the KringleCoin Teller Machine the first step would be to check your wallet balance. From here you would put your wallet address which starts with 0xD. As of right now mine shows this.

![image2](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheBurningRingofFireImages/image2.jpg "Total KrngleCoin")

Then go back to the main screen and go to approve a KringleCoin transfer. But to do that you will need to pick out a hat from the vender and find out the price and the address to send the KringleCoin too. So, now we go to the Wombley Cube's Hat Vending Machine.

![image3](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheBurningRingofFireImages/image3.jpg "Hat Vending Machine")

From here you will pick out a hat which is a cowboy hat. We get the price in KC and the wallet address to purchase this hat.

![image4](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheBurningRingofFireImages/image4.jpg "The Hats Wallet Address, KC Cost, and ID#")

From here we go back to the KTM and purchase ourselves a hat. We go to approve a KringleCoin transfer. We add the "To" address the KC amount and your Wallets key hash.

> "To" Address: 0xa <----The Hats Wallet Address
> 
> Amount (KC): 10 <----The KringleCoin cost amount
> 
> Your Key: 0xf <----Your Wallets Key Hash

Then after we go back to the Hat Vending Machine and click on the Click here to buy. You would need to add your Wallet Address and Hat ID then Click on Make your purchase!

> Your Wallet Address: 0xD <----Your Wallets Address Hash
> 
> Hat ID:86 <----The Hats ID Number

After the purchase goes through you will receive a Transaction ID for the Hat. 0x7 with a `Block# 61032` and can be viewed at the Blockchain Explorer. Once that is done you can access your hat and wear it just like me.

![image5](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheBurningRingofFireImages/image5.jpg "KringleCon Character with a Crypto Bought Hat")

![image6](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheBurningRingofFireImages/image6.jpg "Block# 61032")

<h3 id="blockchain">Blockchain Divination</h3>

Use the Blockchain Explorer in the Burning Ring of Fire to investigate the contracts and transactions on the chain. At what address is the KringleCoin smart contract deployed? This will be Block# 4

> Wallet: 0x8B86BB82b4b0a7C085d64B86aF6B6d99150f92a1
> 
> KringleCoin Contract Address: 0xc27A2D3DE339Ce353c0eFBa32e948a88F1C86554

![image7](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheBurningRingofFireImages/image7.jpg "Block# 4")

<h3 id="smart">Exploit a Smart Contract</h3>

Exploit flaws in a smart contract to buy yourself a Bored Sporc NFT. Resources used for [Merkel Tree](https://github.com/QPetabyte/Merkle_Trees/tree/4cd2896c273ff4836126d8fd39de4b2fd3028bb0).

![image8](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheBurningRingofFireImages/image8.jpg "BoredSporc Gallery")

> BoredSporc Addresses
> 
> BSRS_nft Contract Address: 0x36A3d1182Cf6C15D93E47EF3E27272BFA0E8612A
> 
> RSRS_nft Wallet: 0xe8fC6f6a76BE243122E3d01A1c544F87f1264d3a

Find Proof Values: In order to find proof values, I started to look into the source code of the Bored Sporc website.

![image9](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheBurningRingofFireImages/image9.jpg "Looking at Bored Sporc Website using DevTools")

After some digging, I was able to get a closer look the traffic using the Network tab in DevTools. Interacting with the website and see what populates on the network side. After clicking around I noticed something from a GET request by clicking on the go button on the website.

![image10](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheBurningRingofFireImages/image10.jpg "POST request returned from a GET request from the Go button on the verification page")

With this information I could do a POST request by editing the Proof and Root Hashes. From here I would be able to send whatever information that is getting to get the right POST request. First, I will need to figure out how to set up a Merkel Tree to generate a Proof value. I went to the Ubuntu page and downloaded an Ubuntu Server ISO. Once that was downloaded, I was able to set up a Virtual Machine and, in the Server settings enable Docker Containers. Once that was all said and done, I would need to set up the Docker Container. I was able to find an Ubuntu Server ISO and ran it on my Virtual Machine. I was able to configure the server to run Docker and be able to create a Docker Container for the Merkel Tree. The commands used was `docker build -t merkletrees .` then use the command `docker run -it –rm –name=merkletrees merkletrees`. Once the container was built, I was able to access the directory and python script. The command used to access the merkle_tree.py was `nano merkle_tree.py`. The only line of code that I would need to modify would be the `allowlist = ['My Wallets Address Hash' , 'Left as Default']`.

![image11](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheBurningRingofFireImages/image11.jpg "Merkel_tree.py Script")

Once I was able to modify the one line of code with my Wallet Address Hash the next this would be to save the script and run it. The command used to run the script is `python merkle_tree.py`. The python script was able to provide me with the Root and Proof that I need to send a POST request to the website. Now that we know 

> Root : 0x19ec6a4d480aa86cd7392c6ca10909a4e262822ff997f9aac0c81f287cc4ca52
> 
> Proof : 0x5380c7b7ae81a58eb98d9c78de4a1fd7fd9535fc953ed2be602daaa41767312a

we can take this information and plug it into the POST request with my Wallet ID Hash within the JSON script.

![image12](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheBurningRingofFireImages/image12.jpg "POST request Modified")

![image13](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheBurningRingofFireImages/image13.jpg "Information the was plug in to run the POST Request")

After sending the POST request with the new added information it would return with a 302 POST Request stating everything went well with the request. The response that came back stated that I am still a SPORC. From here I would need to go back to the KTM and submit my `Approved KringleCoin Transfer`. I would need to submit the BSRS Wallet address the amount of the NFT costs with my Wallet Key Hash. Then submit my approved Transfer. Next, I will need to go back to the BSRS website but this time I would do the same steps again but with a `Validate="False"`. Once that is submitted, I would get a request stating I own an NFT. Next, would be to dig through the Gallery on the website to find your NFT.

![image14](https://github.com/visionthex/SANS2022-Holiday-Hack-Challange/blob/main/Images/TheBurningRingofFireImages/image14.jpg "BSRS #000224")

Now I own an NFT to show to others and brag about how much my NFT is going to go to the __MOON!__

[Top](#top)
