---
layout: wiki_archive
---

#### MVP Web Access

While you can access the interface using

> <http://localhost:8000>

And if you know the local IP address of your Raspberry Pi, you can
access it from other computers on your network. This does not allow you
to remotely connect to your MVP outside your local network. That takes a
bit more work, and a knowledge of your local network and router. The
following assumes you are setting things up at home, your home has
internet service, and you have access to your home router. I have a
Linksys router, and will use it as an example of what to do. To access
your MVP from outside your local network requires three things: \* The
ability to find your home IP address \* A static network IP address for
your Raspberry Pi \* Port forwarding for CouchDB and your server

##### Home IP Address

It is unlikely that you have a static IP address for your home, it is an
expensive service of most internet providers that few people are willing
to pay for. Since many people are not on the internet all the time, and
there are a lot of customers sharing a limited number if IP addresses;
most internet providers give out temporary IP addresses as needed. This
is known as the
[DHCP](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol)
protocol. This means your IP address will change over time. On my router
(Security/Apps and Gaming/DDNS) it lists my current IP address. With
this address, I could reach my router from anywhere on the web - but it
could change at any time. To get around this, you need a DDNS service.
This is a company that lets you create a web/host name (ie.
OpenAgBloom.ddns.net), and they take care of tracking what IP address is
assigned to it at any time. My router knows of several companies that
provide this service (some for free). In my case I am using NO-IP.com. I
tell my router the name of the company, my login and password, and my
host name. Every time my IP address changes my router sends a message to
NO-IP.com telling them my new IP address. Now, every time someone types
OpenAgBloom.ddns.com into their browser, they get routed to the service
which looks up the current IP address, and sends them on their way to my
router. Notice I say they go to my router, nobody outside of my
local/private network knows that I have a Raspberry Pi connected up as
my MVP. This is where you have to tell your router how to send people to
your MVP.

##### DHCP Reservations

Just as your internet provider changes your router's IP address, so too
your home router hands out local IP addresses as people connect and
disconnect from your home LAN. What you want to do is tell your router
to reserve an IP address for your Raspberry Pi, and always give it to
your Pi when it connects to the network. On my Linksys this is found
under Connectivity/Local Network, there I find a button that says "DHCP
Reservation". On this page you will see other information on this page,
such as the starting IP address the router will use, how many addresses
it will manage, and how long it will let a device keep an address before
it frees that address for someone else to use. If you click on "DHCP
Reservation" you will see a list of devices that have reserved addresses
(if any), and a list of connected devices for which you can reserve an
address. Find your Raspberry in the list and select it, then save the
reservation. Sometimes my Raspberry doesn't always reconnect properly,
but usually it connects reliable and is where I expect it.

##### Port Forwarding

The last step is telling the router how to forward people outside your
LAN to your Raspberry. All internet requests go to a
["port"](https://en.wikipedia.org/wiki/Port_\(computer_networking\)), an
address that is listening for requests to service them; if none is
provided, things usually default to port 80 which is the standard for
HTTP requests. If your router is set up correctly (with security), it
will refuse to answer any requests from outside your LAN. This port
number is where your Raspberry knows that "5984" means a request for the
CouchDB, and "8000" is the MVP. Port forwarding is where you tell your
router that if a request comes in for port "8000" it should know to
forward that request to your Raspberry Pi. On my Linksys (Security/Apps
and Gaming/Single Port Forwarding) there is a table of port numbers (as
requested from an outside call) that map to internal IP addresses and
port numbers. I am not doing any fancy port switching (setting up two
MVPs, both with CouchDB on 5984), so my external port numbers are the
same as the internal. Specify both protocols, and enable the forwarding.
For the MVP you need two ports (5984 for CouchDB and 8000 for the
server) and will create two forwarding entries in the table. Save the
results and you should be able to connect to your MVP from anywhere on
the web.

##### WARNING

You are opening up your Raspberry Pi to the web, which also means you
are potentially opening up your home LAN as well. The server only
handles HTTP requests, so there is little damage a hacker can do here,
but CouchDB is configured as an ["Admin
Party"](http://forum.openag.media.mit.edu/t/security-ending-the-admin-party/1175)
and anyone who can delete your data and cause other trouble. This is
probably a very low risk, but it is a risk and I have done my [due
diligence](https://github.com/webbhm/OpenAg-MVP-II/blob/master/HomerSimpsonClause.md).
At a minimum, change your Raspberry Pi password. Also, back up your SD
card on a regular basis (Reminder to self - you need to do this).
