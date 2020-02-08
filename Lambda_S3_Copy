import json
import boto3
import os
from urllib.parse import unquote_plus

def lambda_handler(event, context):
    # TODO implement
    
    s3 = boto3.client('s3')

    for record in event['Records']:
        srcKey = unquote_plus(record['s3']['object']['key'])
        srcBucket = record['s3']['bucket']['name']
        print(record)
        print(srcKey)
        destBucket = os.environ['DESTINATION_BUCKET']
        print(destBucket)
        if(srcKey.endswith('/') and record['s3']['object']['size'] == 0):
            print('Object is not a file. Skipping execution...')
        else:
            try:
                print("Starting to copy...")
                copySource = {'Bucket': srcBucket, 'Key':srcKey}
            
                response = s3.copy_object(CopySource=copySource, Bucket=destBucket, Key=srcKey)
                
                print("Object {} successfully copied to destination bucket {}".format(srcKey, destBucket))
            except Exception as e:
               print("ERROR: ",e)
           