# Kubernetesoncloud
Create instance in AWS 
Login to the host and issue the below commands
sudo apt update
sudo apt upgrade

Install the AWS CLI

![image](https://user-images.githubusercontent.com/18350432/116025865-157e7600-a617-11eb-9eff-366fe183f291.png)

install the unzip

![image](https://user-images.githubusercontent.com/18350432/116025967-49f23200-a617-11eb-8cf7-5ed6ca40e217.png)

![image](https://user-images.githubusercontent.com/18350432/116026120-a2c1ca80-a617-11eb-8583-8c73e79d6ddc.png)

Install the aws CLI package

![image](https://user-images.githubusercontent.com/18350432/116026168-c1c05c80-a617-11eb-96b3-fe0fcb221540.png)

![image](https://user-images.githubusercontent.com/18350432/116026282-fe8c5380-a617-11eb-86e8-a92bf39da7a3.png)

![image](https://user-images.githubusercontent.com/18350432/116026320-14017d80-a618-11eb-8b84-a1344709c31a.png)

Install python

![image](https://user-images.githubusercontent.com/18350432/116026401-4c08c080-a618-11eb-88d0-b5fba823c458.png)

Install kops official documentation link: https://kubernetes.io/docs/setup/production-environment/tools/kops/

![image](https://user-images.githubusercontent.com/18350432/116026475-778bab00-a618-11eb-9917-fa04d2f9491b.png)

change permission

![image](https://user-images.githubusercontent.com/18350432/116026686-ccc7bc80-a618-11eb-8d4c-413920512f4b.png)

move to usr/bin

![image](https://user-images.githubusercontent.com/18350432/116026741-e406aa00-a618-11eb-8da7-5271f644bedc.png)

Install kubectl

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

change permission for kubectl file
chmod +x kubectl

Create store exports

export KOPS_CLUSTER_NAME=kubek8
export KOPS_STATE_STORE=s3://demo.k8

check version of kubectl
kubectl version

Create s3 bucket
aws s3api <bucketname>

Create IAM role with the below permissions

![image](https://user-images.githubusercontent.com/18350432/116027232-ea495600-a619-11eb-9f30-3bd8f84a0635.png)

Create Route 53 hosted zone

clustername is same as hosted zone name
private hosted

Create keys

![image](https://user-images.githubusercontent.com/18350432/116027343-38f6f000-a61a-11eb-8bcd-c1da1a653827.png)

Create the kops config files

kops create cluster --state=${KOPS_STATE_STORE} --node-count=2 --master-size=t3.medium --node-size=t3.medium --zones=us-east-2a,us-east-2b --name=${KOPS_CLUSTER_NAME} --dns private --master-count 1

![image](https://user-images.githubusercontent.com/18350432/116027517-bae71900-a61a-11eb-86ef-253a66c92421.png)

EC2 hosts created by kops

![image](https://user-images.githubusercontent.com/18350432/116027656-0f8a9400-a61b-11eb-90d8-04e6ab21d3cd.png)

ssh to the master node

![image](https://user-images.githubusercontent.com/18350432/116027722-3a74e800-a61b-11eb-8b04-bef1c0593229.png)

To validate nodes running

![image](https://user-images.githubusercontent.com/18350432/116027779-5d9f9780-a61b-11eb-8642-ec554e9d7457.png)

create nginx deployment  yaml file in the master

ubuntu@ip-172-20-48-200:~$ kubectl create deployment ngindep --image=nginx --replicas=2 --dry-run=client -o yaml> nginx.yaml

run the yaml file

![image](https://user-images.githubusercontent.com/18350432/116027880-950e4400-a61b-11eb-9a9b-6f714daf2311.png)

see the status of the pods

![image](https://user-images.githubusercontent.com/18350432/116027936-b40cd600-a61b-11eb-9570-98362ce97af4.png)

Destroy the cluster

kops delete cluster --name=<clustername> --yes





