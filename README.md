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

Команда для создания инстанса:

gcloud compute instances create reddit-app --boot-disk-size=10GB --image-family ubuntu-1604-lts --image-project=ubuntu-os-cloud --machine-type=g1-small --tags puma-server --restart-on-failure --zone europe-west3-a --metadata-from-file startup-script=startup.sh

Команда для создания правила firewall:

gcloud firewall-rules create default-puma-server --allow tcp:9292 --target-tags = puma-server

Данные для подключения:

testapp_IP = 35.246.225.173
testapp_port = 9292

Добавлен файл ubuntu.json c параметрами для создания шаблона ВМ, а так же пример файла с переменными.

Созданы скрипты terraform для развертывания новго инстанса с reddit

Скрипты развертывания terraform поделены на модули и среды.

Созданы плэйбуки absible для установки БД и приложения. Модифицированы скрипты packer для использования ansible плэйбуков.

Созданы роли ansible
