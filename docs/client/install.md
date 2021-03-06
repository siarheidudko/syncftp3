﻿# IoCommander v1.1.3 - Установка клиента
###### пример собранной установки (с скриптами установки и удаления по windows и linux) есть в папке [/production](https://github.com/siarheidudko/iocommander/tree/master/production) репозитория

## Зависимости проекта

- socket.io-client
- colors
- fs
- cryptojs
- redux
- lodash
- os
- http
- https
- url
- mkdir
- child_process
- iconv-lite

## Настройка проекта

- Копируете файлы проекта, например в папку /home/iocommander/*

  - ./src-user/* - файлы клиента

- Создаете каталог для временных файлов ./temp/ 

- Создаете/редактируете файл настроек ./src-user/iocommander-usr.conf

```
{
"protocol":"http",
"server":"iocom.sergdudko.tk",
"port":"444",
"login":"fitobel.apt02",
"password":"12345678"
}
```

  - protocol - протокол сокет-сервера http или https
  - server - адрес сокет-вервера
  - port - порт сокет-вервера
  - login - логин на сокет-сервере
  - password - пароль на сокет-сервере

- Устанавливаете nodejs, например в CentOS 7.x он устанавливается из штатного репозитория

```
yum install nodejs -y
```

- Устанавливаете зависимости (или копируете из репозитория ./node_modules/* и файл ./package.json)

- Создаете системную службу (на примере CentOS 7.x/systemd):

  - создаете файл в /etc/systemd/system/iocommander-client.service
  
```
[Unit]
Description=Web and Socket client for iocommander
after=network.target remote-fs.target nss-lookup.target

[Service]
WorkingDirectory=/home/iocommander/
ExecStart=/bin/node /home/iocommander/src-user/iocommander-usr.js
ExecStop=kill -9 $(pidof node)

[Install]
WantedBy=multi-user.target

```

  - обновляете список системных демонов
  
```
systemctl daemon-reload
```

  - запускаете демона
  
```
systemctl start iocommander-client
```

  - проверяете остановку демона
  
```
systemctl stop iocommander-client
```

  - проверяете перезапуск демона
  
```
systemctl restart iocommander-client
```

  - проверяете лог демона
  
```
systemctl status iocommander-client -l
```
