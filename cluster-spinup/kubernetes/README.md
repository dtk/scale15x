Install the kubernetes module
```
cd ~/dtk/modules/
mkdir kubernetes
cd kubernetes
dtk module install scale15-lab/kubernetes

Installing base module 'scale15-lab/kubernetes(0.5.0)' from dtkn catalog ... Done.
```

Create an instance of the kuberentes cluster
```
dtk stage -n kub-cluster1
[INFO] Service instance 'kub-cluster1' has been created. In order to work with service instance, please navigate to: /home/ubuntu/dtk/service/kub-cluster1

cd /home/ubuntu/dtk/service/kub-cluster1
```
Deploy the kubernetes cluster three nodes
```
dtk converge
---
task_id: 2147484958`
```
Can track bring up of cluster using 'dtk task-status' or 'dtk task-status -m refresh'
```
dtk task-status
+-------------------------------+-----------+--------+----------+-------------------+-------------------+
| TASK TYPE                     | STATUS    | NODE   | DURATION | STARTED AT        | ENDED AT          |
+-------------------------------+-----------+--------+----------+-------------------+-------------------+
| assembly_converge             | succeeded |        | 363.5s   | 01:11:46 02/03/17 | 01:17:50 02/03/17 |
|   1 create_nodes_stage        | succeeded |        | 265.6s   | 01:11:46 02/03/17 | 01:16:12 02/03/17 |
|     1.1 create_node           | succeeded | node:1 | 256.2s   | 01:11:46 02/03/17 | 01:16:03 02/03/17 |
|     1.2 create_node           | succeeded | node:2 | 265.6s   | 01:11:46 02/03/17 | 01:16:12 02/03/17 |
|     1.3 create_node           | succeeded | master | 163.3s   | 01:11:46 02/03/17 | 01:14:30 02/03/17 |
|   2 kubernetes install        | succeeded |        | 36.2s    | 01:16:12 02/03/17 | 01:16:48 02/03/17 |
|     2.1 configure_node        | succeeded | master | 33.1s    | 01:16:12 02/03/17 | 01:16:45 02/03/17 |
|     2.2 configure_nodegroup   | succeeded | node   | 36.2s    | 01:16:12 02/03/17 | 01:16:48 02/03/17 |
|       2.2.1 configure_node    | succeeded | node:1 | 36.1s    | 01:16:12 02/03/17 | 01:16:48 02/03/17 |
|       2.2.2 configure_node    | succeeded | node:2 | 34.6s    | 01:16:12 02/03/17 | 01:16:47 02/03/17 |
|   3 kubernetes config master  | succeeded |        | 46.4s    | 01:16:48 02/03/17 | 01:17:35 02/03/17 |
|     3.1 configure_node        | succeeded | master | 46.4s    | 01:16:48 02/03/17 | 01:17:35 02/03/17 |
|   4 kubernetes cluster config | succeeded |        | 6.8s     | 01:17:35 02/03/17 | 01:17:42 02/03/17 |
|     4.1 configure_node        | succeeded | master | 6.8s     | 01:17:35 02/03/17 | 01:17:42 02/03/17 |
|   5 kubernetes config nodes   | succeeded |        | 8.0s     | 01:17:42 02/03/17 | 01:17:50 02/03/17 |
|     5.1 configure_nodegroup   | succeeded | node   | 8.0s     | 01:17:42 02/03/17 | 01:17:50 02/03/17 |
|       5.1.1 configure_node    | succeeded | node:1 | 7.6s     | 01:17:42 02/03/17 | 01:17:50 02/03/17 |
|       5.1.2 configure_node    | succeeded | node:2 | 8.0s     | 01:17:42 02/03/17 | 01:17:50 02/03/17 |
+-------------------------------+-----------+--------+----------+-------------------+-------------------+
18 rows in set
```
Log into master
```
dtk ssh -u ubuntu master
[INFO] You are entering SSH terminal (ubuntu@ec2-54-91-139-58.compute-1.amazonaws.com) ...
Warning: Permanently added 'ec2-54-91-139-58.compute-1.amazonaws.com' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.2 LTS (GNU/Linux 4.4.0-64-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud
```
Tear down cluster
```
dtk uninstall --delete
Are you sure you want to uninstall the infrastructure associated with 'kub-cluster1' and delete this service instance from the server? (yes|no)
yes
```
