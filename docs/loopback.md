In this section, we are going to create a loopback API application for each MagnetoCorp and Digibank. Once we have created these applications, you'll be able to submit transactions and have them be recorded in our blockchain network. 

**1.** From the CLI application, open a new tab and naviagate to your desktop. Once you are at the desktop, install the loopback npm package. You can find these commands below
::

    tecadmin@ubuntubase:~/Desktop$ cd ~
    tecadmin@ubuntubase:~/Desktop$ npm install -g @loopback/cli

**2.** Once you have the loopback installed, go ahead and follow the series of commands and prompts below. I'll explain these after we have completed this.
::

        ----- Create Our App -----
    tecadmin@ubuntubase:~/Desktop$ lb4 app
    ? Project name: magnetocorp
    ? Project description: loopback api for magnetocorp
    ? Project root directory: magnetocorp
    ? Application class name: MagnetocorpApplication
    ? Select features to enable in the project (Press <space> to select, <a> to toggle all, <i> to invert selection)Enable eslint, Enable prettier, Enable mocha, Enable loopbackBuild, Enable vscode, Enable docker, Enable repositories, Enable services
       create .eslintignore
       create .eslintrc.js
       create .mocharc.json
       create .npmrc
       create .prettierignore
       create .prettierrc
       create DEVELOPING.md
       create README.md
       create index.ts
       create package.json
       create tsconfig.json
       create .vscode/settings.json
       create .vscode/tasks.json
       create .gitignore
       create .dockerignore
       create Dockerfile
       create index.js
       create public/index.html
       create src/application.ts
       create src/index.ts
       create src/migrate.ts
       create src/sequence.ts
       create src/__tests__/README.md
       create src/controllers/README.md
       create src/controllers/index.ts
       create src/controllers/ping.controller.ts
       create src/datasources/README.md
       create src/models/README.md
       create src/repositories/README.md
       create src/__tests__/acceptance/home-page.acceptance.ts
       create src/__tests__/acceptance/ping.controller.acceptance.ts
       create src/__tests__/acceptance/test-helper.ts


    Application magnetocorp was created in magnetocorp.
    
    ----- Create Model for our Issue -----

    tecadmin@ubuntubase:~/Desktop$ cd magnetocorp/
    tecadmin@ubuntubase:~/Desktop/magnetocorp$ lb4 model
    ? Model class name: issue
    ? Please select the model base class Entity (A persisted model with an ID)
    ? Allow additional (free-form) properties? No
    Let's add a property to Issue
    Enter an empty property name when done

    ? Enter the property name: issuer
    ? Property type: string
    ? Is issuer the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to Issue
    Enter an empty property name when done

    ? Enter the property name: paperNumber
    ? Property type: string
    ? Is paperNumber the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to Issue
    Enter an empty property name when done

    ? Enter the property name: issueDateTime
    ? Property type: string
    ? Is issueDateTime the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to Issue
    Enter an empty property name when done

    ? Enter the property name: maturityDateTime
    ? Property type: string
    ? Is maturityDateTime the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to Issue
    Enter an empty property name when done

    ? Enter the property name: faceValue
    ? Property type: string
    ? Is faceValue the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to Issue
    Enter an empty property name when done

    ? Enter the property name: paperRate
    ? Property type: string
    ? Is paperRate the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to Issue
    Enter an empty property name when done

    ? Enter the property name: 
       create src/models/issue.model.ts
       update src/models/index.ts

    Model issue was created in src/models/
    
    ----- Create Model for our getPaperRate -----

    tecadmin@ubuntubase:~/Desktop/magnetocorp$ lb4 model
    ? Model class name: getPaperRate
    ? Please select the model base class Entity (A persisted model with an ID)
    ? Allow additional (free-form) properties? No
    Let's add a property to GetPaperRate
    Enter an empty property name when done

    ? Enter the property name: issuer
    ? Property type: string
    ? Is issuer the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to GetPaperRate
    Enter an empty property name when done

    ? Enter the property name: paperNumber
    ? Property type: string
    ? Is paperNumber the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to GetPaperRate
    Enter an empty property name when done

    ? Enter the property name: 
       create src/models/get-paper-rate.model.ts
       update src/models/index.ts

    Model getPaperRate was created in src/models/
    
    ----- Create Model for our getAllPapersFromIssuer -----

    tecadmin@ubuntubase:~/Desktop/magnetocorp$ lb4 model
    ? Model class name: getAllPapersFromIssuer
    ? Please select the model base class Entity (A persisted model with an ID)
    ? Allow additional (free-form) properties? No
    Let's add a property to GetAllPapersFromIssuer
    Enter an empty property name when done

    ? Enter the property name: paperIssuer
    ? Property type: string
    ? Is paperIssuer the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to GetAllPapersFromIssuer
    Enter an empty property name when done

    ? Enter the property name: 
       create src/models/get-all-papers-from-issuer.model.ts
       update src/models/index.ts

    Model getAllPapersFromIssuer was created in src/models/

        ----- Create a Datasource -----
        
    tecadmin@ubuntubase:~/Desktop/digibank$ lb4 datasource
    ? Datasource name: db
    ? Select the connector for db: In-memory db (supported by StrongLoop)
    ? window.localStorage key to use for persistence (browser only): 
    ? Full path to file for persistence (server only): ./data/db.json
       create src/datasources/db.datasource.json
       create src/datasources/db.datasource.ts
       update src/datasources/index.ts

    Datasource db was created in src/datasources/
    
        ----- Create our Repositories -----    

    tecadmin@ubuntubase:~/Desktop/magnetocorp$ lb4 repository
    ? Please select the datasource DbDatasource
    ? Select the model(s) you want to generate a repository (Press <space> to select, <a> to toggle all, <i> to invert selection)GetAllPapersFromIssuer, GetPaperRate, Issue
    ? Please select the repository base class DefaultCrudRepository (Legacy juggler bridge)
    ? Please enter the name of the ID property for GetAllPapersFromIssuer: id
    ? Please enter the name of the ID property for GetPaperRate: id
    ? Please enter the name of the ID property for Issue: id
       create src/repositories/get-all-papers-from-issuer.repository.ts
       create src/repositories/get-paper-rate.repository.ts
       create src/repositories/issue.repository.ts
       update src/repositories/index.ts
       update src/repositories/index.ts
       update src/repositories/index.ts

    Repositories GetAllPapersFromIssuerRepository,GetPaperRateRepository,IssueRepository was created in src/repositories/
    
    ----- Create a Controller for Issue, GetPaperRate and GetAllPapersFromIssuer ----- 

    tecadmin@ubuntubase:~/Desktop/magnetocorp$ lb4 controller
    ? Controller class name: Issue
    ? What kind of controller would you like to generate? REST Controller with CRUD functions
    ? What is the name of the model to use with this CRUD repository? Issue
    ? What is the name of your CRUD repository? IssueRepository
    ? What is the type of your ID? string
    ? What is the base HTTP path name of the CRUD operations? /issues
       create src/controllers/issue.controller.ts
       update src/controllers/index.ts

    Controller Issue was created in src/controllers/

    tecadmin@ubuntubase:~/Desktop/magnetocorp$ lb4 controller
    ? Controller class name: GetPaperRate
    ? What kind of controller would you like to generate? REST Controller with CRUD functions
    ? What is the name of the model to use with this CRUD repository? GetPaperRate
    ? What is the name of your CRUD repository? GetPaperRateRepository
    ? What is the type of your ID? string
    ? What is the base HTTP path name of the CRUD operations? /get-paper-rates
       create src/controllers/get-paper-rate.controller.ts
       update src/controllers/index.ts

    Controller GetPaperRate was created in src/controllers/

    tecadmin@ubuntubase:~/Desktop/magnetocorp$ lb4 controller
    ? Controller class name: GetAllPapersFromIssuer
    ? What kind of controller would you like to generate? REST Controller with CRUD functions
    ? What is the name of the model to use with this CRUD repository? GetAllPapersFromIssuer
    ? What is the name of your CRUD repository? GetAllPapersFromIssuerRepository
    ? What is the type of your ID? string
    ? What is the base HTTP path name of the CRUD operations? /get-all-papers-from-issuers
       create src/controllers/get-all-papers-from-issuer.controller.ts
       update src/controllers/index.ts

    Controller GetAllPapersFromIssuer was created in src/controllers/
    
What you just did above is basically create the bones to our loopback API application. We needed to create our app, model, datasource, repository and controller to actually create our application. Below is a breakdown of each thing we created

**App:**
::

    The LoopBack 4 CLI toolkit comes with templates that generate whole applications, as well as artifacts (for example, controllers, models, and repositories) for existing applications.
    
    tecadmin@ubuntubase:~/Desktop$ lb4 app
    ? Project name: magnetocorp
    ? Project description: loopback application for magnetocorp
    ? Project root directory: magnetocorp
    ? Application class name: MagnetoCorpApplication
    ? Select features to enable in the project (Press <space> to select, <a> to toggle all, <i> to invert selection)Enable eslint, Enable --- Press enter to enable all of these! ---
    prettier, Enable mocha, Enable loopbackBuild, Enable vscode, Enable docker, Enable repositories, Enable services
    
**Model:**
::

    Now we can begin working on the representation of our data for use with LoopBack 4, which needs to aglin with what is in our . To that end, we’re going to create an issue and buy model that can represent instances of a task for our papercontract. A model describes business domain objects and defines a list of properties with name, type, and other constraints. Models are used for data exchange on the wire or between different systems. 
    
    tecadmin@ubuntubase:~/Desktop/magnetocorp$ lb4 model
    ? Model class name: getPaperRate
    ? Please select the model base class Entity (A persisted model with an ID)
    ? Allow additional (free-form) properties? No
    Let's add a property to GetPaperRate
    Enter an empty property name when done

    ? Enter the property name: issuer
    ? Property type: string
    ? Is issuer the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to GetPaperRate
    Enter an empty property name when done

    ? Enter the property name: paperNumber
    ? Property type: string
    ? Is paperNumber the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to GetPaperRate
    Enter an empty property name when done

    ? Enter the property name: 
       create src/models/get-paper-rate.model.ts
       update src/models/index.ts

    Model getPaperRate was created in src/models/
    
**Datasource:**
::

    Datasources are LoopBack’s way of connecting to various sources of data, such as databases, APIs, message queues and more. In LoopBack 4, datasources can be represented as strongly-typed objects and freely made available for injection throughout the application. Typically, in LoopBack 4, datasources are used in conjunction with Repositories to provide access to data.
    
    tecadmin@ubuntubase:~/Desktop/magnetocorp$ lb4 datasource
    ? Datasource name: db
    ? Select the connector for db: In-memory db (supported by StrongLoop)
    ? window.localStorage key to use for persistence (browser only):
    ? Full path to file for persistence (server only): ./data/db.json
       create src/datasources/db.datasource.json
       create src/datasources/db.datasource.ts
       update src/datasources/index.ts

    Datasource db was created in src/datasources/
    
**Repositories:**
::

    A Repository represents a specialized Service interface that provides strong-typed data access (for example, CRUD) operations of a domain model against the underlying database or service.
    
    tecadmin@ubuntubase:~/Desktop/magnetocorp$ lb4 repository
    ? Please select the datasource DbDatasource
    ? Select the model(s) you want to generate a repository (Press <space> to select, <a> to toggle all, <i> to invert selection)GetAllPapersFromIssuer, GetPaperRate, Issue
    ? Please select the repository base class DefaultCrudRepository (Legacy juggler bridge)
    ? Please enter the name of the ID property for GetAllPapersFromIssuer: id
    ? Please enter the name of the ID property for GetPaperRate: id
    ? Please enter the name of the ID property for Issue: id
       create src/repositories/get-all-papers-from-issuer.repository.ts
       create src/repositories/get-paper-rate.repository.ts
       create src/repositories/issue.repository.ts
       update src/repositories/index.ts
       update src/repositories/index.ts
       update src/repositories/index.ts
    
**Controller:**
::

    In LoopBack 4, controllers handle the request-response lifecycle for your API. Each function on a controller can be addressed individually to handle an incoming request (like a POST request to /todos), to perform business logic, and to return a response.
    
    tecadmin@ubuntubase:~/Desktop/magnetocorp$ lb4 controller
    ? Controller class name: Issue
    ? What kind of controller would you like to generate? REST Controller with CRUD functions
    ? What is the name of the model to use with this CRUD repository? Issue
    ? What is the name of your CRUD repository? IssueRepository
    ? What is the type of your ID? string
    ? What is the base HTTP path name of the CRUD operations? /issues
       create src/controllers/issue.controller.ts
       update src/controllers/index.ts

    Controller Issue was created in src/controllers/
    
You can find out more information and great tutorials as to how to build your own loopback API application here: https://loopback.io/doc/en/lb4/index.html

**3.** Within VSCode, go to the ``Edititor Perspective`` and do ``File -> Add Folder to Workplace`` and navigate to the ``magnetocorp`` folder that we just created within the ``Desktop`` folder. Go ahead and open that folder in VScode.

**4.** Now within VSCode, right click on ``magnetocorp`` - the folder you just opened in VSCode. Once you right click, select ``New Folder`` and name it ``data``. Really mysterious right? 

**5.** On the newly created folder, ``data``, right click on that folder and select ``New File`` and name that file ``db.json``. Within that new file, add in this text below
::

    {
      "ids": {
        "Todo": 5
      },
      "models": {
        "Todo": {
          "1": "{\"title\":\"Take over the galaxy\",\"desc\":\"MWAHAHAHAHAHAHAHAHAHAHAHAHAMWAHAHAHAHAHAHAHAHAHAHAHAHA\",\"id\":1}",
          "2": "{\"title\":\"destroy alderaan\",\"desc\":\"Make sure there are no survivors left!\",\"id\":2}",
          "3": "{\"title\":\"terrorize senate\",\"desc\":\"Tell them they're getting a budget cut.\",\"id\":3}",
          "4": "{\"title\":\"crush rebel scum\",\"desc\":\"Every.Last.One.\",\"id\":4}"
        }
    }

**Go ahead and save this file!** This file, db.json, contains an example database.
    
**6.** Within the ``magnetocorp`` folder in VSCode, navigate to the following folder
::

    magnetocorp -> src -> repositories
    
You should see 5 files in there: ``README.md``, ``issue.respistory.ts``, ``get-paper-rate.respostory.ts``, ``get-all-papers-from-issuer.respostory.ts``, and ``index.ts``

**7.** Within the ``buy.respitory.ts`` file, add ``//`` on line 8. Look below as to what to do
::

    typeof Issue.prototype.id
    
    --- CHANGE TO ---
    
    // typeof Issue.prototype.id

**Go ahead and save this file!**
    
**8.** Do the same thing for ``get-paper-rate.respository.ts`` on line 8
::

    typeof GetPaperRate.prototype.id
    
    --- CHANGE TO ---
    
    // typeof GetPaperRate.prototype.id
    
**Go ahead and save this file!**

**9.** Do the same thing for ``get-all-papers-from-issuer.respository.ts`` on line 8
::

    typeof GetAllPapersFromIssuer.prototype.id
    
    --- CHANGE TO ---
    
    // typeof GetAllPapersFromIssuer.prototype.id
    
**Go ahead and save this file!**
    
**10.** Within the ``magnetocorp`` folder in VSCode, navigate to the following folder
::

    magnetocorp -> src -> controllers
    
You should see 6 files in there: ``README.md``, ``issue.controller.ts``, ``get-paper-rate.controller.ts``, ``get-all-papers-from-issuer.controller.ts``, ``ping.controller.ts``, and ``index.ts``

**11.** Within the ``issue.controller.ts`` file, delete all of its contents and paste in what is below
::

    // Copyright IBM Corp. 2017,2018. All Rights Reserved.
    // Node module: @loopback/example-todo
    // This file is licensed under the MIT License.
    // License text available at https://opensource.org/licenses/MIT

    import {
      del,
      get,
      getFilterSchemaFor,
      param,
      patch,
      post,
      put,
      requestBody,
    } from '@loopback/rest';
    import { Issue } from '../models';

    import { BlockChainModule } from '../blockchainClient';

    let blockchainClient = new BlockChainModule.BlockchainClient();

    export class IssueController {
      constructor() { }

      @post('/issue', {
        responses: {
          '200': {
            description: 'Todo model instance',
            content: { 'application/json': { schema: { 'x-ts-type': Issue } } },
          },
        },
      })
     async createIssue(@requestBody() requestBody: Issue): Promise<Issue> {
       console.log('Buy, requestBody: ')
        console.log(requestBody)


        let networkObj = await blockchainClient.connectToNetwork();
        if (!networkObj) {
         let errString = 'Error connecting to network';
          let issue = new Issue({ issuer: errString, paperNumber: errString, issueDateTime: errString, maturityDateTime: errString, paperRate: errString });
          return issue;
        }
        console.log('newtork obj: ')
        console.log(networkObj)

        let dataForIssue = {
          function: 'issue',
          issuer: requestBody.issuer,
          paperNumber: requestBody.paperNumber,
          issueDateTime: requestBody.issueDateTime,
          maturityDateTime: requestBody.maturityDateTime,
          faceValue: requestBody.faceValue,
          paperRate: requestBody.paperRate,
          contract: networkObj.contract
        };

        var resultAsBuffer = await blockchainClient.issue(dataForIssue);

        console.log('result from blockchainClient.submitTransaction in controller: ')
        console.log('result from blockchainClient.submitTransaction in controller: ')
        let result = JSON.parse(Buffer.from(JSON.parse(resultAsBuffer)).toString())
        let issue = new Issue({
          issuer: result.issuer, paperNumber: result.paperNumber, issueDateTime: result.issueDateTime,
          maturityDateTime: result.maturityDateTime, paperRate: result.paperRate
        });
        return issue;
      }

    }

**Go ahead and save this file!**
    
Below is a breakdown of this file above

Below, we are pulling in the `issue` model that we created when we created our loopback API application
::

    import { Issue } from '../models';
    
Below, we are only specifying a `post` API call. A post call, adds data, in this case a transaction against our blockchain network, to our ledgers
::

    @post('/issue', {
        responses: {
          '200': {
          
Below, we are actually submitting a transaction, a `issue` transaction. This transaction is looking for all the data fields we created in our `issue` model file. If all goes well, we will successfully `issue` a commercialpaper. 
::

     async createIssue(@requestBody() requestBody: Issue): Promise<Issue> {
       console.log('Buy, requestBody: ')
        console.log(requestBody)

        let networkObj = await blockchainClient.connectToNetwork();
        if (!networkObj) {
         let errString = 'Error connecting to network';
          let issue = new Issue({ issuer: errString, paperNumber: errString, issueDateTime: errString, maturityDateTime: errString, paperRate: errString });
          return issue;
        }
    

**12.** Within VSCode, right click on the ``src`` folder (within the ``magnetocorp`` folder) and select ``New File``. Go ahead and name this file ``blockchainClient.ts``

**13.** Within our new ``blockchainClient.ts`` file, paste in this code below
::

    import { json } from "body-parser";

    const yaml = require('js-yaml');
    const { FileSystemWallet, Gateway } = require('fabric-network');
    const fs = require('fs');

    // A wallet stores a collection of identities for use
    const wallet = new FileSystemWallet('/home/tecadmin/.fabric-vscode/local_fabric_wallet');


    export module BlockChainModule {

      export class BlockchainClient {
       async connectToNetwork() {

          const gateway = new Gateway();
    
          try {
            console.log('connecting to Fabric network...')


            const identityLabel = 'isabella';
           let connectionProfile = yaml.safeLoad(fs.readFileSync('/home/tecadmin/Desktop/magnetocorp/networkConnection.yaml', 'utf8'));

           let connectionOptions = {
             identity: identityLabel,
             wallet: wallet,
             discovery: {
               asLocalhost: true,
               enabled: true
             }
           };

          // Connect to gateway using network.yaml file and our certificates in _idwallet directory
          await gateway.connect(connectionProfile, connectionOptions);

        console.log('Connected to Fabric gateway.');

        // Connect to our local fabric
        const network = await gateway.getNetwork('mychannel');

        console.log('Connected to mychannel. ');

        // Get the contract we have installed on the peer
        const contract = await network.getContract('papercontract');


        let networkObj = {
          contract: contract,
          network: network
        };

        return networkObj;

      } catch (error) {
        console.log(`Error processing transaction. ${error}`);
        console.log(error.stack);
      } finally {
        console.log('Done connecting to network.');
        // gateway.disconnect();
      }

    }




       async issue(args: any) {

         console.log('args for issue: ')
         console.log(args)

         let response = await args.contract.submitTransaction(args.function,
           args.issuer, args.paperNumber, args.issueDateTime, args.maturityDateTime,
           args.faceValue, args.paperRate
         );

         return response;

       }
      }
    }

    
**Go ahead and save this file!** Below is a breakdown of our `blockchainClient.ts` file

Below, you'll see that we are specifing where our user's credientials are located to validate that our user can actually submit a transaction. 
::

    // A wallet stores a collection of identities for use
    const wallet = new FileSystemWallet('/home/tecadmin/Desktop/magnetocorp/local_fabric_wallet');
    
Below, we are saying that within the `.fabric-vscode/local_fabric_wallet` folder we are using `User1@org1.example.com` as our user. Also, we are saying that our connection profile is `networkConnection.yaml` located one directory back. We will copy the connection profile in the next section.
::

    const identityLabel = 'isabella';
    let connectionProfile = yaml.safeLoad(fs.readFileSync('/home/tecadmin/Desktop/magnetocorp/networkConnection.yaml', 'utf8'));
    
Below, we are connection to our channel, called `mychannel`, and also using our smart contract, called `papercontract`
::

    // Connect to our local fabric
    const network = await gateway.getNetwork('mychannel');

    console.log('Connected to mychannel. ');

    // Get the contract we have installed on the peer
    const contract = await network.getContract('papercontract');
    
Below, we are actually submitting our `issue` transaction. There is a very similar transaction. This will use our `issue` controller as a basis for our actual arguments (args). 
::

       async issue(args: any) {

         console.log('args for issue: ')
         console.log(args)

         let response = await args.contract.submitTransaction(args.function,
           args.issuer, args.paperNumber, args.issueDateTime, args.maturityDateTime,
           args.faceValue, args.paperRate
         );

         return response;

       }

**14.** Now, we need to copy our ``networkConnection.yaml`` file over from ``magnetocorp`` in our ``fabric-samples-cp`` folder and place it into our ``magnetocorp`` folder. You can execute the command below, from our CLI application, as to how to copy 
::

    tecadmin@ubuntubase:~/Desktop/magnetocorp$ cp /home/tecadmin/Desktop/fabric-samples-cp/commercial-paper/organization/magnetocorp/gateway/networkConnection.yaml .
    
**15.** From VSCode, go to the IBM Blockchain Platform extension and right click on ``local_fabric_wallet`` and select ``Add Identity to Wallet``. From there follow the prompt as it follows below
::

    Provide a Name for the Identity:
        isabella
    Enter MSPID:
        Org1MSP
    Choose a method of adding an identity:
        Provide an enrollment ID and secret
    Enter Enrollment ID:
        admin
    Enter Enrollment secret:
        adminpw
    
**16.** We need to modify our ``package.json`` file to include the ``fabric-network`` module. Within our ``magnetocorp`` folder, find the ``package.json`` file and add in the following text below on ``line 58``
::

    "fabric-network": "~1.4.1"
    
So now our ``dependecies`` look like this
::

    "dependencies": {
        "@loopback/boot": "^1.4.0",
        "@loopback/context": "^1.19.0",
        "@loopback/core": "^1.8.1",
        "@loopback/openapi-v3": "^1.6.1",
        "@loopback/repository": "^1.6.1",
        "@loopback/rest": "^1.15.0",
        "@loopback/rest-explorer": "^1.2.1",
        "@loopback/service-proxy": "^1.2.1",
        "fabric-network": "~1.4.1"
    
**Do not forget to add a comma (,) after the "@loopback/service-proxy": "^1.2.1" dependency**

**Go ahead and save this file!**

**17.** Now we can delete the ``node_modules`` and ``package-lock.json`` file so that it will pick up the ``fabric-network`` package on we install again. To do this, within VSCode, right click on ``node_modules`` and select ``Delete``. Do the same for ``node_modules``. If it asks you to confirm this, select ``Move to Trash``.

**18.** Back in our CLI application, do an ``npm install`` within the ``digibank`` folder
::

    tecadmin@ubuntubase:~/Desktop/magnetocorp$ npm install
    *
    *
    *
    added 748 packages from 1578 contributors and audited 4980 packages in 45.757s
    found 3 vulnerabilities (1 low, 2 moderate)
    
**19.** Then you can do an ``npm build`` as well from the same folder
::

    tecadmin@ubuntubase:~/Desktop/digibank$ npm run build

    > digibank@1.0.0 build /home/tecadmin/Desktop/magnetocorp
    > lb-tsc es2017 --outDir dist
    
**20.** We will hold off on starting the server until we have built the DigiBank loopback application as well. 

**21.** Speaking of DigiBank, let's build their loopback API application. It will be very similar to how we built DigiBank's. 

**22.** Go ahead and follow the series of commands and prompts below to create MagnetoCorp's loopback application. I'll explain these after we have completed this.
::

    ----- Create Our App -----
    
    tecadmin@ubuntubase:~/Desktop$ lb4 app
    ? Project name: digibank
    ? Project description: loopback api for digibank
    ? Project root directory: digibank
    ? Application class name: DigibankApplication
    ? Select features to enable in the project (Press <space> to select, <a> to toggle all, <i> to invert selection)Enable eslint, Enable prettier, Enable mocha, Enable loopbackBuild, Enable vscode, Enable docker, Enable repositories, Enable services
       create .eslintignore
       create .eslintrc.js
       create .mocharc.json
       create .npmrc
       create .prettierignore
       create .prettierrc
       create DEVELOPING.md
       create README.md
       create index.ts
       create package.json
       create tsconfig.json
       create .vscode/settings.json
       create .vscode/tasks.json
       create .gitignore
       create .dockerignore
       create Dockerfile
       create index.js
       create public/index.html
       create src/application.ts
       create src/index.ts
       create src/migrate.ts
       create src/sequence.ts
       create src/__tests__/README.md
       create src/controllers/README.md
       create src/controllers/index.ts
       create src/controllers/ping.controller.ts
       create src/datasources/README.md
       create src/models/README.md
       create src/repositories/README.md
       create src/__tests__/acceptance/home-page.acceptance.ts
       create src/__tests__/acceptance/ping.controller.acceptance.ts
       create src/__tests__/acceptance/test-helper.ts


    Application digibank was created in digibank.
    
    
    ----- Create Model for our Buy -----

    tecadmin@ubuntubase:~/Desktop$ cd digibank/
    tecadmin@ubuntubase:~/Desktop/digibank$ lb4 model
    ? Model class name: buy
    ? Please select the model base class Entity (A persisted model with an ID)
    ? Allow additional (free-form) properties? No
    Let's add a property to Buy
    Enter an empty property name when done

    ? Enter the property name: issuer
    ? Property type: string
    ? Is issuer the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to Buy
    Enter an empty property name when done

    ? Enter the property name: paperNumber
    ? Property type: string
    ? Is paperNumber the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to Buy
    Enter an empty property name when done

    ? Enter the property name: currentOwner
    ? Property type: string
    ? Is currentOwner the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to Buy
    Enter an empty property name when done

    ? Enter the property name: newOwner
    ? Property type: string
    ? Is newOwner the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to Buy
    Enter an empty property name when done

    ? Enter the property name: price
    ? Property type: string
    ? Is price the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to Buy
    Enter an empty property name when done

    ? Enter the property name: purchaseDateTime
    ? Property type: string
    ? Is purchaseDateTime the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to Buy
    Enter an empty property name when done

    ? Enter the property name: 
       create src/models/buy.model.ts
       update src/models/index.ts

    Model buy was created in src/models/
    
    ----- Create Model for our Redeem -----

    tecadmin@ubuntubase:~/Desktop/digibank$ lb4 model
    ? Model class name: redeem
    ? Please select the model base class Entity (A persisted model with an ID)
    ? Allow additional (free-form) properties? No
    Let's add a property to Redeem
    Enter an empty property name when done

    ? Enter the property name: issuer
    ? Property type: string
    ? Is issuer the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to Redeem
    Enter an empty property name when done

    ? Enter the property name: paperNumber
    ? Property type: string
    ? Is paperNumber the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to Redeem
    Enter an empty property name when done

    ? Enter the property name: redeemingOwner
    ? Property type: string
    ? Is redeemingOwner the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to Redeem
    Enter an empty property name when done

    ? Enter the property name: redeemingOwner
    ? Property type: string
    ? Is redeemingOwner the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to Redeem
    Enter an empty property name when done

    ? Enter the property name: 
       create src/models/redeem.model.ts
       update src/models/index.ts

    Model redeem was created in src/models/
    
    ----- Create Model for our getPaperRate -----

    tecadmin@ubuntubase:~/Desktop/digibank$ lb4 model
    ? Model class name: getPaperRate
    ? Please select the model base class Entity (A persisted model with an ID)
    ? Allow additional (free-form) properties? No
    Let's add a property to GetPaperRate
    Enter an empty property name when done

    ? Enter the property name: issuer
    ? Property type: string
    ? Is issuer the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to GetPaperRate
    Enter an empty property name when done

    ? Enter the property name: paperNumber
    ? Property type: string
    ? Is paperNumber the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to GetPaperRate
    Enter an empty property name when done

    ? Enter the property name: 
       create src/models/get-paper-rate.model.ts
       update src/models/index.ts

    Model getPaperRate was created in src/models/
    
    ----- Create Model for our getAllPapersFromIssuer -----

    tecadmin@ubuntubase:~/Desktop/digibank$ lb4 model
    ? Model class name: getAllPapersFromIssuer
    ? Please select the model base class Entity (A persisted model with an ID)
    ? Allow additional (free-form) properties? No
    Let's add a property to GetAllPapersFromIssuer
    Enter an empty property name when done

    ? Enter the property name: paperIssuer
    ? Property type: string
    ? Is paperIssuer the ID property? No
    ? Is it required?: Yes
    ? Default value [leave blank for none]: 

    Let's add another property to GetAllPapersFromIssuer
    Enter an empty property name when done

    ? Enter the property name: 
       create src/models/get-all-papers-from-issuer.model.ts
       update src/models/index.ts

    Model getAllPapersFromIssuer was created in src/models/

        ----- Create a Datasource -----
        
    tecadmin@ubuntubase:~/Desktop/digibank$ lb4 datasource
    ? Datasource name: db
    ? Select the connector for db: In-memory db (supported by StrongLoop)
    ? window.localStorage key to use for persistence (browser only): 
    ? Full path to file for persistence (server only): ./data/db.json
       create src/datasources/db.datasource.json
       create src/datasources/db.datasource.ts
       update src/datasources/index.ts

    Datasource db was created in src/datasources/
    
        ----- Create a Repository -----    

    tecadmin@ubuntubase:~/Desktop/digibank$ lb4 repository
    ? Please select the datasource DbDatasource
    ? Select the model(s) you want to generate a repository (Press <space> to select, <a> to toggle all, <i> to invert selection)Buy, GetAllPapersFromIssuer, GetPaperRate, Redeem
    ? Please select the repository base class DefaultCrudRepository (Legacy juggler bridge)
    ? Please enter the name of the ID property for Buy: id
    ? Please enter the name of the ID property for GetAllPapersFromIssuer: id
    ? Please enter the name of the ID property for GetPaperRate: id
    ? Please enter the name of the ID property for Redeem: id
       create src/repositories/buy.repository.ts
       create src/repositories/get-all-papers-from-issuer.repository.ts
       create src/repositories/get-paper-rate.repository.ts
       create src/repositories/redeem.repository.ts
       update src/repositories/index.ts
       update src/repositories/index.ts
       update src/repositories/index.ts
       update src/repositories/index.ts

    Repositories BuyRepository,GetAllPapersFromIssuerRepository,GetPaperRateRepository,RedeemRepository was created in src/repositories/
    
    ----- Create a Controller for the Issue Transaction ----- 

    tecadmin@ubuntubase:~/Desktop/digibank$ lb4 controller
    ? Controller class name: Buy
    ? What kind of controller would you like to generate? REST Controller with CRUD functions
    ? What is the name of the model to use with this CRUD repository? Buy
    ? What is the name of your CRUD repository? BuyRepository
    ? What is the type of your ID? string
    ? What is the base HTTP path name of the CRUD operations? /buys
       create src/controllers/buy.controller.ts
       update src/controllers/index.ts

    Controller Buy was created in src/controllers/

    tecadmin@ubuntubase:~/Desktop/digibank$ lb4 controller
    ? Controller class name: Redeem
    ? What kind of controller would you like to generate? REST Controller with CRUD functions
    ? What is the name of the model to use with this CRUD repository? Redeem
    ? What is the name of your CRUD repository? RedeemRepository
    ? What is the type of your ID? string
    ? What is the base HTTP path name of the CRUD operations? /redeems
       create src/controllers/redeem.controller.ts
       update src/controllers/index.ts

    Controller Redeem was created in src/controllers/

    tecadmin@ubuntubase:~/Desktop/digibank$ lb4 controller
    ? Controller class name: GetPaperRate
    ? What kind of controller would you like to generate? REST Controller with CRUD functions
    ? What is the name of the model to use with this CRUD repository? GetPaperRate
    ? What is the name of your CRUD repository? GetPaperRateRepository
    ? What is the type of your ID? string
    ? What is the base HTTP path name of the CRUD operations? /get-paper-rates
       create src/controllers/get-paper-rate.controller.ts
       update src/controllers/index.ts

    Controller GetPaperRate was created in src/controllers/

    tecadmin@ubuntubase:~/Desktop/digibank$ lb4 controller
    ? Controller class name: GetAllPapersFromIssuer
    ? What kind of controller would you like to generate? REST Controller with CRUD functions
    ? What is the name of the model to use with this CRUD repository? GetAllPapersFromIssuer
    ? What is the name of your CRUD repository? GetAllPapersFromIssuerRepository
    ? What is the type of your ID? string
    ? What is the base HTTP path name of the CRUD operations? /get-all-papers-from-issuers
       create src/controllers/get-all-papers-from-issuer.controller.ts
       update src/controllers/index.ts

    Controller GetAllPapersFromIssuer was created in src/controllers/
    
You had to do the same thing for DigiBank, as you did for MagnetoCorp, and their loopback API application. 

**23.** Within VSCode, go to the ``Edititor Perspective`` and do ``File -> Add Folder to Workplace`` and navigate to the ``digibank`` folder that we just created within the ``Desktop`` folder. Go ahead and open that folder in VScode.

**24.** Now within VSCode, right click on ``digibank`` - the folder you just opened in VSCode. Once you right click, select ``New Folder`` and name it ``data``. Really mysterious right? 

**25.** On the newly created folder, ``data``, right click on that folder and select ``New File`` and name that file ``db.json``. Within that new file, add in this text below
::

    {
      "ids": {
        "Todo": 5
      },
      "models": {
        "Todo": {
          "1": "{\"title\":\"Take over the galaxy\",\"desc\":\"MWAHAHAHAHAHAHAHAHAHAHAHAHAMWAHAHAHAHAHAHAHAHAHAHAHAHA\",\"id\":1}",
          "2": "{\"title\":\"destroy alderaan\",\"desc\":\"Make sure there are no survivors left!\",\"id\":2}",
          "3": "{\"title\":\"terrorize senate\",\"desc\":\"Tell them they're getting a budget cut.\",\"id\":3}",
          "4": "{\"title\":\"crush rebel scum\",\"desc\":\"Every.Last.One.\",\"id\":4}"
        }
    }

**Go ahead and save this file!** This file, db.json, contains an example database.
    
**26.** Within the ``digibank`` folder in VSCode, navigate to the following folder
::

    digibank -> src -> repositories
    
You should see 6 files in there: ``README.md``, ``buy.respistory.ts``, ``redeem.respistory.ts``, ``get-paper-rate.respistory.ts``, ``get-all-papers-from-issuer.respistory.ts`` and ``index.ts``

**27.** Within the ``buy.respitory.ts`` file, add ``//`` on line 8. Look below as to what to do
::

    typeof Buy.prototype.id
    
    --- CHANGE TO ---
    
    // typeof Buy.prototype.id

**Go ahead and save this file!**

**28.** Within the ``Redeem.respitory.ts`` file, add ``//`` on line 8. Look below as to what to do
::

    typeof Redeem.prototype.id
    
    --- CHANGE TO ---
    
    // typeof Redeem.prototype.id

**Go ahead and save this file!**

**29.** Within the ``get-paper-rate.respistory.ts`` file, add ``//`` on line 8. Look below as to what to do
::

    typeof GetPaperRate.prototype.id
    
    --- CHANGE TO ---
    
    // typeof GetPaperRate.prototype.id

**Go ahead and save this file!**

**30.** Within the ``get-all-papers-from-issuer.respistory.ts`` file, add ``//`` on line 8. Look below as to what to do
::

    typeof GetAllPapersFromIssuer.prototype.id
    
    --- CHANGE TO ---
    
    // typeof GetAllPapersFromIssuer.prototype.id

**Go ahead and save this file!**
    
**31.** Within the ``digibank`` folder in VSCode, navigate to the following folder
::

    digibank -> src -> controllers
    
You should see 7 files in there: ``README.md``, ``buy.controller.ts``, ``redeem.controller.ts``, ``get-paper-rate.controller.ts``, ``get-papers-from-issuer.controller.ts``, ``ping.controller.ts``, and ``index.ts``

**32.** Within the ``buy.controller.ts`` file, delete all of its contents and paste in the code that is below
::

    // Copyright IBM Corp. 2017,2018. All Rights Reserved.
    // Node module: @loopback/example-todo
    // This file is licensed under the MIT License.
    // License text available at https://opensource.org/licenses/MIT

    import {
      del,
      get,
      getFilterSchemaFor,
      param,
      patch,
      post,
      put,
      requestBody,
    } from '@loopback/rest';
    import { Buy } from '../models';

    import { BlockChainModule } from '../blockchainClient';

    let blockchainClient = new BlockChainModule.BlockchainClient();

    export class BuyController {
      constructor() { }

      @post('/buy', {
        responses: {
          '200': {
            description: 'Todo model instance',
            content: { 'application/json': { schema: { 'x-ts-type': Buy } } },
          },
        },
      })
      async createBuy(@requestBody() requestBody: Buy): Promise<Buy> {
        console.log('Buy, requestBody: ')
        console.log(requestBody)
        let networkObj = await blockchainClient.connectToNetwork();
        if (!networkObj) {
         let errString = 'Error connecting to network';
          let buy = new Buy({
          issuer: errString, paperNumber: errString, currentOwner: errString, newOwner: errString,
          price: errString, purchaseDateTime: errString
         });
         return buy;
        }
        console.log('newtork obj: ')
        console.log(networkObj)
        // dateStr = dateStr.toDateString();
        let dataForBuy = {
          function: 'buy',
          issuer: requestBody.issuer,
          paperNumber: requestBody.paperNumber,
          currentOwner: requestBody.currentOwner,
          newOwner: requestBody.newOwner,
          price: requestBody.price,
          purchaseDateTime: requestBody.purchaseDateTime,
          contract: networkObj.contract
        };

       var resultAsBuffer = await blockchainClient.buy(dataForBuy);

        console.log('result from blockchainClient.submitTransaction in controller: ')
        let result = JSON.parse(Buffer.from(JSON.parse(resultAsBuffer)).toString())
        let buy = new Buy({
          issuer: result.issuer, paperNumber: result.paperNumber, currentOwner: result.currentOwner,
          newOwner: result.currentOwner, price: result.price, purchaseDateTime: result.purchaseDateTime
        });
        return buy;
      }

    }
  
**Go ahead and save this file!**

**33.** Within the ``redeem.controller.ts`` file, delete all of its contents and paste in the code that is below
::

    // Copyright IBM Corp. 2017,2018. All Rights Reserved.
    // Node module: @loopback/example-todo
    // This file is licensed under the MIT License.
    // License text available at https://opensource.org/licenses/MIT

    import {
      del,
      get,
      getFilterSchemaFor,
      param,
      patch,
      post,
      put,
      requestBody,
    } from '@loopback/rest';
    import { Redeem } from '../models';

    import { BlockChainModule } from '../blockchainClient';

    let blockchainClient = new BlockChainModule.BlockchainClient();

    export class RedeemController {
      constructor() { }

      @post('/redeem', {
        responses: {
          '200': {
            description: 'Todo model instance',
            content: { 'application/json': { schema: { 'x-ts-type': Redeem } } },
          },
        },
      })
      async createIssue(@requestBody() requestBody: Redeem): Promise<Redeem> {
        console.log('Buy, requestBody: ')
        console.log(requestBody)

        let networkObj = await blockchainClient.connectToNetwork();
        if (!networkObj) {
          let errString = 'Error connecting to network';
          let redeem = new Redeem({
            issuer: errString, paperNumber: errString, redeemingOwner: errString,
            redeemDateTime: errString
              });
          return redeem;
        }
        console.log('newtork obj: ')
        console.log(networkObj)

        let dataForRedeem = {
          function: 'redeem',
          issuer: requestBody.issuer,
          paperNumber: requestBody.paperNumber,
          redeemingOwner: requestBody.redeemingOwner,
          redeemDateTime: requestBody.redeemDateTime,
          contract: networkObj.contract
        };

        var resultAsBuffer = await blockchainClient.redeem(dataForRedeem);

       console.log('result from blockchainClient.submitTransaction in controller: ')
       let result = JSON.parse(Buffer.from(JSON.parse(resultAsBuffer)).toString())
       let issue = new Redeem({
          issuer: result.issuer, paperNumber: result.paperNumber, redeemingOwner: result.redeemingOwner,
          redeemDateTime: result.redeemDateTime
        });
        return issue;
      }

    }

**Go ahead and save this file!**

**34.** Within VSCode, right click on the ``src`` folder (within the ``digibank`` folder) and select ``New File``. Go ahead and name this file ``blockchainClient.ts``

**35.** Within our new ``blockchainClient.ts`` file, paste in this code below
::

    const yaml = require('js-yaml');
    const { FileSystemWallet, Gateway } = require('fabric-network');
    const fs = require('fs');

    // A wallet stores a collection of identities for use
    const wallet = new FileSystemWallet('/home/tecadmin/.fabric-vscode/local_fabric_wallet');


    export module BlockChainModule {

      export class BlockchainClient {
        async connectToNetwork() {

          const gateway = new Gateway();
        
          try {
            console.log('connecting to Fabric network...')


            const identityLabel = 'balaji';
            let connectionProfile = yaml.safeLoad(fs.readFileSync('/home/tecadmin/Desktop/digibank/networkConnection.yaml', 'utf8'));

            let connectionOptions = {
              identity: identityLabel,
              wallet: wallet,
              discovery: {
                asLocalhost: true,
                enabled: true
              }
            };

            // Connect to gateway using network.yaml file and our certificates in _idwallet directory
            await gateway.connect(connectionProfile, connectionOptions);

            console.log('Connected to Fabric gateway.');

            // Connect to our local fabric
            const network = await gateway.getNetwork('mychannel');
    
            console.log('Connected to mychannel. ');

            // Get the contract we have installed on the peer
            const contract = await network.getContract('papercontract');


            let networkObj = {
              contract: contract,
              network: network
            };

            return networkObj;

          } catch (error) {
            console.log(`Error processing transaction. ${error}`);
            console.log(error.stack);
          } finally {
            console.log('Done connecting to network.');
            // gateway.disconnect();
          }

        }
    
        async redeem(args: any) {

          console.log('args for redeem: ')
          console.log(args)

          let response = await args.contract.submitTransaction(args.function,
            args.issuer, args.paperNumber, args.redeemingOwner, args.redeemDateTime
          );

          return response;
        }


        async buy(args: any) {

          console.log('args for buy: ')
          console.log(args)

          let response = await args.contract.submitTransaction(args.function,
            args.issuer, args.paperNumber, args.currentOwner, args.newOwner,
            args.price, args.purchaseDateTime
          );

          return response;

        }
      }
    }

    
**Go ahead and save this file!**

**36.** Now, we need to copy our ``networkConnection.yaml`` file over from ``digibank`` in our ``fabric-samples-cp`` folder and place it into our ``digibank`` folder. You can execute the command below, from our CLI application, as to how to copy 
::

    tecadmin@ubuntubase:~/Desktop/digibank$ cp /home/tecadmin/Desktop/fabric-samples-cp/commercial-paper/organization/digibank/gateway/networkConnection.yaml .
    
**37.** From VSCode, go to the IBM Blockchain Platform extension and right click on ``local_fabric_wallet`` and select ``Add Identity to Wallet``. From there follow the prompt as it follows below
::

    Provide a Name for the Identity:
        balaji
    Enter MSPID:
        Org1MSP
    Choose a method of adding an identity:
        Provide an enrollment ID and secret
    Enter Enrollment ID:
        admin
    Enter Enrollment secret:
        adminpw

**38.** Within our ``digibank`` folder in VSCode, find the ``index.js`` file. In here there is a port number we need to change. Since ``magnetocorp`` is occupying port ``3000``, we should make ``digibank`` occupy port ``3001``. You can find the port number within the ``index.js`` file on line 9. Look below at to what to do
::

    port: +process.env.PORT || 3000,
    
    --- CHANGE TO ---
    
    port: +process.env.PORT || 3001,

**39.** We need to modify our ``package.json`` file to include the ``fabric-network`` module. Within our ``digibank`` folder, find the ``package.json`` file and add in the following text below on ``line 58``
::

    "fabric-network": "~1.4.1"
    
So now our ``dependecies`` look like this
::

      "dependencies": {
        "@loopback/boot": "^1.4.0",
        "@loopback/context": "^1.19.0",
        "@loopback/core": "^1.8.1",
        "@loopback/openapi-v3": "^1.6.1",
        "@loopback/repository": "^1.6.1",
        "@loopback/rest": "^1.15.0",
        "@loopback/rest-explorer": "^1.2.1",
        "@loopback/service-proxy": "^1.2.1",
        "fabric-network": "~1.4.1"
    
**Do not forget to add a comma (,) after the "@loopback/service-proxy": "^1.2.1" dependency**

**Go ahead and save this file!**

**40.** Now we can delete the ``node_modules`` and ``package-lock.json`` file so that it will pick up the ``fabric-network`` package on we install again. To do this, within VSCode, right click on ``node_modules`` and select ``Delete``. Do the same for ``node_modules``. If it asks you to confirm this, select ``Move to Trash``.

**41.** Back in our CLI application, do an ``npm install`` within the ``digibank`` folder
::

    tecadmin@ubuntubase:~/Desktop/digibank$ npm install
    *
    *
    *
    added 748 packages from 1578 contributors and audited 4980 packages in 45.757s
    found 3 vulnerabilities (1 low, 2 moderate)
    
**42.** Then you can do an ``npm build`` as well from the same folder
::

    tecadmin@ubuntubase:~/Desktop/digibank$ npm run build

    > magnetocorp-commercialpaper@1.0.0 build /home/tecadmin/Desktop/digibank
    > lb-tsc es2017 --outDir dist
    
**43.** Now, we can start both loopback applications. Let's first go start DigiBank's. To do this, find go to your CLI application - where you generate the ``digibank`` folder. Then run the command below
::

    tecadmin@ubuntubase:~/Desktop/digibank$ npm start

    > digibank@1.0.0 prestart /home/tecadmin/Desktop/magnetocorp
    > npm run build


    > digibank@1.0.0 build /home/tecadmin/Desktop/magnetocorp
    > lb-tsc es2017 --outDir dist


    > digibank@1.0.0 start /home/tecadmin/Desktop/magnetocorp
    > node .

    Server is running at http://[::1]:3000
    Try http://[::1]:3000/ping
    
**44.** Then go to your ``digibank`` CLI application and do the same command
::

    tecadmin@ubuntubase:~/Desktop/digibank$ npm start

    > magnetocorp-commercialpaper@1.0.0 prestart /home/tecadmin/Desktop/digibank
    > npm run build


    > magnetocorp-commercialpaper@1.0.0 build /home/tecadmin/Desktop/digibank
    > lb-tsc es2017 --outDir dist


    > magnetocorp-commercialpaper@1.0.0 start /home/tecadmin/Desktop/digibank
    > node .

    Server is running at http://[::1]:3001
    Try http://[::1]:3001/ping
    
**45.** Proceed to go to ``MagnetoCorp's`` loopback application by going to ``http://[::1]:3000``

![image](vscode-images/2-6-39.png)

**46.** Do the same, but this time for DigiBank. You can go to ``http://[::1]:3001``. It should look the same as MagnetoCorp, but says ``DigiBank's`` instead. 

**47.** You can move forward **with both loopback applications** by clicking on the ``/explorer`` link toward the bottom

**48.** Within the ``MagnetoCorp`` loopback UI (``port 3000``), go ahead and toggle on the ``Issue`` controller. Then click on ``Try it Out``.

![image](vscode-images/2-6-42.png)

**49.** Then paste in the code below to issue a new paper in the white space
::

    {
      "issuer": "MagnetoCorp",
      "paperNumber": "00005",
      "issueDateTime": "2020-05-31",
      "maturityDateTime": "2020-11-30",
      "faceValue": "5000000",
      "paperRate": "0.02"
    }
    
**50.** Once you have the new paper in there, go ahead and click on the blue ``Execute`` button below

**51.** Then you will see the output of our ``issue`` transaction

![image](vscode-images/2-6-45.png)

Don't be alarm by the the ``faceValue`` and ``paperRate`` not appearing in our response. We will confirm that it actually went through here in a second.
    
**52.** From the IBM Blockchain Platform extension in VSCode, connect to the ``local_fabric`` Fabric Gateway and select ``balaji`` as your identity to connect with (it will pop up in the top middle). Then untoggle till you see the ``buy`` transaction under our ``papercontract@0.0.2`` smart contract. Enter the code below - between the brackets - to submit this transaction
::

    "MagnetoCorp", "00005", "MagnetoCorp", "DigiBank", "4900000", "2019-07-31"
    
You should see a success message below in the bottom right
    
**53.** From same Fabric Gateway, right click on ``getAllPapersFromIssuer`` and select ``Evaluate Transaction``. Enter the code below - between the brackets - to submit the query
::

    "MagnetoCorp"
    
You should see all of the MagnetoCorp issued papers

![image](vscode-images/2-6-53.png)
    
**54.** Now, let's go to our ``DigiBank`` loopback application (port: ``3001``) and do a ``redeem`` transaction. To do this, untoggle the ``Redeem`` controller and click on ``Try it out``

**55.** Then paste in what is below in the white space
::

    {
      "issuer": "MagnetoCorp",
      "paperNumber": "00005",
      "redeemingOwner": "DigiBank",
      "redeemDateTime": "2020-11-30"
    }
    
**56.** Once you have that in place, go ahead and click on the blue ``Execute`` button. 
    
Feel free to submit transactions some more through the loopback applications and VSCode. Once you are done, go ahead and clean up the lab station so we can have more fun the labs coming up.
