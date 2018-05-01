#File: lambda_function.py
import boto3
import time
# Enter the region your instances are in. Include only the region without specifying Availability Zone; e.g., 'us-east-1'
region = 'Enter region'
# Enter your instances here: ex. ['X-XXXXXXXX', 'X-XXXXXXXX']

const_inst_id='instance_ID_of_the_server'
instances = [const_inst_id]

def start_server():
    ec2 = boto3.client('ec2', region_name=region)
    ec2.start_instances(InstanceIds=instances)
    #print 'starting your instances: ' + str(instances)

def stop_server():
    ec2 = boto3.client('ec2', region_name=region)
    ec2.stop_instances(InstanceIds=instances)
    #print 'stopping your instances: ' + str(instances)
    
def iterate_and_check():
    ec2 = boto3.client('ec2', region_name=region)
    response = ec2.describe_instances()
    for reservation in response["Reservations"]:
        for instance in reservation["Instances"]:        # This sample print will output entire Dictionary object
            try:
                pub_ip=instance["PublicIpAddress"]
            except:
                continue
                
            inst_id=instance["InstanceId"]
            if (inst_id==const_inst_id) and (pub_ip[0]!='5'):
                # "stop"
                stop_server()
                time.sleep(60)
                # "starting again"
                start_server()
                time.sleep(25)
                iterate_and_check()
                    

def lambda_handler(event, context):
    # "1st start"
    start_server()
    time.sleep(25)
    iterate_and_check()
