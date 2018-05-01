# AWS-Lambda

# start_server_with_ip_5X.py
Problem: Some servers(with IP addresses != 5*) are not accessible for RDP from a network.

Solution: The function will start the server(with specified instance ID) and if the public IP is not like 5* then stop the server and start it again until the IP address is like 5*.
Just enter the Instance ID and region.
Note: Give ec2 access to the lambda function
