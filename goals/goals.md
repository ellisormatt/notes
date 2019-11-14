- set up Jenkins instance
- jenkins successfully build an app
- jenkins set to poll github every 5 mins
- kubernetes cluster created: 1 master, 1 node
- test deploy an app to kubernetes
- jenkins integration into kubernetes

nice to haves
- script/app that automates checking github IPs and adding them to a security group for Jenkins github webhook access
- jenkins github webhook setup



deploy process:
- git force pull git@github.com:ellisormatt/somewebsite.git
- 