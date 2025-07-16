# S3 Manager
Simple demo S3 web interface + infra code.
The interface lets you download & upload files from the bucket.

<img src="https://raw.githubusercontent.com/lfkdev/s3manager/master/Screenshot.png">

## Description
This demo will:
- Spawn EC2 Instance
- Spawn S3 Bucket
- Install Minikube (Cluster)
- Install Caddy (Balancer)
- Install S3 Manager (flask backend + bootstrap frontend)
- All needed Requirements

## Overview
Relevant Code: 
[S3 App](roles/lfk.s3_frontend/templates/app.py.j2)
[Frontend](roles/lfk.s3_frontend/files/frontend/static/index.html)

## Requirements:
Libs:
- python boto3

Ansible Roles:
- aarna-stream.kubectl
- caddy_ansible.caddy_ansible
- geerlingguy.docker

Ansible Collections:
- kubernetes.core
- amazon.aws

## Run
- Setup Ansbile Node
- Add Export vars on node (make sure IAM User has s3/ec2 perms)
```
export AWS_ACCESS_KEY=<key>
export AWS_SECRET_KEY=<key>
```
- Add DNS Entries & set them in Ansible
- Run Playbooks:
```shell
$ ansible-playbook s3_frontend_infra.yml -e first_start=true
$ ansible-playbook s3_frontend.yml -e first_start=true
```

## Techstack:
```
\o/ -> Domain -> Caddy(LB) -> Minikube -> Website -> API -> S3
```

## Initial provisioning:
```shell
Wednesday 16 July 2025  16:49:36 +0200 (0:00:01.266)       0:03:47.569 ******** 
=============================================================================== 
lfk.s3_frontend ------------------------------------------------------- 131.02s
geerlingguy.docker ----------------------------------------------------- 47.67s
caddy_ansible.caddy_ansible -------------------------------------------- 25.08s
gather_facts ------------------------------------------------------------ 9.43s
gantsign.minikube ------------------------------------------------------- 9.14s
aarna-stream.kubectl ---------------------------------------------------- 5.18s
```

## Other
"Would-be-Prod" TODO:
- Move build image to CI/CD & pull from there
- Split tasks into its own roles
- Rate limiter for S3 API
- Metrics/Alerts
- Logging

LLM Prompts used (only for js):
```
Create the JavaScript needed to connect @index.html with the backend which you can view in @app.py. 
Use a minimal approach. Do not explain anything. Do not use any comments in code. 
Do not create any lists. Do not explain anything. Create a properly formatted snippets the user can just copy over.
Do not recreate the full code for each answer.
```