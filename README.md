# Automated Deployment of Hightly Available K3s cluster with MetalLB on VMware Vsphere


## What is needed
+ 6 virtual machines
  * Management VM (Terraform,Ansible playbooks, and kubectl commands will be run from here)
    + 4 cores
    + 8 GB Ram 
    + 80 GB HDD
  * 3 Control-Plane nodes (these will host the internal ETCD HA-cluster as well be the Master nodes for the k3s cluster)
    + 2 cores
    + 4 GB Ram 
    + 60 GB HDD
  * 2 Worker nodes (where the containers, pods, services, etc will be hosted)
    + 2 cores
    + 4 GB Ram 
    + 60 GB HDD
+ Optional


## How it works
+ Terraform - Deploys the virtual machines and configures their initial setup in vcenter.
+ Ansible - Runs playbooks against the configured VMs to install needed packages, and run k3s deploy on first master. Then, joins the other nodes to the k3s cluster
+ MetalLB acts as a load balancer to allow for deployed services in kubernetes to use a vip and be HA.
+ kubectl and other management done from Management VM for on-going development and deployments
