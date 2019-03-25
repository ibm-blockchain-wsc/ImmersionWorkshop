# Welcome to Marbles Connect-a-thon with IBM Blockchain Platform for IBM Cloud Private (IBP4ICP)

The goal of the lab is to give you hands on experience interacting with IBM Blockchain Platform for IBM Cloud Private (IBP4ICP). You will take on the role of an organization that is part of a larger Hyperledger Fabric blockchain consortium called the Marbles business network.

![Marbles Network](images/marbles_network_diagram.png)

All of the components in the above diagram reside within an IBM Cloud Private (ICP) Kubernetes cluster running on Linux on System Z. IBP4ICP packages the Hyperledger Fabric components (Certificate Authority, Orderer, Peer) into Kubernetes Helm charts for deployment and management. For more information on IBP4ICP, please visit the [official IBP4ICP documentation](https://cloud.ibm.com/docs/services/blockchain?topic=blockchain-ibp-icp-about#overview "IBP4ICP documentation").

This lab is broken into two parts. In the first part, you will interact with your deployed peer, and enable the Marbles front end application to connect to the marbles chaincode installed on your peer. In the second part, you will go through the process of enabling the Marbles application to deploy inside an ICP Kubernetes cluster. You will be able to transact marbles with the other lab participants who are all acting as their own organizations in the Marbles business network.

!!! note
    This lab runs on Linux on IBM Z systems in the IBM Washington Systems Center (WSC). In order to connect to this environment, you must use the CISCO AnyConnect client to establish a virtual private network (VPN) connection into the WSC network. You will be given connection information at the beginning of the lab.

!!! tip
    If you find any typos, errors, or just want to provide helpful feedback to make this lab better, please click on the GitHub icon in the lower left corner of this page to be taken to our GitHub repository, from where you can create an Issue to suggest a correction or improvement. Thanks for your feedback!

# Acknowledgements
* Latrell Freeman for providing us with the backbone automation scripts
* Dave Wakeman for providing guidance on using MkDocs to make this Github Pages site
* Thanks to the following people who helped us test out the labs: Steven Bodie, Kevin Breitenother, Victoria Coates, Jack Sykes, MacKenna Kelleher, Keziah Knopp, Jasmine Burgess, Barry Silliman, Austin Grice

# Authors
* Garrett Woodworth
* Jin VanStee

