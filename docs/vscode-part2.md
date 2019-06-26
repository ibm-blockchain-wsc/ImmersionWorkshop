Section 1: Commercial Paper Overview
====================================

This tutorial works with a sample commercial paper trading network
called `PaperNet`. Commercial paper is a type of unsecured lending in
the form of a "promissory note". The papers are normally issued by large
corporations to raise funds to meet short-term financial obligations at
a fixed rate of interest. Once issued at a fixed price, for a fixed
term, another company or bank will purchase them at a discount to the
face value and when the term is up, they will be redeemed for their face
value.

As an example, if a paper was issued at a face value of 10M USD for a
6-month term at 2% interest then it could be bought for 9.8M USD (10M less
2%) by another company or bank who is willing to bear the risk that the
issuer will not default. Once the term is up, then the paper could be
redeemed or sold back to the issuer for its full face value of 10M USD.
Between buying and redemption, the paper can be bought or sold between
different parties on a commercial paper market.

These three key steps of issue, buy and redeem are the main transactions
in a simplified commercial paper marketplace, which we will mirror in
our lab. We will see a commercial paper issued by a company called
MagnetoCorp and, once issued on the commercial paper blockchain network,
another company called DigiBank will first buy the paper and then redeem
it.

You'll act as a developer, end user, and administrator, within different
organizations, performing various steps designed to help you understand
what it's like to collaborate as two different organizations working
independently, but according to mutually agreed rules in a Hyperledger
Fabric network.

Below is an image of our PaperNet network. For our lab, we will create
Isabella who is with MagnetoCorp. Additionally, we will create Balaji
who is with DigiBank. Isabella will issue a paper for the network. The
paper will have an ID number, when it was issued, the maturity date, and
the face value in USD. Balaji, from DigiBank, will then buy the paper and
then eventually redeem it.

![image](vscode-images/papernet_overview.png)

Below is the full breakdown of Part 2 of this lab:

-   Setting the Stage
    :      Based off of Part 1, we have started a blockchain network,
            created a smart contract, created and run tests and then
            submitted transactions. For Part 2, we need to create a
            couple more docker containers that will set us up for
            success for the rest of the lab. One of these containers
            will just monitor the docker network we are operating in. If
            you have no idea what a docker network is, I will explain
            later on. The other container contains Hyperledger Fabric
            tools and is named cliMagnetoCorp, as MagnetoCorp will use
            the Hyperledger Fabric command line interface (cli) within
            this container.

-   Install and Instantiate Smart Contract
    :      Now that we have those new docker containers up and running,
            we will enter our cliMagnetoCorp container and install and
            instantiate our smart contract. Since we are connected to
            the same running local Hyperledger Fabric network, we will
            see the smart contract show up in VSCode.

-   Issue Identities and Submit Transactions
    :      In this section, we will issue two identities. One is an
            end-user named Isabella with MagnetoCorp. She will invoke a
            transaction that will issue a paper. Then we will issue an
            identity for DigiBank named Balaji. Balaji will act as the
            adminstrator for DigiBank and will buy and redeem the paper
            that Isabella issued. Balaji is important in this lab, as we
            will add a Fabric Gateway connection to connect to his
            perspective of the network.

-   Create Fabric Gateways and Submit Transactions
    :      In this section we will create gateways that allows VSCode to
            connect to a running Hyperledger Fabric or IBM Blockchain
            Platform instance through a connection profile. In this lab,
            we will connect to our `local_fabric` network, which is also
            the Papernet network. We will create two gateways and
            associate our identities to these gateways. That way we can
            ensure the appropriate people are making the transactions
            they should.
            
-   Lab Cleanup
    :      This is the most bittersweet part of the entire lab. It means that this lab portion is over and we have to clean up. If you have kids (I don't), I'd imagine their faces are sad and full of despair when you (the guardian) tell them to clean up their mess. I'd also like to imagine your face is making a similar expression when we get to this lab. It's okay, more fun is going to be had soon - very soon!      

-   Loopback APIs
    :      We have proven that we can submit transactions through the
            command line interface (CLI) and the VSCode user interface.
            In this section, we will deploy two loopback API
            applications (for each of our organizations) and submit
            transactions through loopback. We will also include some
            transactions through the CLI and VSCode.

Section 2: Setting the Stage
============================

**1.** Navigate to your Desktop and then do a git clone of a repository
to gather all the things you need to run through this tutorial :

    tecadmin@ubuntubase:~$ cd Desktop/
    tecadmin@ubuntubase:~/Desktop$ ls -l
    total 0
    drwxr-xr-x  16 tecadmin  tecadmin  512 Jun 11 12:34 Kale
    tecadmin@ubuntubase:~/Desktop$ git clone https://github.com/austingrice/fabric-samples-cp.git
    Cloning into 'fabric-samples-cp'...
    remote: Enumerating objects: 85, done.
    remote: Counting objects: 100% (85/85), done.
    remote: Compressing objects: 100% (71/71), done.
    remote: Total 2658 (delta 26), reused 71 (delta 13), pack-reused 2573
    Receiving objects: 100% (2658/2658), 927.08 KiB | 0 bytes/s, done.
    Resolving deltas: 100% (1293/1293), done.
    tecadmin@ubuntubase:~/Desktop$ ls -l
    total 0
    drwxr-xr-x  22 tecadmin  tecadmin  704 Jun 11 12:41 fabric-samples-cp
    drwxr-xr-x  16 tecadmin  tecadmin  512 Jun 11 12:34 Kale

**2.** Then, do a `docker network list` to see all the running Docker
networks :

    tecadmin@ubuntubase:~/Desktop$ docker network list
    NETWORK ID          NAME                            DRIVER              SCOPE
    ad2e1a3e2fc2        bridge                          bridge              local
    35837170ae5b        fabricvscodelocalfabric_basic   bridge              local
    c5e0411b0d34        host                            host                local
    42ffa501f2f9        none                            null                local

**3.** The network we are operating out of is the
`fabricvscodelocalfabric_basic` network. You can see that by entering
the following command below :

    tecadmin@ubuntubase:~/Desktop$ docker network inspect fabricvscodelocalfabric_basic

That command will show you all the containers running in this network.
In a nutshell, docker networks are natural ways to isolate containers
from other containers or other networks. Having containers within a
network allows them to communicate with other containers in the same
network.

**4.** Within VSCode, go to the `Explorer` perspective and click on
`File` and select `Add Folder to Workplace..`. This will allow us to
work from an Untitled Workplace, but have the `fabric-samples-cp` folder
in there.

**5.** Within VSCode, navigate to the folder below within MagnetoCorp :

    fabric-samples-cp -> commercial-paper -> organizations -> magnetocorp -> configuration -> cli

You will see two files in there. One file is `monitordocker.sh` that
will produce log messages across the network that you specify it to look
at. If you click on this file to open it up, you'll see the file is
called to look at the `fabricvscodelocalfabric_basic` Docker network.
The other file is `docker-compose.yml`, which pulls down a
`fabric-tools` container that is connected to our local network. When we
spun up our `local_fabric` network, back in Part 1, it placed all the
cryptographic material in our
`/home/tecadmin/.fabric-vscode/crypto-config/` directory. It is then
taking all the crypto material and placing it in our fabric-tools
container. This will make more sense once we install and instantiate the
smart contract from this container instead of VSCode.

**6.** Now from the terminal navigate to the cli directory within
MagnetoCorp. **NOTE:** scroll over to see the entire command below :

    tecadmin@ubuntubase:~/Desktop$ cd fabric-samples-cp/commercial-paper/organization/magnetocorp/configuration/cli/
    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/magnetocorp/configuration/cli/$ ls -l
    total 16
    -rw-r--r--  1 tecadmin  tecadmin  1168 Jun 11 12:41 docker-compose.yml
    -rwxr-xr-x  1 tecadmin  tecadmin   751 Jun 11 12:44 monitordocker.sh

**7.** From here, we can actually start the `monitordocker.sh` script by
entering the command below. **NOTE:** scroll over to see the entire
command below :

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/magnetocorp/configuration/cli/$ ./monitordocker.sh fabricvscodelocalfabric_basic
    #

**8.** Since this terminal is occupied with log messages, let's open
another terminal tab. We can open a new tab by clicking on `File` and
then selecting `New Tab`

**9.** When you opened a new tab, you should have been taken to the same
file path that you were in on the previous tab. Now that we have a
command line ready, go ahead and enter the command below that will
create a `cliMagnetoCorp` container for our docker network to use.
**NOTE:** scroll over to see the entire command below :

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/magnetocorp/configuration/cli/$ docker-compose -f docker-compose.yml up -d cliMagnetoCorp
    .
    . # We'll see docker messages
    .
    Status: Downloaded newer image for hyperledger/fabric-tools:latest
    Creating cliMagnetoCorp ... 
    Creating cliMagnetoCorp ... done

![image](vscode-images/papernet_magnetocorp.png)

When we first install the smart contract, we will go through the
cliMagnetoCorp container, which is our Administrator Console. This will
allow us to use Fabric peer commands.

**10.** We can also do a `docker ps -a` command to see all of our docker
containers. We should see two new containers - `cliMagnetoCorp` and
`logspout` from steps 9 and 10.

**11.** Equally, we could do
`docker network inspect fabricvscodelocalfabric_basic` to see all of our
containers together in one network - and no, not in a blockchain
network. They are, however, the components that make up our local
blockchain network :-)

Section 3: Install and Instantiate Commercial Paper Smart Contract
==================================================================

Before we actually install the commercial paper smart contract, let's
actually open the file to see what the smart contract is trying to do.

**1.** From your explorer perspective within VSCode, navigate from the
`fabric-samples-cp` folder to the contract folder of MagnetoCorp :

    fabric-samples-cp -> commercial-paper -> organization -> magnetocorp -> contract

Within the lib folder, you'll see 3 javascript (.js) files in there.
Click on the papercontract.js file, which will open it within VSCode

![image](vscode-images/2-2-1.png)

Let's dissect our papercontract.js file as it is our smart contract. We
will only go over the issue transaction, but the other transactions
follow pretty closely to this one

Below, these 2 lines of code bring into scope two key Hyperledger Fabric
classes that will be used extensively by the smart contract --
`Contract and Context` :

    // Fabric smart contract classes
    const { Contract, Context } = require('fabric-contract-api');

Below, we define the smart contract class `CommercialPaperContract`
based on the built-in Fabric Contract class. The methods which implement
the key transactions to issue, buy and redeem commercial paper are
defined within this class :

    /**
    * Define commercial paper smart contract by extending Fabric Contract class
    *
    */
    class CommercialPaperContract extends Contract {

Below, this method defines the commercial paper `issue` transaction for
the commercial paper blockchain network. The parameters that are passed
to this method will be used to create the new commercial paper. Locate
and examine the buy and redeem transactions within the smart contract :

    /**
    * Issue commercial paper
    *
    * @param {Context} ctx the transaction context
    * @param {String} issuer commercial paper issuer
    * @param {Integer} paperNumber paper number for this issuer
    * @param {String} issueDateTime paper issue date
    * @param {String} maturityDateTime paper maturity date
    * @param {Integer} faceValue face value of paper
    */
    async issue(ctx, issuer, paperNumber, issueDateTime, maturityDateTime, faceValue) {

Within the `issue` transaction, this statement creates a new commercial
paper in memory using the CommercialPaper class with the supplied
transaction inputs. Examine the buy, get paper and redeem transactions
to see how they similarly use this class :

    // create an instance of the paper
    let paper = CommercialPaper.createInstance(issuer, paperNumber, issueDateTime, maturityDateTime, faceValue);

Below, this statement adds the new commercial paper to the ledger using
`ctx.paperList`, an instance of a PaperList class that was created when
the smart contract context CommercialPaperContext was initialized.
Again, examine the buy and redeem methods to see how they use this class
:

    // Add the paper to the list of all similar commercial papers in the ledger world state
    await ctx.paperList.addPaper(paper);

Below you will find that this statement returns a binary buffer as
response from the issue transaction for processing by the caller of the
smart contract :

    // Must return a serialized paper to caller of smart contract
    return paper.toBuffer();

**2.** Now that we have an understanding of the smart contract, let's
actually install it on our peer through our terminal application.
**NOTE:** scroll over to see the entire command below :

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/magnetocorp/configuration/cli/$ docker exec cliMagnetoCorp peer chaincode install -n papercontract -v 0 -p /opt/gopath/src/github.com/contract -l node
    2019-06-11 17:48:23.721 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 001 Using default escc
    2019-06-11 17:48:23.721 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 002 Using default vscc
    2019-06-11 17:48:23.862 UTC [chaincodeCmd] install -> INFO 003 Installed remotely response:<status:200 payload:"OK" >

A message saying 200 is a great sign to see.

If you notice, we are not in the contract folder of our command line
interface. Instead, we are entering the `cliMagnetoCorp` docker
container with `docker exec cliMagnetoCorp` and navigating to the
`/opt/gopath/src/github.com/contract` file path within our container to
grab the files we need to install the smart contract. The
`-n papercontract` flag names our smart contract papercontract. The
`-v 0` gives our smart contract a version of 0. Finally, the `-l node`
tells us that the language of our smart contract is nodejs. The picture
below goes into detail, visually, as to how we are actually installing a
copy of the commercial paper smart contract on our peer.

![image](vscode-images/papernet_magnetoinstall.png)

**3.** Since our network is connected to our VSCode instance, you can
refresh the `Local Fabric Ops panel` in VSCode under the
`IBM Blockchain Extension`. The refresh button (`unclosed circle icon`)
is revealed when you hover your mouse over the Local Fabric Ops panel

![image](vscode-images/2-2-3.png)

**4.** Since we have installed the smart contract, we should actually
make it active by instantiating it. **NOTE:** scroll over to see the
entire command below :

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/magnetocorp/configuration/cli/$ docker exec cliMagnetoCorp peer chaincode instantiate -n papercontract -v 0 -l node -c '{"Args":["org.papernet.commercialpaper:instantiate"]}' -C mychannel -P ""
    2019-06-11 17:50:34.673 UTC [chaincodeCmd] InitCmdFactory -> INFO 001 Retrieved channel (mychannel) orderer endpoint:   orderer.example.com:17050
    2019-06-11 17:50:34.675 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 002 Using default escc
    2019-06-11 17:50:34.675 UTC [chaincodeCmd] checkChaincodeCmdParams -> INFO 003 Using default vscc
    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/magnetocorp/configuration/cli/$

As you can see in the image below, we are instantiating a copy of the
commercial paper smart contract on our MagnetoCorp peer. Similar to the
installation of the smart contract, the instantiation goes into the
`cliMagnetoCorp` container. After successfully instantiating the smart
contract, there will be a commercial paper smart contract docker image
and container.

![image](vscode-images/papernet_magnetoinstant.png)

**5.** You will know our instantiate command worked when we get our
command prompt back without any error messages. You can really verify it
worked by going back to the VSCode and refreshing the Local Fabric Ops
panel and you should see it under the instantiate section.

![image](vscode-images/2-2-5.png)

Section 4: Create Identities and Submit Transactions
====================================================

Now that we have a ready-to-use smart contract, let's issue some
identities so that those identities can invoke and query transactions.

**1.** You should be within the cli folder of the MagnetoCorp folder.
You can confirm this by issuing the command below. **NOTE:** scroll over
to see the entire command below :

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/magnetocorp/configuration/cli/$ pwd
    /home/tecadmin/Desktop/fabric-samples-cp/commercial-paper/organization/magnetocorp/configuration/cli
    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/magnetocorp/configuration/cli/$ 

**2.** This is a good sign. Issue the following command below to get to
the application folder within MagnetoCorp. **NOTE:** scroll over to see
the entire command below :

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/magnetocorp/configuration/cli/$ cd ../../application/
    tecadmin@ubuntubase:~/Desktop/fabric-samples/commercial-paper/organization/magnetocorp/application$

**3.** Within VSCode, navigate to the same folder :

    fabric-samples-cp -> commercial-paper -> organization -> magnetocorp -> appplication

**4.** In that folder, you should see a file called `addtoWallet.js`.
Go ahead and click on it to open it up.

**5.** On line 25, you should see what is below :

    const key = fs.readFileSync(path.join(credPath, '/msp/keystore/<PUT_PRIVATE_KEY_HERE>')).toString();

**6.** To put in the file name of your actual private key, you can enter the command below
in your terminal application to find the key's file name. **NOTE:** scroll over
to see the entire command below :

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/magnetocorp/application$ ls -l /home/tecadmin/.fabric-vscode/runtime/crypto-config/peerOrganizations/org1.example.com/users/User1@org1.example.com/msp/keystore/
    -rw-------@ 1 tecadmin  tecadmin  241 Jun 11 08:57 e7a117b799890646fe1d6e688d9c979845a411830400b673e2fe7dc01f91f9b8_sk

**7.** Now, copy your private key's file name,
`e7a117b799890646fe1d6e688d9c979845a411830400b673e2fe7dc01f91f9b8_sk` in this example- but your name will differ- 
and paste it in the field asking for your private key. For example, line 25
looks like this now. **NOTE:** scroll over to see the entire key file name below:

    const key = fs.readFileSync(path.join(credPath, '/msp/keystore/e7a117b799890646fe1d6e688d9c979845a411830400b673e2fe7dc01f91f9b8_sk')).toString(); 

**NOTE:** It is of the upmost importance that you are doing this from the
`magnetocorp/application` folder and you save this file. We will do the
DigiBank folder here in a second.

**8.** Go ahead and save this file by either doing `File -> Save` or
`Control + s`.

**9.** Back in your terminal application, you can enter the command
below to install some dependencies. **NOTE:** scroll over to see the
entire command below :

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/magnetocorp/application$ npm install 
    .
    . # A bunch of output, with some of the output repeating
    .
    node-pre-gyp WARN Using request for node-pre-gyp https download 
    [grpc] Success: "/home/tecadmin/Desktop/fabric-samples/commercial-paper/organization/magnetocorp/application/node_modules/grpc/src/node/extension_binary/node-v57-darwin-x64-unknown/grpc_node.node" is installed via remote
    npm notice created a lockfile as package-lock.json. You should commit this file.
    npm WARN nodejs@1.0.0 No description
    npm WARN nodejs@1.0.0 No repository field.

    added 318 packages in 36.994s

**10.** Since we are in our command line, let's issue the following
command that will create Isabella. **NOTE:** scroll over to see the
entire command below :

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/magnetocorp/application$ node addToWallet.js 
    done

**11.** We will know it worked if we can execute the following command
successfully. **NOTE:** scroll over to see the entire command below :

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/magnetocorp/application$ ls -l ../identity/user/isabella/wallet/
    total 0
    drwxr-xr-x  5 tecadmin  tecadmin  160 Jun 11 12:53 User1@org1.example.com
    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/magnetocorp/application$ ls -l ../identity/user/isabella/wallet/User1@org1.example.com/
    total 24
    -rw-r--r--  1 tecadmin  tecadmin  1037 Jun 11 12:53 User1@org1.example.com
    -rw-r--r--  1 tecadmin  tecadmin   246 Jun 11 12:53 e7a117b799890646fe1d6e688d9c979845a411830400b673e2fe7dc01f91f9b8-priv
    -rw-r--r--  1 tecadmin  tecadmin   182 Jun 11 12:53 e7a117b799890646fe1d6e688d9c979845a411830400b673e2fe7dc01f91f9b8-pub

Keys are vital to understanding how transactions and identity work
within a blockchain network. Below is a breakdown of the keys and
certificate used in this example:

-   a **private key** `e7a117b799...-priv` used to sign transactions on
    Isabella's behalf, but not distributed outside of her immediate
    control
-   a **public key** `e7a117b799...-pub` which is cryptographically
    linked to Isabella's private key. This public key is contained
    within Isabella's X.509 certificate
-   a **certificate** `User1@org.example.com` which contains Isabella's
    public key and other X.509 attributes added by the Certificate
    Authority at certificate creation. This certificate is distributed
    to the network so that different actors at different times can
    cryptographically verify information signed by Isabella's private
    key

**12.** Before we submit our first transaction, let's go over it below.
You can find the code by clicking on `issue.js` within the
`magnetocorp/application` folder in VSCode.

Below we bring two key Hyperledger Fabric SDK classes into scope --
`Wallet and Gateway`. Because Isabella's X.509 certificate is in the
local file system, the application uses FileSystemWallet :

    // Bring key classes into scope, most importantly Fabric SDK network class 
    const { FileSystemWallet, Gateway } = require('fabric-network');

Below, this line is very important. Because we are connecting to our
local\_fabric we started at the beginning of Part 1, the crypto material
is stored under the .fabric-vscode/runtime folder. This is important for
grabbing our unique private key:

    const fixtures = path.resolve(__dirname, '/home/tecadmin/.fabric-vscode/runtime');

Below, this statement identifies that the application will use
Isabella's wallet when it connects to the blockchain network channel.
The application will select a particular identity within Isabella's
wallet. (The wallet must have been loaded with Isabella's X.509
certificate -- that's what addToWallet.js does):

    // A wallet stores a collection of identities for use 
    const wallet = new FileSystemWallet('../identity/user/isabella/wallet');

This line of code, below, connects to the network using the gateway
identified by connectionProfile, using the identity referred to in
connectionOptions. See how `../gateway/networkConnection.yaml` and
`User1@org1.example.com` are used for these values respectively:

    // Connect to gateway using application specified parameters 
    await gateway.connect(connectionProfile, connectionOptions);

Below in the couple lines of code, the application connects to the
network channel `mychannel`, where the papercontract was previously
instantiated. If you had a different channel name, you would have to
modify this line of code:

    // Access commercial paper network 
    const network = await gateway.getNetwork('mychannel');

Below, this statement gives the application addressability to the smart
contract defined by the namespace `org.papernet.commercialpaper` within
`papercontract`. Once an application has issued `getContract`, it can
submit any transaction implemented within it:

    // Get addressability to commercial paper contract 
    const contract = await network.getContract('papercontract', 'org.papernet.comm...');

Below, these lines of code submit a transaction to the network using the
issue transaction defined within the smart contract.
`MagnetoCorp, 00001` are the values to be used by the issue transaction
to create a new commercial paper:

    // issue commercial paper 
    const issueResponse = await contract.submitTransaction('issue','MagnetoCorp', '00001', '2020-05-31', '2020-11-30','5000000');

This statement, below, processes the response from the issue
transaction. The response needs to be deserialized from a buffer into
paper, a CommercialPaper object which can be interpreted correctly by
the application:

    // process response let paper =
    CommercialPaper.fromBuffer(issueResponse);

**13.** Now that we have Isabella from MagnetoCorp, let's perform the
issue transaction from our terminal. **NOTE:** scroll over to see the
entire command below:

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/magnetocorp/application$ node issue.js
    Connect to Fabric gateway.
    Use network channel: mychannel.
    Use org.papernet.commercialpaper smart contract.
    Submit commercial paper issue transaction.
    2019-02-22T17:55:20.631Z - info: [TransactionEventHandler]: _strategySuccess: strategy success for transaction "f8e124886d6cb84434cb6a996f4889145c0541199c88bab7d4d85ae41266e51e"
    Process issue transaction response.
    MagnetoCorp commercial paper : 00001 successfully issued for value 5000000
    Transaction complete.
    Disconnect from Fabric gateway.
    Issue program complete.

This successfully committed a transaction to the ledger. See how it
outputted a transaction hash for us. You can look at our
`monitoring docker` terminal tab as well.

As you can see in the image below, we are using the certificate
belonging to Isabella to submit our paper issue transaction. Once we
verify that Isabella can submit a transaction (via her certificate), the
gateway allows the application to focus on transaction generation,
submission and response. It coordinates the transaction proposal,
ordering and notification processing between the different network
components.

![image](vscode-images/papernet_magnetoissue.png)

**14.** Since we have created an identity for MagnetoCorp, let's also
create Balaji from DigiBank. To do so, we will need a third command line
tab. We can add another command line tab by clicking on
`File -> New Tab.` This will create a new tab in the terminal from the
exact folder directory we were in from our second command line tab. This
third tab will act as DigiBank.

**15.** We now need to switch to a new directory, specifically the
application folder of DigiBank. **NOTE:** scroll over to see the entire
command below:

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/magnetocorp/application$ cd ../../digibank/application/
    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/digibank/application$

**16.** Within VSCode, navigate to the application folder of DigiBank :

    fabric-samples-cp -> commercial-paper -> organization -> digibank -> application

**17.** Similarly, you will see `<PUT_PRIVATE_KEY_HERE>` in the
`addtoWallet.js` file within the `application` folder. On line 25, you
should see what is below :

    const key = fs.readFileSync(path.join(credPath, '/msp/keystore/<PUT_PRIVATE_KEY_HERE>')).toString();

**18.** To put in an actual private keys's file name, you can enter the command below
in your terminal application to find the key's file name. **NOTE:** scroll over
to see the entire key below:

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/digibank/application$ ls -l /home/tecadmin/.fabric-vscode/runtime/crypto-config/peerOrganizations/org1.example.com/users/Admin@org1.example.com/msp/keystore/
    -rw-------@ 1 tecadmin  tecadmin  241 Jun 11 08:57 4fd5a19cad827af71cf356d629f95c41f77e27db09d268a3c72aabdaead43737_sk

**19.** Now, copy your private key's file name,
`4fd5a19cad827af71cf356d629f95c41f77e27db09d268a3c72aabdaead43737_sk` in our example- yours will differ- 
and paste in the field asking for your private key. For example, line 25
looks like this now. **NOTE:** scroll over to see the entire file name below:

    const key = fs.readFileSync(path.join(credPath, '/msp/keystore/4fd5a19cad827af71cf356d629f95c41f77e27db09d268a3c72aabdaead43737_sk')).toString(); 

**NOTE:** It is of the upmost importance that you are doing this from the
`digibank/application` folder and you save this file.

**20.** Now we can install some dependencies that are required to create
our identity. To do this, enter the command that is below. **NOTE:**
scroll over to see the entire command below :

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/digibank/application$ npm install 
    .
    . # A bunch of output, with some of the output repeating
    .
    node-pre-gyp WARN Using request for node-pre-gyp https download 
    [grpc] Success: "/home/tecadmin/Desktop/fabric-samples/commercial-paper/organization/magnetocorp/application/node_modules/grpc/src/node/extension_binary/node-v57-darwin-x64-unknown/grpc_node.node" is installed via remote
    npm notice created a lockfile as package-lock.json. You should commit this file.
    npm WARN nodejs@1.0.0 No description
    npm WARN nodejs@1.0.0 No repository field.

    added 318 packages in 36.994s

**21.** Since we are in our command line, let's issue the following
command that will create Balaji. **NOTE:** scroll over to see the
entire command below:

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/digibank/application$ node addToWallet.js 
    done

**22.** We will know it worked if we can execute the following command
successfully. **NOTE:** scroll over to see the entire command below :

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/digibank/application$ ls -l ../identity/user/balaji/wallet/
    total 0
    drwxr-xr-x  5 tecadmin  tecadmin  160 Jun 11 12:53 Admin@org1.example.com
    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/digibank/application$ ls -l ../identity/user/balaji/wallet/Admin@org1.example.com/
    total 24
    -rw-r--r--  1 tecadmin  tecadmin  1037 Jun 11 12:53 User1@org1.example.com
    -rw-r--r--  1 tecadmin  tecadmin   246 Jun 11 12:53 4fd5a19cad827af71cf356d629f95c41f77e27db09d268a3c72aabdaead43737-priv
    -rw-r--r--  1 tecadmin  tecadmin   182 Jun 11 12:53 4fd5a19cad827af71cf356d629f95c41f77e27db09d268a3c72aabdaead43737-pub

Based on the picture below, we now have 2 participants in this network.
Obviously, this is MagnetoCorp (Isabella) and DigiBank (Balaji). Both
participants are allowed to interact with the commercial paper
blockchain network through their application.

![image](vscode-images/papernet_magnetodigi.png)

**23.** Since we have issued a paper from Isabella, let's go ahead and
submit a couple of transactions from Balaji and DigiBank. Go ahead and
get the latest status of our paper by entering the command below.
**NOTE:** scroll over to see the entire command below:

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/digibank/application$ node getPaper.js
    Connect to Fabric gateway.
    Use network channel: mychannel.
    Use org.papernet.commercialpaper smart contract.
    Submit commercial paper getPaper transaction.
    Process getPaper transaction response.
     +--------- Paper Retrieved ---------+ 
     | Paper number: "00001"
     | Paper is owned by: "MagnetoCorp"
     | Paper is currently: "ISSUED"
     | Paper face value: "5000000"
     | Paper is issued by: "MagnetoCorp"
     | Paper issue on: "2020-05-31"
     | Paper matures on: "2020-11-30"
     +-----------------------------------+ 
    Transaction complete.
    Disconnect from Fabric gateway.
    getPaper program complete.

**24.** Now that we know the current status of our `00001` paper,
let's go ahead and buy and redeem the paper by entering the command
below. **NOTE:** scroll over to see the entire command below :

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/digibank/application$ node buy.js
    Connect to Fabric gateway.
    Use network channel: mychannel.
    Use org.papernet.commercialpaper smart contract.
    Submit commercial paper buy transaction.
    2019-02-28T19:52:17.372Z - info: [TransactionEventHandler]: _strategySuccess: strategy success for transaction "871e7743c58e406575d4e553330faae3711c0a65a2f677b6e6d398650069d81a"
    Process buy transaction response.
    MagnetoCorp commercial paper : 00001 successfully purchased by DigiBank
    Transaction complete.
    Disconnect from Fabric gateway.
    Buy program complete.

**25.** We can finish the cycle of paper `00001` by doing a redeem
transaction. The command is below. **NOTE:** scroll over to see the
entire command below :

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/digibank/application$ node redeem.js 
    Connect to Fabric gateway.
    Use network channel: mychannel.
    Use org.papernet.commercialpaper smart contract.
    Submit commercial paper redeem transaction.
    2019-02-28T19:52:46.452Z - info: [TransactionEventHandler]: _strategySuccess: strategy success for transaction "c26ecbf1077d99a5ea025c339ffabd88eb22cf4e6ac5ff8d9b570cd6c38eb531"
    Process redeem transaction response.
    MagnetoCorp commercial paper : 00001 successfully redeemed with MagnetoCorp
    Transaction complete.
    Disconnect from Fabric gateway.
    Redeem program complete

**26.** To confirm that we actually redeemed the paper, you can do a
`getPaper` transaction to see that it was, indeed, redeemed. **NOTE:**
scroll over to see the entire command below :

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/digibank/application$ node getPaper.js
    Connect to Fabric gateway.
    Use network channel: mychannel.
    Use org.papernet.commercialpaper smart contract.
    Submit commercial paper getPaper transaction.
    Process getPaper transaction response.
    +--------- Paper Retrieved ---------+ 
    | Paper number: "00001"
    | Paper is owned by: "MagnetoCorp"
    | Paper is currently: "REDEEMED"
    | Paper face value: "5000000"
    | Paper is issued by: "MagnetoCorp"
    | Paper issue on: "2020-05-31"
    | Paper matures on: "2020-11-30"
    +-----------------------------------+ 
    Transaction complete.
    Disconnect from Fabric gateway.
    getPaper program complete

Now, we have run through the full lifecycle of one paper through the
command line interface (CLI). In the following sections we will use a
mixture of the CLI, the VSCode user interface, and a loopback API service
application.

Section 5: Create Fabric Gateways and Submit Transactions
=========================================================

In the previous section, we created two identities -
`Isabella and Balaji` - and then completed a full lifecycle of one paper.
Let's create a fabric gateway for Isabella and Balaji and then submit
some more transactions.

**1.** Within VSCode, go to the IBM Blockchain Platform Extension. One
of the sections you'll see is called `Fabric Gateways`. If you click on
the gear icon in the bottom left, select `Command Palette..`. You'll be
given a prompt and you can enter this command below :

    >IBM Blockchain Platform: Add Gateway

**2.** For our first Gateway, let's create MagnetoCorp. So when it
prompts you for: `Enter a name for the gateway` enter the following
below :

    MagnetoCorp

**3.** Then it will prompt you for a path to the connection profile.
Click on browse and it will open a file window. Navigate to the path
below and select `networkConnection.yaml`. **NOTE:** scroll over to see
the entire file path below :

    Desktop -> fabric-samples-cp -> commercial-paper -> organization -> magnetocorp -> gateway -> networkConnection.yaml
    .

**4.** Then it will place that new gateway in the `Fabric Gateway`
section within the IBM Blockchain Platform Extension. Now that we have a
gateway, we need to create an identity to use this gateway. To do this,
hover your cursor over the `Fabric Wallets` section of the extension.
There you'll see a `+` icon. Click on that `+` icon to add a wallet.

**5.** Then it will prompt you: `Choose a method to add a wallet` and
for that select `Specify an existing file system wallet`. We are
selecting this because we already have added Isabella as an identity and
she has a wallet folder.

**6.** Then it will prompt you: `Enter file path to a wallet directory`
and then select `Browse`. It will then pop-up a file window. From there,
you can navigate to the following path below. **NOTE:** scroll over to
see the entire file path below:

    Desktop -> fabric-samples-cp -> commercial-paper -> organization -> magnetocorp -> identity -> user -> isabella -> wallet
    .

Once you have selected `wallet`, click on `select` to choose this
option. Then it will add a wallet, called `wallet`, to our
`Fabric Wallets` section of the extension.

**7.** Once you see the wallet called `wallet` in the `Fabric Wallet`
section, go ahead and right click on `wallet`. How many times can you
say `wallet` in a sentence. From there, select `Edit Wallet` and it will
open a `settings.json` file with your wallet name and wallet path
highlighted. Go ahead and **only** change the `wallet name` to
`MagnetoCorpWallet`. Look below to see the example:

    "name": "wallet",
    "walletPath": "/home/tecadmin/Desktop/fabric-samples-cp/commercial-paper/organization/magnetocorp/identity/user/isabella/wallet"

    ---- CHANGE TO -----

    "name": "MagnetoCorpWallet",
    "walletPath": "/home/tecadmin/Desktop/fabric-samples-cp/commercial-paper/organization/magnetocorp/identity/user/isabella/wallet"

**8.** Once you have made that change, go ahead and save this file by
doing a `File -> Save` or `Control + S`. Also - leave this file open as
we will want to change the name for DigiBank once we create their
wallet.

**9.** Speaking of DigiBank, we now need to do the same process for
them. So click on the gear icon in the bottom left, select
`Command Palette..`. You'll be given a prompt and you can enter this
command below:

    >IBM Blockchain Platform: Add Gateway

**10.** For our second Gateway, let's create DigiBank. So when it
prompts you for: `Enter a name for the gateway` enter the following
below:

    DigiBank

**11.** Then it will prompt you for a path to the connection profile.
Click on browse and it will open a file window. Navigate to the path
below and select `networkConnection.yaml`. **NOTE:** scroll over to see
the entire file path below:

    Desktop -> fabric-samples-cp -> commercial-paper -> organization -> digibank -> gateway -> networkConnection.yaml
    .

**12.** Then it will place that new gateway in the `Fabric Gateway`
section within the IBM Blockchain Platform Extension. Now that we have a
gateway, we need to create an identity to use this gateway. To do this,
hover your cursor over the `Fabric Wallets` section of the extension.
There you'll see a `+` icon. Click on that `+` icon to add a wallet.

**13.** Then it will prompt you: `Choose a method to add a wallet` and
for that select `Specify an existing file system wallet`. We are
selecting this because we already have added Isabella as an identity and
she has a wallet folder.

**14.** Then it will prompt you: `Enter file path to a wallet directory`
and then select `Browse`. It will then pop-up a file window. From there,
you can navigate to the following path below. **NOTE:** scroll over to
see the entire file path below:

    Desktop -> fabric-samples-cp -> commercial-paper -> organization -> digibank -> identity -> user -> balaji -> wallet
    .

Once you have selected `wallet`, click on `select` to choose this
option. Then it will add a wallet, called `wallet`, to our
`Fabric Wallets` section of the extension.

**15.** Once you see the wallet called `wallet` in the `Fabric Wallet`
section, go ahead and right click on `wallet`. From there, select
`Edit Wallet` and it will open a `settings.json` file with your wallet
name and wallet path highlighted. Go ahead and **only** change the
`wallet name` to `DigiBankWallet`. Look below to see the example:

    "name": "wallet",
    "walletPath": "/home/tecadmin/Desktop/fabric-samples-cp/commercial-paper/organization/digibank/identity/user/balaji/wallet"

    ---- CHANGE TO -----

    "name": "DigiBankWallet",
    "walletPath": "/home/tecadmin/Desktop/fabric-samples-cp/commercial-paper/organization/digibank/identity/user/balaji/wallet"

**16.** Once you have made that change, go ahead and save this file by
doing a `File -> Save` or `Control + S`. Now within your
`Fabric Wallets` section, you should have `MagnetCorpWallet` and
`DigiBankWallet` as our two custom wallets.

**17.** Now that we have two wallets, we can associate our wallets to
our two gateways. To do this `right click` on `MagnetoCorp` within the
`Fabric Gateways` section. Then select `Associate A Wallet`. Then it
will prompt you for which wallet to associate with this gateway. You
will want to select `MagnetoCorpWallet`.

What this does is when you connect with a specific gateway, it will
automatically use that wallet you associated it with. For example,
whenever you click on MagnetoCorp within the `Fabric Gateway` section,
it will automatically use the `MagnetoCorpWallet` wallet without
prompting you.

**18.** Do the same thing for DigiBank. `Right click` on `DigiBank`
within the `Fabric Gateways` section. Then select `Associate A Wallet`.
Then it will prompt you for which wallet to associate with this gateway.
You will want to select `DigiBankWallet`.

**19.** To confirm that we have done this successfully, you can click on
both gateways. You'll see the identities it is using once you connect to
a specific gateway. To disconnect from a gateway, there is a `door` in
the `Fabric Gateways` section in which you can click on to leave.

![image](vscode-images/2-4-19.1.png)

![image](vscode-images/2-4-19.2.png)

**20.** Now that we have our gateways figured out, let's do another
lifecycle of a commercial paper. To do this, we need to do an `issue`
transaction. First click on the `MagnetoCorp` gateway and untoggle till
you see the transactions within the `papercontract@0`. From there,
`right click` on the `issue` transaction and select
`Submit Transaction`. Within the brackets, place the text below:

    "MagnetoCorp", "00002", "2020-05-31", "2020-11-30", "5000000"

You can hit enter again to bypass the next prompt asking for transient
data. That will execute the transaction and issue paper `00002`

**21.** To make sure we are all operating on the same paper number, we
need to change a few files. I have broken down the files we need to
change below within VSCode in the Editor perspective.

From `digibank/application` folder, within the `getPaper.js` file
on line `68`:

    const getPaperResponse = await contract.evaluateTransaction('getPaper', 'MagnetoCorp', '00001');

    ---- CHANGE TO ----

    const getPaperResponse = await contract.evaluateTransaction('getPaper', 'MagnetoCorp', '00002');

**Make sure you save this file.**

From `` `digibank/application `` folder, within the `redeem.js` file on
line `67`:

    const redeemResponse = await contract.submitTransaction('redeem', 'MagnetoCorp', '00001', 'DigiBank', '2020-11-30');

    ---- CHANGE TO ----

    const redeemResponse = await contract.submitTransaction('redeem', 'MagnetoCorp', '00002', 'DigiBank', '2020-11-30');

**Make sure you save this file.**

**22.** Now we can execute more transactions. First, jump back to the
CLI and do a `getPaper.js` transaction. Below you will see what the
command is to execute the transaction. **NOTE:** scroll over to see the entire command below:

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/digibank/application$ node getPaper.js
    Connect to Fabric gateway.
    Use network channel: mychannel.
    Use org.papernet.commercialpaper smart contract.
    Submit commercial paper getPaper transaction.
    Process getPaper transaction response.
     +--------- Paper Retrieved ---------+ 
     | Paper number: "00002"
     | Paper is owned by: "MagnetoCorp"
     | Paper is currently: "ISSUED"
     | Paper face value: "5000000"
     | Paper is issued by: "MagnetoCorp"
     | Paper issue on: "2020-05-31"
     | Paper matures on: "2020-11-30"
     +-----------------------------------+ 
    Transaction complete.
    Disconnect from Fabric gateway.
    getPaper program complete.

**23.** Within VSCode and the IBM Blockchain Platform, we can buy the
same paper. To do this, leave the `MagnetoCorp` gateway, and then click on the
`DigiBank` gateway.

**24.** Now, untoggle till you see the `buy` transaction within the
`papercontract@0` smart contract. From there, `right click` on the `buy`
transaction and select `Submit Transaction`. Once it gives you a prompt,
enter the text below between the brackets:

    "MagnetoCorp","00002","MagnetoCorp","DigiBank","4900000","2019-07-31"

Then hit `enter` to go to the next prompt. Hit `enter` once again to
bypass the transient data prompt. Then that will execute the `buy`
transaction.

**25.** To confirm that the transaction worked (other than the log
messages in the output window), we can do a `getPaper` transaction from
the CLI again. **NOTE:** scroll over to see the entire command below:

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/digibank/application$ node getPaper.js
    Connect to Fabric gateway.
    Use network channel: mychannel.
    Use org.papernet.commercialpaper smart contract.
    Submit commercial paper getPaper transaction.
    Process getPaper transaction response.
    +--------- Paper Retrieved ---------+ 
     | Paper number: "00002"
     | Paper is owned by: "DigiBank"
     | Paper is currently: "TRADING"
     | Paper face value: "5000000"
     | Paper is issued by: "MagnetoCorp"
     | Paper issue on: "2020-05-31"
     | Paper matures on: "2020-11-30"
     +-----------------------------------+ 
    Transaction complete.
    Disconnect from Fabric gateway.
    getPaper program complete.

**26.** From the same CLI, we can do a `redeem.js` transaction. **NOTE:** scroll over to see the entire command below:

    tecadmin@ubuntubase:~/Desktop/fabric-samples/commercial-paper/organization/digibank/application$ node redeem.js 
    Connect to Fabric gateway.
    Use network channel: mychannel.
    Use org.papernet.commercialpaper smart contract.
    Submit commercial paper redeem transaction.
    2019-02-28T19:52:46.452Z - info: [TransactionEventHandler]: _strategySuccess: strategy success for transaction "c26ecbf1077d99a5ea025c339ffabd88eb22cf4e6ac5ff8d9b570cd6c38eb531"
    Process redeem transaction response.
    MagnetoCorp commercial paper : 00002 successfully redeemed with MagnetoCorp
    Transaction complete.
    Disconnect from Fabric gateway.
    Redeem program complete.


**27.** Again, we can confirm that this was recorded by doing another
`getPaper.js` transaction. **NOTE:** scroll over to see the entire
command below:

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/digibank/application$ node getPaper.js
    Connect to Fabric gateway.
    Use network channel: mychannel.
    Use org.papernet.commercialpaper smart contract.
    Submit commercial paper getPaper transaction.
    Process getPaper transaction response.
     +--------- Paper Retrieved ---------+ 
     | Paper number: "00002"
     | Paper is owned by: "MagnetoCorp"
     | Paper is currently: "REDEEMED"
     | Paper face value: "5000000"
     | Paper is issued by: "MagnetoCorp"
     | Paper issue on: "2020-05-31"
     | Paper matures on: "2020-11-30"
     +-----------------------------------+ 
    Transaction complete.
    Disconnect from Fabric gateway.
    getPaper program complete.


Section 6: Lab Clean-Up
=========================================================

This lab has run its course, but now it is time to clean up. Don't worry, this is a very short section! 

**1.** Entering the following commands to stop and remove our docker containers. Then we can remove the images as well. Look at the following commands below
::

    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/digibank/application$ docker stop $(docker ps -a -q)
    *
    *
    * Docker container IDs
    *
    *
    tecadmin@ubuntubase:~/Desktop/fabric-samples-cp/commercial-paper/organization/digibank/application$ docker rm $(docker ps -a -q)
    *
    *
    * Docker container IDs
    
That's it!

