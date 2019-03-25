
Visual Studio Code Overview Lab
---

**Note: This is a rough draft of a lab right now, which means grammar is
optional now. I will fix this before the lab is ready for showtime :)**

Welcome to the Visual Studio Code (VSCode) Overview Lab. Throughout the
course of this lab experience you will see how impactful the VSCode
application and the IBM Blockchain Platform extension is when creating
your smart contract (chaincode). The first part (`part 1`) of this lab
is very basic and is meant to walk you through getting started with the
IBM Blockchain Platform extension. `Part 2` follows a tutorial called
`Commercial Paper` which will utilize the new application programming
model in Hyperledger Fabric version `1.4` - which is the first long term
support release of Hyperledger Fabric.

Speaking of Hyperledger Fabric, we will be using a locally deployed
Fabric whose components will run as Docker containers on your lab
workstation. If you want to deploy your smart contract to a production
environment, you can connect your IBM Blockchain Platform VSCode
extension to the IBM Blockchain Platform in the public IBM Cloud.
Furthermore, in the future you will be able to connect this to your IBM
Blockchain Platform running in IBM Cloud Private. This will empower you
and your company to write and test your smart contract within VSCode
before you deploy it into production. We might incorporate this
capability into the `Blockchain Immersion Workshop` later this year. To
keep abreast of all the updates to the workshop, check the workshop's
github page for updates.

We hope you enjoy this lab and please let us know if you run into an
issue or think something doesn't look right.

In this lab we will be using the following versions:

-   Visual Studio Code: 1.31.1
-   IBM Blockchain Platform Extension: 0.3.2
-   Hyperledger Fabric: v1.4

Special thanks to the following contributors to this lab:

-   Matthew Golby-Kirk
-   Matt Lucas
-   Dennis Miller
-   Jin VanStee
-   Barry Silliman
-   Garrett Woodworth
-   Austin Grice

Foreword: Why and the Benefits of VSCode and IBM Blockchain
===========================================================

One of the hurdles in getting started with blockchain is the creation
and testing of a smart contract or "chaincode." Before, you had to
package your smart contract, install it on your blockchain peer and then
instantiate the chaincode on the channel. Furthermore, you had to submit
transactions and hope that all of the lines of code you created simply
worked. This hassle created a lot of questions. For example, does the
smart contract even work before installing it on our blockchain network?
How do we know that our smart contract is good for all the participants
in our network? Does our smart contract have to abide by some legalities
that have been set in place by the state or federal government? These
questions, and many more, have to be answered when formulating our
blockchain network and creating the smart contract. What if we could
have an environment for testing our smart contract before it goes into
production? The IBM Blockchain Platform extension has been created to
assist users in developing, testing, and deploying smart contracts,
enabling users to connect to a local Hyperledger Fabric development
environment (what the lab today covers) to test smart contracts before
deploying them into a production environment (IBM Blockchain Platform
running in the cloud or within your own premises with IBM Blockchain
Platform on IBM Cloud Private).

Within VSCode, you can employ a series of commands to gain the maximum
benefit of your blockchain network. Over the course of this lab, we will
use quite a few of these commands. Below is a series of commands:

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

As you can see, these commands can do a lot. With the IBM Blockchain
Platform extension only being at version 0.3.2 (as of 3/12/2019), you
can expect the list of commands and features to evolve. If you think
there is a feature or enhancement that should be created, you can create
an issue here:

<https://github.com/IBM-Blockchain/blockchain-vscode-extension/issues>

Equally, if you want to stay on top of all the releases of the extension
and what updates came with each release, you can view that here:

<https://github.com/IBM-Blockchain/blockchain-vscode-extension/releases>
