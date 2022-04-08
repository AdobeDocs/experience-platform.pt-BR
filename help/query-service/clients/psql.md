---
keywords: Experience Platform; home; tópicos populares; PSQL; psqlconnect para serviço de consulta; serviço de consulta; serviço de consulta;
solution: Experience Platform
title: Conectar o PSQL ao Serviço de Consulta
topic-legacy: connect
description: O PSQL é uma interface de linha de comando que vem quando você instala o PostgreSQL em sua máquina. Você pode instalá-lo seguindo estas instruções.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 4d9e6ce81809c6e6ee1188177a937ac8fc609996
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Conectar o PSQL ao Serviço de Consulta

PSQL é uma interface de linha de comando que vem instalada quando você instala [!DNL PostgreSQL] na sua máquina. Este documento aborda as etapas para conectar o PSQL com o Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Este guia supõe que você já tenha acesso ao [!DNL PSQL] e estão familiarizados com como usá-lo. Mais informações sobre [!DNL PSQL] podem ser encontradas no [funcionário [!DNL PSQL] documentação](https://www.postgresql.org/docs/current/app-psql.html).

Depois de instalar o PSQL no computador, você está pronto para conectar o PSQL com o Serviço de query. Retorne ao [!DNL Platform] UI, em seguida selecione **[!UICONTROL Queries]**, seguida de **[!UICONTROL Credenciais]**.

Em **[!UICONTROL Comando PSQL]** selecione a **[!UICONTROL Copiar para a área de transferência]** ícone (![Ícone Copiar](../images/clients/psql/copy-icon.png)) para copiar a string de comando.

![A guia Query dashboard Credentials com o ícone de cópia realçado.](../images/clients/psql/connect-bi.png)

Cole a string de comando em um terminal ou uma janela de linha de comando e pressione **Enter** no teclado.

>[!IMPORTANT]
>
>Se você estiver em um PC, use um editor de texto para remover as quebras de linha na string de comando e, em seguida, copie a string. Se estiver usando a versão 12.0 ou superior, será necessário adicionar `PGGSSENCMODE=disable` à string de conexão. Além disso, se você estiver usando credenciais que não estão expirando, substitua o campo de senha pela senha de credencial que não está expirando. Para saber mais sobre credenciais que não estão expirando, leia o [guia de credenciais](../ui/credentials.md).

Você deve ver um resultado como este:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Se você não vir pelo menos a versão 10.5, será necessário baixar essa versão ou mais recente.

## Próximas etapas

Agora que você se conectou a [!DNL Query Service], você pode usar o PSQL para gravar queries. Para obter mais informações sobre como gravar e executar consultas, leia o guia em [execução de consultas](../best-practices/writing-queries.md).
