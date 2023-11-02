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


                   <----- Node 1 
    Chef server <---
                   <----- Node 2.

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
    
![Diagram](c/users/B.Radhaprathap/drawio/ansible_Push.png)







