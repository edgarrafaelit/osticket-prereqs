<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket on a Windows virtual machine in Microsoft Azure.
Before we start, there are easier and more user-friendly ways of going about this. This project was designed to showcase an understanding of and ability to execute with the given technologies, concepts, software, etc, that make up a working installation of osTicket. Some of those concepts include: PHP, IIS, and SQL databases. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Azure Virtual Machine
- osTicket Installation Files
- HeidiSQL

<h2>Installation Steps</h2>

<p>
<img src="https://imgur.com/5GLBkV3" height="80%" width="80%" alt="Virtual Machine"/>
</p>
<p>
We're using Microsoft Azure to run this lab. Azure allows us to quickly spin up virtual machines without messing about with .iso files, which can be tricky and it's pretty cheap.
  Today we are creating a Windows 10 machine with 16 gigabytes of RAM and 4 virtual CPUs. 
</p>
<br />

<p>
<img src="https://imgur.com/oC7Hc81" height="80%" width="80%" alt="Internet INformation Services"/>
</p>
<p>
From our Virtual Machine we need to enable the IIS, Internet Information Services. 
This is a built in web server that comes on all windows machines. Then we enable Common Gateway Interface.
Essentially we are opening a Gateway (CGI) to allow our web server (IIS) to execute third party software, in this case, osTicket.
Type "Turn win" into the Windows search bar, this should be enough to trigger the smart suggestion, "Turn Windows Features on or off".
Click the box marked Internet Information Services then follow this path and check the box -> World Wide Web Services -> Application Development Features -> [X] CGI
</p>
<br />

<p>
<img src="https://imgur.com/DUQtfHo" height="80%" width="80%" alt="PHP Manager for IIS installer"/>
</p>
<p>
The next step is to download and <a href="https://www.iis.net/downloads/community/2018/05/php-manager-150-for-iis-10">install PHP Manager for ISS</a>
</p>
<br />

<p>
<img src="https://imgur.com/n67G5el" height="80%" width="80%" alt="URL Rewrite installer"/>
</p>
<p>
We now want to download and install <a href="https://download.microsoft.com/download/1/2/8/128E2E22-C1B9-44A4-BE2A-5859ED1D4592/rewrite_amd64_en-US.msi"> URL Rewrite Module </a>
  This will help osTicket to resolve complicated URLs on the backend to help the user experience.
</p>

<p>
<img src="https://imgur.com/rwd9x3K" alt="Extracting our PHP .ZIP file"/>
</p>
<p>
 With that done it's time to <a href="https://windows.php.net/downloads/releases/php-8.2.3-Win32-vs16-x64.zip"> download our PHP.zip file</a>. PHP is a scripting language designed for web development.
In this case osTicket functions out of a website, that website uses PHP to run the osTicket software.
Create a file in you PC's C: drive titles "PHP" then extract the contents of the .ZIP file to the file we just created.
</p>

<p>
<img src="https://imgur.com/IXdDoj3" height="80%" width="80%" alt="Installing visual C++ REdistributable"/>
</p>
<p>
Download and <a href="https://aka.ms/vs/17/release/vc_redist.x64.exe"> install Microsoft Visual C++ Redistribuatable</a>. This is a collection of resources, called libraries, that are required by many applications written in C++. In this case we'll be installing MySQL, an application written in C++.
</p>

<p>
<img src="https://imgur.com/qdTJQB7" height="80%" width="80%" alt="Configuring MySQL"/>
</p>
<p> The very next thing we do is <a href="https://drive.google.com/file/d/1_OWh9p7VQLcrB0q_V7qT8yHl0xo5gv7z/view?usp=share_link"> install MySQL</a>. This will act as a database for all our users and their tickets. Choose the "Typical" installation type. After install the program will start on its own. Choose the "Standard" configuration then choose the credentials you'd like to use to access your database.
</p>

<p>
<img src="https://imgur.com/8fBwUgB" height="80%" width="80%" alt="Registering PHP onto our IIS Server"/>
</p>
<p>
From the search bar type in "IIS" to bring up the Internet Information Services Manager.
Right click and "run as administrator". From here navigate to the PHP Manager we installed and click "register a new PHP version".
Click the three dots to the right of the search bar and navigate to C:\PHP\php-cgi.exe then click "open" and "OK".
Make sure you restart your IIS server to ensure these changes take effect.
</p>

<p>
<img src="https://imgur.com/s7l10PV" height="80%" width="80%" alt="Extracting osTicket to c:inetpub\wwwroot"/>
</p>
<p>
We're now ready to <a href="https://drive.google.com/drive/u/0/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6> install osTicket</a>.
Extract the "upload" folder to destination "C:inetpup\wwwroot" then rename the folder to "osTicket".
 </p>

<p>
<img src="https://imgur.com/jSjojZp" height="80%" width="80%" alt="Checking we did everything right"/>
</p>
<p>
 Restart your IIS Server then navigate through the right hand drop-down menu through "osTicket -> Sites -> Default Web Sites -> osTicket"
 From this folder we can navigate to os Ticket by clicking "Browse *:80(http)" on the right hand side of the screen.
  </p>

<p>
<img src="https://imgur.com/RzNfD84" height="80%" width="80%" alt="showing where you can enable PHP extensions to osTicket from PHP Manager"/>
</p>
<p>
 From this screen we can see that we have connected with osTicket, but there's some red X's that we want to be Green cpheck marks. So open up IIS one more time, navigate back to the osTicket folder click PHP Manaager and click "enable or disable an extension".
  </p>

<p>
<img src="https://imgur.com/KWLqrmo" height="80%" width="80%" alt="enabling random extensions like we know what they do"/>
</p>
<p>
 From this menu we want to enable the extensions:
  php_imap.dll
  php_intl.dll
  php_opcache.dll
 </p>

<p>
<img src="https://imgur.com/tyC7GBi" height="80%" width="80%" alt="We made checks appear! Cool"/>
</p>
<p>
 Refresh the site in your browser and observe that we now have three more green checks.
  </p>

<p>
<img src="https://imgur.com/aslRK4Q" height="80%" width="80%" alt="where to find the important file to rename"/>
</p>
<p>
 Before can continue our installation we need to make sure that osTicket can execute the proper file from our installation files.
  Navigate to "C:inetpub\wwwroot\osTicket\include\ostsample-config.php" and rename it to "ost-config.php"
 </p>

<p>
<img src="https://imgur.com/6F9TV8H" height="80%" width="80%" alt="removing inheritence of permissions from C:inetpub\wwwroot\include\ost-config.php"/>
</p>
<p>
 Then change the permissions on "ost-config.php" so that EVERYONE has read, write and execute access. The surest way to do this is to right click on "ost-config.php", click "Properties", navigate to the "Security" tab and click "Advanced". From here we can choose "disable inheritence" and click "remove all inheritence".
 This makes sure there arent any other rules that may interfere with the permissions that we're about to assign to this file.
   </p>

<p>
<img src="https://imgur.com/ikGm3s4" height="80%" width="80%" alt="Giving Full Control to the whole dang world"/>
</p>
<p>
Now we click "Add", select the principal "Everyone" and assign them "Full control" to ost-config.php
 </p>

<p>
<img src="https://imgur.com/U6rj1jt" height="80%" width="80%" alt="HeidiSQL installer"/>
</p>
<p>
Now we need a way to acces our MySQL database. A user friendly way of doing that is by using HeidiSQL, which we'll install now.
 </p>

<p>
<img src="https://imgur.com/nq3ptp5g" height="80%" width="80%" alt="Creating a session on HeidiSQL"/>
</p>
<p>
Once HeidiSQL is installed we create a new session called "osTicket"
 </p>

<p>
<img src="https://imgur.com/d4aq8PH" height="80%" width="80%" alt="Creating a databse on HeidiSQL"/>
</p>
<p>
Within that session we create right click on the name of our session, "osTicket, and navigate to "create new" the choose "database". The database will also be called "osTicket".
 </p>

<p>
<img src="https://imgur.com/MjeUsOJ" height="80%" width="80%" alt="Databse information from osTIcket website"/>
</p>
<p>
Using the database and session information we just created fill out the forms on the osTicket website.
 </p>

<p>
<img src="https://imgur.com/7uOoAVS" height="80%" width="80%" alt="OMG no way we r so l33t c0mp2tr"/>
</p>
<p>
Congratulations! You've sucessfully installed osTicket onto your Virtual Machine! Check out my subsequent tutorial on Post-Installation configuration. Fun!
 </p>

<p>
<img src="https://imgur.com/lavL3rw" height="80%" width="80%" alt="Changing permissions on C:inetpub\wwroot\include\ost-config.php back to read and execute only"/>
</p>
<p>
 Don't forget to change the permissions on "C:inetpup\wwwroot\include\ost-config.php" back to read/execute only
