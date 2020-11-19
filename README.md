# DeployWindowsNodeOfK8s




Linux 节点

- 准备网段

```
export POD_SUBNET=10.100.0.1/16

cat <<EOF > ./kubeadm-config.yaml
apiVersion: kubeadm.k8s.io/v1beta2
kind: ClusterConfiguration
kubernetesVersion: v${1}
imageRepository: registry.aliyuncs.com/k8sxio
controlPlaneEndpoint: "${APISERVER_NAME}:6443"
networking:
  serviceSubnet: "10.96.0.0/16"
  podSubnet: "${POD_SUBNET}"
  dnsDomain: "cluster.local"
EOF

vi   kube-flannel.yml

  net-conf.json: |
    {
      "Network": "10.100.0.1/16",
      "Backend": {
        "Type": "vxlan"
      }
    }


cat /run/flannel/subnet.env
FLANNEL_NETWORK=10.100.0.0/16
FLANNEL_SUBNET=10.100.0.1/24
FLANNEL_MTU=1450
FLANNEL_IPMASQ=true

iptables -t nat --line-numbers -vnL POSTROUTING
iptables -S -t nat

https://developer.aliyun.com/article/468460


```
- nodeport 不能访问

iptables -P FORWARD ACCEPT




```
cat /run/flannel/subnet.env

对端flannel.4096 的mac 地址

bridge fdb|grep flannel  （Get-HnsNetwork |where{$_.name -eq "flannel.4096"}）

kubectl cluster-info dump|grep -i service-cluster-ip-range



ip tuntap list
ip  tunnel show
ip -d link  show tunl0

```


Windows 节点

```
Get-Service -Name docker,kubelet,hns,rancher-wins,containerd
docker ps |findstr  flannel

Get-Service  |Sort-Object status
Get-Service  |Select-Object -Property Status
Get-Service  |?{$_.Status -like 'Running'}
Get-Service   "n*" | ?{$_.Status -like 'Running'}
Get-Service   "vm*"

Get-Service   "*RM","ssh*","EventLog","*license*"

Stop-Service kubelet
docker ps -aq | ForEach-Object { docker stop -t 1 $_ } | ForEach-Object { docker rm -vf $_ }



hnsdiag list  endpoints

hnsdiag list  loadbalancers

Get-HnsNetwork |where{$_.name -eq "flannel.4096"}


Get-HnsEndpoint |ft IPAddress,MACAddress,IsRemoteEndpoint,Policies

get-netadapter
get-vmnetworkadapter -all




PS C:\Users\Administrator> hnsdiag list  loadbalancers
ID                                   | Virtual IPs      | Direct IP IDs
5a2ad38e-693d-43cf-8510-2facee763aa1 |                  | cb9beaae-7389-4f78-8e5d-d0e1700245af
3c89c920-c65a-4c81-a1de-056fe4097e95 |  10.96.0.10      | 11fcf2c4-30ff-42bb-bb29-56a0d0612582 bdf93f5a-26b4-4c38-86c6-782f20ffed40
07c13623-7132-4231-be75-89d312ea3ed2 |                  | 193be841-f8a7-4510-bbe2-d5e2396d574c
073c49a0-4a4f-4096-9974-22498f5691dd |  10.96.160.232   | 193be841-f8a7-4510-bbe2-d5e2396d574c
30709b59-d78b-4ccf-896c-b1ca414f739f |  10.96.0.1       | 237949bd-c351-4506-b2bb-0dbf623ab8bd
0b4f6bc6-973c-49c9-b623-56bcdaf44f3b |  10.96.104.23    | cb9beaae-7389-4f78-8e5d-d0e1700245af
731125ce-5f9f-46c7-9515-88c01f3cf645 |  10.96.0.10      | 11fcf2c4-30ff-42bb-bb29-56a0d0612582 bdf93f5a-26b4-4c38-86c6-782f20ffed40
bd6bd0ec-9de6-4850-9a19-3f2d448f30ad |  10.96.0.10      | 11fcf2c4-30ff-42bb-bb29-56a0d0612582 bdf93f5a-26b4-4c38-86c6-782f20ffed40


PS C:\Users\Administrator> vfpctrl /port  cb9beaae-7389-4f78-8e5d-d0e1700245af /layer VNET_ENCAP_LAYER /group VNET_GROUP_ENCAP_IPV4_OUT /list-rule | Select-Object -First 10

 ITEM LIST
===========



[kubelet-check] The HTTP call equal to 'curl -sSL http://localhost:10248/healthz' failed with error: Get "http://localhost:10248/healthz": dial tcp [::1]:10248: connectex: No connection could be made because the target machine actively refused it.


kubeadm reset


WARNING: The names of some imported commands from the module 'hns' include unapproved verbs that might make them less 
discoverable. To find the commands with unapproved verbs, run the Import-Module command again with the Verbose 
parameter. For a list of approved verbs, type Get-Verb.
Invoke-HnsRequest : @{Error=找不到适配器。 ; ErrorCode=2151350278; Success=False}
At C:\k\flannel\hns.psm1:233 char:16
+ ...      return Invoke-HnsRequest -Method POST -Type networks -Data $Json ...
+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,Invoke-HNSRequest

vEthernet(NIC1)--右键--配置--驱动--卸载



Invoke-HnsRequest : @{Error=已存在具有此名称的网络。 ; ErrorCode=2151350288; Success=False}
At C:\k\flannel\hns.psm1:233 char:16
+ ...      return Invoke-HnsRequest -Method POST -Type networks -Data $Json ...
+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,Invoke-HNSRequest


Get-NetIPAddress | Format-Table
 
Get-HNSNetwork | Remove-HNSNetwork

https://github.com/Microsoft/SDN/issues/238
```



- 查看日志

```
eventvwr

```

- 查看版本

```
winver
```

- 查看补丁情况
```
wmic qfe GET hotfixid

systeminfo

```


- 查看重启情况

```
systeminfo 

```
- 分析网络
```
ipconfig /all
tracert
route print
```

