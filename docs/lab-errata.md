     
##Lab 3 errata and notes:

*Steps 20 & 21* - These steps have commands that span multiple lines in the document (3 or 4). You cannot copy and paste from the document to the command line in one operation because newline characters in the document will cause it to be 3 different commands, which will fail. You either have to type the whole command by hand, or, what may be easier-  copy and paste the lines one at a time and then hit Enter after pasting the last line of the command in the terminal. Better yet, copy the commands from here:

 *Step 20 command*: 
```
docker exec cliMagnetoCorp peer chaincode install -n papercontract -v 0.0.3-p /opt/gopath/src/github.com/contract -l node
```
 *Step 21 command*:
```
docker exec cliMagnetoCorp peer chaincode instantiate -n papercontract -v 0.0.3-l node -c '{"Args":["org.papernet.commercialpaper:instantiate"]}' -C mychannel -P "AND ('Org1MSP.member')"
```

     
*Step 72*-ish  - you will see a popup asking you to choose between something like  ‘orderer.example.com’ or ‘peer0.org1.example.com’ --  choose the one that starts with peer*

*Step 95* – the instructions are missing the ” to the right of MagnetoCorp. It should be:
```
"MagnetoCorp","00005"
```

