[[opcua-asyncio]]] is a similar tool
# Syncronize
read data -> wait for reply ->use data
# Asyncronize 
## Polling
read data -> wait for reply 
				-> do other things ->check completion ->if complete use data and interrupt job
## Idle wait completion
read data -> wait for reply 
				-> do other things ->check completion ->if things not finish wait util finish -> use data
## Callback
read massive data x 3 ->Client thread x3 ->if all complete continue main thread
# Link
[Snap7 Client](https://snap7.sourceforge.net/snap7_client.html#smartconnect)
[Tutorials - S7-1200 & Snap7 Python](https://www.youtube.com/watch?v=2AkYBtDDpio)