# Lab 4: Configure High Availability in Your Amazon VPC 

## Objectives

After completing this lab, you should be able to do the following:
- Create an Amazon [EC2 Auto Scaling group](https://docs.aws.amazon.com/es_es/autoscaling/ec2/userguide/auto-scaling-groups.html) and register it with an [Application Load Balancer spanning across multiple Availability Zones](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/how-elastic-load-balancing-works.html#availability-zones).
- Create a highly available [Amazon Aurora database (DB) cluster](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.CreateInstance.html).
- Modify an [Aurora DB cluster to be highly available](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Concepts.AuroraHighAvailability.html).
- Modify an [Amazon Virtual Private Cloud (Amazon VPC) configuration to be highly available using redundant NAT gateways](https://www.google.com/search?udm=0&q=one+amazon+vpc+highly+available+using+redundant+NAT+gateways).
- Confirmed your database can perform a failover to a read replica instance.

{{ ![](https://github.com/user-attachments/assets/9270080d-58ae-414c-965f-2c042d48db0a) }} img1[^1]

## Diagram

```mermaidjs
graph TD
    subgraph "VPC"
        subgraph "Availability Zone 1"
            direction LR
            ps1[Public Subnet 1]
            pvs1[Private Subnet 1]
        end
        subgraph "Availability Zone 2"
            direction LR
            ps2[Public Subnet 2]
            pvs2[Private Subnet 2]
        end
        igw[Internet Gateway]
        nat1(NAT Gateway 1)
        nat2(NAT Gateway 2)

        igw --> nat1
        igw --> nat2

        nat1 --> pvs1
        nat2 --> pvs2
        igw --> ps1
        igw --> ps2
    end

```
<a href="https://mermaid.live/edit#pako:eNqVklFrwjAUhf9KuE8bVGmiXWseBqIwBmPIJnvQ7iG1UQNtWtJE58T_vqROZquDLU_JOd-996TpHhZFyoHCSrFyjabjWCK7KpMchRjeJqMYjmrLGW6YyFgiMqF3aFZIjvA56VYqFF9oUUj09NJ0ygrPJybJxAK9mkRyjfB7i9g4RIkN0_waw2X6x1jkP7FIKxa5jEXaschvscRqO3-UmitHPdiKLdudsZJpfPM8nJ4shG8bJmmYxJqN1qjTua97XFXJOe2o2nBftTnjJJPLLmWFr4nfZH1T8OyvI1KgWhnuQc5VztwR9g6KQa95zmOgdpvyJTOZdo9xsGUlk7OiyE-VqjCrNdAlyyp7MmVqbz0WzL7qD2IncjUqjNRAiV-3ALqHD6CDqEuw3w8HYe-uRyJMPNgB7eMujsJ-FAVBMPAjcvDgsx7pd6MwOHwB_oTYuw">
  <img
  style="
    display: block;
    margin: auto;
    width: 100%;"
  src="https://mermaid.ink/img/pako:eNqVklFrwjAUhf9KuE8bVGmiXWseBqIwBmPIJnvQ7iG1UQNtWtJE58T_vqROZquDLU_JOd-996TpHhZFyoHCSrFyjabjWCK7KpMchRjeJqMYjmrLGW6YyFgiMqF3aFZIjvA56VYqFF9oUUj09NJ0ygrPJybJxAK9mkRyjfB7i9g4RIkN0_waw2X6x1jkP7FIKxa5jEXaschvscRqO3-UmitHPdiKLdudsZJpfPM8nJ4shG8bJmmYxJqN1qjTua97XFXJOe2o2nBftTnjJJPLLmWFr4nfZH1T8OyvI1KgWhnuQc5VztwR9g6KQa95zmOgdpvyJTOZdo9xsGUlk7OiyE-VqjCrNdAlyyp7MmVqbz0WzL7qD2IncjUqjNRAiV-3ALqHD6CDqEuw3w8HYe-uRyJMPNgB7eMujsJ-FAVBMPAjcvDgsx7pd6MwOHwB_oTYuw?type=png"/>
</a>

## Resources
- AvailabilityZone1: `us-west-2a`
- AvailabilityZone2: `us-west-2b`
- InventoryAppSettingsPageURL: `http://Inventory-LB-1476728143.us-west-2.elb.amazonaws.com/settings.php`
- InventoryAppURL: `Inventory-LB-1476728143.us-west-2.elb.amazonaws.com`
- LabRegion: `us-west-2`

## Task 1: Inspect your existing lab environment
The following resources have been provisioned for you through AWS CloudFormation:
- An Amazon VPC
- Public and private subnets in two Availability Zones
- An internet gateway (not shown in the diagram) associated with the public subnets
- A NAT gateway in one of the public subnets
- An Application Load Balancer deployed across the two public subnets to receive and forward incoming application traffic
- An EC2 instance in one of the private subnets, running a basic inventory tracking application
- An Aurora DB cluster containing a single DB instance in one of the private subnets to store inventory data

[^1]: Preceding image depicts the initial architecture, it consists of a VPC to facilitate networking with Public and Private subnets. This initial architecture also depicts an Application Load Balancer (ALB) to be able to distribute the incoming traffic to multiple EC2 instances. In-order to tighten the security posture we have an EC2 instance (App server) and an instance of Amazon Aurora (relational database) provisioned in the Private subnet. To further enhance high-availability we will improvise this architecture with Auto-scaling groups and multi-AZ database cluster.

## Task 2: Create a launch template

## Task 3: Create an Auto Scaling group
## Task 4: Test the application
## Task 5: Test high availability of the application tier
## Task 6: Configure high availability of the database tier
## Task 7: Make the NAT gateway highly available
## Task 8: Force a failover of the Aurora database
