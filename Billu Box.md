You can download the lab link below

https://www.vulnhub.com/entry/billu-b0x,188/


First we will scan the machine with nmap

![Screen Shot 2022-01-06 at 16 04 10](https://user-images.githubusercontent.com/79763515/148390479-ffe7c836-d09c-4fba-86c1-38a87ec9b5d6.png)


Nmap results show us that port 80 is open. Lets take a look on web site


![Screen Shot 2022-01-06 at 16 05 00](https://user-images.githubusercontent.com/79763515/148390648-2c5e1ed8-16c0-43ed-8658-e3f192f0b7fa.png)


We will use dirb command to enumerate url's by using big.txt 

dirb http://10.0.2.4 /usr/share/wordlists/dirb/big.txt


![Screen Shot 2022-01-06 at 16 11 47](https://user-images.githubusercontent.com/79763515/148391301-dbb46746-4282-48a7-a59c-a5ae1176a4b3.png)

Let's visit highlighted url's 


Browsing to the “test” file returned that the “file” parameter is empty.

![Screen Shot 2022-01-06 at 16 14 49](https://user-images.githubusercontent.com/79763515/148391824-ef871fc2-66d3-4d5d-929f-305ee86580a5.png)


The other one gave us the login panel for phpmyadmin


![Screen Shot 2022-01-06 at 16 12 40](https://user-images.githubusercontent.com/79763515/148391900-99f6759b-50e5-4ff2-9cb4-4ef48a70f256.png)


With the Local File Read vulnerability we can potentially disclose sensitive information/credentials used by the Phpmyadmin for set up.

We already know that web root directory /var/www/phpmy/config.inc we can easily capture the confg file

We will use curl command for sending a POST request

curl -X POST --data "file=/var/www/phpmy/config.inc.php" http://10.0.2.4/test

![Screen Shot 2022-01-06 at 16 17 26](https://user-images.githubusercontent.com/79763515/148393236-3e3927ef-58ef-467a-b44a-2652b1cb4ccb.png)



Bingo.! We got the username and password for root.

As we know from the nmap results that port ssh is open, let's connect to the machine



![Screen Shot 2022-01-06 at 16 19 20](https://user-images.githubusercontent.com/79763515/148393562-34d5349a-c10d-401a-b992-7ec3f0385e10.png)




















