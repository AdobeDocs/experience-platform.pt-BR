---
keywords: Experience Platform;home;popular topics;PSQL;psqlconnect to query service;Query service;query service;
solution: Experience Platform
title: Conectar com o PSQL
topic: connect
description: 'O PSQL é uma interface de linha de comando que aparece quando você instala o PostgreSQL em sua máquina. Você pode instalá-lo seguindo estas instruções. '
translation-type: tm+mt
source-git-commit: bc1bbdddd75b11ac180b5e6faa391fd74e5f7e02
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 1%

---


# PSQL

O PSQL é uma interface de linha de comando que é instalada quando você instala [!DNL PostgreSQL] em seu computador. Este documento aborda as etapas para conectar o PSQL com o Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia supõe que você já tenha acesso a [!DNL PSQL] e esteja familiarizado com como usá-lo. Mais informações sobre [!DNL PSQL] podem ser encontradas na [documentação oficial [!DNL PSQL]](https://www.postgresql.org/docs/current/app-psql.html.

## Connect PSQL e [!DNL Query Service]

Depois de instalar o PSQL no computador, você está pronto para conectar o PSQL ao Serviço de Query. Retorne à interface de usuário [!DNL Platform] e selecione **[!UICONTROL Query]**, seguido por **[!UICONTROL Credenciais]**.

![Imagem](../images/clients/psql/connect-bi.png)

Selecione o ícone para copiar a seção chamada **[!UICONTROL Comando PSQL]** e cole a string de comando em um terminal ou uma janela de linha de comando antes de pressionar enter.

>[!IMPORTANT]
>
>Se você estiver em um PC, use um editor de texto para remover as quebras de linha na string de comando e, em seguida, copie a string. Além disso, se estiver usando a versão 12.0 ou superior, será necessário adicionar `PGGSSENCMODE=disable` à cadeia de conexão.

Você deve ver um resultado como este:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Se você não vir pelo menos a versão 10.5, é necessário baixar essa versão ou mais recente.

## Próximas etapas

Agora que você se conectou a [!DNL Query Service], é possível usar o PSQL para gravar query. Para obter mais informações sobre como gravar e executar query, leia o guia em [query em execução](../best-practices/writing-queries.md).