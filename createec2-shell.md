#  How to create an instance & route 53 records through automation using the shell .

For this we need "AWS Command Line"

>> There is a concept called "IAM".
        Identity access management
 
Let us discuss about:- 

### Authenication & Authorization ###

Ex :- for logging into a server we need 

        Username + Password  ---> This is called authentication.

Authorization :- 

    Ex:- Just like we don't have permission to enter every place in a company so we need some
    authorization to enter all the places in company.

1) AWS has 1000's of services , And if you create a user he can't get all the admin access you will give limited access.

2) i.e premissions ---> so you will certain permissions this is called universal conecpt and it is know as "IAM".


### We have 4 Concepts in "IAM" :- 

    1) User 
    2) Group
    3) permissions
    4) Roles --> It was for non humans, you should attach this role to aws services so that they can't 
                create resources .
                So why AWS  introduced roles .

--> Suppose we have an ec2 instance but we can't create other services like route53,EKS,Loadbalancer directly .

. So we should have AWS Services also to have cetain permissions ,so that they can't create resources.

--> why should you have AWS services also 
 
Suppose we have aws command line - Using aws command line we can create all the services ideally in cloud .

If there is not having iam role then our ec2 cannot do anything .


How to create a IAM role :- 

    --> Go to Iam Role 
    --> Select Roles 
    --> Create Role
**(REMEMBER:- Roles is not for humans but for servers)**
    --> Select - ec2
    --> click on NEXT
Here You should select permissions --> 
    1) If it was normal user we can have username & Password & Permissions
    2) If it is ROLE then 
            . What is service --> In Our case it is ec2
            . what are the permission --> Administrator access

    --> Select Admistatr access (ALL PERMISSIONS)
    --> click on -NEXT 
    --> Give any name :- Ex :- Roboshop-shell
                    (Once check the permissions)
--> Create role 

**now we can attach it only for ecc2 instance**

--> Now go to Instances (Work Station)
        --> Select action
        --> Security
        --> Modify IAM Role 
        --> by default we can see the "Roboshop-shell"
        --> Click on update .

* what we done till now :- 
    . Created a Instance 
    . Then created Role 
    . Given administrative access 
    . and attached the role to ec2 instance.

**Now our ec2 can do & create anything**


We can check below command by serching "How to create an instance using AWS command line"

aws ec2 run-instances --image-id ami-xxxxxxxx --count 1 --instance-type t2.micro --key-name MyKeyPair --security-group-ids sg-903004f8 --subnet-id subnet-6e7f829e


The below are not required as we don't provide the details in manual too.
    --count 1
    --subnet-id subnet-6e7f829e
    --key-name MyKeyPair 



syntax :- aws ec2 run-instances --image-id ami-03265a0778a880afb  --instance-type t2.micro --security-group-ids sg-0b3a6df94f038e0fc 

> By using the above command Instace will be created .

And now we need to query our prviate ip address so we need to create route 53 as well 

how to query form the provided information :- There is some thing called JQ (Json query)


aws ec2 run-instances --image-id ami-03265a0778a880afb  --instance-type t2.micro --security-group-ids sg-0b3a6df94f038e0fc | jq -r '.Instances[0].PrivateIpAddress'


jq -r '.Instances[0].PrivateIpAddress' ---> this provides immediate private ip address within seconds.

**So now what our script should do** 

    create all the instances :-  
        1) Web 
        2) mongodb
        3) catlaogue
        4) cart
        5) user
        6) redis
        7) mysql
        8) shipping 
        9) payment
        10) rabbitmq
        11) dispatch



#### script ####

#!/bin/bash

#now we previous discussed about array same way just giving a variable

    NAMES=("Web" "mongodb" "catlaogue" "cart" "user" "redis" "mysql" "shipping" "rabbitmq" "payment" "dispatch")
    INSTANCE_TYPE=""

#We have some condition if "Mysql" "Mongodb" instance should be t3medium rest all should be t2micro. so we will write a condition .
#Let us write a condition.       
#looping through array 
>>We all know that in programming "||" Means (or) AND "&&" Means (and)

    for i in "${NAMES[@]}"  
    do 
        echo "ALL NAMES: $i"
    done 

        








aws route53 change-resource-record-sets --hosted-zone-id Z02946853G9H9IVS4XYSF --change-batch '
{
            "Comment": "CREATE/DELETE/UPSERT a record ",
            "Changes": [{
            "Action": "CREATE",
                        "ResourceRecordSet": {
                                    "Name": "$i.$DOMAIN_NAME",
                                    "Type": "A",
                                    "TTL": 300,
                                 "ResourceRecords": [{ "Value": "$IP_ADDRESS"}]
}}]
}
'