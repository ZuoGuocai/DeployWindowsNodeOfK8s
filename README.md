# DeployWindowsNodeOfK8s


troubshooting

```

hnsdiag list  endpoints

hnsdiag list  loadbalancers

Get-HnsNetwork |where{$_.name -eq "flannel.4096"}


Get-HnsEndpoint |ft IPAddress,MACAddress,IsRemoteEndpoint,Policies

```
