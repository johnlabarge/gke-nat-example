# GKE Cluster routing internet traffic through basic NAT
This set of scripts creates a Google Cloud Container Engine cluster that 
routes all outbound internet traffic. Traffic heading for the kubernetes master is routed at a higher priority through the default internet gateway. 
through a NAT instance. 

#### How it works in a nutshell

1. Creates a network
2. Creates a subnet for the cluster 
3. Creates a subnet for the nat instance 
4. Creates a NAT compute instance 
5. Creates Firewall rules for NAT instance 
6. Creates the GKE cluster in the cluster's subnet created from step 2 with tag route-through-nat
7. Creates the route from the cluster to the master for instances with tag, route-through-nat
8. Creates the NAT route from the cluster to the NAT for all destinations at a lower priority than the master route above for instances with tag route-through-nat

#### Creating the cluster 

###### Prerequisites 

1. Updated gcloud sdk 
2. Updated kubectl cli
3. A Project in Google Cloud in which you want to deploy this cluster 
3. Authenticated to google cloud

###### Creating the network, subnets, nat, routes, firewall rules and gke cluster 

    $ git clone https://www.github.com/johnlabarge/gke-nat-example.git
    $ cd gke-nat-example
    $ ./create

This also runs a quick test for you by

1. installing curl on the machine 
2. curling a well known website 
3. copying the captured traffic (tcpdump) logs from the Nat computer to 
the local directory.

#### Deleting the Cluster
###### Deleting the network, subnets, nat, routes, firewall rules and gke cluster 

`$ ./delete`
