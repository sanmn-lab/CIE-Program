Verfication 1(Set up SystemD)

Verfication 2(Create Specific User[jump-host-user,dashboard-user,counting-user])

![image.png](attachment:7343a1e7-ff2a-4df6-a131-3c0e53902ced:image.png)

![image.png](attachment:75428063-f16e-4291-80e2-8ac4032a3bae:image.png)

Set dashboard-user for Dashboard-EC2

![image.png](attachment:ac651c5c-5232-4ff1-9e1e-28eac00dbcc9:image.png)

Set counting-user for Counting-EC2

![image.png](attachment:c307b6b8-17ca-4999-9cb6-ab0b7a0dbab4:image.png)

Change dashboard-user and counting-user

![image.png](attachment:53195dc3-8e6c-4cec-b9de-a3d9b512e064:image.png)


Verfication 3(ELB : LoadBalancer to Recover Single Point of Failure)

![image.png](attachment:63682fdf-3671-4e41-93a0-ac7fe33b81fe:image.png)

![image.png](attachment:1765b1ef-70fb-41af-8982-00f28c300507:image.png)


Set Permission

chmod 400 Dashboard-EC2-Key.pem

chmod 400 Counting-EC2-Key.pem

![image.png](attachment:1ffe4378-e7bb-4693-b404-2e962096ef91:image.png)



Install and unzip App

![image.png](attachment:fd8a1bf1-66fa-43b3-b961-3f59a71139e6:image.png)

![image.png](attachment:002ee934-a7a0-4978-9403-b88656c9869f:image.png)

![image.png](attachment:5ca9822e-db55-458f-8ec2-7fa182704a71:image.png)



Unhealthy ⇒ Healthy

![image.png](attachment:640617cd-3663-4856-81bb-eed950c7c5a6:image.png)

![image.png](attachment:4ba5e96a-ca56-4247-a416-c8495a5c6ae9:image.png)

![image.png](attachment:dd8f4e60-4784-4985-9adb-80f585eda554:image.png)
