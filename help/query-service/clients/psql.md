---
keywords: Experience Platform;página inicial;tópicos populares;PSQL;psqlconnect to query service;Query service;query service;
solution: Experience Platform
title: Conectar o PSQL ao Serviço de consulta
description: O PSQL é uma interface de linha de comando fornecida quando você instala o PostgreSQL em sua máquina. Você pode instalá-lo seguindo estas instruções.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Conectar o PSQL ao Serviço de consulta

O PSQL é uma interface de linha de comando que vem instalada quando você instala [!DNL PostgreSQL] na sua máquina. Este documento aborda as etapas para conectar o PSQL ao Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia supõe que você já tenha acesso ao [!DNL PSQL] e estão familiarizados com como usá-lo. Mais informações sobre [!DNL PSQL] pode ser encontrado no [oficial [!DNL PSQL] documentação](https://www.postgresql.org/docs/current/app-psql.html).

Depois de instalar o PSQL no computador, você estará pronto para conectar o PSQL ao Serviço de consulta. Retorne para a [!DNL Platform] e selecione **[!UICONTROL Consultas]**, seguido por **[!UICONTROL Credenciais]**.

No **[!UICONTROL Comando PSQL]** , selecione a **[!UICONTROL Copiar para a área de transferência]** ícone (![Ícone Copiar](../images/clients/psql/copy-icon.png)) para copiar a string de comando.

![A guia Credenciais do painel de consultas com o ícone de cópia destacado.](../images/clients/psql/connect-bi.png)

Cole a string de comando em um terminal ou janela de linha de comando e pressione **Enter** no teclado.

>[!IMPORTANT]
>
>Se você estiver em um PC, use um editor de texto para remover as quebras de linha na string de comando e, em seguida, copie a string. Se você estiver usando a versão 12.0 ou superior, será necessário adicionar `PGGSSENCMODE=disable` à cadeia de conexão. Além disso, se você estiver usando credenciais sem expiração, substitua o campo de senha pela senha de credencial sem expiração. Para saber mais sobre credenciais sem expiração, leia o [guia de credenciais](../ui/credentials.md).

Você deve ver um resultado como este:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Se você não vir pelo menos a versão 10.5, é necessário baixar essa versão ou mais recente.

## Próximas etapas

Agora que você se conectou com [!DNL Query Service], você pode usar o PSQL para gravar consultas. Para obter mais informações sobre como gravar e executar consultas, leia o manual no [execução de consultas](../best-practices/writing-queries.md).
