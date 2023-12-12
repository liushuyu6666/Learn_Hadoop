# HDFS
## overview
break up files into chunk. (horizontal or vertical split) ??
store in individual hard drive, 
process in parallel, 
physically close,
more than one copy for failure,
buy commodity computer
name node: where to go to find the copy, log, track everything on the data node 
data node: client also need to access to them
## read
talk to name node -> which data node -> to a specific data node (API can be used in your app)
## write
talk to name node -> create a new entry for new data -> send to data node -> data node talk to each other, replicate those blocks across multiple nodes -> stored -> acknowledge the client node -> name node know new files exists
## name node resilience
1. back up metadata: local disk and NFS backup (what is NFS)
2. secondary name node: make copy from the primary at all time
3. HDFS federation: namespace, only lose portion of the data
4. HDFS high availability: hot backup name node, use zookeeper

