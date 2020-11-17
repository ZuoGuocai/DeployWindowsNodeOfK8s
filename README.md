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
Get-Service -Name docker,kubelet,hns,rancher-wins,containerd
docker ps |findstr  flannel

Get-Service  |Sort-Object status
Get-Service  |Select-Object -Property Status
Get-Service  |?{$_.Status -like 'Running'}
Get-Service   "n*" | ?{$_.Status -like 'Running'}
Get-Service   "vm*"




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






```
