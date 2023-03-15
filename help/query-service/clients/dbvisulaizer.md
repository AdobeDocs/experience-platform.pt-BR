---
keywords: Experience Platform;início;tópicos populares;serviço de consulta;serviço de consulta;Db Visualizer;DbVisualizer;db visualizer;conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar DbVisualizer ao Serviço de consulta
description: Este documento aborda as etapas para conectar o DbVisualizer ao Adobe Experience Platform Query Service.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: 106a2e4606e94f71d6359cf947e05f193c19c660
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 1%

---

# Conectar [!DNL DbVisualizer] para [!DNL Query Service] {#connect-dbvisualizer}

Este documento aborda as etapas para conectar o [!DNL DbVisualizer] ferramenta de banco de dados com o Adobe Experience Platform [!DNL Query Service].

## Introdução

Este guia requer que você já tenha acesso à [!DNL DbVisualizer] e estão familiarizados com como navegar em sua interface. Para baixar o [!DNL DbVisualizer] aplicativo de desktop ou para obter mais informações, consulte a [oficial [!DNL DbVisualizer] documentação](https://www.dbvis.com/download/).

Para adquirir as credenciais necessárias para conexão [!DNL  DbVisualizer] Para o Experience Platform, você deve ter acesso ao espaço de trabalho Consultas na interface do usuário da Platform. Entre em contato com o administrador da organização de IMS se você não tiver acesso ao espaço de trabalho de Consultas.

## Criar uma conexão de banco de dados {#connect-database}

Depois de instalar o aplicativo de desktop no computador local, siga as instruções oficiais do BDVisualizer para [criar uma nova conexão de banco de dados](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection).

Depois de selecionar **[!DNL PostgreSQL]** do [!DNL Connections] lista, um [!DNL Object View] para o novo [!DNL PostgreSQL] conexão é exibida.

### Definir propriedades do driver para sua conexão {#properties}

No [!DNL PostgreSQL] guia exibição de objetos, selecione a **[!DNL Properties]** , seguido pela guia **[!DNL Driver Properties]** na barra lateral de navegação. Mais informações sobre [propriedades do driver](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties) podem ser encontradas na documentação oficial.

Em seguida, insira as propriedades de driver descritas na tabela abaixo.

>[!IMPORTANT]
>
>Para conectar o DBVisualizer ao Adobe Experience Platform, é necessário habilitar o uso de SSL. Consulte a [Documentação de modos SSL](./ssl-modes.md) para saber mais sobre o suporte SSL para conexões de terceiros ao Adobe Experience Platform Query Service e como se conectar usando `verify-full` Modo SSL.

| Propriedade | Descrição |
| ------ | ------ |
| `PGHOST` | O nome do host para o [!DNL PostgreSQL] servidor. Esse valor é o seu Experience Platform **[!UICONTROL Host] credencial**. |
| `ssl` | Definir o valor SSL `1` para habilitar o uso de SSL. |
| `sslmode` | Isso controla o nível de proteção SSL. É recomendável usar o `require` Modo SSL ao conectar clientes de terceiros ao Adobe Experience Platform. A variável `require` garante que a criptografia seja necessária em todas as comunicações e que a rede seja confiável para se conectar ao servidor correto. A validação do certificado SSL do servidor não é necessária. |
| `user` | O nome de usuário conectado ao banco de dados é a ID da organização. É uma sequência alfanumérica terminando em `@Adobe.Org`. Esse valor é o seu Experience Platform **[!UICONTROL Nome de usuário] credencial**. |

Use a barra de pesquisa para encontrar cada propriedade e, em seguida, selecione a célula correspondente para o valor do parâmetro. A célula será destacada em azul. Insira a credencial da Platform no campo de valor e selecione **[!DNL Apply]** para adicionar a propriedade do driver.

>[!NOTE]
>
>Para adicionar um segundo `user` perfil, selecione `user` na coluna parâmetro, selecione o ícone azul + (mais) para adicionar credenciais para cada usuário. Selecionar **[!DNL Apply]** para adicionar a propriedade do driver.

A variável [!DNL Edited] mostra uma marca de seleção para indicar que o valor do parâmetro foi atualizado.

### Credenciais do Serviço de consulta de entrada {#query-service-credentials}

Para encontrar as credenciais necessárias para conectar o BBVisualizer ao Serviço de consulta, faça logon na interface do usuário da plataforma e selecione **[!UICONTROL Consultas]** na navegação à esquerda, seguido por **[!UICONTROL Credenciais]**. Para obter mais informações sobre como encontrar **host**, **porta**, **banco de dados**, **nome de usuário**, e **senha** credenciais, leia as [guia de credenciais](../ui/credentials.md).

![A página Credenciais do espaço de trabalho Consultas do Experience Platform com as Credenciais e as Credenciais que Estão Expirando são destacadas.](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] O também oferece credenciais sem expiração para permitir uma configuração única com clientes de terceiros. Consulte a documentação para [instruções completas sobre como gerar e usar credenciais sem expiração](../ui/credentials.md#non-expiring-credentials). É necessário concluir esse processo se você deseja conectar o BDVisualizer como uma configuração única. A variável `credential` e `technicalAccountId` os valores adquiridos incluem o valor para o DBVisualizer `password` parâmetro.

## Autenticação {#authentication}

Para exigir uma ID de usuário e autenticação baseada em senha sempre que uma conexão for estabelecida, navegue até a [!DNL Properties] e selecione **[!DNL Authentication]** na barra lateral de navegação em [!DNL PostgreSQL].

No painel Autenticação de conexão, marque a opção **[!DNL Require Userid]** e **[!DNL Require Password]** marque as caixas de seleção e selecione **[!DNL Apply]**. Mais informações sobre [definindo opções de autenticação](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options) encontra-se na documentação oficial.

## Conectar à Platform

Você pode fazer uma conexão usando credenciais com ou sem expiração. Para fazer uma conexão, selecione o **[!DNL Connection]** na guia [!DNL PostgreSQL] guia visualização de objetos e insira suas credenciais de Experience Platform para as seguintes configurações. Instruções complementares para [configurar uma conexão manual](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually) estão disponíveis no site oficial do DBVisualizer.

>[!NOTE]
>
>Todas as credenciais exigidas pelo BDVisualizer na tabela abaixo são as mesmas para credenciais com e sem expiração, a menos que seja declarado na descrição do parâmetro.

| Parâmetro de conexão | Descrição |
|---|---|
| **[!UICONTROL Nome]** | Crie um nome para a conexão. É recomendável fornecer um nome amigável para reconhecer a conexão. |
| **[!UICONTROL Servidor de banco de dados]** | Este é o seu Experience Platform **[!UICONTROL Host]** credencial. |
| **[!UICONTROL Porta do banco de dados]** | A porta para [!DNL Query Service]. Você deve usar a porta **80** ou **5432** para se conectar com [!DNL Query Service]. |
| **[!UICONTROL Banco de dados]** | Use seu Experience Platform **[!UICONTROL Banco de dados]** valor da credencial: `prod:all`. |
| **[!UICONTROL ID de usuário do banco de dados]** | Esta é a ID da sua organização da Platform. Use seu Experience Platform **[!UICONTROL Nome de usuário]** valor da credencial. A ID estará no formato de `ORG_ID@AdobeOrg`. |
| **[!UICONTROL Senha do banco de dados]** | Esta sequência alfanumérica é o seu Experience Platform **[!UICONTROL Senha]** credencial. Se você quiser usar credenciais sem expiração, esse valor será os argumentos concatenados do `technicalAccountID` e a variável `credential` baixado no arquivo JSON de configuração. O valor da senha tem o formato: {technicalAccountId}:{credential}. O arquivo JSON de configuração para credenciais sem expiração é um download único durante a inicialização do qual o Adobe não mantém uma cópia. |

Depois de inserir todas as credenciais relevantes, selecione **[!DNL Connect]**.

A variável [!DNL Connect] aparecerá na primeira ocasião da sessão. Digite sua ID de usuário e senha e selecione **[!DNL Connect]**. Uma mensagem é exibida no log para confirmar uma conexão bem-sucedida.

## Próximas etapas

Agora que você se conectou [!DNL DbVisualizer] com [!DNL Query Service], você pode usar [!DNL DbVisualizer] para gravar consultas. Para obter mais informações sobre como gravar e executar consultas, leia o [guia sobre a execução da consulta](../best-practices/writing-queries.md).
