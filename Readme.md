# openstack-sandiego
OpenStack San Diego Meetup

In this tutorial, you'll be starting up a number of web servers to run your new ecommerce startup. These virtual servers will be running in an OpenStack cloud that has all the computing, storage and networking resources you need.

Before you start, you'll neeed an account login and password from the person in charge of this lab. If you're doing this virtually, you can send a tweet to "@OpenStackSD" and we'll direct message you some credentials.

<UL>
<LI>Get a username and password for the OpenStack cloud
</UL>

We'll be using the CityCloud OpenStack cloud at https://citycontrolpanel.com
<UL>
<LI>Log into the <A HREF="https://citycontrolpanel.com" target="_new">OpenStack cloud</A> with the username and password above.
</UL>

We're going to need a network to run our web servers. Let's us a private IP address range of 10.10.10.0/24 that we will call web-net.

<UL>
<LI>Click "Network"->"Networks"->"Create Network"
<LI>Call the new network "webserver-network" and build it in the "Los Angeles" data center
<LI>Under the "Advanced" drop down enter in the subnet range of 10.10.10.0/24.
<LI>Click "Create Network" to proceed
</UL>

Your web developers want an "Ubuntu 16.04" flavored Linux web server (LAMP). LAMP has all the software packages your developer needs to run the web server (Linux, Apache, MySQL, PHP/Perl).
<UL>
<LI>Click "Servers"->"Create Server"
<LI>Create the new server in the "Los Angeles" zone
<LI>Select "Linux"->"Ubuntu 16.04 Xenial Xerus" type server
<LI>Add the "LAMP" software packages
<LI>Double check that it is connected to the "webserver-network" subnet
<LI>It is OK that we are not connecting to the Internet so disregard the warning about there not being an Internet connection.
<LI>Disable "Disaster Recovery" since this is just a demo machine
<LI>Enter in a password for this new machine and remember the username and password!
<LI>Click "Create Server" to proceed
</UL>

Your first web server is now starting up!  Take a look at what internal private IP address it has been assigned. It should be on the 10.10.10.0 subnet. Next we start up the web server.

<UL>
<LI>Click the gear icon by the new server and select "Console"
<LI>Login using the username and password that you created above
<LI>Start the web server with the command "sudo /etc/init.d/apache2 start"
</UL>

Next we're going to create a floating IP address on the public Internet that can be used to access servers on our internal network.

Floating IP addresses can be moved from server to server. We're going to create one and assign it to this machine. Your server will still have it's private IP address on the webserver-network subnet.

<UL>
<LI>Click the gear icon by the new server and select "Connect floating IP"
<LI>"Create new IP" and "Add floating IP"
<LI>Use a web browser to connect to the web server at http://floating_IP/
</UL>

The web page should now start up!!

Uh oh, your web developers broke the server and need a replacement! They want you to startup a replacement server and assign it the floating IP.

<UL>
<LI>Create a new Ubunutu Linux server in the Los Angeles zone in the webserver-network subnet
<LI>Login via the console and start up the web server
<LI>Under the server gear icon, disconnect the "floating IP" from the old server
<LI>Assign the existing "floating IP" to the new server
<LI>Use a web browser to connect to the web server at http://floating_IP/
<LI>Destroy the old server
<LI>Double check that the page is alive http://floating_IP/
</UL>

Congrats! You swapped servers using the floating IPs without anyone knowing!

Business it picking up! You need a second web server to handle the load and load balancing between the two. We're going to take our floating IP and assign it to the load balancer which will send traffic across the two virtual machines.
<UL>
<LI>Clone the existing Ubunutu server (don't assign it a floating IP)
<LI>Create a Load Balancer and assign it the floating IP
<LI>Drag both servers into the load balancing pool
<LI>Use a web browser to connect to the web server at http://floating_IP/
</UL>

Try out pausing each of the servers individually (and both) to validate that the load balancer is working correctly.

Congrats! You are well on your way to building your own OpenStack powered business!
