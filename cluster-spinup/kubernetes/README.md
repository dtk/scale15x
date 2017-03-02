```
ubuntu@ip-172-31-14-21:~$ cd dtk/modules/
ubuntu@ip-172-31-14-21:~/dtk/modules$ mkdir kubernetes
ubuntu@ip-172-31-14-21:~/dtk/modules$ cd kubernetes
ubuntu@ip-172-31-14-21:~/dtk/modules/kubernetes$ dtk module install scale15-lab/kubernetes
Installing base module 'scale15-lab/kubernetes(0.5.0)' from dtkn catalog ... Done.
```

```
ubuntu@ip-172-31-14-21:~/dtk/modules/kubernetes$ dtk stage -n kub-cluster1
[INFO] Service instance 'kub-cluster1' has been created. In order to work with service instance, please navigate to: /home/ubuntu/dtk/service/kub-cluster1
ubuntu@ip-172-31-14-21:~/dtk/modules/kubernetes$ cd /home/ubuntu/dtk/service/kub-cluster1
ubuntu@ip-172-31-14-21:~/dtk/service/kub-cluster1$ dtk converge
---
task_id: 2147484958`
```
```
ubuntu@ip-172-31-14-21:~/dtk/service/kub-cluster1$ dtk task-status
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

