---
keywords: Experience Platform;home;popular topics;PSQL;psql
solution: Experience Platform
title: Conectar com o PSQL
topic: connect
description: 'O PSQL é uma interface de linha de comando que aparece quando você instala os Postgres em sua máquina. Você pode instalá-lo seguindo estas instruções. '
translation-type: tm+mt
source-git-commit: 1bb896f7629d7b71b94dd107eeda87701df99208
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 1%

---


# Conectar com o PSQL

O PSQL é uma interface de linha de comando que aparece quando você instala [!DNL Postgres] em sua máquina. Você pode instalá-lo seguindo estas instruções.

## Instale os pôsteres em um Mac

Abra uma janela de terminal e emita estes três comandos:

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

```shell
brew install postgres
```

```shell
which psql
```

Depois de emitir esses comandos, você deverá ver o seguinte:

```shell
/usr/local/bin/psql
```

## Instalar [!DNL Postgres] em um PC

Baixe e instale [!DNL Postgres] a partir deste [local](https://www.postgresql.org/download/windows/).

Edite sua variável de caminho:

![Imagem](../images/clients/psql/path.png)

Adicione as duas linhas mostradas que incluem &quot;[!DNL Postgres]&quot;.

Salve as atualizações e abra um prompt de comando e digite:

```shell
psql -V
```

Você deve ver algo assim:

```shell
psql (PostgreSQL) 9.5.14
```

## Connect PSQL e [!DNL Query Service]

Retorne à [!DNL Platform] interface do usuário na página Ferramentas **[!UICONTROL do]** Connect BI.

Clique em **[!UICONTROL copiar]** para Comando **** PSQL.

![Imagem](../images/clients/psql/connect-bi.png)

>[!IMPORTANT]
>
>Se você estiver em um PC, use um editor de texto para remover as quebras de linha na string de comando e, em seguida, copie a string.

Cole a string de comando em um terminal ou uma janela de comando e pressione Enter.

Você deve ver um resultado como este:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Se você não vir pelo menos a versão 10.5, é necessário baixar essa versão ou mais recente.