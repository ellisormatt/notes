- set up awscli
- install kubectl
- install kops
- 

S3 kope state bucket: kops-state-bucket-mellisor
domain: kubernetes.mattellisor.com

kops create cluster --name=kubernetes.mattellisor.com --state=s3://kops-state-bucket-mellisor --zones us-east-2 --node-count=2 --node-size=t2.micro --master-size=t2.micro --dns-zone=kubernetes.mattellisor.com


kops create cluster \
--name=kubernetes.mattellisor.com \
--state=s3://kops-state-bucket-mellisor \
--zones=us-east-2a \
--node-count=2 \
--node-size=t2.micro \
--master-size=t2.micro \
--dns-zone=kubernetes.mattellisor.com


--cloud=aws \