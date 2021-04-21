---
keywords: Experience Platform; home; tópicos populares; PSQL; psqlconnect para serviço de consulta; serviço de consulta; serviço de consulta;
solution: Experience Platform
title: Conectar o PSQL ao Serviço de Consulta
topic-legacy: connect
description: O PSQL é uma interface de linha de comando que vem quando você instala o PostgreSQL em sua máquina. Você pode instalá-lo seguindo estas instruções.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 1%

---

# Conectar o PSQL ao Serviço de Consulta

O PSQL é uma interface de linha de comando que vem instalada quando você instala [!DNL PostgreSQL] em sua máquina. Este documento aborda as etapas para conectar o PSQL com o Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia supõe que você já tenha acesso a [!DNL PSQL] e está familiarizado com como usá-lo. Mais informações sobre [!DNL PSQL] podem ser encontradas na [documentação oficial [!DNL PSQL]](https://www.postgresql.org/docs/current/app-psql.html).

Depois de instalar o PSQL no computador, você está pronto para conectar o PSQL com o Serviço de query. Retorne à interface [!DNL Platform] e selecione **[!UICONTROL Queries]**, seguido por **[!UICONTROL Credentials]**.

![Imagem](../images/clients/psql/connect-bi.png)

Selecione o ícone para copiar a seção denominada **[!UICONTROL PSQL Command]** e cole a string de comando em um terminal ou janela de linha de comando antes de pressionar Enter.

>[!IMPORTANT]
>
>Se você estiver em um PC, use um editor de texto para remover as quebras de linha na string de comando e, em seguida, copie a string. Além disso, se estiver usando a versão 12.0 ou superior, será necessário adicionar `PGGSSENCMODE=disable` à string de conexão.

Você deve ver um resultado como este:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Se você não vir pelo menos a versão 10.5, será necessário baixar essa versão ou mais recente.

## Próximas etapas

Agora que você se conectou a [!DNL Query Service], é possível usar o PSQL para gravar queries. Para obter mais informações sobre como gravar e executar consultas, leia o guia em [executar consultas](../best-practices/writing-queries.md).
