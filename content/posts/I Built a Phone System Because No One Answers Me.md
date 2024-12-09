---
title: I Built a Phone System Because No One Answers Me
date: 2024-12-09
draft: false
tags:
  - NetworkChuck
  - RaspberryPi
---
!![Image Description](/images/Pasted%20image%2020241209091545.png)


# Yes....I put a phone system in my house

- In this video...I put a phone system in my house and business.
- Why?
- Because no one answers their phones. My wife and daughters all have iphones and apple watches....but seem to never be able to answer their phones. I can NEVER get ahold of someone when I need to!
- As a complete nerd and former phone system engineer....this solution was obvious.....install a phone system and put a phone in every room.


# But....it's not that simple....

- My wife is very artsy and particular about the design of our house and what goes in it. She won't allow just anything to be put on a wall or a side table. These phones had to be old, aesthetic, mid-century....which means I couldn't use a typical SIP phone like I normally would. 
- Also, my kids are obsessed with the old phones they see on the older tv shows and movies. They had to have them.

# So....what phone system? Do we need anything for this?

- For most people, nothing. We're using the 3CX phone system and it's going to be free for up to 10 users, which is more than enough for even a large family like mine. It is also hosted completely free in the cloud forever and you can literally get this setup in minutes.
- FULL DISCLOSURE, this video is sponsored by 3CX. I have worked with them for a long time and collaborated on a video a while back where we installed a phone system on a Raspberry Pi 4. This is no longer supported so I needed to redeploy a phone system anyway, to solve my domestic issues and I really needed a phone system for my business. 

# Do we need any hardware? Phones?

- Physical phones are optional. But they are very fun and I highly recommend them. 
- In the event you do what some physical phones, you'll need 2 things:
	- A phone....duh
	- A device inside your network that can connect your physical phone to the 3CX cloud instance.
		- This can be either a:
			- Raspberry Pi (4/5) running the 3CX SBC (Session Border Controller)
				- Raspberry Pi 4: https://geni.us/mzJF55
				- Raspberry Pi 5: https://geni.us/z0BVIc
			- A *router phone*, a fancier phone that has SBC capabilities baked in.

## Phones? What phones?

- Here are the phones that I purchased and can verify work pretty well.
- Also, here is the official list of supported phones that work with 3CX: https://www.3cx.com/sip-phones/

- Snom D735: https://geni.us/IZmO
	- about $85. A very solid option.
- Fanvil X3SG: https://geni.us/oA1i
	- about $69, very solid as well.
- Yealink T54W (a router phone): https://geni.us/GhUAAy
	- around $150, more expensive because it's pretty and is a router phone.
- Fanvil H2U: https://geni.us/WBGTg
	- compact and weird. Hotel-like, if you wanna go for that aesthetic. $63

### Old Phones (requiring an ATA)

- Sangyn Vintage Phone (red, table top): https://geni.us/AxmFI4
	- $35 and gorgeous. Probably my favorite. Feels solid.
- TelPal Corded wall phone: https://geni.us/JZazPcI
	- $32 and INCREDIBLE. Put this sucker on a wall and you are in the 1970s. Feels very solid. My second favorite, comes in a variety of colors. 

### ATA

- You'll need an ATA (analog telephone adapter) for these old phones. I recommend this one:
	- Grandstream HT801: https://geni.us/TaZ7p


# The SETUP (Phone System Install)

- This setup isn't crazy and is pretty easy to follow in the video. 
- Here is your link to sign up for 3CX: https://www.3cx.com/signup/?source=networkchuck

## Setting up the 3CX SBC on a Raspberry Pi

- The Pis
	- Raspberry Pi 4: https://geni.us/mzJF55
	- Raspberry Pi 5: https://geni.us/z0BVIc
- The documentation: https://www.3cx.com/docs/installing-pbx-raspberry-pi/


# Setting up a SIP Trunk ( a real phone number)

- To get a **REAL** phone number to call the outside world and vice-versa, you'll need to setup an account with a SIP provider and setup a SIP Trunk to your phone system. 
- There are many options for this but one of my favorites is voip.ms. 
- Here is the documentation for 3CX: https://www.3cx.com/docs/sip-trunk/voip-ms-canada/





