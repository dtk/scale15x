Install the swarm module
```
cd dtk/modules/
mkdir swarm
cd swarm/
dtk module install scale15-lab/swarm

[INFO] Getting dependent module info for 'scale15-lab/swarm(0.6.0)' from dtkn catalog ...
[INFO] Installing dependent modules from dtkn catalog ...
Installing dependent module 'dtk-provider/ruby-provider(master)' ... Done.
Installing dependent module 'dtk_stdlib/dtk_stdlib(0.5.0)' ... Done.
Installing dependent module 'scale15/utils(0.5.0)' ... Done.
Installing dependent module 'puppetlabs/docker(5.3.0)' ... Done.
Installing dependent module 'puppetlabs/stdlib(master)' ... Done.
Installing dependent module 'repository/epel(master)' ... Done.
Installing dependent module 'puppetlabs/apt(master)' ... Done.
Installing base module 'scale15-lab/swarm(0.6.0)' from dtkn catalog ... Done.
```
Stage an instance of the kubernetes cluster
```
dtk stage -n swarm-cluster1
[INFO] Service instance 'swarm-cluster1' has been created. In order to work with service instance, please navigate to: 
```
Spin up the cluster
```
cd  /home/ubuntu/dtk/service/swarm-cluster1
dtk converge
---
task_id: 2147486222

```
```
ubuntu@ip-172-31-14-21:~/dtk/service/swarm-cluster1$ dtk task-status
+-----------------------------+-----------+----------+----------+-------------------+-------------------+
| TASK TYPE                   | STATUS    | NODE     | DURATION | STARTED AT        | ENDED AT          |
+-----------------------------+-----------+----------+----------+-------------------+-------------------+
| assembly_converge           | succeeded |          | 255.7s   | 01:39:49 02/03/17 | 01:44:05 02/03/17 |
|   1 create_nodes_stage      | succeeded |          | 201.3s   | 01:39:49 02/03/17 | 01:43:11 02/03/17 |
|     1.1 create_node         | succeeded | master   | 110.2s   | 01:39:49 02/03/17 | 01:41:40 02/03/17 |
|     1.2 create_node         | succeeded | worker:1 | 201.3s   | 01:39:49 02/03/17 | 01:43:11 02/03/17 |
|     1.3 create_node         | succeeded | worker:2 | 192.2s   | 01:39:49 02/03/17 | 01:43:02 02/03/17 |
|   2 apt_install             | succeeded |          | 19.7s    | 01:43:11 02/03/17 | 01:43:31 02/03/17 |
|     2.1 configure_nodegroup | succeeded | worker   | 19.7s    | 01:43:11 02/03/17 | 01:43:31 02/03/17 |
|       2.1.1 configure_node  | succeeded | worker:1 | 19.7s    | 01:43:11 02/03/17 | 01:43:31 02/03/17 |
|       2.1.2 configure_node  | succeeded | worker:2 | 15.2s    | 01:43:11 02/03/17 | 01:43:26 02/03/17 |
|     2.2 configure_node      | succeeded | master   | 16.7s    | 01:43:11 02/03/17 | 01:43:28 02/03/17 |
|   3 install gems            | succeeded |          | 4.0s     | 01:43:31 02/03/17 | 01:43:35 02/03/17 |
|     3.1 nodegroup actions   | succeeded | worker   | 4.0s     | 01:43:31 02/03/17 | 01:43:35 02/03/17 |
|       3.1.1 action          | succeeded | worker:1 | 3.2s     | 01:43:31 02/03/17 | 01:43:34 02/03/17 |
|       3.1.2 action          | succeeded | worker:2 | 4.0s     | 01:43:31 02/03/17 | 01:43:35 02/03/17 |
|     3.2 action              | succeeded | master   | 3.2s     | 01:43:31 02/03/17 | 01:43:34 02/03/17 |
|   4 provision docker        | succeeded |          | 26.4s    | 01:43:35 02/03/17 | 01:44:01 02/03/17 |
|     4.1 configure_nodegroup | succeeded | worker   | 26.0s    | 01:43:35 02/03/17 | 01:44:01 02/03/17 |
|       4.1.1 configure_node  | succeeded | worker:1 | 25.2s    | 01:43:35 02/03/17 | 01:44:00 02/03/17 |
|       4.1.2 configure_node  | succeeded | worker:2 | 26.0s    | 01:43:35 02/03/17 | 01:44:01 02/03/17 |
|     4.2 configure_node      | succeeded | master   | 26.3s    | 01:43:35 02/03/17 | 01:44:01 02/03/17 |
|   5 create swarm            | succeeded |          | 3.7s     | 01:44:01 02/03/17 | 01:44:05 02/03/17 |
|     5.1 configure_node      | succeeded | master   | 3.7s     | 01:44:01 02/03/17 | 01:44:05 02/03/17 |
+-----------------------------+-----------+----------+----------+-------------------+-------------------+
22 rows in set
```
See the cluster nodes using a dtk action
```
ubuntu@ip-172-31-14-21:~/dtk/service/swarm-cluster1$ dtk exec-sync master/swarm::cluster.list_swarm_nodes
========================= start 'swarm::cluster.list_swarm_nodes' =========================


============================================================
STAGE 1: configure_nodes
TIME START: 2017-03-02 01:49:16 +0000
ACTION: master/swarm::cluster.list_swarm_nodes
STATUS: succeeded
DURATION: 0.2s
RESULTS:

NODE: master
RUN: docker node ls (syscall)
RETURN CODE: 0
STDOUT:
  ID                           HOSTNAME          STATUS  AVAILABILITY  MANAGER STATUS
  93unccxrj6u89w6ssvj0h08ox    ip-172-31-14-79   Ready   Active
  xk43v1ybwqm0isz2ez5gnrb7l    ip-172-31-11-77   Ready   Active
  xt3lip9hosn2641b8qlftkps0 *  ip-172-31-11-255  Ready   Active        Leader

------------------------------------------------------------

========================= end: 'swarm::cluster.list_swarm_nodes' (total duration: 0.2s) =========================
```
Log into master mahine
```
ubuntu@ip-172-31-14-21:~/dtk/service/swarm-cluster1$ dtk ssh -u ubuntu master
[INFO] You are entering SSH terminal (ubuntu@ec2-184-72-73-247.compute-1.amazonaws.com) ...
Warning: Permanently added 'ec2-184-72-73-247.compute-1.amazonaws.com' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.2 LTS (GNU/Linux 4.4.0-64-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

6 packages can be updated.
0 updates are security updates.

```
```
ubuntu@ip-172-31-14-21:~/dtk/service/swarm-cluster1$ dtk uninstall --delete
Are you sure you want to uninstall the infrastructure associated with 'swarm-cluster1' and delete this service instance from the server? (yes|no)
yes
[INFO] DTK module 'swarm-cluster1' has been uninstalled successfully.
```
```

