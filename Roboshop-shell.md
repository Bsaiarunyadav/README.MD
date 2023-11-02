Here we will create the ROBOSHOP Using the shellscript.

Our main point is that to :- 

    1) create a instance 
    2) update the route53 


>>    As we already we already know that we should run it will root access and to check whether the script was success full or not we write validations

The script will be 

    DATE=$(date +%F)
    LOGSDIR=/tmp
    SCRIPT_NAME=$0
    LOGFILE=$LOGSDIR/$0-$DATE.log
    USERID=$(id -u)
    R="\e[31m"
    N="\e[0m"
    Y="\e[33m"
    G="\e[32m"


    if [ $USERID -ne 0 ];
    then 
        echo -e "$R ERROR :: Run this script with root access $N"
        exit 1
    fi

    VALIDATE(){
        if [ $1 -ne 0 ];
        then 
            echo -e "$2 ... $R FAILURE $N"
        else
            echo -e "$2 ... $G SUCCESS $N"
        fi
    }



##### Mongodb.sh :-


        cp Mongodb.repo /etc/yum.repos.d/Mongodb.repo &>> $LOGFILE

        VALIDATE $? "Copied MongoDB repo into yum.repos.d"

        yum install mongodb-org -y &>> $LOGFILE

        VALIDATE $? "Installation of MongoDB"

        systemctl enable mongod &>> $LOGFILE

        VALIDATE $? "Enabling MongoDB"

        systemctl start mongod &>> $LOGFILE

        VALIDATE $? "Starting MongoDB"

        sed -i 's/127.0.0.1/0.0.0.0/' /etc/mongod.conf &>> $LOGFILE

        VALIDATE $? "Edited MongoDB conf"

        systemctl restart mongod &>> $LOGFILE

        VALIDATE $? "Restarting MonogoDB"

Setup repo file as we can't edit after.

> And add the repo configuration in to that file.

##### Mongodb.repo

        [mongodb-org-4.2]
        name=MongoDB Repository
        baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/4.2/x86_64/
        gpgcheck=0
        enabled=1




> As it fails at installation step ... There are 2 possibilities for failing at this step.

. make sure mongodb repo file is properly copied...
. go to /etc/yum.repos.d folder location from terminal and verify mongodb.repo exists or not.
. if exists, then open it and cross check with file in git repo if something is added or removed by mistake.
. also files names are case sensitive.... just cross check whether the repofile is mongodb.repo or Mongodb.repo
. You can also open log file and see whats the exact issue...
    
    
    SYNTAX :- LOG_FILE=/tmp/$SCRIPT_NAME-$DATE.log 

    COMMAND :-  tail -f /tmp/mongodb.sh-2023-10-06.log





# CATALOGUE.SH



username="roboshop"

directory="/app"







