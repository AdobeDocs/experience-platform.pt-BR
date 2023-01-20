---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, Power BI, power bi, conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar o Power BI ao Serviço de Consulta
description: Este documento aborda as etapas para conectar o Power BI com o Adobe Experience Platform Query Service.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 1%

---

# Connect [!DNL Power BI] para Serviço de Consulta

Este documento aborda as etapas para conexão [!DNL Power BI] Área de trabalho com o Serviço de consulta da Adobe Experience Platform.

## Introdução

Este guia requer que você já tenha acesso ao [!DNL Power BI] aplicativos de desktop e estão familiarizados com como navegar em sua interface. Para baixar [!DNL Power BI] Para obter mais informações, consulte o [funcionário [!DNL Power BI] documentação](https://docs.microsoft.com/pt-BR/power-bi/).

>[!IMPORTANT]
>
> O [!DNL Power BI] o aplicativo de desktop é **only** disponível em dispositivos Windows.

Para adquirir as credenciais necessárias para conexão [!DNL Power BI] para o Experience Platform, você deve ter acesso ao espaço de trabalho Consultas na interface do usuário da plataforma. Entre em contato com o administrador da organização caso não tenha acesso ao espaço de trabalho de consultas.

Depois de instalar [!DNL Power BI], será necessário instalar `Npgsql`, um pacote de driver .NET para PostgreSQL. Mais informações sobre o Npgsql podem ser encontradas no [Documentação Npgsql](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>Você deve baixar a v4.0.10 ou inferior, já que versões mais recentes resultam em erros.

Em &quot;[!DNL Npgsql GAC Installation]&quot; na tela de configuração personalizada, selecione **[!DNL Will be installed on local hard drive]**.

Para garantir que o Npgsql foi instalado corretamente, reinicie o computador antes de prosseguir para as próximas etapas.

## Connect [!DNL Power BI] para Serviço de Consulta {#connect-power-bi}

Para ligar [!DNL Power BI] para o Serviço de Consulta, abra [!DNL Power BI] e selecione **[!DNL Get Data]** na faixa do menu superior. Em seguida, digite &quot;[!DNL PostgreSQL]&quot; na barra de pesquisa para restringir a lista de fontes de dados. Nos resultados exibidos, selecione **[!DNL PostgreSQL database]**, seguida de **[!DNL Connect]**.

O [!DNL PostgreSQL] a caixa de diálogo do banco de dados é exibida, solicitando valores para o servidor e o banco de dados. Instruções adicionais sobre como [conectar-se a um banco de dados PostgreSQL do Power Query Desktop](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop) pode ser encontrada no [!DNL PowerBI] documentação.

Esses valores necessários são obtidos de suas credenciais do Adobe Experience Platform. Para encontrar suas credenciais, faça logon na interface do usuário da plataforma e selecione **[!UICONTROL Queries]** no menu de navegação esquerdo, seguido por **[!UICONTROL Credenciais]**. Para obter mais informações sobre como encontrar o nome do banco de dados, o host, a porta e as credenciais de logon, leia a [guia de credenciais](../ui/credentials.md).

![O espaço de trabalho Consultas do Experience Platform com a guia Credenciais e as credenciais de Expiração destacadas.](../images/clients/power-bi/query-service-credentials-page.png)

No **[!DNL Server]** do [!DNL PostgreSQL database] , insira o valor do host encontrado no Serviço de query [!UICONTROL Credenciais] seção. Para produção, adicione porta `:80` ao final da string de host. Por exemplo, `made-up.platform-query.adobe.io:80`.

O **[!DNL Database]** pode ser &quot;all&quot; ou um nome de tabela de conjunto de dados. Por exemplo, `prod:all`.

>[!IMPORTANT]
>
>As estruturas de dados aninhadas em ferramentas de BI de terceiros podem ser niveladas para melhorar sua usabilidade e reduzir a carga de trabalho necessária para recuperar, analisar, transformar e relatar dados. Consulte a documentação no[`FLATTEN` recurso](../essential-concepts/flatten-nested-data.md) para obter instruções sobre como ativar essa configuração ao se conectar a um banco de dados.

### Modo de Conectividade de Dados {#data-connectivity-mode}

Em seguida, você pode selecionar **[!DNL Data Connectivity mode]**. No [!DNL PostgreSQL database] , selecione **[!DNL Import]** seguida de **[!DNL OK]** para exibir uma lista de todas as tabelas disponíveis ou selecione **[!DNL DirectQuery]** para consultar a fonte de dados diretamente sem importar ou copiar dados diretamente para o [!DNL Power BI].

Para saber mais sobre o **[!DNL Import]** , leia a seção sobre [importação de uma tabela](#import). Para saber mais sobre **[!DNL DirectQuery]** , leia a seção sobre [consulta de um conjunto de dados sem importar dados](#direct-query).

Selecionar **[!DNL OK]** depois de confirmar os detalhes do banco de dados.

### Autenticação {#authentication}

Depois de confirmar o modo de conectividade de dados, um prompt solicitando o nome de usuário, senha e configurações do aplicativo é exibido. Nesse caso, o nome de usuário é a ID da organização e a senha é o token de autenticação. Ambos podem ser encontrados na página de credenciais do Serviço de Consulta.

Preencha estes detalhes e selecione **[!DNL Connect]** para continuar até a próxima etapa.

## Importar uma tabela {#import}

Ao selecionar a variável **[!DNL Import]** [!DNL Data Connectivity mode], o conjunto de dados completo é importado, permitindo usar as tabelas e colunas selecionadas na [!DNL Power BI] aplicativo de desktop como está.

>[!IMPORTANT]
>
>Para ver as alterações de dados ocorridas desde a importação inicial, é necessário atualizar os dados no [!DNL Power BI] importando o conjunto de dados completo novamente.

Para importar uma tabela, insira os detalhes do servidor e do banco de dados [conforme descrito acima](#connect-power-bi) e selecione o **[!DNL Import]** [!DNL Data Connectivity mode], seguida de **[!DNL OK]**. O [!DNL Navigator] for exibida, exibindo uma lista de todas as tabelas disponíveis. Selecione a tabela que deseja visualizar, seguida por **[!DNL Load]** para trazer o conjunto de dados para o Power BI. A tabela agora é importada para [!DNL Power BI].

[Informações gerais sobre conexão com dados no desktop PowerBi](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data) app pode ser encontrado na documentação oficial.

### Importar tabelas usando SQL personalizado

[!DNL Power BI] e outras ferramentas de terceiros como [!DNL Tableau] no momento, não permite que usuários importem objetos aninhados, como objetos XDM na Plataforma. Para considerar isso, [!DNL Power BI] permite usar o SQL personalizado para acessar esses campos aninhados e criar uma visualização nivelada dos dados. [!DNL Power BI] em seguida, carrega essa visualização nivelada dos dados aninhados anteriormente como uma tabela normal.

No [!DNL PostgreSQL database] , selecione **[!DNL Advanced options]** para inserir uma consulta SQL personalizada no **[!DNL SQL statement]** seção. Essa consulta personalizada deve ser usada para nivelar seus pares de nome-valor JSON em um formato de tabela. A documentação oficial também fornece informações sobre como [conectar o Power BI usando uma instrução SQL nas opções avançadas](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-using-advanced-options).

Após ter inserido seu query personalizado, selecione **[!DNL OK]** para continuar a conectar o banco de dados. Consulte a [autenticação](#authentication) seção acima para obter orientação sobre como conectar um banco de dados a partir dessa parte do workflow.

Uma vez concluída a autenticação, uma pré-visualização dos dados nivelados aparecerá no [!DNL Power BI] Painel da área de trabalho como uma tabela. O servidor e o nome do banco de dados são listados na parte superior da caixa de diálogo. Selecionar **[!DNL Load]** para concluir o processo de importação.

As visualizações agora estão disponíveis para edição e exportação do [!DNL Power BI] Aplicativo de desktop.

## Consultar o conjunto de dados sem importar dados {#direct-query}

O **[!DNL DirectQuery]** [!DNL Data Connectivity mode] consulta a fonte de dados diretamente sem importar ou copiar dados para o [!DNL Power BI] Desktop. Usando esse modo de conexão, você pode atualizar todas as visualizações com dados atuais por meio da interface do usuário. No entanto, o tempo necessário para produzir ou atualizar a visualização varia de acordo com o desempenho da fonte de dados subjacente.

Mais informações sobre [a utilização de [!DNL DirectQuery]](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-use-directquery) bem como uma discussão abrangente sobre a sua [opções de conectividade, casos de uso e limitações](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-about) pode ser encontrada no [!DNL PowerBI] documentação.

Para usar isso [!DNL Data Connectivity mode], selecione o **[!DNL DirectQuery]** alternar então **[!DNL Advanced options]** para inserir uma consulta SQL personalizada no **[!DNL SQL statement]** seção. Certifique-se de que **[!DNL Include relationship columns]** está selecionada. Após concluir seu query, selecione **[!DNL OK]** para continuar.

Uma pré-visualização do query é exibida. Selecionar **[!DNL Load]** para ver os resultados da query.

## Próximas etapas

Ao ler este documento, você deve entender como se conectar ao [!DNL Power BI] Aplicativo de desktop e os diferentes modos de conexão de dados disponíveis. Para obter mais informações sobre como gravar e executar queries, consulte o [orientação para a execução da consulta](../best-practices/writing-queries.md).
