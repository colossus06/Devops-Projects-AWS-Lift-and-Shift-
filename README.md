# Devops-Projects-3-AWS-Lift-and-Shift

## BACKEND STACK SETUP

![image](https://user-images.githubusercontent.com/96833570/211188261-eea8c42b-8046-45d8-9568-da55314393e9.png)



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


## Building the artifact locally

Now build the artifact locally and store it in S3 bucket. Then we will download this to our tomcat app server.


`choco install jdk8`

`choco install maven -y`

`choco install awscli -y`

### Configuring aws cli/iam user

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
