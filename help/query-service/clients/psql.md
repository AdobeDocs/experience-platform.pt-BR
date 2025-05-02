---
keywords: Experience Platform;home;popular tópicos;PSQL;psqlconnect to query service;Query service;query service;
solution: Experience Platform
title: Conectar o PSQL ao Serviço de consulta
description: Saiba como conectar o cliente PSQL ao Serviço de consulta do Adobe Experience Platform, incluindo versões PostgreSQL compatíveis e instruções de configuração.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: f75ea97e8631984dcd1d4a7f8aff3c10cba7b11f
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---

# Conectar o PSQL ao Serviço de consulta

O PSQL é uma interface de linha de comando instalada com o PostgreSQL em sua máquina. Este documento aborda as etapas para conectar o PSQL ao Adobe Experience Platform Query Service.

>[!IMPORTANT]
>
>O Serviço de consulta oferece suporte somente à conexão com o PSQL versão 14.x. As versões anteriores à 14.x (como 10.x a 13.x) e posteriores (15.x e superior) não são oficialmente compatíveis. Verifique se você instalou uma versão de cliente compatível. Para referência, consulte as [Datas do fim da vida útil do PostgreSQL](https://endoflife.date/postgresql).

Antes de começar, verifique se você tem acesso ao PSQL e familiaridade básica com o uso do cliente. Mais informações sobre o PSQL podem ser encontradas na [documentação oficial do PSQL](https://www.postgresql.org/docs/current/app-psql.html).

>[!IMPORTANT]
>
>Ao baixar o PostgreSQL, certifique-se de selecionar a versão 14.x. Por padrão, o site PostgreSQL oferece a versão mais recente, que pode não ser compatível com o Serviço de consulta.

Depois que o PSQL for instalado, você poderá conectá-lo ao Serviço de consulta. Retorne à interface do Experience Platform e selecione **[!UICONTROL Consultas]**, seguidas por **[!UICONTROL Credenciais]**.

Na seção **[!UICONTROL Comando PSQL]**, selecione o ícone **[!UICONTROL Copiar para a área de transferência]** (![Ícone Copiar](/help/images/icons/copy.png)) para copiar a cadeia de caracteres de comando.

![A guia Credenciais do painel Consultas com o ícone copiar realçado.](../images/clients/psql/copy-credentials.png)

Cole a sequência de comando no terminal e pressione **Enter** no teclado.

>[!IMPORTANT]
>
>Se você estiver em um PC, use um editor de texto para remover as quebras de linha na string de comando e, em seguida, copie a string. Se você estiver usando a versão 12.0 ou posterior, será necessário adicionar `PGGSSENCMODE=disable` à cadeia de conexão. Esta configuração desabilita a criptografia GSSAPI, que é desnecessária para conexões com o Serviço de consulta e pode causar erros de conexão.<br>Além disso, se você estiver usando credenciais sem expiração, substitua o campo de senha pela senha de credencial sem expiração. Para saber mais sobre credenciais sem expiração, leia o [guia de credenciais](../ui/credentials.md).

Você deve ver um resultado como este:

```shell
psql (14.4, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Se você não vir a versão 14.x, baixe e instale uma versão 14.x do PSQL com suporte na [página oficial de downloads do PostgreSQL](https://www.postgresql.org/download/).

>[!NOTE]
>
>Siga as instruções de instalação do sistema operacional e verifique a versão do PSQL instalada executando o `psql --version` no terminal.

## Próximas etapas

Agora que você se conectou ao Serviço de consulta, é possível usar o PSQL para gravar consultas. Consulte o manual sobre [execução de consultas](../best-practices/writing-queries.md) para obter mais informações.
