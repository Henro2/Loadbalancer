
<h1>Implimenting Load balancers With  Nginx</h1>	






**Step 1**


**Provissioning EC2 instance called myapcheserver**

-  Created an ubuntu instance in Aws called myapacheserver

    ![Alt text](Images/instance.png)


**Step 2**

**Inbound Rule**


- Added inbound rule to allow access to port 8000


   ![Alt text](Images/rule.png)


-  With Termius, I connected successfully to myapacheserver

    ![Alt text](Images/termiusConnection.png)




- With **sudo apt update**, I updated it


   ![Alt text](Images/update.png)


**Step 3**

**Installing Apache2 webserver** 

-  With **sudo apt install apache2 -y**. I installed apache2 webserver


   ![Alt text](Images/apache2installed.png)

- With this command,   <mark>systemctl status apache2</mark>, I checked to see if apache2 is installed and running.

   ![Alt text](Images/apacherunning.png)

**Step 4**

**Configuring Apache to serve a page showing its public Ip address**

-  I configured apache to serve a content on port 8000 by using nano command to edit **ports.conf** file in **etc/apache2/ports.conf** using super user privilage.

    ![Alt text](Images/portadded.png)

-  With super user privilages, I used nano command to edit **000-default.conf** file and changed port 80 to **port 8000**. The file is located in **etc/apache2/site-available/000-default.conf**.

     ![Alt text](Images/00edit.png)

-  Restarted apache with **systemctl reload apache2** for changes to take effect.





<h1>Creating my new html file</h1>


- In **var/www/html** folder, I created index.html and edited it using nano command to paste the code to show the public ip address



  ![Alt text](Images/htmlcode.png)


- With sudo chown **www-data:www-data ./index.html**, i changed index.html ownership

  ![Alt text](Images/editedInd.png)

-  I restarted apache2 with **sudo systemctl restart apache2**


- In my web browser, I typed in http://54.90.200.130:8000/ and the following page came up:

   ![Alt text](Images/webpage.png)



- **Step 5**


**Configuring Nginx as Load Balancer**


-  I provissioned another ubuntu Ec2 instance called Loadbalancer.



-  ![Alt text](Images/nginxloadInst.png)

- With **sudo apt update** command, I updated the instance.

   ![Alt text](Images/nginxUpate.png)


- With **sudo apt install nginx -y** command, I installed nginx and checked the status using **systemctl status nginx** command

  ![Alt text](Images/nginxinstalled.png)


  -  With cd command, i entered into **conf.d** directory and use **ls** command to show the contents and to locate the **loadbalancer.conf file** The file does not exist. So, i created it using touch command and change the ownwership. 


  ![Alt text](Images/loadfileconf.png)

-  With nano command, I pasted the required code in loadbalancer.conf and edited it with the required parameters as shown bellow. 

    ![Alt text](Images/loadbalnceredited.png)

    ![Alt text](loadbalnceredited2png.png)

    




  

-  To prevent nginx loadbalancer from loading its default config on port 80 which will load nginx default page, I changed the port to an unknown port which is not added in the inboud rule.  This activated my new configuration file which will listen on port 80 





-  using this command, **Curl localhost**, loaded my apache server content as shown bellow: 

  ![Alt text](Images/curlloadbalancer.png)


  -  Using the public ip address of myloadbalancer in my browser, it opened my apache server content.

![Alt text](Images/loadbalanceip.png)



**Project completed** 


  


    

