---
keywords: Experience Platform;início;tópicos populares;serviço de consulta;serviço de consulta;Power BI;power bi;conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar o Power BI ao Serviço de consulta
description: Este documento aborda as etapas para conectar o Power BI ao Serviço de consulta da Adobe Experience Platform.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 26f0725f0f239707bd719ed46929648f8d557155
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 0%

---

# Conectar [!DNL Power BI] para o Serviço de consulta

Este documento aborda as etapas para a conexão [!DNL Power BI] Desktop com o Serviço de consulta da Adobe Experience Platform.

## Introdução

Este guia requer que você já tenha acesso à [!DNL Power BI] e estão familiarizados com como navegar em sua interface. Para baixar [!DNL Power BI] Área de trabalho ou para obter mais informações, consulte [oficial [!DNL Power BI] documentação](https://docs.microsoft.com/en-us/power-bi/).

>[!IMPORTANT]
>
> A variável [!DNL Power BI] o aplicativo de desktop é **somente** disponível em dispositivos Windows.

Para adquirir as credenciais necessárias para conexão [!DNL Power BI] Para o Experience Platform, você deve ter acesso ao espaço de trabalho Consultas na interface do usuário da Platform. Entre em contato com o administrador da organização se você não tiver acesso ao espaço de trabalho de consultas.

Após a instalação [!DNL Power BI], será necessário instalar `Npgsql`, um pacote de driver .NET para PostgreSQL. Mais informações sobre o Npgsql podem ser encontradas no [Documentação Do Npgsql](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>Você deve baixar a v4.0.10 ou inferior, pois as versões mais recentes resultam em erros.

Em &quot;[!DNL Npgsql GAC Installation]&quot; na tela configuração personalizada, selecione **[!DNL Will be installed on local hard drive]**.

Para garantir que o Npgsql foi instalado corretamente, reinicie o computador antes de prosseguir para as próximas etapas.

## Conectar [!DNL Power BI] para o Serviço de consulta {#connect-power-bi}

Para conectar [!DNL Power BI] para o Serviço de consulta, abra [!DNL Power BI] e selecione **[!DNL Get Data]** na faixa de opções do menu superior. Em seguida, digite &quot;[!DNL PostgreSQL]&quot; na barra de pesquisa para restringir a lista de fontes de dados. Nos resultados exibidos, selecione **[!DNL PostgreSQL database]**, seguido por **[!DNL Connect]**.

A variável [!DNL PostgreSQL] é exibida, solicitando valores para o servidor e o banco de dados. Instruções adicionais sobre como [conectar-se a um banco de dados PostgreSQL no Power Query Desktop](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop) encontra-se no sítio Web [!DNL PowerBI] documentação.

Esses valores obrigatórios foram obtidos de suas credenciais do Adobe Experience Platform. Para encontrar suas credenciais, faça logon na interface do usuário da Platform e selecione **[!UICONTROL Consultas]** na navegação à esquerda, seguido por **[!UICONTROL Credenciais]**. Para obter mais informações sobre como localizar o nome do banco de dados, o host, a porta e as credenciais de logon, leia a [guia de credenciais](../ui/credentials.md).

>[!IMPORTANT]
>
>Como usuário do Power BI Tableau, você pode conectar o Customer Journey Analytics às ferramentas de BI na guia de credenciais do Serviço de consulta. Consulte a documentação de credenciais para obter instruções sobre como [conectar suas ferramentas de BI ao Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics).

![O espaço de trabalho Experience Platform Queries com a guia Credenciais e as credenciais de Expiração são destacadas.](../images/clients/power-bi/query-service-credentials-page.png)

No **[!DNL Server]** do campo [!DNL PostgreSQL database] , insira o valor do host encontrado no Serviço de consulta [!UICONTROL Credenciais] seção. Para produção, adicione a porta `:80` ao final da cadeia de caracteres do host. Por exemplo, `made-up.platform-query.adobe.io:80`.

A variável **[!DNL Database]** o campo pode ser &quot;todos&quot; ou um nome de tabela de conjunto de dados. Por exemplo, `prod:all`.

>[!IMPORTANT]
>
>As estruturas de dados aninhadas em ferramentas de BI de terceiros podem ser niveladas para melhorar sua usabilidade e reduzir a carga de trabalho necessária para recuperar, analisar, transformar e relatar dados. Consulte a documentação no[`FLATTEN` recurso](../key-concepts/flatten-nested-data.md) para obter instruções sobre como ativar essa configuração ao conectar-se a um banco de dados.

### Modo de Conectividade de Dados {#data-connectivity-mode}

Em seguida, você pode selecionar o **[!DNL Data Connectivity mode]**. No [!DNL PostgreSQL database] , selecione **[!DNL Import]** seguido por **[!DNL OK]** para exibir uma lista de todas as tabelas disponíveis, ou selecione **[!DNL DirectQuery]** para consultar a fonte de dados diretamente sem importar ou copiar dados diretamente para [!DNL Power BI].

Para saber mais sobre o **[!DNL Import]** , leia a seção sobre [importação de uma tabela](#import). Para saber mais sobre **[!DNL DirectQuery]** , leia a seção sobre [consulta de um conjunto de dados sem importar dados](#direct-query).

Selecionar **[!DNL OK]** após confirmar os detalhes do banco de dados.

### Autenticação {#authentication}

Após confirmar o modo de conectividade de dados, é exibido um prompt solicitando seu nome de usuário, senha e configurações do aplicativo. Nesse caso, o nome de usuário é a ID da organização e a senha é o token de autenticação. Ambos podem ser encontrados na página de credenciais do Serviço de consulta.

Preencha esses detalhes e selecione **[!DNL Connect]** para prosseguir para a próxima etapa.

## Importar uma tabela {#import}

Ao selecionar a variável **[!DNL Import]** [!DNL Data Connectivity mode], o conjunto de dados completo é importado, o que permite usar as tabelas e colunas selecionadas na [!DNL Power BI] aplicativo de desktop como está.

>[!IMPORTANT]
>
>Para ver as alterações de dados ocorridas desde a importação inicial, atualize os dados em [!DNL Power BI] importando o conjunto de dados completo novamente.

Para importar uma tabela, insira os detalhes do servidor e do banco de dados [conforme descrito acima](#connect-power-bi) e selecione o **[!DNL Import]** [!DNL Data Connectivity mode], seguido por **[!DNL OK]**. A variável [!DNL Navigator] será exibida, exibindo uma lista de todas as tabelas disponíveis. Selecione a tabela que deseja visualizar, seguida de **[!DNL Load]** para trazer o conjunto de dados para o Power BI. A tabela agora é importada para o [!DNL Power BI].

[Informações gerais sobre a conexão com dados no desktop PowerBi](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data) aplicativo pode ser encontrado na documentação oficial.

### Importar tabelas usando SQL personalizado

[!DNL Power BI] e outras ferramentas de terceiros, como [!DNL Tableau] No momento, não permitir que os usuários importem objetos aninhados, como objetos XDM na Platform. Para levar em conta isso, [!DNL Power BI] O permite usar SQL personalizado para acessar esses campos aninhados e criar uma exibição nivelada dos dados. [!DNL Power BI] em seguida, o carrega essa exibição nivelada dos dados aninhados anteriormente como uma tabela normal.

No [!DNL PostgreSQL database] , selecione **[!DNL Advanced options]** para inserir uma consulta SQL personalizada no **[!DNL SQL statement]** seção. Essa consulta personalizada deve ser usada para nivelar seus pares de nome-valor JSON em um formato de tabela. A documentação oficial também fornece informações sobre [conectar o Power BI usando uma instrução SQL nas opções avançadas](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-using-advanced-options).

Depois de inserir sua consulta personalizada, selecione **[!DNL OK]** para continuar conectando seu banco de dados. Consulte a [autenticação](#authentication) acima para obter orientação sobre como conectar um banco de dados a partir dessa parte do fluxo de trabalho.

Quando a autenticação estiver concluída, uma pré-visualização dos dados nivelados será exibida na [!DNL Power BI] Painel da área de trabalho como uma tabela. O nome do servidor e do banco de dados são listados na parte superior da caixa de diálogo. Selecionar **[!DNL Load]** para concluir o processo de importação.

As visualizações agora estão disponíveis para edição e exportação no [!DNL Power BI] Aplicativo de desktop.

## Consultar o conjunto de dados sem importar dados {#direct-query}

A variável **[!DNL DirectQuery]** [!DNL Data Connectivity mode] consulta a fonte de dados diretamente sem importar ou copiar dados para a [!DNL Power BI] Área de trabalho. Usando esse modo de conexão, você pode atualizar todas as visualizações com dados atuais por meio da interface do. No entanto, o tempo necessário para produzir ou atualizar a visualização varia de acordo com o desempenho da fonte de dados subjacente.

Mais informações sobre [a utilização de [!DNL DirectQuery]](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-use-directquery) bem como uma discussão abrangente sobre a sua [opções de conectividade, casos de uso e limitações](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-about) encontra-se no sítio Web [!DNL PowerBI] documentação.

Para usar este [!DNL Data Connectivity mode], selecione o **[!DNL DirectQuery]** alternar e depois **[!DNL Advanced options]** para inserir uma consulta SQL personalizada no **[!DNL SQL statement]** seção. Assegure que **[!DNL Include relationship columns]** está selecionada. Após concluir o query, selecione **[!DNL OK]** para continuar.

Uma pré-visualização do query é exibida. Selecionar **[!DNL Load]** para ver os resultados da consulta.

## Próximas etapas

Após a leitura deste documento, você deve entender como se conectar ao [!DNL Power BI] Aplicativo de desktop e os diferentes modos de conexão de dados disponíveis. Para obter mais informações sobre como gravar e executar queries, consulte [orientação para execução de consulta](../best-practices/writing-queries.md).
