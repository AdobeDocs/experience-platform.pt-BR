---
keywords: Experience Platform;início;tópicos populares;serviço de consulta;serviço de consulta;Db Visualizer;DbVisualizer;db visualizer;conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar DbVisualizer ao Serviço de consulta
description: Este documento aborda as etapas para conectar o DbVisualizer ao Adobe Experience Platform Query Service.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 1%

---

# Conectar [!DNL DbVisualizer] a [!DNL Query Service] {#connect-dbvisualizer}

Este documento aborda as etapas para conectar a ferramenta de banco de dados [!DNL DbVisualizer] ao Adobe Experience Platform [!DNL Query Service].

## Introdução

Este guia requer que você já tenha acesso ao aplicativo de desktop [!DNL DbVisualizer] e esteja familiarizado com como navegar em sua interface. Para baixar o aplicativo de desktop [!DNL DbVisualizer] ou obter mais informações, consulte a [documentação [!DNL DbVisualizer] oficial](https://www.dbvis.com/download/).

Para adquirir as credenciais necessárias para conectar [!DNL  DbVisualizer] ao Experience Platform, você deve ter acesso ao espaço de trabalho de Consultas na interface do usuário da Platform. Entre em contato com o administrador da organização se não tiver acesso ao espaço de trabalho de Consultas.

## Criar uma conexão de banco de dados {#connect-database}

Depois de instalar o aplicativo de desktop em seu computador local, siga as instruções oficiais do BDVisualizer para [criar uma nova conexão de banco de dados](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection).

Depois de selecionar **[!DNL PostgreSQL]** na lista [!DNL Connections], uma guia [!DNL Object View] para a nova conexão [!DNL PostgreSQL] será exibida.

### Definir propriedades do driver para sua conexão {#properties}

Na guia de exibição de objeto [!DNL PostgreSQL], selecione a guia **[!DNL Properties]**, seguida pela **[!DNL Driver Properties]** na barra lateral de navegação. Mais informações sobre [propriedades do driver](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties) podem ser encontradas na documentação oficial.

Em seguida, insira as propriedades de driver descritas na tabela abaixo.

>[!IMPORTANT]
>
>Para conectar o DBVisualizer ao Adobe Experience Platform, é necessário habilitar o uso de SSL. Consulte a [documentação sobre modos SSL](./ssl-modes.md) para saber mais sobre o suporte SSL para conexões de terceiros ao Serviço de Consulta da Adobe Experience Platform e como se conectar usando o modo SSL `verify-full`.

| Propriedade | Descrição |
| ------ | ------ |
| `PGHOST` | O nome do host do servidor [!DNL PostgreSQL]. Este valor é a sua credencial de Experience Platform **[!UICONTROL Host]**. |
| `ssl` | Defina o valor SSL `1` para habilitar o uso de SSL. |
| `sslmode` | Isso controla o nível de proteção SSL. É recomendável usar o modo SSL `require` ao conectar clientes de terceiros ao Adobe Experience Platform. O modo `require` garante que a criptografia seja necessária em todas as comunicações e que a rede seja confiável para se conectar ao servidor correto. A validação do certificado SSL do servidor não é necessária. |
| `user` | O nome de usuário conectado ao banco de dados é a ID da organização. É uma sequência alfanumérica terminando em `@Adobe.Org`. Este valor é a sua credencial de Experience Platform **[!UICONTROL Nome de usuário]**. |

Use a barra de pesquisa para encontrar cada propriedade e, em seguida, selecione a célula correspondente para o valor do parâmetro. A célula será destacada em azul. Insira sua credencial da Platform no campo de valor e selecione **[!DNL Apply]** para adicionar a propriedade de driver.

>[!NOTE]
>
>Para adicionar um segundo perfil `user`, selecione `user` na coluna de parâmetro e, em seguida, selecione o ícone azul + (mais) para adicionar credenciais para cada usuário. Selecione **[!DNL Apply]** para adicionar a propriedade de driver.

A coluna [!DNL Edited] mostra uma marca de seleção para indicar que o valor do parâmetro foi atualizado.

### Credenciais do Serviço de consulta de entrada {#query-service-credentials}

Para localizar as credenciais necessárias para conectar o BBVisualizer ao Serviço de Consulta, faça logon na Interface do Usuário da Plataforma e selecione **[!UICONTROL Consultas]** na navegação à esquerda, seguido de **[!UICONTROL Credenciais]**. Para obter mais informações sobre como localizar suas credenciais de **host**, **porta**, **banco de dados**, **nome de usuário** e **senha**, leia o [guia de credenciais](../ui/credentials.md).

![A página Credenciais do espaço de trabalho Consultas do Experience Platform com as Credenciais e as Credenciais que Estão Expirando realçadas.](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] também oferece credenciais sem expiração para permitir uma configuração única com clientes de terceiros. Consulte a documentação de [instruções completas sobre como gerar e usar credenciais sem expiração](../ui/credentials.md#non-expiring-credentials). É necessário concluir esse processo se você deseja conectar o BDVisualizer como uma configuração única. Os valores `credential` e `technicalAccountId` adquiridos compõem o valor do parâmetro DBVisualizer `password`.

## Autenticação {#authentication}

Para exigir uma ID de usuário e autenticação baseada em senha sempre que uma conexão for estabelecida, navegue até a guia [!DNL Properties] e selecione **[!DNL Authentication]** na barra lateral de navegação em [!DNL PostgreSQL].

No painel Autenticação de Conexão, marque as caixas de seleção **[!DNL Require Userid]** e **[!DNL Require Password]** e selecione **[!DNL Apply]**. Mais informações sobre [definição de opções de autenticação](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options) podem ser encontradas na documentação oficial.

## Conectar à Platform

Você pode fazer uma conexão usando credenciais com ou sem expiração. Para fazer uma conexão, selecione a guia **[!DNL Connection]** na guia de exibição de objetos [!DNL PostgreSQL] e insira suas credenciais de Experience Platform para as seguintes configurações. Instruções complementares para [configurar uma conexão manual](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually) estão disponíveis no site oficial do DBVisualizer.

>[!NOTE]
>
>Todas as credenciais exigidas pelo BDVisualizer na tabela abaixo são as mesmas para credenciais com e sem expiração, a menos que seja declarado na descrição do parâmetro.

| Parâmetro de conexão | Descrição |
|---|---|
| **[!UICONTROL Nome]** | Crie um nome para a conexão. É recomendável fornecer um nome amigável para reconhecer a conexão. |
| **[!UICONTROL Servidor de Banco de Dados]** | Esta é a credencial do seu Experience Platform **[!UICONTROL Host]**. |
| **[!UICONTROL Porta de Banco de Dados]** | A porta para [!DNL Query Service]. Você deve usar a porta **80** ou **5432** para se conectar com [!DNL Query Service]. |
| **[!UICONTROL Banco de dados]** | Use seu Experience Platform **[!UICONTROL Valor de credencial do banco de dados]**: `prod:all`. |
| **[!UICONTROL Id de Usuário do Banco de Dados]** | Esta é a ID da sua organização da Platform. Use o valor da credencial do Experience Platform **[!UICONTROL Nome de usuário]**. A ID estará no formato de `ORG_ID@AdobeOrg`. |
| **[!UICONTROL Senha do Banco de Dados]** | Esta sequência alfanumérica é a credencial Experience Platform **[!UICONTROL Password]**. Se você quiser usar credenciais sem expiração, esse valor serão os argumentos concatenados de `technicalAccountID` e `credential` baixados no arquivo JSON de configuração. O valor da senha tem o formato: {technicalAccountId}:{credential}. O arquivo JSON de configuração para credenciais sem expiração é um download único durante a inicialização do qual o Adobe não mantém uma cópia. |

Depois de inserir todas as credenciais relevantes, selecione **[!DNL Connect]**.

A caixa de diálogo [!DNL Connect] aparece na primeira ocasião da sessão. Digite sua ID de usuário e senha e selecione **[!DNL Connect]**. Uma mensagem é exibida no log para confirmar uma conexão bem-sucedida.

## Próximas etapas

Agora que você conectou o [!DNL DbVisualizer] com o [!DNL Query Service], é possível usar o [!DNL DbVisualizer] para gravar consultas. Para obter mais informações sobre como gravar e executar consultas, leia o [manual sobre execução de consultas](../best-practices/writing-queries.md).
