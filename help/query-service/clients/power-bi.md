---
keywords: Experience Platform;home;popular topics;query service;Query service;Power BI;power bi;connect to query service;
solution: Experience Platform
title: Conectar o Power BI ao serviço do Query
topic: connect
description: Este documento percorre as etapas para conectar o Power BI ao Serviço de Query Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Conectar [!DNL Power BI] ao Query Service (PC)

Este documento cobre as etapas para conexão do Power BI com o Serviço de Query Adobe Experience Platform.

>[!NOTE]
>
> Este guia supõe que você já tenha acesso a [!DNL Power BI] e esteja familiarizado com como navegar em sua interface. Mais informações sobre [!DNL Power BI] podem ser encontradas na [oficial [!DNL Power BI] documentação](https://docs.looker.com/).
>
> Além disso, o Power BI está **disponível apenas** em dispositivos Windows.

Após instalar o Power BI, será necessário instalar `Npgsql` um pacote de driver .NET para o PostgreSQL. Mais informações sobre o Npgsql podem ser encontradas na [documentação Npgsql](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>Você deve baixar a versão v4.0.10 ou inferior, já que as versões mais recentes resultam em erros.

Em &quot;[!DNL Npgsql GAC Installation]&quot; na tela de configuração personalizada, selecione **[!DNL Will be installed on local hard drive]**.

Para garantir que o npgsql esteja instalado corretamente, reinicie o computador antes de prosseguir para as etapas seguintes.

## Conectar [!DNL Power BI] a [!DNL Query Service]

Para conectar [!DNL Power BI] a [!DNL Query Service], abra [!DNL Power BI] e selecione **[!DNL Get Data]** na faixa superior do menu.

![](../images/clients/power-bi/open-power-bi.png)

Selecione **[!DNL PostgreSQL database]**, seguido por **[!DNL Connect]**.

![](../images/clients/power-bi/get-data.png)

Agora você pode inserir valores para o servidor e o banco de dados. Para obter mais informações sobre como localizar seu nome de banco de dados, host, porta e credenciais de logon, visite a página [credenciais em Platform](https://platform.adobe.com/query/configuration). Para localizar suas credenciais, faça logon em [!DNL Platform] e selecione **[!UICONTROL Query]**, seguido por **[!UICONTROL Credenciais]**.

**[!DNL Server]** é o host encontrado sob os detalhes da conexão. Para produção, adicione a porta `:80` ao final da string do host. **[!DNL Database]** pode ser &quot;all&quot; ou um nome de tabela de conjunto de dados.

Além disso, você pode selecionar **[!DNL Data Connectivity mode]**. Selecione **[!DNL Import]** para exibir uma lista de todas as tabelas disponíveis, ou selecione **[!DNL DirectQuery]** para criar diretamente um query.

Para saber mais sobre o modo **[!DNL Import]**, leia a seção em [visualizar e importar uma tabela](#preview). Para saber mais sobre o modo **[!DNL DirectQuery]**, leia a seção em [criar instruções SQL](#create). Selecione **[!DNL OK]** depois de confirmar os detalhes do banco de dados.

![](../images/clients/power-bi/connectivity-mode.png)

Um prompt solicitando seu nome de usuário, senha e configurações do aplicativo é exibido. Preencha esses detalhes e selecione **[!DNL Connect]** para continuar com a próxima etapa.

![](../images/clients/power-bi/import-mode.png)

## Pré-visualização e importação de uma tabela {#preview}

Se você tiver selecionado o modo **[!DNL Import]**, uma caixa de diálogo será exibida, exibindo uma lista de todas as tabelas disponíveis. Selecione a tabela que deseja pré-visualização, seguida por **[!DNL Load]** para trazer o conjunto de dados para [!DNL Power BI].

![](../images/clients/power-bi/preview-table.png)

A tabela agora é importada para o Power BI.

![](../images/clients/power-bi/import-table.png)

## Criar instruções SQL {#create}

Se você selecionou o modo **[!DNL DirectQuery]**, precisará preencher a seção Opções avançadas com o query SQL que deseja criar.

Em **[!DNL SQL statement]**, insira o query SQL que deseja criar. Verifique se a caixa de seleção **[!DNL Include relationship columns]** está selecionada. Depois de gravar seu query, selecione **[!DNL OK]** para continuar.

![](../images/clients/power-bi/direct-query-mode.png)

Uma pré-visualização do seu query é exibida. Selecione **[!DNL Load]** para ver os resultados do query.

![](../images/clients/power-bi/preview-direct-query.png)

## Próximas etapas

Agora que você se conectou a [!DNL Query Service], é possível usar [!DNL Power BI] para gravar query. Para obter mais informações sobre como gravar e executar query, leia o guia em [query em execução](../best-practices/writing-queries.md).