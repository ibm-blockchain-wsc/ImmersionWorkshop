Section 1: Lab Part 2 Overview
==============================

In this part of the lab, you will use the Hyperledger Fabric network that you
created in the Part 1 of the lab and configure the Marbles User Interface
(UI) web application so that it will integrate with the marbles
chaincode that you installed in the previous lab.

You will use two browser sessions to simulate acting as a user for each
of the two organizations in the network- *United Marbles* and *Marbles
Inc*.

Then you can explore the Marbles UI to execute chaincode transactions
and see some of the Hyperledger Fabric concepts in action.

Section 2: Marbles user interface setup
=======================================

**Step 2.1:** Switch to the *~/zmarbles/marblesUI* directory:

    bcuser@ubuntu18042:~/zmarbles$ cd ~/zmarbles/marblesUI
    bcuser@ubuntu18042:~/zmarbles/marblesUI$ 

**Step 2.2:** You will need to do an *npm install* to install the
packages needed by the Marbles user interface. First you will verify
that the *node\_modules* directory does not exist. This directory will
be created when you run an npm *install* in the next step, so right now
it shouldn't exist:

    bcuser@ubuntu18042:~/zmarbles/marblesUI$ ls -l node_modules
    ls: cannot access 'node_modules': No such file or directory
    bcuser@ubuntu18042:~/zmarbles/marblesUI$ 

**Step 2.3:** Now run the *npm install*:

    bcuser@ubuntu18042:~/zmarbles/marblesUI$ npm install
      .
      .  (output not shown here)
      .
    
    
**Step 2.4:** When this command ends, list the *node\_modules* directory
again. It is there now:

    bcuser@ubuntu18042:~/zmarbles/marblesUI$ ls -l node_modules
      .
      .  (output not shown here)
      .
    bcuser@ubuntu18042:~/zmarbles/marblesUI$
    
**Step 2.5:** Change to the *config* directory:

    bcuser@ubuntu18042:~/zmarbles/marblesUI$ cd config
    bcuser@ubuntu18042:~/zmarbles/marblesUI/config$ 

**Step 2.6:** There are four files in this directory:

    bcuser@ubuntu18042:~/zmarbles/marblesUI/config$ ls
    connection_profile1.json  connection_profile2.json  marbles1.json  marbles2.json
    bcuser@ubuntu18042:~/zmarbles/marblesUI/config$ 

**Step 2.7:** There are two files for the first fictitious company,
*United Marbles*, and two files for the second fictitious company,
*Marbles Inc.* Look at the *marbles1.json* file with the *cat* command:

    bcuser@ubuntu18042:~/zmarbles/marblesUI/config$ cat marbles1.json 
    {
        "cred_filename": "connection_profile1.json",
        "use_events": false,
        "keep_alive_secs": 120,
        "company": "United Marbles",
        "usernames": [
            "amy",
            "alice",
            "ava"
        ],
        "port": 3001,
        "last_startup_hash": ""
    }
    bcuser@ubuntu18042:~/zmarbles/marblesUI/config$ 
    
**Step 2.8:** Notice that this file points to one of the other existing
files, *connection\_profile1.json*, as the value of the *cred\_filename*
name/value pair. You will look at that in a moment. Take a note of the
usernames array- *amy*, *alice*, and *ava*. If you are comfortable with
the *vi* editor you could change those names to your favorite names if
you would like. You can also use the *sed* command to change the name
inline without entering *vi*. Here is an example of a command to change
the name *alice* to *vincent*. **This step is optional- you do not have
to do this is you prefer the name alice to vincent**:

    bcuser@ubuntu18042:~/zmarbles/marblesUI/config$ sed -i "s/alice/vincent/" marbles1.json   # optional
    bcuser@ubuntu18042:~/zmarbles/marblesUI/config$ 

**Step 2.9:** Here is the file after I changed *alice* to *vincent* with
the previous sed command:

    bcuser@ubuntu18042:~/zmarbles/marblesUI/config$ cat marbles1.json 
    {
        "cred_filename": "connection_profile1.json",
        "use_events": false,
        "keep_alive_secs": 120,
        "company": "United Marbles",
        "usernames": [
            "amy",
            "vincent",
            "ava"
        ],
        "port": 3001,
        "last_startup_hash": ""
    }
    bcuser@ubuntu18042:~/zmarbles/marblesUI/config$ 

**NOTE:** Your file will look different if you choose to skip the
optional *Step 2.9* or if you made changes other than the example change
I showed. The purpose of this step is to ensure that your file changed
the way you intended it to (if it changed at all).

The other key thing to note is the port number. It is *3001* here. In
the *marbles2.json* file for *Marbles Inc*, port *3002* will be
specified. This is how, later in this lab, you will pretend to be a user
of one company or the other- by using port 3001 in the URL to pretend to
be a "United Marbles" user and by using port 3002 in the URL to pretend
to be a "Marbles Inc" user.

**Step 2.10:** It is time to look at the main configuration file the
Marbles app uses. It is the file specified as the *cred\_filename* value
in the *marbles1.json* file. This name *cred\_filename* for the JSON
name/value pair and the filename, *blockchain\_creds1.json*, indicate
that security credentials are specified in this file, and they are, but
actually information about the Hyperledger Fabric network itself is
specified in this file as well. This file is too large to fit in one
screen, so I will teach you one more Linux command, named *more*. (Pun
intended). Type this:

    bcuser@ubuntu18042:~/zmarbles/marblesUI/config$ more connection_profile1.json
      .
      .  (output not shown)
      .
    bcuser@ubuntu18042:~/zmarbles/marblesUI/config$ 

This command will print as much of the file as it can on your screen but
will pause until you hit enter before displaying the rest of the file's
contents. Here are the complete contents of this file:

    {
       "name": "Docker Compose Network",
       "x-networkId": "not-important",
       "x-type": "hlfv1",
       "description": "Connection Profile for an IBM Blockchain Network",
       "version": "1.0.0",
       "client": {
           "organization": "Org0MSP"
       },
       "channels": {
           "mychannel": {
               "orderers": [
                   "fabric-orderer"
               ],
               "peers": {  
                   "fabric-peer-org1" : {
                                       "x-chaincode": {}
                                    }
               },
               "chaincodes": [
                   "marbles:v4"
               ],
               "x-blockDelay": 1000
           }
       },
       "organizations": {
           "Org0MSP": {
               "mspid": "Org0MSP",
               "peers": [
                   "fabric-peer-org1"
               ],
               "certificateAuthorities": [
                   "fabric-ca-org1"
               ]
           }
       },
       "orderers": {
           "fabric-orderer": {
               "url": "grpcs://localhost:7050",
               "grpcOptions": {
                   "ssl-target-name-override": "orderer.blockchain.com",
                   "grpc.http2.keepalive_time": 300,
                   "grpc.keepalive_time_ms": 300000,
                   "grpc.http2.keepalive_timeout": 35,
                   "grpc.keepalive_timeout_ms": 3500
               },
               "tlsCACerts": {
                   "path": "../../crypto-config/ordererOrganizations/blockchain.com/orderers/orderer.blockchain.com/tls/ca.crt"
               }
           }

       },
       "peers": {
           "fabric-peer-org1": {
               "url": "grpcs://localhost:7051",
               "eventUrl": "grpcs://localhost:7053",
               "grpcOptions": {
                   "ssl-target-name-override": "peer0.unitedmarbles.com",
                   "grpc.http2.keepalive_time": 300,
                   "grpc.keepalive_time_ms": 300000,
                   "grpc.http2.keepalive_timeout": 35,
                   "grpc.keepalive_timeout_ms": 3500
               },
               "tlsCACerts": {
                   "path": "../../crypto-config/peerOrganizations/unitedmarbles.com/peers/peer0.unitedmarbles.com/tls/ca.crt"
               }
           }
       },
       "certificateAuthorities": {
           "fabric-ca-org1": {
               "url": "https://localhost:7054",
               "httpOptions": {
                   "ssl-target-name-override": "ca.unitedmarbles.com",
                   "verify": true
               },
               "tlsCACerts": {
                   "path": "../../crypto-config/peerOrganizations/unitedmarbles.com/ca/ca.unitedmarbles.com-cert.pem"
               },
               "registrar": [
                   {
                       "enrollId": "admin",
                       "enrollSecret": "adminpw"
                   }
               ],
               "caName": "ca-org0"
           }
       }
    }

This is a standard Hyperledger Fabric connection profile. This lab does
not use Hyperledger Composer, but I think the Hyperledger Composer team
did a nice job describing Hyperledger Fabric connection profiles, as
they use them too. See
<https://hyperledger.github.io/composer/latest/reference/connectionprofile>
for their description. They also reference a link in the Hyperledger
Fabric Node.js SDK documentation at
<https://fabric-sdk-node.github.io/tutorial-network-config.html> which
is a little more advanced, and it describes the profile in YAML form
versus the JSON form that this Marbles demo app uses.

**IMPORTANT: if you used a channel name other than the default of
mychannel, you must change this value from mychannel to the value you
used.** Either use the *vi* editor if you are comfortable with that, or,
you could use *sed*. For example, here is a *sed* command, to change the
channel name from *mychannel* to *tim*, along with "before" and "after"
*grep* commands to show the changes **(These commands are examples and
only needed if you did not use the default channel name of mychannel)**

!!! warning
        This step is necessary only if you did not use this lab's default channel name of *mychannel*
        earlier in Part 1 of this lab. And of course, this example shows the steps for changing the
        channel name to *tim*, so tailor the command shown here according to whatever *non-default* 
        channel name you may have chosen.
```

    bcuser@ubuntu18042:~/zmarbles/marblesUI/config$ grep mychannel connection_profile[12].json 
    blockchain_creds1.json:            "channel_id": "mychannel",
    blockchain_creds2.json:            "channel_id": "mychannel", 
    bcuser@ubuntu18042:~/zmarbles/marblesUI/config$ sed -i "s/mychannel/tim/" connection_profile[12].json 
    bcuser@ubuntu18042:~/zmarbles/marblesUI/config$ grep -1 channels connection_profile[12].json 
    connection_profile1.json-  },
    connection_profile1.json:  "channels": {
    connection_profile1.json-      "tim": {
    --
    connection_profile2.json-  },
    connection_profile2.json:  "channels": {
    connection_profile2.json-      "tim": {
    bcuser@ubuntu18042:~/zmarbles/marblesUI/config$ 

```

**Step 2.11:** The considerations for *marbles2.json* and
*connection\_profile2.json* are the same as for *marbles1.json* and
*connection\_profile1.json* except that they apply to "Marbles Inc."
instead of "United Marbles". If you would like to compare the
differences between *connection\_profile1.json* and
*connection\_profile2.json*, try the *diff* command and observe its
output. This command lists sections of the two files that it finds
different. The lines from the first file, *blockchain\_creds1.json*,
start with '<' (added by the diff command output, not in the actual
file), and the lines from the second file, *blockchain\_creds2.json*,
start with '\>':

    bcuser@ubuntu18042:~/zmarbles/marblesUI/config$ diff connection_profile1.json connection_profile2.json 
    8c8
    < 		"organization": "Org0MSP"
    ---
    > 		"organization": "Org1MSP"
    16c16
    <  				"fabric-peer-org1" : {
    ---
    >  				"fabric-peer-org2" : {
    27,28c27,28
    < 		"Org0MSP": {
    < 			"mspid": "Org0MSP",
    ---
    > 		"Org1MSP": {
    > 			"mspid": "Org1MSP",
    30c30
    < 				"fabric-peer-org1"
    ---
    > 				"fabric-peer-org2"
    33c33
    < 				"fabric-ca-org1"
    ---
    > 				"fabric-ca-org2"
    54,56c54,56
    < 		"fabric-peer-org1": {
    < 			"url": "grpcs://localhost:7051",
    < 			"eventUrl": "grpcs://localhost:7053",
    ---
    > 		"fabric-peer-org2": {
    > 			"url": "grpcs://localhost:9051",
    > 			"eventUrl": "grpcs://localhost:9053",
    58c58
    < 				"ssl-target-name-override": "peer0.unitedmarbles.com",
    ---
    > 				"ssl-target-name-override": "peer0.marblesinc.com",
    65c65
    < 				"path": "../../crypto-config/peerOrganizations/unitedmarbles.com/peers/peer0.unitedmarbles.com/tls/ca.crt"
    ---
    > 				"path": "../../crypto-config/peerOrganizations/marblesinc.com/peers/peer0.marblesinc.com/tls/ca.crt"
    70,71c70,71
    < 		"fabric-ca-org1": {
    < 			"url": "https://localhost:7054",
    ---
    > 		"fabric-ca-org2": {
    > 			"url": "https://localhost:8054",
    73c73
    < 				"ssl-target-name-override": "ca.unitedmarbles.com",
    ---
    > 				"ssl-target-name-override": "ca.marblesinc.com",
    77c77
    < 				"path": "../../crypto-config/peerOrganizations/unitedmarbles.com/ca/ca.unitedmarbles.com-cert.pem"
    ---
    > 				"path": "../../crypto-config/peerOrganizations/marblesinc.com/ca/ca.marblesinc.com-cert.pem"
    81,82c81,82
    < 					"enrollId": "admin",
    < 					"enrollSecret": "adminpw"
    ---
    > 					"enrollId": "admin2",
    > 					"enrollSecret": "adminpw2"
    85c85
    < 			"caName": "ca-org0"
    ---
    > 			"caName": "ca-org1"
    bcuser@ubuntu18042:~/zmarbles/marblesUI/config$ 

Section 3: Start the Marbles user interface
===========================================

In this section, you will use the Marbles user interface. You will start
two browser sessions- one will be as a "United Marbles" user, and the
other as a "Marbles Inc" user. Here in this lab, you are serving both
companies' applications from the same server, so you will differentiate
between the two companies by the port number. You will connect to port
3001 when acting as a United Marbles user, and you will connect to port
3002 when acting as a Marbles Inc user. In the real world, each of the
two companies would probably either serve the user interface from their
own server, or perhaps both companies would log in to a server provided
by a service provider- think "Blockchain-as-a-service". The chosen
topology is use-case dependent and beyond the scope of this lab.

**Step 3.1:** You are now ready to start the server for UnitedMarbles.
Back up to the *~/zmarbles/marblesUI* directory:

    bcuser@ubuntu18042:~/zmarbles/marblesUI/config$ cd ..
    bcuser@ubuntu18042:~/zmarbles/marblesUI$ 

**Step 3.2:** You will now use *gulp* to start up the server, with this
command:

    bcuser@ubuntu18042:~/zmarbles/marblesUI$ gulp marbles1
    [16:02:03] Using gulpfile ~/zmarbles/marblesUI/gulpfile.js
    [16:02:03] Starting 'env_tls'...
    [16:02:03] Finished 'env_tls' after 50 μs
    [16:02:03] Starting 'build-sass'...
    [16:02:03] Finished 'build-sass' after 6.07 ms
    [16:02:03] Starting 'watch-sass'...
    [16:02:03] Finished 'watch-sass' after 6.36 ms
    [16:02:03] Starting 'watch-server'...
    [16:02:03] Finished 'watch-server' after 1.98 ms
    [16:02:03] Starting 'server'...
    info: Checking connection profile is done
    info: Loaded config file /home/bcuser/zmarbles/marblesUI/config/marbles1.json
    info: Loaded connection profile file /home/bcuser/zmarbles/marblesUI/config/connection_profile1.json



    Connection Profile Lib Functions:()
      getNetworkName()
      getNetworkCredFileName()
      buildTlsOpts()
      getFirstChannelId()
      getChannelId()
      loadPem()
      getMarblesField()
      getChaincodeId()
      getChaincodeVersion()
      getFirstCaName()
      getCA()
      getCasUrl()
      getAllCaUrls()
      getCaName()
      getCaTlsCertOpts()
      getEnrollObj()
      getFirstPeerName()
      getPeer()
      getPeersUrl()
      getAllPeerUrls()
      getPeerEventUrl()
      getPeerTlsCertOpts()
      getMarbleUsernamesConfig()
      getCompanyNameFromFile()
      getMarblesPort()
      getEventsSetting()
      getKeepAliveMs()
      getFirstOrdererName()
      getOrderer()
      getOrderersUrl()
      getOrdererTlsCertOpts()
      getBlockDelay()
      getKvsPath()
      getFirstOrg()
      getClientsOrgName()
      getClientOrg()
      getMarbleUsernames()
      getOrgsMSPid()
      getAdminPrivateKeyPEM()
      getAdminSignedCertPEM()


    ----------------------------------- Server Up - localhost:3001 -----------------------------------
    Welcome aboard:	 United Marbles
    Channel:	 mychannel
    Org:		 Org0MSP
    CA:		 fabric-ca-org1
    Orderer:	 fabric-orderer
    Peer:		 fabric-peer-org1
    Chaincode ID:	 marbles
    Chaincode Version:  v4
    ------------------------------------------ Websocket Up ------------------------------------------


    debug: loading pem from a path: /home/bcuser/zmarbles/crypto-config/peerOrganizations/unitedmarbles.com/ca/ca.unitedmarbles.com-cert.pem
    debug: loading pem from a path: /home/bcuser/zmarbles/crypto-config/ordererOrganizations/blockchain.com/orderers/orderer.blockchain.com/tls/ca.crt
    debug: loading pem from a path: /home/bcuser/zmarbles/crypto-config/peerOrganizations/unitedmarbles.com/peers/peer0.unitedmarbles.com/tls/ca.crt
    info: [fcw] Going to enroll peer_urls=[grpcs://localhost:7051], channel_id=mychannel, uuid=marblesDockerComposeNetworkmychannelOrg0MSPfabricpeerorg1, ca_url=https://localhost:7054, orderer_url=grpcs://localhost:7050, enroll_id=admin, enroll_secret=adminpw, msp_id=Org0MSP, kvs_path=/home/bcuser/.hfc-key-store/marblesDockerComposeNetworkmychannelOrg0MSPfabricpeerorg1
    debug: enroll id: "admin", secret: "adminpw"
    debug: msp_id:  Org0MSP ca_name: ca-org0
    info: [fcw] Successfully enrolled user 'admin'
    debug: added peer grpcs://localhost:7051
    debug: [fcw] Successfully got enrollment marblesDockerComposeNetworkmychannelOrg0MSPfabricpeerorg1
    info: Success enrolling admin
    debug: loading pem from a path: /home/bcuser/zmarbles/crypto-config/peerOrganizations/unitedmarbles.com/ca/ca.unitedmarbles.com-cert.pem
    debug: loading pem from a path: /home/bcuser/zmarbles/crypto-config/ordererOrganizations/blockchain.com/orderers/orderer.blockchain.com/tls/ca.crt
    debug: loading pem from a path: /home/bcuser/zmarbles/crypto-config/peerOrganizations/unitedmarbles.com/peers/peer0.unitedmarbles.com/tls/ca.crt
    debug: Checking if chaincode is already instantiated or not 1

    info: Checking for chaincode...
    debug: [fcw] Querying Chaincode: read()
    debug: [fcw] Sending query req: chaincodeId=marbles, fcn=read, args=[selftest], txId=null
    debug: [fcw] Peer Query Response - len: 1 type: number
    debug: [fcw] Successful query transaction.

    ----------------------------- Chaincode found on channel "mychannel" -----------------------------


    info: Checking chaincode and ui compatibility...
    debug: [fcw] Querying Chaincode: read()
    debug: [fcw] Sending query req: chaincodeId=marbles, fcn=read, args=[marbles_ui], txId=null
    warn: [fcw] warning - query resp is not json, might be okay: string 4.0.1
    debug: [fcw] Successful query transaction.
    info: Chaincode version is good
    info: Checking ledger for marble owners listed in the config file

    info: Fetching EVERYTHING...
    debug: [fcw] Querying Chaincode: read_everything()
    debug: [fcw] Sending query req: chaincodeId=marbles, fcn=read_everything, args=[], txId=null
    debug: [fcw] Peer Query Response - len: 529 type: object
    debug: [fcw] Successful query transaction.
    debug: This company has registered marble owners
    debug: Looking for marble owner: amy
    debug: Did not find marble username: amy
    info: We need to make marble owners


    - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
    info: Detected that we have NOT launched successfully yet
    debug: Open your browser to http://localhost:3001 and login as "admin" to initiate startup
    - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

The first line of the output just listed reads:

    [16:02:03] Using gulpfile ~/zmarbles/marblesUI/gulpfile.js
    
I am not going to go into detail on the *gulp* tool here, but if you are
curious, if you look into the *gulpfile.js* file (you would have to use
another PuTTY or SSH session as this one is now tied up) you would find
that a *marbles1* task (*marbles1* being your argument to the *gulp*
command) is defined:

    gulp.task('marbles1', ['env_tls', 'watch-sass', 'watch-server', 'server']);

The *marbles1* task specifies four more tasks to run, the first of which
is *env\_tls*. This task is adding a value to a map named *env*. This
value points to the *marbles1.json* file:

    gulp.task('env_tls', function () {
           env['creds_filename'] = 'marbles1.json';
    });

The last of the tasks, *server*, when it is started, is receiving this
map named *env* as part of its invocation:

    gulp.task('server', function(a, b) {
            if(node) node.kill();
            node = spawn('node', ['app.js'], {env: env, stdio: 'inherit'}); //command, file, options
    });

The syntax is a bit arcane, and this is not a course in JavaScript, but
there is a line in the main file for the server, *app.js*, that reads
this *creds\_filename* value:

    var cp = require(__dirname + '/utils/connection_profile_lib/index.js')(process.env.creds_filename, logger);

Then within *utils/connection\_profile\_lib/index.js* is where all the
magic, a.k.a. code, happens to make use of the values specified in that
file.

You did not need to know all this to run the application, but you might
need to know where to start looking when your boss asks you to tailor
the marbles application because she wants a return on the time and money
you spent taking this lab- assuming you don't get off the hook when you
tell her that nowhere was JavaScript mentioned on the agenda.

**Step 3.3:** Open up a web browser window or tab and point to
*http://<your\_IP\_goes\_here\>:3001*. Substitute your team's assigned 
IP address instead of *<your\_IP\_goes\_here\>*. 
You should see a window pop up that looks like this:

![image](images/lab3/2019-01-20_13-13-53_UserChoice.png)

**Step 3.4:** You are given a choice between *Express* and *Guided* for
setting up the demo. Don't short-change yourself- pick *Guided*,
you'll learn more. After you click *Guided*, you will see this:

![image](images/lab3/2019-01-20_13-18-31_GuidedStep1.png)

Read the text in the window to see what's going on.

**Step 3.5:** If you do not see *Step 1 Complete*, ask an instructor for
help. Otherwise, click *Next Step* and you should see this:

![image](images/lab3/2019-01-20_13-19-49_GuidedStep2.png)

Click the '+' sign if you wish to see the settings used to contact the
Fabric Certificate Authority.

**Step 3.6:** If you do not see *Step 2 Complete*, ask an instructor for
help. Otherwise, click *Next Step* and you should see this:

![image](images/lab3/2019-01-20_13-20-56_GuidedStep3.png)

Click the '+' sign to see information about your environment and your
marbles chaincode.

**Step 3.7:** If you do not see *Step 3 Complete*, ask an instructor for
help. Otherwise, click *Next Step* and you should see this:

![image](images/lab3/2019-01-20_13-22-12_GuidedStep4-010.png)

**Step 3.8:** Unlike the first three steps, which did not require
further input from you to complete, this step will not proceed until you
click the *Create* button. Before you do that you have an opportunity to
review and change the names that you use for new marbles owners in
addition to the owner named 'Barry' that should already exist (though
not evident from this screen) if you created it in the first part of
this lab.

Click the *Create* button when you are ready and after several seconds
you should see *Step 4 Complete* on the screen:

![image](images/lab3/2019-01-20_13-24-08_GuidedStep4-020.png)

**Step 3.9:** If you do not see *Step 4 Complete*, ask an instructor for
help. Otherwise, click *Next Step* and you should see this:

![image](images/lab3/2019-01-20_13-25-29_GuidedStep5.png)

This should just give you a smiley face and a message saying that setup
is complete.

**Step 3.10:** Click *Enter* and you should be returned to a screen that
looks similar to this (your names may differ):

![image](images/lab3/UnitedMarblesMainPage.png)

**Step 3.11:** What about John's marble for Marbles Inc.? You only
started up the server for United Marbles, so why does Marbles Inc show
up and why is John so lonely? When you did the previous lab, the first
two commands I had you do were an *init\_owner* for John, tying him to
Marbles Inc, and then an *init\_marble*, giving him a marble. Remember,
the "blockchain" is shared among all participants of the channel, so
United Marbles and Marbles Inc both see the same chain- they see each
other's marbles.

But the user names specified in *config/marbles2.json* are not created
until you start the server for *marbles2* and log in the first time.
List the contents of *marbles2.json* file (switch to a free terminal
session or start a new one), e.g.:

    bcuser@ubuntu18042:~$ cd ~/zmarbles/marblesUI
    bcuser@ubuntu18042:~/zmarbles/marblesUI$ cat config/marbles2.json 
    {
        "cred_filename": "connection_profile2.json",
        "use_events": false,
        "keep_alive_secs": 120,
        "company": "Marbles Inc",
        "usernames": [
            "cliff",
            "cody",
            "chuck"
        ],
        "port": 3002,
        "last_startup_hash": ""
    }
    bcuser@ubuntu18042:~/zmarbles/marblesUI$ 

**Step 3.12:** Start the second server, the one for Marbles Inc:

    bcuser@ubuntu18042:~/zmarbles/marblesUI$ gulp marbles2
    [16:07:49] Using gulpfile ~/zmarbles/marblesUI/gulpfile.js
    [16:07:49] Starting 'env_tls2'...
    [16:07:49] Finished 'env_tls2' after 50 μs
    [16:07:49] Starting 'build-sass'...
    [16:07:49] Finished 'build-sass' after 7.9 ms
    [16:07:49] Starting 'watch-sass'...
    [16:07:49] Finished 'watch-sass' after 6.38 ms
    [16:07:49] Starting 'watch-server'...
    [16:07:49] Finished 'watch-server' after 1.9 ms
    [16:07:49] Starting 'server'...
    info: Checking connection profile is done
    info: Loaded config file /home/bcuser/zmarbles/marblesUI/config/marbles2.json
    info: Loaded connection profile file /home/bcuser/zmarbles/marblesUI/config/connection_profile2.json



    Connection Profile Lib Functions:()
      getNetworkName()
      getNetworkCredFileName()
      buildTlsOpts()
      getFirstChannelId()
      getChannelId()
      loadPem()
      getMarblesField()
      getChaincodeId()
      getChaincodeVersion()
      getFirstCaName()
      getCA()
      getCasUrl()
      getAllCaUrls()
      getCaName()
      getCaTlsCertOpts()
      getEnrollObj()
      getFirstPeerName()
      getPeer()
      getPeersUrl()
      getAllPeerUrls()
      getPeerEventUrl()
      getPeerTlsCertOpts()
      getMarbleUsernamesConfig()
      getCompanyNameFromFile()
      getMarblesPort()
      getEventsSetting()
      getKeepAliveMs()
      getFirstOrdererName()
      getOrderer()
      getOrderersUrl()
      getOrdererTlsCertOpts()
      getBlockDelay()
      getKvsPath()
      getFirstOrg()
      getClientsOrgName()
      getClientOrg()
      getMarbleUsernames()
      getOrgsMSPid()
      getAdminPrivateKeyPEM()
      getAdminSignedCertPEM()


    ----------------------------------- Server Up - localhost:3002 -----------------------------------
    Welcome aboard:	 Marbles Inc
    Channel:	 mychannel
    Org:		 Org1MSP
    CA:		 fabric-ca-org2
    Orderer:	 fabric-orderer
    Peer:		 fabric-peer-org2
    Chaincode ID:	 marbles
    Chaincode Version:  v4
    ------------------------------------------ Websocket Up ------------------------------------------


    debug: loading pem from a path: /home/bcuser/zmarbles/crypto-config/peerOrganizations/marblesinc.com/ca/ca.marblesinc.com-cert.pem
    debug: loading pem from a path: /home/bcuser/zmarbles/crypto-config/ordererOrganizations/blockchain.com/orderers/orderer.blockchain.com/tls/ca.crt
    debug: loading pem from a path: /home/bcuser/zmarbles/crypto-config/peerOrganizations/marblesinc.com/peers/peer0.marblesinc.com/tls/ca.crt
    info: [fcw] Going to enroll peer_urls=[grpcs://localhost:9051], channel_id=mychannel, uuid=marblesDockerComposeNetworkmychannelOrg1MSPfabricpeerorg2, ca_url=https://localhost:8054, orderer_url=grpcs://localhost:7050, enroll_id=admin2, enroll_secret=adminpw2, msp_id=Org1MSP, kvs_path=/home/bcuser/.hfc-key-store/marblesDockerComposeNetworkmychannelOrg1MSPfabricpeerorg2
    debug: enroll id: "admin2", secret: "adminpw2"
    debug: msp_id:  Org1MSP ca_name: ca-org1
    info: [fcw] Successfully enrolled user 'admin2'
    debug: added peer grpcs://localhost:9051
    debug: [fcw] Successfully got enrollment marblesDockerComposeNetworkmychannelOrg1MSPfabricpeerorg2
    info: Success enrolling admin
    debug: loading pem from a path: /home/bcuser/zmarbles/crypto-config/peerOrganizations/marblesinc.com/ca/ca.marblesinc.com-cert.pem
    debug: loading pem from a path: /home/bcuser/zmarbles/crypto-config/ordererOrganizations/blockchain.com/orderers/orderer.blockchain.com/tls/ca.crt
    debug: loading pem from a path: /home/bcuser/zmarbles/crypto-config/peerOrganizations/marblesinc.com/peers/peer0.marblesinc.com/tls/ca.crt
    debug: Checking if chaincode is already instantiated or not 1

    info: Checking for chaincode...
    debug: [fcw] Querying Chaincode: read()
    debug: [fcw] Sending query req: chaincodeId=marbles, fcn=read, args=[selftest], txId=null
    debug: [fcw] Peer Query Response - len: 1 type: number
    debug: [fcw] Successful query transaction.

    ----------------------------- Chaincode found on channel "mychannel" -----------------------------


    info: Checking chaincode and ui compatibility...
    debug: [fcw] Querying Chaincode: read()
    debug: [fcw] Sending query req: chaincodeId=marbles, fcn=read, args=[marbles_ui], txId=null
    warn: [fcw] warning - query resp is not json, might be okay: string 4.0.1
    debug: [fcw] Successful query transaction.
    info: Chaincode version is good
    info: Checking ledger for marble owners listed in the config file

    info: Fetching EVERYTHING...
    debug: [fcw] Querying Chaincode: read_everything()
    debug: [fcw] Sending query req: chaincodeId=marbles, fcn=read_everything, args=[], txId=null
    debug: [fcw] Peer Query Response - len: 2291 type: object
    debug: [fcw] Successful query transaction.
    debug: This company has registered marble owners
    debug: Looking for marble owner: cliff
    debug: Did not find marble username: cliff
    info: We need to make marble owners


    - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
    info: Detected that we have NOT launched successfully yet
    debug: Open your browser to http://localhost:3002 and login as "admin" to initiate startup
    - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

If you peek at your browser session from United Marbles, (port 3001),
you will not notice any changes yet.

**Step 3.13:** Open a browser tab or window and navigate to
*http://<your\_IP\_here\>:3002*. You will again be given a choice of
*Express* or *Guided* and feel free to choose whichever path suits your
fancy. If you choose *Express*, everything should hopefully sail through
until you see a screen with all Marbles Inc. owners and marbles, as well
as all United Marbles owners and marbles:

![image](images/lab3/MarblesIncUpdatedPage.png)

**Step 3.14:** If you go back to your screen for United Marbles (port
3001) you should observe that it has been updated to show the owners and
marbles for Marbles Inc. in addition to United Marbles' own owners and
marbles:

![image](images/lab3/UnitedMarblesUpdatedPage.png)

Remember, you are looking at the United Marbles session but you see all
the new users and marbles created by the Marbles Inc administrator.

**Step 3.15:** Play with your marbles!! Here are some things you can do.
When you do things as one user, e.g. as the United Marbles admin, go to
the other user's screen to see that the changes one organization makes
are visible to the other organization:

-   On two different browser sessions, you should be logged in as the
    administrator for each of the two fictitious companies. When you are
    the United Marbles administrator, you can create marbles for you or
    anybody in United Marbles. You can delete marbles for you or anybody
    in United Marbles. You can take marbles from anybody in United
    Marbles and give them to anybody in the network, even to Marbles Inc
    people. (And vice versa when you are a Marbles Inc administrator).
-   Try clicking on the little magnifying glass to the left of the
    browser window and follow the directions
-   Right click on a marble (Hint: this is the same as using the
    magnifying glass)
-   Click on the **Settings** button and **Enable** story mode. Try an
    action that is allowed, and try an action that shouldn't be allowed,
    such as trying to steal a marble from the other company. **Disable**
    story mode when it gets too tedious, which shouldn't take long.

**Step 3.16:** If you want that extra rush, try these optional advanced
assignments:

-   Break out the previous lab's material and enter the *cli* container
    and issue some commands to create, update or delete marbles. See if
    the Marbles UI reflects your changes
-   Look at some of the marbles chaincode container logs while you work
    with the Marbles UI - **Hint:** *docker logs \[-f\] container\_name*
    will show a container's log. Try it without the optional *-f*
    argument first and then try it with it. *-f* ties up your terminal
    session but then shows new log messages as they are created. Press
    **Ctrl-c** to get out of it.
-   Look at the peer or orderer logs while you work with the Marbles UI
-   Click the **Start Up Help** button in the upper left in the Marbles
    UI and then number *4* in the window that pops up. Edit the list of
    names at the bottom and click **Create**. Do your new users show up in
    both companies' sessions? What happens if you add a name that exists
    already? 

Section 4: Lab cleanup
===========================================

**Step 4.1:** In both of your terminals sessions that were used to start
each Web UI, press *Crtl-c* to end the Web UI process. You can also close
the tabs in your browser that were displaying the Web UI.

**Step 4.2:** Navigate to the *zmarbles* directory:
    
    bcuser@ubuntu18042:~/zmarbles/marblesUI$ cd ~/zmarbles
    bcuser@ubuntu18042:~/zmarbles$ 
    
**Step 4.3:** Enter this Docker command to show the running Docker containers
that make up your Hyperledger Fabric network:

    bcuser@ubuntu18042:~/zmarbles$ docker ps
    CONTAINER ID        IMAGE                                                                                                      COMMAND                  CREATED             STATUS              PORTS                                                                       NAMES
    1e5c05183d6f        dev-peer1.unitedmarbles.com-marbles-1.0-dea1aa08dc7c6f282a31dd498670173c21d3e75ef0ef1d170b95e1212fbacb77   "chaincode -peer.add…"   26 minutes ago      Up 26 minutes                                                                                   dev-peer1.unitedmarbles.com-marbles-1.0
    a7d6b658a35a        dev-peer0.marblesinc.com-marbles-1.0-4077677f13838bacbfd8ff943e7348c00f3c4d6ca6e2838efd14204ca87ea12b      "chaincode -peer.add…"   31 minutes ago      Up 31 minutes                                                                                   dev-peer0.marblesinc.com-marbles-1.0
    62a185d148d2        dev-peer0.unitedmarbles.com-marbles-1.0-7e92f069adb7469939a96dcba723fa2019745461f05a562e81cec38e46424aa1   "chaincode -peer.add…"   39 minutes ago      Up 39 minutes                                                                                   dev-peer0.unitedmarbles.com-marbles-1.0
    84b6c0ee74aa        hyperledger/fabric-tools:1.4.1                                                                             "bash"                   About an hour ago   Up About an hour                                                                                cli
    e6eabd9fd96d        hyperledger/fabric-peer:1.4.1                                                                              "peer node start"        About an hour ago   Up About an hour    0.0.0.0:9051->7051/tcp, 0.0.0.0:9052->7052/tcp, 0.0.0.0:9053->7053/tcp      peer0.marblesinc.com
    8174f3021744        hyperledger/fabric-peer:1.4.1                                                                              "peer node start"        About an hour ago   Up About an hour    0.0.0.0:8051->7051/tcp, 0.0.0.0:8052->7052/tcp, 0.0.0.0:8053->7053/tcp      peer1.unitedmarbles.com
    1a22b9eb5be5        hyperledger/fabric-peer:1.4.1                                                                              "peer node start"        About an hour ago   Up About an hour    0.0.0.0:10051->7051/tcp, 0.0.0.0:10052->7052/tcp, 0.0.0.0:10053->7053/tcp   peer1.marblesinc.com
    11423ca89763        hyperledger/fabric-peer:1.4.1                                                                              "peer node start"        About an hour ago   Up About an hour    0.0.0.0:7051-7053->7051-7053/tcp                                            peer0.unitedmarbles.com
    18b9e5efbfc9        hyperledger/fabric-couchdb:s390x-0.4.15                                                                    "tini -- /docker-ent…"   About an hour ago   Up About an hour    4369/tcp, 9100/tcp, 0.0.0.0:6984->5984/tcp                                  couchdb1
    77288f8c0060        hyperledger/fabric-couchdb:s390x-0.4.15                                                                    "tini -- /docker-ent…"   About an hour ago   Up About an hour    4369/tcp, 9100/tcp, 0.0.0.0:7984->5984/tcp                                  couchdb2
    43214da184da        hyperledger/fabric-ca:1.4.1                                                                                "sh -c 'fabric-ca-se…"   About an hour ago   Up About an hour    0.0.0.0:7054->7054/tcp                                                      ca_Org0
    1ea639c77a3a        hyperledger/fabric-ca:1.4.1                                                                                "sh -c 'fabric-ca-se…"   About an hour ago   Up About an hour    0.0.0.0:8054->7054/tcp                                                      ca_Org1
    07df27e35368        hyperledger/fabric-couchdb:s390x-0.4.15                                                                    "tini -- /docker-ent…"   About an hour ago   Up About an hour    4369/tcp, 9100/tcp, 0.0.0.0:8984->5984/tcp                                  couchdb3
    93e0465394b6        hyperledger/fabric-orderer:1.4.1                                                                           "orderer"                About an hour ago   Up About an hour    0.0.0.0:7050->7050/tcp                                                      orderer.blockchain.com
    4201915cc3b2        hyperledger/fabric-couchdb:s390x-0.4.15                                                                    "tini -- /docker-ent…"   About an hour ago   Up About an hour    4369/tcp, 9100/tcp, 0.0.0.0:5984->5984/tcp                                  couchdb0
    bcuser@ubuntu18042:~/zmarbles$ 

**Step 4.4:** Enter this command to bring down your Hyperledger Fabric network:

    bcuser@ubuntu18042:~/zmarbles$ docker-compose down
    WARNING: The CHANNEL_NAME variable is not set. Defaulting to a blank string.
    Stopping cli                     ... done
    Stopping peer0.marblesinc.com    ... done
    Stopping peer1.unitedmarbles.com ... done
    Stopping peer1.marblesinc.com    ... done
    Stopping peer0.unitedmarbles.com ... done
    Stopping couchdb1                ... done
    Stopping couchdb2                ... done
    Stopping ca_Org0                 ... done
    Stopping ca_Org1                 ... done
    Stopping couchdb3                ... done
    Stopping orderer.blockchain.com  ... done
    Stopping couchdb0                ... done
    Removing cli                     ... done
    Removing peer0.marblesinc.com    ... done
    Removing peer1.unitedmarbles.com ... done
    Removing peer1.marblesinc.com    ... done
    Removing peer0.unitedmarbles.com ... done
    Removing couchdb1                ... done
    Removing couchdb2                ... done
    Removing ca_Org0                 ... done
    Removing ca_Org1                 ... done
    Removing couchdb3                ... done
    Removing orderer.blockchain.com  ... done
    Removing couchdb0                ... done
    Removing network zmarbles_default
    bcuser@ubuntu18042:~/zmarbles$ 

**Step 4.5:** Enter this and you should not see any running Docker containers:

    bcuser@ubuntu18042:~/zmarbles$ docker ps
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
    bcuser@ubuntu18042:~/zmarbles$ 

**Step 4.6:** Add the *--all* argument to the prior command and you will see some
*Exited* Docker containers:

    bcuser@ubuntu18042:~/zmarbles$ docker ps --all
    CONTAINER ID        IMAGE                                                                                                      COMMAND                  CREATED             STATUS                          PORTS               NAMES
    1e5c05183d6f        dev-peer1.unitedmarbles.com-marbles-1.0-dea1aa08dc7c6f282a31dd498670173c21d3e75ef0ef1d170b95e1212fbacb77   "chaincode -peer.add…"   28 minutes ago      Exited (0) About a minute ago                       dev-peer1.unitedmarbles.com-marbles-1.0
    a7d6b658a35a        dev-peer0.marblesinc.com-marbles-1.0-4077677f13838bacbfd8ff943e7348c00f3c4d6ca6e2838efd14204ca87ea12b      "chaincode -peer.add…"   33 minutes ago      Exited (0) About a minute ago                       dev-peer0.marblesinc.com-marbles-1.0
    62a185d148d2        dev-peer0.unitedmarbles.com-marbles-1.0-7e92f069adb7469939a96dcba723fa2019745461f05a562e81cec38e46424aa1   "chaincode -peer.add…"   41 minutes ago      Exited (0) About a minute ago                       dev-peer0.unitedmarbles.com-marbles-1.0
    bcuser@ubuntu18042:~/zmarbles$ 

**Step 4.7:** Enter this command to remove these containers:

    bcuser@ubuntu18042:~/zmarbles$ docker rm $(docker ps --all --quiet)
    1e5c05183d6f
    a7d6b658a35a
    62a185d148d2
    bcuser@ubuntu18042:~/zmarbles$ 

**Step 4.8:** Repeat the command from *Step 4.6* and you should not see any containers:

    bcuser@ubuntu18042:~/zmarbles$ docker ps --all
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
    bcuser@ubuntu18042:~/zmarbles$  

**Step 4.9:** List your Docker images:

    bcuser@ubuntu18042:~/zmarbles$ docker images
    REPOSITORY                                                                                                 TAG                 IMAGE ID            CREATED             SIZE
    dev-peer1.unitedmarbles.com-marbles-1.0-dea1aa08dc7c6f282a31dd498670173c21d3e75ef0ef1d170b95e1212fbacb77   latest              c0e41de218a2        30 minutes ago      137MB
    dev-peer0.marblesinc.com-marbles-1.0-4077677f13838bacbfd8ff943e7348c00f3c4d6ca6e2838efd14204ca87ea12b      latest              ab7f5fa821ee        35 minutes ago      137MB
    dev-peer0.unitedmarbles.com-marbles-1.0-7e92f069adb7469939a96dcba723fa2019745461f05a562e81cec38e46424aa1   latest              d41acea306aa        43 minutes ago      137MB
    hyperledger/fabric-ca                                                                                      1.4.1               a836041637e8        2 weeks ago         220MB
    hyperledger/fabric-tools                                                                                   1.4.1               330902566372        2 weeks ago         1.52GB
    hyperledger/fabric-ccenv                                                                                   latest              8583516cfc43        2 weeks ago         1.41GB
    hyperledger/fabric-orderer                                                                                 1.4.1               1b709e319b2d        2 weeks ago         148MB
    hyperledger/fabric-peer                                                                                    1.4.1               719392658c28        2 weeks ago         154MB
    hyperledger/fabric-couchdb                                                                                 s390x-0.4.15        81ee917e0be2        5 weeks ago         1.55GB
    hyperledger/fabric-baseos                                                                                  s390x-0.4.15        d4eb16b952d6        5 weeks ago         120MB
    bcuser@ubuntu18042:~/zmarbles$ 

**Step 4.10:** This command will format the output from *docker images*:

    bcuser@ubuntu18042:~/zmarbles$ docker images --format '{{.Repository}}:{{.Tag}}'
    dev-peer1.unitedmarbles.com-marbles-1.0-dea1aa08dc7c6f282a31dd498670173c21d3e75ef0ef1d170b95e1212fbacb77:latest
    dev-peer0.marblesinc.com-marbles-1.0-4077677f13838bacbfd8ff943e7348c00f3c4d6ca6e2838efd14204ca87ea12b:latest
    dev-peer0.unitedmarbles.com-marbles-1.0-7e92f069adb7469939a96dcba723fa2019745461f05a562e81cec38e46424aa1:latest
    hyperledger/fabric-ca:1.4.1
    hyperledger/fabric-tools:1.4.1
    hyperledger/fabric-ccenv:latest
    hyperledger/fabric-orderer:1.4.1
    hyperledger/fabric-peer:1.4.1
    hyperledger/fabric-couchdb:s390x-0.4.15
    hyperledger/fabric-baseos:s390x-0.4.15
    bcuser@ubuntu18042:~/zmarbles$ 

**Step 4.11:** The output from the prior step is in a format acceptable to the Docker command to remove images, so 
this command will feed that output into the Docker *rmi* command, and remove these images:

    bcuser@ubuntu18042:~/zmarbles$ docker rmi $(docker images --format '{{.Repository}}:{{.Tag}}')
    Untagged: dev-peer1.unitedmarbles.com-marbles-1.0-dea1aa08dc7c6f282a31dd498670173c21d3e75ef0ef1d170b95e1212fbacb77:latest
    Deleted: sha256:c0e41de218a260a73053d538aa45ca0f925cd3ee7d8898151ea7df39dc1ac813
    Deleted: sha256:40fc70560501ded0fbf1d7bc6a2e77de321041a62770822f692977cd363f16be
    Deleted: sha256:4a8c59ccf0d503088d13b041260d4741509656336b431e6bb7e64b20a91b90fb
    Deleted: sha256:8ce2cde820ef4ccfef99f8389315141614441b89219de487da33db3494874c8b
    Untagged: dev-peer0.marblesinc.com-marbles-1.0-4077677f13838bacbfd8ff943e7348c00f3c4d6ca6e2838efd14204ca87ea12b:latest
    Deleted: sha256:ab7f5fa821ee42c139722b2360909c95c1b2586cb437686122af1e571bd34802
    Deleted: sha256:f7a0e17801a42a44340f27cb7c7332314534d1ed2d4573cb5334f27289dc5ff0
    Deleted: sha256:8085444130169915f706aecfac10aaeee4d3e641e63e4686258c513e6fe85830
    Deleted: sha256:e0f59705093caa197dde37fba5d05aa4635465b5d42e8d48234b9a28d3423a48
    Untagged: dev-peer0.unitedmarbles.com-marbles-1.0-7e92f069adb7469939a96dcba723fa2019745461f05a562e81cec38e46424aa1:latest
    Deleted: sha256:d41acea306aa6d858cca4f55bb92b20335da5a588550411d32fc77def25d3775
    Deleted: sha256:493804d997703675b48104eed5e6868b1e6f14bf954fbb56ac5784a82838ccbf
    Deleted: sha256:3504ecc13cf81ec4947132a9261600f1e9cdeee94672df62469f2061bd1a4b2a
    Deleted: sha256:8267b35c52b6b78b7341b95c5c044a69feb53075c704b2eea87a4d4b6036be06
    Untagged: hyperledger/fabric-ca:1.4.1
    Untagged: hyperledger/fabric-ca@sha256:f77aa0ff885c572b090d1ff7564780daafd50d9e839b6241c2ab12c37f47b94a
    Deleted: sha256:a836041637e817846f71541e47e8749f6188676a1ac282f006ca03758290f4ff
    Deleted: sha256:8fa3260318e50be92f0118657fa3aa395e264cfa2fbe0dbedb9419fff1547bfd
    Deleted: sha256:f0c44e96c65ce80eaeb561f89fa23ae82c5af54b1b1b050ecadd827b45bebd23
    Deleted: sha256:e2e8ca9c5a2fb8c69e32428be2f27d6bb0c1e1b7e58af5d4d5aa788ce8d9fd68
    Deleted: sha256:a353d8ddb009e3c0dd6bd0558a1e3ed847951f42ae632a91ad49029bb69b9fc0
    Deleted: sha256:f1079f0f139b61ea01f32de10d58de81e1fc393038d3fa774221a736f942023f
    Deleted: sha256:165d46e0e538aacfcecf19a4088c2e7b490384e7b3cecb090a16b19cba8722d9
    Deleted: sha256:85fb95169355a4e6fcd52672b1e60739f120ee9e541413732cb53d8e5c97beae
    Untagged: hyperledger/fabric-tools:1.4.1
    Untagged: hyperledger/fabric-tools@sha256:c458ddc3109d3519b209baaf9abff113641267ec2adb01dfdcf8f4c9e77a2fa0
    Deleted: sha256:330902566372ecfc06a396c05d026a0d17fa40379dc1327894869ad370023637
    Deleted: sha256:1021b7b3b232c0954f944c6d2baec3ef80dc9481bcabea5a12db4f7d276c86f7
    Deleted: sha256:9427db3491c3adcb8cecfcf50bb3c8deeab27d3739538c2cd246ee6b856515a9
    Deleted: sha256:dba040b6371fcdc2b78128d10e952cc716b75ba67f2dc330086c908fb830fa1d
    Untagged: hyperledger/fabric-ccenv:latest
    Untagged: hyperledger/fabric-ccenv@sha256:bb929eef560b50e0fbd730c6b195e49fece28dd4612ec30db0ce2cc096483463
    Deleted: sha256:8583516cfc43491e2db2e393408121b85636f622d39d2a8e3c46ac278d3d3ce2
    Deleted: sha256:3d53a661451588e08ea4f0b1e6fac40633b4dcef9fb895ad12f9309453d85dfa
    Deleted: sha256:04e554cb54244558f5567c17ebcb7a02b64822036ece595fefb4f98d2ab31a7a
    Deleted: sha256:a2ec3c9f4ab3e2a789239638d99aa4a760998c8424d29313d5461bcfd2929612
    Untagged: hyperledger/fabric-orderer:1.4.1
    Untagged: hyperledger/fabric-orderer@sha256:09f31ca4dabe1eb2af870ea062561ca6686fc59a296ecc3b4bd7e32102c48934
    Deleted: sha256:1b709e319b2d2e7d137112ff5e24b7b6a0ddf0a5bf8843c47adfc9095b3f8778
    Deleted: sha256:43747e128cff58f58f5642bce1b27613ecb3dec5aa8fc7caf0ce5e2397415371
    Deleted: sha256:fb1a267f0371757e83dcf6221291269b29a7089a0f7a8545ff3f538509e19e0e
    Untagged: hyperledger/fabric-peer:1.4.1
    Untagged: hyperledger/fabric-peer@sha256:05315d05b2892d34b4ed48f6502d28fe15a71090c36a39c97022a44475a984ad
    Deleted: sha256:719392658c28f69bb25ccc71a8da86050f646f4ffaf51a279cdcea079b5f993e
    Deleted: sha256:04d6dbf6b6fcdaaedb6d55a021bd1dcb0695ecfbe9e2538fe2dd1365987eea0b
    Deleted: sha256:4c58d7859aeaf30d72dada842ce28df9d542e2ffc1ab2213b81483f080adceef
    Deleted: sha256:6299707a98af34860777b48b86df6ec7ae8cf45ae76cbf4cbedcb1dc55888061
    Untagged: hyperledger/fabric-couchdb:s390x-0.4.15
    Untagged: hyperledger/fabric-couchdb@sha256:e8701a2dd7400d200a6c3b1ffd42331e2d5255d30c1efb117fc5a10bbf9063b6
    Deleted: sha256:81ee917e0be2fe0b5f46cf6ed34d32169118c8d995cee636ce47ffb96d3afd95
    Deleted: sha256:e4cdccb03102bce02d4e9179cf1eed5808e97bb77fb7bf7596776900caf3f22a
    Deleted: sha256:12e70245586bf85d0f2eabc4ba33c1df77d51e604c294551e43c9dec425f619c
    Deleted: sha256:f7a35da6c7b30fa6fa11e2f6e44938ea4df158db403064832a73d1e9b11aa719
    Deleted: sha256:1b774897931652fde3bb2609e0f46fa4c3a3f522db395359a2aeee1a218aab54
    Deleted: sha256:1132017bbb8c969f03a11ec80e77eea71a3fc54dbae9e2b588b01fc5c0502972
    Deleted: sha256:de23c4b00ab7d92310f73b45cacf5b861a8f40c5b069c0660eb1bc6d472c98e7
    Deleted: sha256:62306dc38b9fc0fb7922d4d1358d135e1c7411b01e51bb631fc5269308387c42
    Deleted: sha256:8bc0cb77c66908a5059433ca0b41f453721de3bc529ecc258ff91818ce19e87f
    Deleted: sha256:8445d7f0d5111f5ee7fe4ada50d718df0977e9b071045e09b3d619effd16d7e0
    Deleted: sha256:f593f65839abaaf5f0c18604b7f065b4cab58bfeafa867b7be75fc6ca52e187a
    Deleted: sha256:18eaede2be21b8fdba162857cbf79ce9a04cb2671da8c40dc804280e791e9742
    Deleted: sha256:ef88e98e5731409ad689aec3233fcca8d5f1b38e435558308d8289fb3d5a5383
    Deleted: sha256:9941b43bff58fff3234b1f356d65f1d383265156c82ba90805a00ba758e5fa14
    Deleted: sha256:31699b2e24542ffbc8cf9678644e62ab195263be033713327992314d59ddffbb
    Untagged: hyperledger/fabric-baseos:s390x-0.4.15
    Untagged: hyperledger/fabric-baseos@sha256:94fefcbeb2c0da7ac6371ad589b66b2bbe7cfb76bf28ba7aaf85790bed82c839
    Deleted: sha256:d4eb16b952d6c8b742cbe47caf6522c71f9b1654a31abc582918905d64db07e7
    Deleted: sha256:234cfc5f3368cd92d65d03e5da6bc0bd985ab94c4931e692faa758bd6d811c7b
    Deleted: sha256:3e2d2d75f895801cefdecac9e2584d964caf0ed7fb1d8afeffeaea5e287ea9cb
    Deleted: sha256:d8e11f36fc45b7073d3b0eb3636428dedebb40f392bea9fa5751ed92848ca875
    bcuser@ubuntu18042:~/zmarbles$ 

**Step 4.12:**  Now you should not see any images:

    bcuser@ubuntu18042:~/zmarbles$ docker images
    REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
    bcuser@ubuntu18042:~/zmarbles$          IMAGE ID            CREATED             SIZE
   
**Step 4.13:** You may type *exit* from your terminal session(s) to log out of the system

    bcuser@ubuntu18042:~/zmarbles$ exit
    logout
    Connection to 192.168.22.1xx closed.
    Barrys-MacBook-Pro:ImmersionWorkshop silliman$ 

**End of lab!**
