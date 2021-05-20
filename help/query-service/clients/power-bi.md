---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, Power BI, power bi, conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar o Power BI ao Serviço de Consulta
topic-legacy: connect
description: Este documento aborda as etapas para conectar o Power BI com o Adobe Experience Platform Query Service.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 2109abd02b9c6c321c21a8fe3826509d22b1c2e2
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 1%

---

# Conecte [!DNL Power BI] ao Serviço de Consulta (PC)

Este documento aborda as etapas para conectar o Power BI com o Adobe Experience Platform Query Service.

>[!NOTE]
>
> Este guia pressupõe que você já tenha acesso a [!DNL Power BI] e esteja familiarizado com como navegar em sua interface. Mais informações sobre [!DNL Power BI] podem ser encontradas na documentação [oficial [!DNL Power BI] documentação](https://docs.microsoft.com/pt-BR/power-bi/).
>
> Além disso, o Power BI está **somente** disponível em dispositivos Windows.

Após instalar o Power BI, será necessário instalar `Npgsql`, um pacote de driver .NET para PostgreSQL. Mais informações sobre Npgsql podem ser encontradas na [Documentação Npgsql](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>Você deve baixar a v4.0.10 ou inferior, já que versões mais recentes resultam em erros.

Em &quot;[!DNL Npgsql GAC Installation]&quot; na tela de configuração personalizada, selecione **[!DNL Will be installed on local hard drive]**.

Para garantir que o npgsql tenha sido instalado corretamente, reinicie o computador antes de prosseguir para as próximas etapas.

## Conecte [!DNL Power BI] a [!DNL Query Service]

Para conectar [!DNL Power BI] a [!DNL Query Service], abra [!DNL Power BI] e selecione **[!DNL Get Data]** na faixa do menu superior.

![](../images/clients/power-bi/open-power-bi.png)

Selecione **[!DNL PostgreSQL database]**, seguido por **[!DNL Connect]**.

![](../images/clients/power-bi/get-data.png)

Agora é possível inserir valores para o servidor e o banco de dados. Para obter mais informações sobre como encontrar o nome do banco de dados, o host, a porta e as credenciais de logon, visite a página [credenciais no Platform](https://platform.adobe.com/query/configuration). Para localizar suas credenciais, faça logon em [!DNL Platform], selecione **[!UICONTROL Queries]**, seguido por **[!UICONTROL Credentials]**.

**[!DNL Server]** é o host encontrado nos detalhes da conexão. Para produção, adicione a porta `:80` ao final da cadeia de caracteres do host. **[!DNL Database]** pode ser &quot;all&quot; ou um nome de tabela de conjunto de dados.

Além disso, você pode selecionar seu **[!DNL Data Connectivity mode]**. Selecione **[!DNL Import]** para exibir uma lista de todas as tabelas disponíveis ou selecione **[!DNL DirectQuery]** para criar diretamente uma consulta.

Para saber mais sobre o modo **[!DNL Import]**, leia a seção em [visualizar e importar uma tabela](#preview). Para saber mais sobre o modo **[!DNL DirectQuery]**, leia a seção sobre [criação de instruções SQL](#create). Selecione **[!DNL OK]** após confirmar os detalhes do banco de dados.

![](../images/clients/power-bi/connectivity-mode.png)

Um prompt solicitando seu nome de usuário, senha e configurações do aplicativo é exibido. Preencha estes detalhes e selecione **[!DNL Connect]** para continuar na próxima etapa.

![](../images/clients/power-bi/import-mode.png)

## Visualizar e importar uma tabela {#preview}

Se você selecionou o modo **[!DNL Import]** , é exibida uma caixa de diálogo exibindo uma lista de todas as tabelas disponíveis. Selecione a tabela que deseja visualizar, seguida por **[!DNL Load]** para trazer o conjunto de dados para [!DNL Power BI].

![](../images/clients/power-bi/preview-table.png)

A tabela agora é importada para o Power BI.

![](../images/clients/power-bi/import-table.png)

## Criar instruções SQL {#create}

Se você selecionou o modo **[!DNL DirectQuery]** , precisará preencher a seção Advanced options com a consulta SQL que deseja criar.

Em **[!DNL SQL statement]**, insira a consulta SQL que deseja criar. Certifique-se de que a caixa de seleção **[!DNL Include relationship columns]** esteja marcada. Depois de gravar sua consulta, selecione **[!DNL OK]** para continuar.

![](../images/clients/power-bi/direct-query-mode.png)

Uma pré-visualização do query é exibida. Selecione **[!DNL Load]** para ver os resultados da consulta.

![](../images/clients/power-bi/preview-direct-query.png)

## Próximas etapas

Agora que você se conectou a [!DNL Query Service], é possível usar [!DNL Power BI] para gravar consultas. Para obter mais informações sobre como gravar e executar consultas, leia o guia em [executar consultas](../best-practices/writing-queries.md).
