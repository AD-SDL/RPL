# Purpose
The purpose of this package is to house all the message and service types 

# Services 

## Destroy
**Requests -**  
string: id, type  

**Response -**  
int64: status  

## GetId
**Requests -**  
None  

**Response -**  
string: name, id, type  

## GetNextTransfer 
**Requests -**  
None   

**Response -**  
int64: status  
string: next_transfer

## GetNodeInfo
**Requests -**  
string: name_or_id  

**Response -**  
Message (NodeEntry): entry  
int64: status  

## GetNodeList
**Requests -**  
None  

**Response -**  
Array of Message (NodeEntry): node_list  
int64 status  

## LoadService
**Requests -**  
string: name, contents
bool: replace    

**Response -**  
int64: status

## LoadTransfer
**Requests -**  
string: to_id, to_name, from_id, from_name, item, cur_name, other_name  

**Response -**  
int64: status

## Protocol
**Requests -**  
None  

**Response -**  
int64: status

## Register
**Requests -**  
string: name, type  

**Response -**  
int64: status  
string: id

## Run
**Requests -**  
string: id, type, file  

**Response -**  
int64: status

## SendFiles
**Requests -**  
string: files  

**Response -**  
int64: status

# Messages 

## ArmReset 
int64: state  
string: id  

## ArmStateUpdate  
int64: state  
string: id  

## CompletedOT2  
string: file  

## CompletedTransfer  
string: identifier_cur, identifier_other  

## NodeEntry
string: name, type, id  
int64: state  

## OT2Reset  
int64: state  
string: id    

## OT2StateUpdate  
int64: state  
string: id   