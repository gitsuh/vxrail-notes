# vxrail-notes


Configure the NICs because the Intel X710 cards do not work well with our Cisco switches. They fail to autonegotiate and cause the ports to enter admin down due to flapping.<br>
esxcli network nic down -n vmnic0<br>
esxcli network nic set --speed=10000 --duplex=full --nic-name=vmnic0<br>
esxcli network nic up -n vmnic0<br>
esxcli network nic down -n vmnic1<br>
esxcli network nic set --speed=10000 --duplex=full --nic-name=vmnic1<br>
esxcli network nic up -n vmnic1<br>
esxcli network nic list<br>
vim-cmd hostsvc/net/query_networkhint --pnic-name=vmnic0 | egrep "devId|portId"<br>
vim-cmd hostsvc/net/query_networkhint --pnic-name=vmnic1 | egrep "devId|portId"<br>


#Configure the time so all the systems are in sync before they can use NTP<br>
esxcli system time set -H XX -m XX -s XX<br>

#Use Current UTC time<br>
esxcli network vswitch standard portgroup set -p "Management Network" --vlan-id NUM<br>
esxcli network vswitch standard portgroupset -p "VM Network" --vlan-id NUM<br>
/etc/init.d/loudmouth restart<br>
