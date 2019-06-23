
#Welcome to the Visual Studio Code Lab

Welcome to the Visual Studio Code (VSCode) Overview Lab. Visual Studio Code, or VSCode for short, is a popular source code editor developed by Microsoft for Windows, Linux and macOS. It is freely available and it includes support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring. VSCode allows for extensions that add support for popular languages, themes, debuggers, and more. IBM has developed a VSCode extension called the IBM Blockchain Platform Extension to help users develop their smart contracts. 

Throughout this lab you will experience using VSCode and the IBM Blockchain Platform Extension for the creation of a smart contract (chaincode). The first part of this lab is very basic and is meant to walk you through the fundamentals of the IBM Blockchain Platform Extension. Part 2 follows a tutorial called Commercial Paper which will utilize the new application programming model in Hyperledger Fabric version 1.4 - which is the first long term
support release of Hyperledger Fabric.

Speaking of Hyperledger Fabric, in this lab we will be using a locally deployed Fabric runtime whose components will run as Docker containers on your lab workstation. 
You can also configure your IBM Blockchain Platform VSCode Extension to connect to multiple remote IBM Blockchain Platform environments (e.g., dev/test, staging, production). When you are ready to test your smart contract against a remote environment, 
you can connect your IBM Blockchain Platform VSCode
Extension to the IBM Blockchain Platform running in the public IBM Cloud or on your own premises. You will get to deploy onto your own premises (well, premises provided to you in our lab environment!) in tomorrow's lab. 

In this lab we will be using the following versions:

-   Visual Studio Code: 1.35.1
-   IBM Blockchain Platform Extension: 1.0.3
-   Hyperledger Fabric: v1.4.1

The Benefits of VSCode IBM Blockchain Platform Extension
===========================================================

One of the hurdles in getting started with blockchain is the difficulty around the creation and testing of smart contracts across various DevOps environments. The VSCode IBM Blockchain Platform Extension has been created to assist users in developing, testing, and deploying smart contracts, enabling users to connect to a local Hyperledger Fabric development environment (what the lab today covers) to test smart contracts before deploying them into various remote runtimes (IBM Blockchain Platform
running in the cloud or within your own premises with IBM Blockchain Platform on IBM Cloud Private).

Within VSCode, you can employ a series of commands to gain the maximum
benefit of your blockchain network. Over the course of this lab, we will
use many of these commands. Below is a list of commands:

| Command                               | Description                                                                       |
|---------------------------------------|-----------------------------------------------------------------------------------|
| Add Gateway                           | Add a Hyperledger Fabric instance gateway                                         |
| Add Identity To Wallet                | Add an identity to be used when connecting to a Hyperledger Fabric gateway        |
| Connect Via Gateway                   | Connect to a Hyperledger Fabric blockchain using a gateway                        |
| Create Smart Contract Project         | Create a new JavaScript or TypeScript smart contract project                      |
| Create Identity (register and enroll) | Create, register and enroll a new identity from the runtime certificate authority |
| Debug                                 | Debug a Smart Contract                                                            |
| Delete Gateway                        | Delete a Hyperledger Fabric instance gateway                                      |
| Delete Package                        | Delete a smart contract package                                                   |
| Disconnect From Gateway               | Disconnect from the blockchain gateway you're currently connected to              |
| Edit Gateway                          | Edit connection profile or wallet used for connecting to a blockchain gateway     |
| Export Connection Details             | Export connection details for the a Hyperledger Fabric instance                   |
| Export Package                        | Export an already-packaged smart contract package to use outside VSCode           |
| Generate Smart Contract Tests         | Create a functional level test file for instantiated smart contracts              |
| Import Package                        | Import a smart contract package                                                   |
| Install Smart Contract                | Install a smart contract package onto a peer                                      |
| Instantiate Smart Contract            | Instantiate an installed smart contract package onto a channel                    |
| Open Fabric Runtime Terminal          | Open a terminal with access to the Fabric runtime (peer CLI)                      |
| Package a Smart Contract Project      | Create a new smart contract package from a project in the Explorer                |
| Refresh Fabric Gateways               | Refresh the Fabric Gateways view                                                  |
| Refresh Smart Contract Packages       | Refresh the Smart Contract Packages view                                          |
| Restart Local Fabric Ops              | Refresh the Local Fabric Ops view                                                 |
| Start Fabric Runtime                  | Start a Hyperledger Fabric instance                                               |
| Stop Fabric Runtime                   | Stop a Hyperledger Fabric instance                                                |
| Submit Transaction                    | Submit a transaction to a smart contract                                          |
| Evaluate Transaction                  | Evaluate a smart contract transaction                                             |
| Teardown Fabric Runtime               | Teardown the local_fabric runtime (hard reset)                                    |
| Toggle Development Mode               | Toggle the Hyperledger Fabric instance development mode                           |
| Upgrade Smart Contract                | Upgrade an instantiated smart contract                                            |
| View Homepage                         | View the extensions homepage                                                      |

As you can see, these commands can do a lot. The IBM Blockchain
Platform Extension development team works hard to add to the list of available commands and features.
If you think there is a feature or enhancement that should be created, you can create
an issue here:

<https://github.com/IBM-Blockchain/blockchain-vscode-extension/issues>

Equally, if you want to stay on top of all the releases of the extension
and what updates came with each release, you can view that here:

<https://github.com/IBM-Blockchain/blockchain-vscode-extension/releases>

!!! tip
    If you find any typos, errors, or just want to provide helpful feedback to make this lab better, please click on the GitHub icon in the lower left corner of this page to be taken to our GitHub repository, from where you can create an Issue to suggest a correction or improvement. Thanks for your feedback!

# Acknowledgements
Special thanks to the following contributors to this lab:

* Matthew Golby-Kirk
* Matt Lucas
* Dennis Miller
* Jin VanStee
* Barry Silliman
* Garrett Woodworth

# Author
* Austin Grice
