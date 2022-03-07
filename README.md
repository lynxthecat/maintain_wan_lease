# maintain-wan-lease
Keywords: Asus Merlin, WAN IP renewal, WAN LED indicator red and modem bridge mode. 

Resolve problem with Asus Merlin routers in terms of release/renew of udhcpc.

Namely if a modem set up in bridge mode such as the Huawei B818-263 drops eth0, then absent a udhcpc release/renew, a loss in internet connectivity can result. It seems by default Asus routers do not issue the appropriate udhcpc release/renew calls. This script resolves this in an efficient manner by monitoring the eth0 interface and reacting to changes as they occur.  

For background see here: 

http://www.snbforums.com/threads/router-not-getting-internet-back-after-wan-drop.71954/post-709554

http://www.snbforums.com/threads/problem-udhcpc-does-not-deconfig-upon-wan-cable-disconnect.74397/

One way to install it is to place the script inside /jffs/scripts/, chmod +x maintain-wan-lease, and then create or edit 'post-mount' inside /jffs/scripts/ such that it includes at least the lines:

```
#!/bin/sh

/jffs/scripts/maintain-wan-lease &
```

Then chmod +x post-mount. 

See here for details concerning setting up scripts in Asus Merlin:

https://github.com/RMerl/asuswrt-merlin.ng/wiki/User-scripts

To test, try manually unplugging eth0 and plugging it back into the router. You should see the appropriate lines end up on the system log confirming release and renew. 

For further support, please consult the snbforums forum. 

See for example this post:

http://www.snbforums.com/threads/rt-ax88u-isps-dhcp-does-not-function-properly-but-manual-udhcpc-call-works.74457/post-749666
