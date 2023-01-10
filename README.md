# Devops-Projects-3-AWS-Lift-and-Shift


![image](https://user-images.githubusercontent.com/96833570/211544752-3a0a22db-c310-42ec-8e87-a627181fdc04.png)




## BACKEND STACK SETUP


![image](https://user-images.githubusercontent.com/96833570/211214592-65776762-545c-47de-a8b9-b8a505beacc1.png)



![image](https://user-images.githubusercontent.com/96833570/211188366-037f728d-9edb-4352-95ef-22d3ed09c93d.png)



### Db Setup

`cat /var/lib/cloud/instances/${instance-id}/user-data.txt`

![image](https://user-images.githubusercontent.com/96833570/211167718-987c7ea0-0b39-4009-9830-439de8aac1dc.png)


### Memcached setup


![image](https://user-images.githubusercontent.com/96833570/211188094-a2d20862-bccd-4cbc-8474-a24102662e10.png)

![image](https://user-images.githubusercontent.com/96833570/211188244-843bc717-798e-47ce-880f-7bf39abe696a.png)

### Rabbitmq setup

![image](https://user-images.githubusercontent.com/96833570/211188312-82b811fa-29fe-4193-a2f4-32901962249c.png)

![image](https://user-images.githubusercontent.com/96833570/211188323-322c5571-5bce-4db1-9614-c320e61c2c06.png)


## Updating private ip addresses of the servers in Route53

![image](https://user-images.githubusercontent.com/96833570/211204890-a88a7525-db8c-4316-b738-2015a42642d8.png)


![image](https://user-images.githubusercontent.com/96833570/211213304-22002b86-19b1-4465-a076-13f6f167ade8.png)


## Building the artifact locally

Now build the artifact locally and store it in S3 bucket. Then we will download this to our tomcat app server.


`choco install jdk8`

`choco install maven -y`

`choco install awscli -y`

### Configuring aws cli/iam user with full s3 access

Credentials are important. 
I deleted these users and creds after completion of these projects. 
Please don't expose your credentials on your repos or anywhere public. 


![image](https://user-images.githubusercontent.com/96833570/211206531-684484ef-914e-4329-b903-4f8683c4a961.png)



`mvn install`


Let's create a bucket and copy our artifact:

```
aws s3 mb s3://devops-projects-artifact-st
aws s3 cp vprofile-v2.war s3://devops-projects-artifact-st/vprofile-v2.war

```

### Creating and attaching an IAM role for tomcat app service

We want to able to download the war file on our app server. 


![image](https://user-images.githubusercontent.com/96833570/211214669-bb1022bf-2d21-4192-8180-2a06ad478a76.png)

![image](https://user-images.githubusercontent.com/96833570/211214687-53e13359-36a6-4bea-9d74-ee668b3677e3.png)

## Setup App Server

`curl http://169.254.169.254/latest/user-data`

![image](https://user-images.githubusercontent.com/96833570/211541247-ac0a48b5-c85a-4aa1-a338-386fa545425b.png)

![image](https://user-images.githubusercontent.com/96833570/211541319-f8ab2e42-12b6-492f-a9d0-fd88fe369a3e.png)


We need to delete default app on tomcat8 and download our war file from s3.

![image](https://user-images.githubusercontent.com/96833570/211214822-adc3793b-1bf5-439c-a95a-a0e7981ef7e8.png)

```
sudo -i
apt install awscli -y
systemctl stop tomcat
cd /var/lib/tomcat8/webapps/
rm -rf ROOT
aws s3 ls
aws s3 cp s3://devops-projects-artifact-st/devops-project.war /tmp/
cd /tmp/
cp devops-project.war /var/lib/tomcat8/webapps/ROOT.war
systemctl start tomcat8
cd /var/lib/tomcat8/webapps/ROOT/WEB-INF/classes
cat application.properties
```

We can check db connection via telnet:

![image](https://user-images.githubusercontent.com/96833570/211215351-c9110bb4-222a-4652-9bce-7c0b21faf313.png)




<hr>

## Setup load balancer and target groups

![image](https://user-images.githubusercontent.com/96833570/211546007-e20a6c56-4d28-4644-86ca-cf83908e3acd.png)




## Validation






https://user-images.githubusercontent.com/96833570/211554501-9cd28d3a-7cd1-4161-bd08-90f5e8954534.mp4





