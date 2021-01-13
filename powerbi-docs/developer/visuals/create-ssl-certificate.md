---
title: Создание SSL-сертификатов для визуальных элементов Power BI для более эффективного использования встроенной бизнес-аналитики Power BI
description: Сведения о создании SSL-сертификатов с помощью визуальных средств Power BI в Windows, Mac, Linux или вручную. Получайте оптимальную встроенную бизнес-аналитику в Power BI.
author: KesemSharabi
ms.author: kesharab
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: reference
ms.date: 05/08/2020
ms.openlocfilehash: 7897d25f3ac49c0f1b728f2aaf05b8612de67055
ms.sourcegitcommit: eeaf607e7c1d89ef7312421731e1729ddce5a5cc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2021
ms.locfileid: "97885529"
---
# <a name="create-an-ssl-certificate"></a>Создание SSL-сертификата

В этой статье описывается создание и установка SSL-сертификатов для визуальных элементов Power BI.

Для выполнения процедур в Windows, macOS X и Linux необходимо установить пакет **pbiviz** визуальных средств Power BI. Дополнительные сведения см. в статье [Настройка среды для разработки визуального элемента Power BI](./environment-setup.md). 

## <a name="create-a-certificate-on-windows"></a>Создание сертификата в Windows

Чтобы создать сертификат с помощью командлета PowerShell `New-SelfSignedCertificate` в Windows 8 и более поздней версии, выполните следующую команду:

```powershell
pbiviz --install-cert
```

Для использования средства `pbiviz` в Windows 7 требуется, чтобы служебная программа OpenSSL была доступна из командной строки. Инструкции по установке OpenSSL см. на странице [OpenSSL](https://www.openssl.org) или [Двоичные файлы OpenSSL](https://wiki.openssl.org/index.php/Binaries).

Дополнительные сведения и инструкции по установке сертификата см. в разделе о [создании и установке сертификата для Windows](./environment-setup.md#create-and-install-a-certificate).

## <a name="create-a-certificate-on-macos-x"></a>Создание сертификата в macOS X

Служебная программа OpenSSL, как правило, доступна в операционной системе macOS X.

Для установки служебной программы OpenSSL также можно выполнить любую из следующих команд:

- Из диспетчера пакетов *Brew*:
  
  ```cmd
  brew install openssl
  brew link openssl --force
  ```

- С помощью *MacPorts*:
  
  ```cmd
  sudo port install openssl
  ```

После установки служебной программы OpenSSL выполните следующую команду для создания нового сертификата:

```cmd
pbiviz --install-cert
```

Дополнительные сведения и инструкции см. на вкладке OSX в разделе [Создание и установка сертификата](./environment-setup.md#create-and-install-a-certificate).

## <a name="create-a-certificate-on-linux"></a>Создание сертификата в Linux

Служебная программа OpenSSL, как правило, доступна в операционной системе Linux.

Сначала выполните следующие команды, чтобы проверить, установлены ли `openssl` и `certutil`:

```sh
which openssl
which certutil
```

Если `openssl` и `certutil` не установлены, установите служебные программы `openssl` и `libnss3`.

### <a name="create-the-ssl-configuration-file"></a>Создание файла конфигурации SSL

Создайте файл с именем */tmp/openssl.cnf*, содержащий следующий текст:

```
authorityKeyIdentifier=keyid,issuer
basicConstraints=CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names

[ alt_names ]
DNS.1=localhost
```

### <a name="generate-root-certificate-authority"></a>Создание корневого центра сертификации

Чтобы создать корневой центр сертификации (ЦС) для подписания локальных сертификатов, выполните следующие команды:

```sh
touch $HOME/.rnd
openssl req -x509 -nodes -new -sha256 -days 1024 -newkey rsa:2048 -keyout /tmp/local-root-ca.key -out /tmp/local-root-ca.pem -subj "/C=US/CN=Local Root CA/O=Local Root CA"
openssl x509 -outform pem -in /tmp/local-root-ca.pem -out /tmp/local-root-ca.crt
```

### <a name="generate-a-certificate-for-localhost"></a>Создайте сертификат для localhost 

Чтобы создать сертификат для `localhost` с помощью созданного ЦС и *openssl.cnf*, выполните следующие команды:

```sh
PBIVIZ=`which pbiviz`
PBIVIZ=`dirname $PBIVIZ`
PBIVIZ="$PBIVIZ/../lib/node_modules/powerbi-visuals-tools/certs"
# Make sure that $PBIVIZ contains the correct certificate directory path. ls $PBIVIZ should list 'blank' file.
openssl req -new -nodes -newkey rsa:2048 -keyout $PBIVIZ/PowerBIVisualTest_private.key -out $PBIVIZ/PowerBIVisualTest.csr -subj "/C=US/O=PowerBI Visuals/CN=localhost"
openssl x509 -req -sha256 -days 1024 -in $PBIVIZ/PowerBIVisualTest.csr -CA /tmp/local-root-ca.pem -CAkey /tmp/local-root-ca.key -CAcreateserial -extfile /tmp/openssl.cnf -out $PBIVIZ/PowerBIVisualTest_public.crt
```

### <a name="add-root-certificates"></a>Добавление корневых сертификатов

Чтобы добавить корневой сертификат в базу данных браузера Chrome, выполните следующую команду:

```sh
certutil -A -n "Local Root CA" -t "CT,C,C" -i /tmp/local-root-ca.pem -d sql:$HOME/.pki/nssdb
```

Чтобы добавить корневой сертификат в базу данных браузера Mozilla Firefox, выполните следующую команду:

```sh
for certDB in $(find $HOME/.mozilla* -name "cert*.db")
do
certDir=$(dirname ${certDB});
certutil -A -n "Local Root CA" -t "CT,C,C" -i /tmp/local-root-ca.pem -d sql:${certDir}
done
```

Чтобы добавить корневой сертификат на уровне системы, выполните следующую команду:

```sh
sudo cp /tmp/local-root-ca.pem /usr/local/share/ca-certificates/
sudo update-ca-certificates
```

### <a name="remove-root-certificates"></a>Удаление корневых сертификатов

Чтобы удалить корневой сертификат, выполните следующую команду:

```sh
sudo rm /usr/local/share/ca-certificates/local-root-ca.pem
sudo update-ca-certificates --fresh
```

## <a name="generate-a-certificate-manually"></a>Создание сертификата вручную

SSL-сертификат также можно создать вручную с помощью служебной программы OpenSSL. Вы можете указать любые средства для создания сертификатов.

Если служебная программа OpenSSL уже установлена, создайте новый сертификат, выполнив следующую команду:

```cmd
openssl req -x509 -newkey rsa:4096 -keyout PowerBIVisualTest_private.key -out PowerBIVisualTest_public.crt -days 365
```

Для поиска сертификатов веб-сервера `PowerBI-visuals-tools` в большинстве случаев можно выполнить следующие команды:

- Глобальные экземпляры средств:
  
  ```cmd
  %appdata%\npm\node_modules\PowerBI-visuals-tools\certs
  ```

- Локальные экземпляры средств:
  
  ```cmd
  <Power BI visual project root>\node_modules\PowerBI-visuals-tools\certs
  ```

### <a name="pem-format"></a>Формат PEM

При использовании формата сертификата Privacy Enhanced Mail (PEM) сохраните файл сертификата как *PowerBIVisualTest_public.crt* и сохраните закрытый ключ как *PowerBIVisualTest_private. key*.

### <a name="pfx-format"></a>Формат PFX

При использовании формата сертификата Personal Information Exchange (PFX) сохраните файл сертификата как *PowerBIVisualTest_public.pfx*.

Если для файла сертификата PFX требуется парольная фраза, выполните следующие действия:

1. В файле конфигурации укажите:
   
   ```cmd
   \PowerBI-visuals-tools\config.json
   ```
   
1. В разделе `server` укажите парольную фразу, заменив заполнитель \<YOUR PASSPHRASE>:

    ```cmd
    "server":{
        "root":"webRoot",
        "assetsRoute":"/assets",
        "privateKey":"certs/PowerBIVisualTest_private.key",
        "certificate":"certs/PowerBIVisualTest_public.crt",
        "pfx":"certs/PowerBIVisualTest_public.pfx",
        "port":"8080",
        "passphrase":"<YOUR PASSPHRASE>"
    }
    ```

## <a name="next-steps"></a>Дальнейшие действия
- [Разработка визуального элемента "Круговая карточка" в Power BI](develop-circle-card.md)
- [Примеры визуальных элементов Power BI](samples.md)
- [Публикация визуализаций Power BI в Центре партнеров](office-store.md)