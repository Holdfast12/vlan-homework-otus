<b>VLAN</b><br>
Есть набор хостов:<br>
testClient1 - 10.10.10.254<br>
testClient2 - 10.10.10.254<br>
testServer1- 10.10.10.1<br>
testServer2- 10.10.10.1<br>
Их необходимо развести вланами<br>
testClient1 <-> testServer1<br>
testClient2 <-> testServer2<br>
<b>BOND</b><br>
между centralRouter и inetRouter<br>
"пробросить" 2 линка (общая inernal сеть) и объединить их в бонд<br>
проверить работу c отключением интерфейсов<br>