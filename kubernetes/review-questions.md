Qs:

1. Kubernetes Component that communicates with the workstation 
   - API Server

2. Kubernetes Component that STORE all cluster data in JSON documents
    ETCD Database

3. Role of KubeLet in worker nodes?
    Accept requests from 'scheduler' and gets the containers created or deleted from container runtime 'docker'

4. What is POD?
    A Wrapper for Containers. 
    All containers in POD are Co-located, they share the same NODE, POD IP, set Volumes.
    Only components that USE CPU, RAM and Network bandwidth.
    ReplicaSet provides Self Healing & Scalability to PODs
    Deployment provides RollingUpdates and rollback to previous versions.
    Jobs provide One Use POD. Not used for applications but for batch process.

5.  Rolling Update?

    Ability to deploy a newer or older version of same multi-instance application.
    Negligible downtime / no downtime.