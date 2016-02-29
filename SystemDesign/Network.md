#Computer Network

##What happens when you visit a website? What exactly goes on after you type a URL into a browser?

When you visit a website a lot of things happen behind the scenes that you may not be aware of. Let’s go through a list of those things in the order that they occur:

1.	When you visit a website, the web browser that you are using (whether it is Chrome, Safari, Firefox, Internet Explorer etc.) will contact what’s called a DNS (Domain Name System) server that will translate the human readable website name into a numeric IP address. It’s important to remember that every website name is basically an alias for an IP address. So, DNS converts that URL into an IP address, and each website has its own unique IP address.
(first it will search the DNS in browser cache, then in the operating system cache, or local host;
then it request the DNS to translate to IP)

```
	DNS is interesting because of the fact that it is basically works in a hierarchical structure. There are many DNS servers distributed throughout the world, and if one DNS server does not know a particular IP address, then it will ask another DNS server that is “higher up” in the hierarchy. How does your personal computer know which DNS server to use? Well, your ISP (Internet Service Provider) actually sends some extra network information to your computer whenever you connect to the Internet. That “extra” network information includes which DNS server your computer should be using whenever you visit a website.
```

Once a DNS server finds the IP address of the website you are looking for, that IP address is returned to your browser.

2. Your browser will now use the IP address returned by DNS to communicate with the web server that hosts the website that you want to visit. It will connect to port number 80 on the web server using a protocol called TCP.

3. Now that your browser has a connection with the website’s web server, your browser will retrieve the html code(or some other resources) of the specific page that is requested.

4. Once your browser receives the HTML code from the web server, it will display that HTML code to you in the browser window.

5. If and when you close that particular browser window, the connection with the web server will end.

###What is URL?

	http://www.github.com:8080/index.html?user=rwang23&lang=zh-CN#home
	  |          |          |       |                  |          |
	protocol     |          |       |                  |          |
	          hostname     port     |                  |          |
	              \        /    pathname             search      hash
	                 host
##HTTP
#### HTTP Status Messages

|HTTP Status|Description|Message|
|------|----|--------|
|200|The request is OK (this is the standard response for successful HTTP requests)|OK|
|301|The requested page has moved to a new URL | Moved Permanently|
|304|Indicates the requested page has not been modified since last requested|Not Modified|
|400|The request cannot be fulfilled due to bad syntax|Bad Request|
|404|The requested page could not be found but may be available again in the future|Not Found|
|500|A generic error message, given when no more specific message is suitable|Internal Server Error|

##What is cookie
An HTTP cookie (also called web cookie, Internet cookie, browser cookie or simply cookie), is a small piece of data sent from a website and stored in the user's web browser while the user is browsing. Every time the user loads the website, the browser sends the cookie back to the server to notify the user's previous activity.
###Pros and Cons
####Pros
In some ways, cookies make browsing the Internet faster and easier.
For example, certain websites customize site information based on your location (city). Also, after you have registered on a site like Amazon, for example, you do not have to enter the same information every time you visit the site.
####Cons
Since most websites will not allow their site to be accessed unless cookies are enabled, browsers are usually set to accept cookies by default. As a result, cookies are being stored "invisibly" on your hard drive every time you browse the Internet. Since your IP address is usually collected, your browsing history and online activities become public knowledge.
Also, your browser may start and run slower, and your system may lag or hang up if hard drive space is limited
When you visit websites that contain ads, third-party cookies (from sites you've never visited) can also be placed on your computer

##What is a MAC address?

MAC stands for Media Access Control. The MAC address is globally unique – which means that no two devices in the world (in theory) will share a MAC addresses.

###What do the numbers mean in the MAC address?

A MAC address is typically represented by six groups of 2 hexadecimal numbers. When presented in a friendly format for humans to read, the six groups are generally separated by either a hypen (a “-“) or a colon (a “:”). So, a MAC address could look like this: 01-33-45-69-89-yz, or even this: 01:33:45:69:89:yz, where each group of 2 hexadecimal numbers is separated by the hyphen or by the colon. Each group is composed of 1 byte – or 1 octet – since both terms represent 8 bits.

The first three bytes of a MAC address (which is also the first half of the MAC address) are specific for each manufacturer of the hardware. What does that mean? Well, if you see a MAC address that starts with “00:05:69″, then you know that the hardware was manufactured by the company VMWare. Similarly, you can identify hardware manufactured by Intel just by looking at the first three bytes of the MAC address. The last three bytes (or the second half of the MAC address) are assigned by the manufacturer as they please – as long as those last three bytes are unique then the manufacturer can assign those bytes as they see fit.

###Can a MAC address be changed?

MAC addresses were originally meant to be both globally unique and permanent, but in newer hardware it is actually possible to change the MAC address. So, yes, the MAC address can be changed on most new hardware.

###Are MAC addresses only for devices with an ethernet interface?

No, this is a popular misconception. Even iPhones – which have no Ethernet interface – still have (and need) a MAC address.

###How to get a MAC address using PHP?

Retrieving the MAC address of a client connecting to your website using PHP is not possible. This is not some limitation of PHP – this is simply because the MAC address is lost once the client’s packets have been routed from their local subnet to the gateway that leads out to the Internet. The client’s local router can of course access the MAC address, but once the packets proceed past that point and into the ‘outside’ world of the Internet, the MAC address simply can not be retrieved.

###What are some uses for the MAC address?

One common method used to secure wireless routers is to add a list of all the MAC addresses of all devices that should have access to the router’s network. If a device’s MAC address is not on that list, then it is not allowed to access the Internet through that router. This is commonly known as MAC address filtering.

I’ve also seen hotels use MAC addresses to give their guests a fixed period of free time – like 30 minutes of free time daily – to access the Internet. Because guests will have to go through the hotel’s router to access the Internet, the hotel router can remember the MAC addresses of devices that accessed the Internet. This way, if you try to access the Internet again after exceeding your daily free 30 minutes, you will be denied. The reason these hotels don’t use cookies is because it is too simple to get around that – you can easily delete your cookies to access the Internet again. But, the only drawback is that if a guest has multiple devices – like an iPhone and a laptop – then he/she could get a full hour of free Internet time, since the MAC address is only different for every device, and they have no way of knowing that both devices (like the iPhone and the laptop) belong to the same guest.

##What is the difference between baud rate and bit rate?

Bits, as you probably know, are the 0’s and 1’s that binary data consists of. The bit rate is a measure of the number of bits that are transmitted per unit of time – where the unit of time can be anything. Generally you will see the bit rate measured in bits per second. This means that if a network is transmitting 15,000 bits ever second, the bit rate is 15,000 bps – where bps obviously stands for bits per second.

The baud rate, which is also known as symbol rate, measures the number of symbols that are transmitted per unit of time. A symbol typically consists of a fixed number of bits depending on what the symbol is defined as. The baud rate is measured in symbols per second.

###The difference between baud rate and bit rate

To summarize, the bit rate measures the number of bits transmitted per second, whereas the baud rate measures the number of symbols transmitted per second – and that is the major difference between the two.

###Can the baud rate equal the bit rate?

Because symbols are comprised of bits, the baud rate will equal the bit rate only when there is just one bit per symbol.
