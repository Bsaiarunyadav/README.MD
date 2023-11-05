Ansible :- 

*   Disadvantages of shellscript:- 
    1) shellscript is homogenius 
        . useradd roboshop--> centos
        . add user roboshop--> ubuntu
    One shellscript can only work one paticular distribution.
    2) Every time we need to validate .
    3) Imperative vs Declarative .
        . Imperative :- little tough sysntax & Very strict syntax & Follows in sequence.
        . declerative :- easy syntax , No need of sequence , we can write anywhere .
                            ( What ever you write we get it )
    
------> Here just keep an idea that the shell-script was imperative and the ansible was declerative.

1) Ansible can query the server , it can understand what os it is ,based on that it can change the command.
2) you no need to write validations.
3) Ansible can connect any no.of servers , no need to login to the server.
4) Also it was declerative, No need of sequence in and easy syntax .

### How it works .
1) Before ansible there is pull mechanism.
---> There are 2 things :- 
    1) chef 
    2) Puppet

![README.MD](Images/pullvspush.jpg) 

### How the pull mechanism works here ?

* In pull mechanism the nodes will pull the code from the server .
    1) first node will connect to server.
    2) Pull the configuration.
    3) Run the configuration.
Another Disadvantage is that we need to configure how to frequently nodes should connect to the server
once in 30 min .
(In this case for every 30 min nodes will connect to the CHEF SERVER & Pull the configuration )
*  Ex:- LIC agent

* Push mechanism .
    . Here no.of steps will be reduced .
    . here we no need of any agent .
    configuration server ---> Ansible server 
. And directly we can push the configuration .

### Push mechanism
    
![README.MD](Images/push.jpg) 

* For example :- Take LIC Used case .

AT ealier times :- 1) You pay to agent .
                   2)  Agent pay to LIC Office

Present times :- 1) We are able to pay directly and no need of the agent .

> Important :- 
    Another disadvantage of pull :- 
        1) Pull mechanism will have additional agent software .
        2) There May not be any change in configuartion all the time.
        3) change in configuration is very rare , so The wastage of data ,Power etc...
        ex :- Evry 30 min , The traffic is geting more ,there is some data ,Power , Node is connecting to the server & it is fetching it ,but mostly there will be no change ,so it was waste of data .

PUSH :- 1) Here we don't have any agent & We can directly push the configuration ,"This is ADVANTAGE".
        2) Also here there is no wastage of data also .

* Earlier we are using the using "Chef & Puppet" which is popular , But now a days we are using the Ansible server.


#### How to install ANSIBLE:- 
        1) Take root access.
        2) Yum install Ansible 

"Ansible devopled basing on python That is why it will download python package".

##### how to attach NODE to Ansible :- 

![README.MD](Images/push_to_Node.png)

    - After installing Ansible 
    - Run (Basically we wont use this )

Command Line :- 
Ansible -i <Privateip>, all -e ansible -e ansible_user centos -e ansible_Password=DevOps321 -m ping 

        here We are telling ansible :- 
            - i ---> Inventory
            -m  ping ---> if the server is like we will get "Pong" In response  
            if not ---> It shows Failed ..

    * In background ansible uses "SSH" authentication where it needs :- Ip , pass, username .

    In linux we keep the command in shellscript in the same way.
    Ex  :- Shellscript.

In ansible it is know as **Playbook**

* PlayBook ---> keeping all the ansible collections (i.e command in linux) and run it .


Session 18 :- 

As we know the anisble uses ssh authentiation .
-genrally while working with ansible we will find a thing called "Inventory".
-Inventory is nothing but list of hosts that server is managing .

- so we have our ansible server 

   ANSIBLE----> NODE 1

   So in inventory we have 1 i.e NODE 1.
 
Note :- Genrally Inventory is recommended but not compulsory .

So There is proper way :- 

Think There is a company "ROBOSHOP"
geography :- IND,us,UK,AUS Etc.
Env:- Dev,QA,PROD
Component:- WEB,APP,DB
Server :- Mongodb , CART, catalogue

We have 4 different kinds of server basing upon 4 things.   
    - Naming the servers is the best practice .
for ex:- Roboshop-us-dev-db-mongodb01
    (By seeing the above name we can understand where it belongs to)

* This method also will be followed in Real time basis.

-we always group the server .
    - So let us take a inventory file and group "nginx" Servers.

    - Lets take it as Mongodb.

>    [Mongodb] (We have to create a Route 53 record for it )

roboshop-us-dev-db-monogodb-01.Join devops.online [app]
 









