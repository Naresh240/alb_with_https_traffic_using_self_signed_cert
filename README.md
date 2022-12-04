# spring-boot-hello
## Pre-requisites:
  - Run springboot application in server
  
## Create ALB under aws with two target group one with 80

![image](https://user-images.githubusercontent.com/58024415/205478316-7a268e75-3f0a-4c39-8906-07beb0c14735.png)

## Create ALB

![image](https://user-images.githubusercontent.com/58024415/205478347-84c06371-a3a7-4b40-a9be-32c77458754b.png)

## Create Self Signed Certificate

A self-signed SSL certificate is an SSL Certificate that is issued by the person creating it rather than a trusted certificate authority. This can be good for testing environments.

## Step 1: Generate a CA private key
```bash
openssl genrsa -out ca.key 2048
```

## Step 2: Create a self-signed certificate, valid for 365 days
```bash
openssl req -x509 \
  -new -nodes  \
  -days 365 \
  -key ca.key \
  -out ca.crt \
  -subj "/CN=*.us-east-1.elb.amazonaws.com"
```

## Open AWS ACM --> Import certificate
* Please copy contents of ```ca.crt``` to “Certificate body” and contents of ```ca.key``` to “Certificate private key”. 
* Please keep “Certificate chain” empty and click “Next” button

![image](https://user-images.githubusercontent.com/58024415/205475310-106d32d6-c47c-41c6-b1ba-5fa2665850a3.png)

* Certificate creation

![image](https://user-images.githubusercontent.com/58024415/205478545-32842a72-46ac-46c1-9185-b85505bf1346.png)


## Attach Listeners to port 443 and ACM

![image](https://user-images.githubusercontent.com/58024415/205478487-93807953-1d99-4620-9b71-8c032eba5599.png)

## Check Application output

![image](https://user-images.githubusercontent.com/58024415/205478569-834b262f-5621-43c9-b393-4eac366a9caf.png)
