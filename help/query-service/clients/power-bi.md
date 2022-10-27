---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, Power BI, power bi, conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar o Power BI ao Serviço de Consulta
topic-legacy: connect
description: Este documento aborda as etapas para conectar o Power BI com o Adobe Experience Platform Query Service.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 1%

---

# Connect [!DNL Power BI] para Serviço de Consulta

Este documento aborda as etapas para conexão [!DNL Power BI] Área de trabalho com o Serviço de consulta da Adobe Experience Platform.

## Introdução

Este guia requer que você já tenha acesso ao [!DNL Power BI] aplicativos de desktop e estão familiarizados com como navegar em sua interface. Para baixar [!DNL Power BI] Para obter mais informações, consulte o [funcionário [!DNL Power BI] documentação](https://docs.microsoft.com/pt-BR/power-bi/).

>[!IMPORTANT]
>
> O [!DNL Power BI] o aplicativo de desktop é **only** disponível em dispositivos Windows.

Para adquirir as credenciais necessárias para conexão [!DNL Power BI] para o Experience Platform, você deve ter acesso ao espaço de trabalho Consultas na interface do usuário da plataforma. Entre em contato com o administrador da Organização IMS caso não tenha acesso ao espaço de trabalho de Consultas.

Depois de instalar [!DNL Power BI], será necessário instalar `Npgsql`, um pacote de driver .NET para PostgreSQL. Mais informações sobre o Npgsql podem ser encontradas no [Documentação Npgsql](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>Você deve baixar a v4.0.10 ou inferior, já que versões mais recentes resultam em erros.

Em &quot;[!DNL Npgsql GAC Installation]&quot; na tela de configuração personalizada, selecione **[!DNL Will be installed on local hard drive]**.

Para garantir que o Npgsql foi instalado corretamente, reinicie o computador antes de prosseguir para as próximas etapas.

## Connect [!DNL Power BI] para Serviço de Consulta {#connect-power-bi}

Para ligar [!DNL Power BI] para o Serviço de Consulta, abra [!DNL Power BI] e selecione **[!DNL Get Data]** na faixa do menu superior.

![O [!DNL Power BI] guia inicial do painel com os dados Get realçados.](../images/clients/power-bi/open-power-bi.png)

Digite &quot;[!DNL PostgreSQL]&quot; na barra de pesquisa para restringir a lista de fontes de dados. Nos resultados que forem exibidos, selecione **[!DNL PostgreSQL database]**, seguida de **[!DNL Connect]**.

![A caixa de diálogo Obter dados com [!DNL PostgreSQL] e Connect realçados.](../images/clients/power-bi/get-data.png)

O [!DNL PostgreSQL] a caixa de diálogo do banco de dados é exibida, solicitando valores para o servidor e o banco de dados. Esses valores são obtidos de suas credenciais do Adobe Experience Platform. Para encontrar suas credenciais, faça logon na interface do usuário da plataforma e selecione **[!UICONTROL Queries]** no menu de navegação esquerdo, seguido por **[!UICONTROL Credenciais]**. Para obter mais informações sobre como encontrar o nome do banco de dados, o host, a porta e as credenciais de logon, leia a [guia de credenciais](../ui/credentials.md).

![O espaço de trabalho Consultas do Experience Platform com a guia Credenciais e as credenciais de Expiração destacadas.](../images/clients/power-bi/query-service-credentials-page.png)

Para o **[!DNL Server]** no Power BI, insira o valor do host encontrado na seção Credenciais do Serviço de Consulta. Para produção, adicione porta `:80` ao final da string de host. Por exemplo, `made-up.platform-query.adobe.io:80`.

O **[!DNL Database]** pode ser &quot;all&quot; ou um nome de tabela de conjunto de dados. Por exemplo, `prod:all`.

>[!IMPORTANT]
>
>As estruturas de dados aninhadas em ferramentas de BI de terceiros podem ser niveladas para melhorar sua usabilidade e reduzir a carga de trabalho necessária para recuperar, analisar, transformar e relatar dados. Consulte a documentação no[`FLATTEN` recurso](../best-practices/flatten-nested-data.md) para obter instruções sobre como ativar essa configuração ao se conectar a um banco de dados.

![O [!DNL Power BI] painel com os campos de entrada do servidor e do banco de dados realçados.](../images/clients/power-bi/postgresql-database-dialog.png)

### Modo de Conectividade de Dados

Em seguida, você pode selecionar **[!DNL Data Connectivity mode]**. Selecionar **[!DNL Import]** seguida de **[!DNL OK]** para exibir uma lista de todas as tabelas disponíveis ou selecione **[!DNL DirectQuery]** para consultar a fonte de dados diretamente sem importar ou copiar dados diretamente para o [!DNL Power BI].

Para saber mais sobre **[!DNL Import]** , leia a seção sobre [importação de uma tabela](#import). Para saber mais sobre **[!DNL DirectQuery]** , leia a seção sobre [consulta de um conjunto de dados sem importar dados](#direct-query).

Selecionar **[!DNL OK]** depois de confirmar os detalhes do banco de dados.

![O [!DNL PostgreSQL] caixa de diálogo do banco de dados com o modo Conectividade de dados realçada.](../images/clients/power-bi/connectivity-mode.png)

### Autenticação

Um prompt solicitando seu nome de usuário, senha e configurações do aplicativo é exibido. Nesse caso, o nome de usuário é a ID da organização e a senha é o token de autenticação. Ambos podem ser encontrados na página de credenciais do Serviço de Consulta.

Preencha estes detalhes e selecione **[!DNL Connect]** para continuar até a próxima etapa.

![A caixa de diálogo do banco de dados com nome de usuário, senha e menu suspenso de configurações do aplicativo foi realçada.](../images/clients/power-bi/import-mode.png)

## Importar uma tabela {#import}

Ao selecionar a variável **[!DNL Import]** [!DNL Data Connectivity mode], o conjunto de dados completo é importado, permitindo usar as tabelas e colunas selecionadas na [!DNL Power BI] aplicativo de desktop como está.

>[!IMPORTANT]
>
>Para ver as alterações de dados ocorridas desde a importação inicial, é necessário atualizar os dados no [!DNL Power BI] importando o conjunto de dados completo novamente.

Para importar uma tabela, insira os detalhes do servidor e do banco de dados [conforme descrito acima](#connect-power-bi) e selecione o **[!DNL Import]** [!DNL Data Connectivity mode], seguida de **[!DNL OK]**. Uma caixa de diálogo é exibida, exibindo uma lista de todas as tabelas disponíveis. Selecione a tabela que deseja visualizar, seguida por **[!DNL Load]** para trazer o conjunto de dados para o Power BI.

![A caixa de diálogo Navegador com uma tabela e Carregar realçada.](../images/clients/power-bi/preview-table.png)

A tabela agora é importada para [!DNL Power BI].

![O [!DNL Power BI] painel com instruções sobre como criar visualizações personalizadas realçadas.](../images/clients/power-bi/import-table.png)

### Importar tabelas usando SQL personalizado

[!DNL Power BI] e outras ferramentas de terceiros, como o Tableau, atualmente não permitem que os usuários importem objetos aninhados, como objetos XDM na Platform. Para considerar isso, [!DNL Power BI] permite usar o SQL personalizado para acessar esses campos aninhados e criar uma visualização nivelada dos dados. [!DNL Power BI] em seguida, carrega essa visualização nivelada dos dados aninhados anteriormente como uma tabela normal.

No [!DNL PostgreSQL] provedor de banco de dados, selecione **[!DNL Advanced options]** para inserir uma consulta SQL personalizada no **[!DNL SQL statement]** seção. Essa consulta personalizada deve ser usada para nivelar seus pares de nome-valor JSON em um formato de tabela.

![O [!DNL PostgreSQL] realçada a caixa de diálogo do banco de dados com as opções avançadas do modo de conectividade de dados. Isso permite criar uma instrução SQL personalizada.](../images/clients/power-bi/custom-sql-statement.png)

Após ter inserido seu query personalizado, selecione **[!DNL OK]** para continuar a conectar o banco de dados. Consulte a [autenticação](#authentication) seção acima para obter orientação sobre como conectar um banco de dados a partir dessa parte do workflow.

Uma vez concluída a autenticação, uma pré-visualização dos dados nivelados aparecerá no [!DNL Power BI] Painel da área de trabalho como uma tabela. O servidor e o nome do banco de dados são listados na parte superior da caixa de diálogo. Selecionar **[!DNL Load]** para concluir o processo de importação.

![Uma visualização de uma tabela nivelada e importada na [!DNL Power BI] painel.](../images/clients/power-bi/imported-table-preview.png)

As visualizações agora estão disponíveis para edição e exportação do [!DNL Power BI] Aplicativo de desktop.

## Consultar o conjunto de dados sem importar dados {#direct-query}

O **[!DNL DirectQuery]** [!DNL Data Connectivity mode] consulta a fonte de dados diretamente sem importar ou copiar dados para o [!DNL Power BI] Desktop. Usando esse modo de conexão, você pode atualizar todas as visualizações com dados atuais por meio da interface do usuário. No entanto, o tempo necessário para produzir ou atualizar a visualização varia de acordo com o desempenho da fonte de dados subjacente.

Para usar isso [!DNL Data Connectivity mode], selecione o **[!DNL DirectQuery]** alternar então **[!DNL Advanced options]** para inserir uma consulta SQL personalizada no **[!DNL SQL statement]** seção. Certifique-se de que **[!DNL Include relationship columns]** está selecionada. Após concluir seu query, selecione **[!DNL OK]** para continuar.

![O [!DNL PostgreSQL] caixa de diálogo do banco de dados com as configurações necessárias para usar o modo Conectividade de dados realçado.](../images/clients/power-bi/direct-query-mode.png)

Uma pré-visualização do query é exibida. Selecionar **[!DNL Load]** para ver os resultados da query.

![Uma pré-visualização dos resultados tabularizados da query de exemplo.](../images/clients/power-bi/preview-direct-query.png)

## Próximas etapas

Ao ler este documento, você deve entender como se conectar ao [!DNL Power BI] Aplicativo de desktop e os diferentes modos de conexão de dados disponíveis. Para obter mais informações sobre como gravar e executar queries, consulte o [orientação para a execução da consulta](../best-practices/writing-queries.md).
