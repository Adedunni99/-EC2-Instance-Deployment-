1. EC2 Instance Deployment Runbook
   

    Goal:
   
    1. Launch a t3.micro EC2 instance (Amazon Linux 2023)
   
    2. Set up Apache web server via user-data
   
    3. Connect via EC2 Instance Connect
   
    4. Validate web page in browser
   
********A.  Launch Virtual Server (EC2)********
   
****Steps****

1. Log in to AWS Console –EC2 – Instances

2. Click Launch instance
   

    **Fill in the details**

   1. Name: My-instance

   2. AMI: Choose Amazon Linux 2023

   3. Instance type: Select t3.micro 

   4. Key pair: Existing keypair “dun-dun-doon 

   5. Network settings:

   6. llow SSH (port 22) and HTTP (port 80)
   7. 
![WhatsApp Image 2025-10-20 at 22 48 14](https://github.com/user-attachments/assets/bfddf981-a064-4eba-8f98-56a2e5c3fef8)

   8. Storage: Keep default (8 GiB)


****Install Apache using user-data script****

   1. Scroll to Advanced details – paste this in User data:

    #!/bin/bash
    yum update -y
    yum install -y httpd
    systemctl start httpd
    systemctl enable httpd
    echo "<h1>Welcome to my EC2 Web Server!</h1>" > /var/www/html/index.html
    
  2.  Click Launch Instance

  3.  Instance successfully launched
     
![WhatsApp Image 2025-10-20 at 22 48 49](https://github.com/user-attachments/assets/e22a63c2-6a48-47c0-923e-2b3c08a35178)



********B.  Connectivity Test********

   
   Connect to instance:
     
   1.  Go to EC2 > Instances
     
   2.  Select My-instance
     
   3  Click Connect
  
   4. Choose EC2 Instance Connect → Connect
      
![WhatsApp Image 2025-10-20 at 22 49 08](https://github.com/user-attachments/assets/e0ade91b-1988-4baa-99ab-cb2f6b08d590)


   6. Now connected to the instance!

   7. Test metadata access:

  Run this command:
    
     curl http://169.254.169.254/latest/meta-data/
     
![WhatsApp Image 2025-10-20 at 22 49 26](https://github.com/user-attachments/assets/37a72ec0-21e4-4720-9566-df26852ad17b)

********C.  Web Server Setup********

Apache was installed and started via the user-data script.


********D.  Content Validation********
   
  1.  In EC2 > Instances, copy the Public IPv4 address (3.82.21.239)
     
  Open browser

  2. Copy and paste this to the browser

    http://3.82.21.239
    
It will bring this:

Welcome to my EC2 Web Server!

![WhatsApp Image 2025-10-20 at 22 49 43](https://github.com/user-attachments/assets/f13e57ce-215f-4cd5-a688-deddeeee4634)




