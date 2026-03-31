# SciCat jobs - how to use them 

If you want to post a jobs, check the structure of the job's body. From swagger endpoints we see that there are 4 fields:

 * types (mandatory)
 * jobsParams (mandatory)
 * ownerUser
 * ownerGroup


## **jobTypes**

Possible values can be seen from the [example config file](https://github.com/SciCatProject/scicat-backend-next/blob/master/jobConfig.example.yaml):

1. jobType: template_job
2. jobType: archive
3. jobType: retrieve
4. jobType: public
5. jobType: email_demo
6. jobType: url_demo
7. jobType: rabbitmq_demo
8. jobType: switch_demo
9. jobType: validate_demo


## **actionTypes**

Per job one can execute several actions. There are these actionTypes:

1.  actionType: log
2.  actionType: validate
3.  actionType: rabbitmq
4.  actionType: url
5.  actionType: switch
6.  actionType: email
7.  actionType: error
