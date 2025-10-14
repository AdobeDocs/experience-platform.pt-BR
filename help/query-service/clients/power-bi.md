---
keywords: Experience Platform;home;tópicos populares;serviço de consulta;Serviço de consulta;Power BI;power bi;conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar o Power BI ao Serviço de consulta
description: Este documento aborda as etapas para conectar o Power BI ao Serviço de consulta da Adobe Experience Platform.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 0%

---

# Conectar [!DNL Power BI] ao Serviço de consulta

Este documento aborda as etapas para conectar a Área de Trabalho do [!DNL Power BI] ao Serviço de Consulta da Adobe Experience Platform.

## Introdução

Este guia requer que você já tenha acesso ao aplicativo de desktop [!DNL Power BI] e esteja familiarizado com como navegar em sua interface. Para baixar a Área de Trabalho [!DNL Power BI] ou obter mais informações, consulte a [documentação [!DNL Power BI] oficial](https://docs.microsoft.com/en-us/power-bi/).

>[!IMPORTANT]
>
> O aplicativo de área de trabalho [!DNL Power BI] está **somente** disponível em dispositivos Windows.

Para adquirir as credenciais necessárias para conectar [!DNL Power BI] ao Experience Platform, você deve ter acesso ao espaço de trabalho Consultas na interface do usuário do Experience Platform. Entre em contato com o administrador da organização se você não tiver acesso ao espaço de trabalho de consultas.

## Conectar [!DNL Power BI] ao Serviço de consulta {#connect-power-bi}

Para conectar [!DNL Power BI] ao Serviço de Consulta, abra [!DNL Power BI] e selecione **[!DNL Get Data]** na faixa de opções do menu superior. Em seguida, digite &quot;[!DNL PostgreSQL]&quot; na barra de pesquisa para restringir a lista de fontes de dados. A partir dos resultados que aparecem, selecione **[!DNL PostgreSQL database]**, seguido por **[!DNL Connect]**.

A caixa de diálogo do banco de dados [!DNL PostgreSQL] é exibida, solicitando valores para o servidor e o banco de dados. Instruções adicionais sobre como [conectar-se a um banco de dados PostgreSQL a partir do Power Query Desktop](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop) podem ser encontradas na documentação oficial [!DNL PowerBI].

Esses valores obrigatórios foram obtidos de suas credenciais do Adobe Experience Platform. Para encontrar suas credenciais, faça logon na interface do usuário do Experience Platform e selecione **[!UICONTROL Consultas]** na navegação à esquerda, seguido de **[!UICONTROL Credenciais]**. Para obter mais informações sobre como localizar o nome do banco de dados, o host, a porta e as credenciais de logon, leia o [guia de credenciais](../ui/credentials.md).

>[!IMPORTANT]
>
>Como usuário do Power BI ou Tableau, você pode conectar o Customer Journey Analytics às suas ferramentas de BI na guia de credenciais do Serviço de consulta. Consulte a documentação de credenciais para obter instruções sobre como [conectar suas ferramentas de BI ao Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics).

![O espaço de trabalho Consultas do Experience Platform com a guia Credenciais e as credenciais Expirando foram realçadas.](../images/clients/power-bi/query-service-credentials-page.png)

No campo **[!DNL Server]** da caixa de diálogo [!DNL PostgreSQL database], insira o valor do host encontrado na seção [!UICONTROL Credenciais] do Serviço de Consulta. Para produção, adicione a porta `:80` ao final da cadeia de caracteres do host. Por exemplo, `made-up.platform-query.adobe.io:80`.

O campo **[!DNL Database]** pode ser &quot;all&quot; ou um nome de tabela de conjunto de dados. Por exemplo, `prod:all`.

>[!IMPORTANT]
>
>As estruturas de dados aninhadas em ferramentas de BI de terceiros podem ser niveladas para melhorar sua usabilidade e reduzir a carga de trabalho necessária para recuperar, analisar, transformar e relatar dados. Consulte a documentação sobre o recurso [`FLATTEN`](../key-concepts/flatten-nested-data.md) para obter instruções sobre como ativar essa configuração ao conectar-se a um banco de dados.

### Modo de Conectividade de Dados {#data-connectivity-mode}

Em seguida, você pode selecionar seu **[!DNL Data Connectivity mode]**. Na caixa de diálogo [!DNL PostgreSQL database], selecione **[!DNL Import]** seguido de **[!DNL OK]** para exibir uma lista de todas as tabelas disponíveis, ou selecione **[!DNL DirectQuery]** para consultar a fonte de dados diretamente sem importar ou copiar dados diretamente para [!DNL Power BI].

Para saber mais sobre o modo **[!DNL Import]**, leia a seção sobre [importação de uma tabela](#import). Para saber mais sobre o modo **[!DNL DirectQuery]**, leia a seção sobre [consulta a um conjunto de dados sem importar os dados](#direct-query).

Selecione **[!DNL OK]** depois de confirmar os detalhes do banco de dados.

### Autenticação {#authentication}

Após confirmar o modo de conectividade de dados, é exibido um prompt solicitando seu nome de usuário, senha e configurações do aplicativo. Nesse caso, o nome de usuário é a ID da organização e a senha é o token de autenticação. Ambos podem ser encontrados na página de credenciais do Serviço de consulta.

Preencha estes detalhes e selecione **[!DNL Connect]** para prosseguir para a próxima etapa.

## Importar uma tabela {#import}

Selecionando o **[!DNL Import]** [!DNL Data Connectivity mode], o conjunto de dados completo é importado, o que permite usar as tabelas e colunas selecionadas no aplicativo de desktop [!DNL Power BI] como está.

>[!IMPORTANT]
>
>Para ver as alterações de dados ocorridas desde a importação inicial, atualize os dados em [!DNL Power BI] importando o conjunto de dados completo novamente.

Para importar uma tabela, insira os detalhes do servidor e do banco de dados [conforme descrito acima](#connect-power-bi) e selecione o **[!DNL Import]** [!DNL Data Connectivity mode], seguido de **[!DNL OK]**. A caixa de diálogo [!DNL Navigator] é exibida, exibindo uma lista de todas as tabelas disponíveis. Selecione a tabela que deseja visualizar, seguida de **[!DNL Load]** para trazer o conjunto de dados para a Power BI. A tabela foi importada para [!DNL Power BI].

[Informações gerais sobre como se conectar aos dados no aplicativo &#x200B;](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data) do PowerBi desktop podem ser encontradas na documentação oficial.

### Importar tabelas usando SQL personalizado

Atualmente, o [!DNL Power BI] e outras ferramentas de terceiros, como o [!DNL Tableau], não permitem que os usuários importem objetos aninhados, como objetos XDM no Experience Platform. Para levar em conta isso, [!DNL Power BI] permite que você use SQL personalizado para acessar esses campos aninhados e criar uma exibição nivelada dos dados. [!DNL Power BI] carrega essa exibição nivelada dos dados aninhados anteriormente como uma tabela normal.

Na caixa de diálogo [!DNL PostgreSQL database], selecione **[!DNL Advanced options]** para inserir uma consulta SQL personalizada na seção **[!DNL SQL statement]**. Essa consulta personalizada deve ser usada para nivelar seus pares de nome-valor JSON em um formato de tabela. A documentação oficial também fornece informações sobre como [conectar o PowerBI usando uma instrução SQL nas opções avançadas](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-using-advanced-options).

Após inserir sua consulta personalizada, selecione **[!DNL OK]** para continuar conectando seu banco de dados. Consulte a seção [autenticação](#authentication) acima para obter orientação sobre como conectar um banco de dados a partir desta parte do fluxo de trabalho.

Uma vez concluída a autenticação, uma pré-visualização dos dados nivelados será exibida no painel da Área de Trabalho [!DNL Power BI] como uma tabela. O nome do servidor e do banco de dados são listados na parte superior da caixa de diálogo. Selecione **[!DNL Load]** para concluir o processo de importação.

As visualizações agora estão disponíveis para edição e exportação no aplicativo de desktop [!DNL Power BI].

## Consultar o conjunto de dados sem importar dados {#direct-query}

O **[!DNL DirectQuery]** [!DNL Data Connectivity mode] consulta a fonte de dados diretamente sem importar ou copiar dados para a Área de Trabalho [!DNL Power BI]. Usando esse modo de conexão, você pode atualizar todas as visualizações com dados atuais por meio da interface do. No entanto, o tempo necessário para produzir ou atualizar a visualização varia de acordo com o desempenho da fonte de dados subjacente.

Mais informações sobre [o uso de [!DNL DirectQuery]](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-use-directquery), bem como uma discussão abrangente sobre suas [opções de conectividade, casos de uso e limitações](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-about), podem ser encontradas na documentação oficial [!DNL PowerBI].

Para usar este [!DNL Data Connectivity mode], selecione o alternador **[!DNL DirectQuery]** e depois **[!DNL Advanced options]** para inserir uma consulta SQL personalizada na seção **[!DNL SQL statement]**. Verifique se **[!DNL Include relationship columns]** está selecionado. Depois de concluir a consulta, selecione **[!DNL OK]** para continuar.

Uma pré-visualização do query é exibida. Selecione **[!DNL Load]** para ver os resultados da consulta.

## Próximas etapas

Após a leitura deste documento, você deve entender como se conectar ao aplicativo de desktop [!DNL Power BI] e aos diferentes modos de conexão de dados disponíveis. Para obter mais informações sobre como gravar e executar consultas, consulte a [orientação para a execução da consulta](../best-practices/writing-queries.md).
