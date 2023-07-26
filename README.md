<h3><b>VLAN</b></h3>
<br>
В сети "testLAN" есть набор хостов с дублирующимися ip:<br>
testClient1 - 10.10.10.254<br>
testClient2 - 10.10.10.254<br>
testServer1- 10.10.10.1<br>
testServer2- 10.10.10.1<br>
Их необходимо развести вланами<br>
testClient1 <-> testServer1<br>
testClient2 <-> testServer2<br><br>
команда запуска стенда с виланами:<br>

```bash
vagrant up testClient1 testClient2 testServer1 testServer2
```
<br><br>
<h3><b>BOND</b></h3>
<br>
между centralRouter и inetRouter<br>
"пробросить" 2 линка (общая inernal сеть) и объединить их в бонд<br><br>
Команда запуска стенда с бондом:<br>

```bash
vagrant up inetRouter centralRouter
```

<h3>проверить работу c отключением интерфейсов</h3>
Проверка работы с отключением интерфейсов показала, что трафик всегда продолжает идти по одному из включенных.
<br>

<img src=".//screenshots//bond0.png"></img>