### Creating NodeId’s
Creating new NodeIds
```
from asyncua import ua
ua.NodeId(1, 2)  # Integer Identifier
ua.NodeId('Test', 2)  # String Identifier
NodeId(Identifier='Test', NamespaceIndex=2, NodeIdType=<NodeIdType.String: 3>)
ua.NodeId(b'Test', 2)  # Bytes Identifier
NodeId(Identifier=b'Test', NamespaceIndex=2, NodeIdType=<NodeIdType.ByteString: 5>)
```
NodeId can also be built from a single string
```
ua.NodeId.from_string('ns=2;i=4')
NodeId(Identifier=4, NamespaceIndex=2, NodeIdType=<NodeIdType.Numeric: 2>)
```
Functions
```
<key>=<val>
ua.NodeId.from_string(ns,(i,s,g,b), (srv,nsu))
```
### Accessing Nodes
client node get node
```
node = client.get_node("ns=2;i=2")
name = (await node.read_browse_name()).Name
value = (await node.read_value())
await node.write_value(5.0)
```
server node get node
```
parent = await node.get_parent()
print(parent)
```
node get parent
```
parent = await node.get_parent()
Node(NodeId(Identifier=1, NamespaceIndex=2, NodeIdType=<NodeIdType.FourByte: 1>))
```
node get child
```
await parent.get_children()
[Node(NodeId(Identifier=2, NamespaceIndex=2, NodeIdType=<NodeIdType.FourByte: 1>))]

 # Get a specific child (by NodeId) of a node
await parent.get_child("2:MyVariable")
Node(NodeId(Identifier=2, NamespaceIndex=2, NodeIdType=<NodeIdType.FourByte: 1>))
```