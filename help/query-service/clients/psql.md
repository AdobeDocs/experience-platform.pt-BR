---
keywords: Experience Platform;home;popular tópicos;PSQL;psqlconnect to query service;Query service;query service;
solution: Experience Platform
title: Conectar o PSQL ao Serviço de consulta
description: O PSQL é uma interface de linha de comando fornecida quando você instala o PostgreSQL em sua máquina. Você pode instalá-lo seguindo estas instruções.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Conectar o PSQL ao Serviço de consulta

O PSQL é uma interface de linha de comando instalada quando você instala o [!DNL PostgreSQL] no computador. Este documento aborda as etapas para conectar o PSQL com o Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia supõe que você já tenha acesso ao [!DNL PSQL] e esteja familiarizado com como usá-lo. Mais informações sobre [!DNL PSQL] podem ser encontradas na [documentação [!DNL PSQL] oficial](https://www.postgresql.org/docs/current/app-psql.html).

Depois de instalar o PSQL no computador, você estará pronto para conectar o PSQL ao Serviço de consulta. Retorne à interface do usuário do [!DNL Experience Platform] e selecione **[!UICONTROL Consultas]**, seguidas por **[!UICONTROL Credenciais]**.

Na seção **[!UICONTROL Comando PSQL]**, selecione o ícone **[!UICONTROL Copiar para a área de transferência]** (![Ícone Copiar](/help/images/icons/copy.png)) para copiar a cadeia de caracteres de comando.

![A guia Credenciais do painel Consultas com o ícone copiar realçado.](../images/clients/psql/connect-bi.png)

Cole a cadeia de comando em um terminal ou em uma janela de linha de comando e pressione **Enter** no teclado.

>[!IMPORTANT]
>
>Se você estiver em um PC, use um editor de texto para remover as quebras de linha na string de comando e, em seguida, copie a string. Se você estiver usando a versão 12.0 ou posterior, será necessário adicionar `PGGSSENCMODE=disable` à cadeia de conexão. Além disso, se você estiver usando credenciais sem expiração, substitua o campo de senha pela senha de credencial sem expiração. Para saber mais sobre credenciais sem expiração, leia o [guia de credenciais](../ui/credentials.md).

Você deve ver um resultado como este:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Se você não vir pelo menos a versão 10.5, é necessário baixar essa versão ou mais recente.

## Próximas etapas

Agora que você se conectou com [!DNL Query Service], é possível usar o PSQL para gravar consultas. Para obter mais informações sobre como gravar e executar consultas, leia o manual em [executando consultas](../best-practices/writing-queries.md).
