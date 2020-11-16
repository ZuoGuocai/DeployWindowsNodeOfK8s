# DeployWindowsNodeOfK8s




Linux 节点

```
cat /run/flannel/subnet.env

对端flannel.4096 的mac 地址

bridge fdb|grep flannel  （Get-HnsNetwork |where{$_.name -eq "flannel.4096"}）

kubectl cluster-info dump|grep -i service-cluster-ip-range




```


Windows 节点

```

hnsdiag list  endpoints

hnsdiag list  loadbalancers

Get-HnsNetwork |where{$_.name -eq "flannel.4096"}


Get-HnsEndpoint |ft IPAddress,MACAddress,IsRemoteEndpoint,Policies

```
