+++
title = "Подключение PPPoE с указанием имени службы в Ubuntu"
date = 2010-08-23T00:00:00+03:00
tags = ["pppoe", "ubuntu"]
draft = true
+++

Провайдер требует указать имя службы для подключения PPPoE?
Немного подправим конфиги, и все получится.
Например, в файле /etc/ppp/peers/dsl-provider у нас хранятся настройки подключения.
Находим строку:

```plugin rp-pppoe.so eth0```

Дописываем: rp_pppoe_service имя_службы

```plugin rp-pppoe.so rp_pppoe_service имя_службы eth0```

Если используется пакет pppoe, то находим строку:

```pty "/usr/sbin/pppoe -I eth0 -T 80 -m 1452"```

Дописываем: -S имя_службы

```pty "/usr/sbin/pppoe -I eth0 -T 80 -m 1452 -S имя_службы"```


via http://my.runtu.org/blog/maksipes
