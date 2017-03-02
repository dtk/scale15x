```
ubuntu@ip-172-31-14-21:~/dtk/service/kub-cluster1$ dtk ssh master
[INFO] You are entering SSH terminal (ubuntu@ec2-204-236-209-19.compute-1.amazonaws.com) ...
Warning: Permanently added 'ec2-204-236-209-19.compute-1.amazonaws.com' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.2 LTS (GNU/Linux 4.4.0-64-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

6 packages can be updated.
0 updates are security updates.


ubuntu@ip-172-31-13-96:~$ kubectl version
Client Version: version.Info{Major:"1", Minor:"5", GitVersion:"v1.5.2", GitCommit:"08e099554f3c31f6e6f07b448ab3ed78d0520507", GitTreeState:"clean", BuildDate:"2017-01-12T04:57:25Z", GoVersion:"go1.7.4", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"5", GitVersion:"v1.5.3", GitCommit:"029c3a408176b55c30846f0faedf56aae5992e9b", GitTreeState:"clean", BuildDate:"2017-02-15T06:34:56Z", GoVersion:"go1.7.4", Compiler:"gc", Platform:"linux/amd64"}
ubuntu@ip-172-31-13-96:~$ kubectl create -f http://fission.io/fission.yaml
namespace "fission" created
namespace "fission-function" created
deployment "controller" created
deployment "router" created
service "poolmgr" created
deployment "poolmgr" created
deployment "kubewatcher" created
service "etcd" created
deployment "etcd" created
ubuntu@ip-172-31-13-96:~$ kubectl create -f http://fission.io/fission-nodeport.yaml
service "router" created
service "controller" created
ubuntu@ip-172-31-13-96:~$ export FISSION_URL=http://localhost:31313
ubuntu@ip-172-31-13-96:~$ export FISSION_ROUTER=localhost:31314
ubuntu@ip-172-31-13-96:~$ curl http://fission.io/linux/fission > fission && chmod +x fission && sudo mv fission /usr/local/bin/
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 6408k  100 6408k    0     0  11.7M      0 --:--:-- --:--:-- --:--:-- 11.6M
ubuntu@ip-172-31-13-96:~$ fission env create --name nodejs --image fission/node-env
environment 'nodejs' created
ubuntu@ip-172-31-13-96:~$ cd
ubuntu@ip-172-31-13-96:~$ curl https://raw.githubusercontent.com/fission/fission/master/examples/nodejs/hello.js > hello.js
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100    88  100    88    0     0    222      0 --:--:-- --:--:-- --:--:--   222
ubuntu@ip-172-31-13-96:~$ fission function create --name hello --env nodejs --code hello.js
function 'hello' created
ubuntu@ip-172-31-13-96:~$ fission route create --method GET --url /hello --function hello
trigger '402f6505-a7a6-41b1-baa8-bffe190dec63' created
ubuntu@ip-172-31-13-96:~$ curl http://$FISSION_ROUTER/hello
Hello, world!
```
