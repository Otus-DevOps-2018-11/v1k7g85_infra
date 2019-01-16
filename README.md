# v1k7g85_infra
v1k7g85 Infra repository

Для ssh доступа к хосту someinternalhost по алиасу и с помощью одной команды предлягается такое решение:

1. Добавляем в файл .ssh/config строки

host bastion
 HostName 35.207.78.88
 IdentityFile ~/.ssh/id_rsa_gcp

host someinternalhost
 HostName 127.0.0.1
 Port 9999
 IdentityFile ~/.ssh/id_rsa_gcp

2. Пробрасывам нудный хост на порт 9999 командой:

ssh -A -f -N -L 9999:10.156.0.3:22 bastion

3. далее можем подключаться командой:

ssh someinternalhost


Данные для подключения:

bastion_IP = 35.207.78.88
someinternalhost_IP = 10.156.0.3
