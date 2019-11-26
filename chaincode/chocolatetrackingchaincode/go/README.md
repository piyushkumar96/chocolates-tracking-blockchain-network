# Commands for install, instantiate, invoke, query with chaincode

#create package of chaindode

docker exec -it cli peer chaincode package -n chtrkcc  -p github.com/chaincode/chocolatetrackingchaincode/go/  -v 1.0 -s -S -i "AND('OrgA.admin')" ccpack.out

#sign the package

docker exec -it cli peer chaincode signpackage ccpack.out signedccpack.out

#Install chaincode

docker exec -it cli peer chaincode install -n chtrkcc  -v 1.0 -p github.com/chaincode/chocolatetrackingchaincode/go/

#Instaintiating chaincode

docker exec -it cli peer chaincode instantiate -o orderer.chocotrackingntw.com:7050 --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/chocotrackingntw.com/orderers/orderer.chocotrackingntw.com/msp/tlscacerts/tlsca.chocotrackingntw.com-cert.pem -C chocotrackchannel -n chtrkcc   -v 1.0 -c '{"Args":["init"]}' -P "OR ('Org1MSP.peer','Org2MSP.peer')"

#Invoke Chaincode

docker exec -it cli peer chaincode invoke -o orderer.chocotrackingntw.com:7050 --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/chocotrackingntw.com/orderers/orderer.chocotrackingntw.com/msp/tlscacerts/tlsca.chocotrackingntw.com-cert.pem -C chocotrackchannel -n chtrkcc -c '{"Args":[ "createCocoaBeanBag","BB101", "IN", "F201"]}'


docker exec -it cli peer chaincode invoke -o orderer.chocotrackingntw.com:7050 --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/chocotrackingntw.com/orderers/orderer.chocotrackingntw.com/msp/tlscacerts/tlsca.chocotrackingntw.com-cert.pem -C chocotrackchannel -n chtrkcc -c '{"Args":[ "createChocolateBar", "B302", "BB101"]}'


#Query Chaincode

docker exec -it cli peer chaincode query -o orderer.chocotrackingntw.com:7050  -C chocotrackchannel -n chtrkcc -c '{"Args":[ "getCocoaBeanBagById","BB101"]}'

docker exec -it cli peer chaincode query -o orderer.chocotrackingntw.com:7050  -C chocotrackchannel -n chtrkcc -c '{"Args":[ "getChocolateBarById","B302"]}'

docker exec -it cli peer chaincode query -o orderer.chocotrackingntw.com:7050  -C chocotrackchannel -n chtrkcc -c '{"Args":[ "getCBCountryCount","IN"]}'


