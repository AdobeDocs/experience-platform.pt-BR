---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, Db Visualizer, DbVisualizer, db visulaizer, conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar o DbVisualizer ao Serviço de query
description: Este documento aborda as etapas para conectar o DbVisualizer ao Serviço de query do Adobe Experience Platform.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: 106a2e4606e94f71d6359cf947e05f193c19c660
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 1%

---

# Connect [!DNL DbVisualizer] para [!DNL Query Service] {#connect-dbvisualizer}

Este documento aborda as etapas para conectar o [!DNL DbVisualizer] ferramenta de banco de dados com Adobe Experience Platform [!DNL Query Service].

## Introdução

Este guia requer que você já tenha acesso ao [!DNL DbVisualizer] aplicativos de desktop e estão familiarizados com como navegar em sua interface. Para baixar o [!DNL DbVisualizer] para aplicativos de desktop ou para obter mais informações, consulte o [funcionário [!DNL DbVisualizer] documentação](https://www.dbvis.com/download/).

Para adquirir as credenciais necessárias para conexão [!DNL  DbVisualizer] para o Experience Platform, você deve ter acesso ao espaço de trabalho Consultas na interface do usuário da plataforma. Entre em contato com o administrador da Organização IMS caso não tenha acesso ao espaço de trabalho de Consultas.

## Criar uma conexão de banco de dados {#connect-database}

Depois de instalar o aplicativo de desktop na máquina local, siga as instruções oficiais do BDVisualizer para [criar uma nova conexão de banco de dados](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection).

Depois de selecionar **[!DNL PostgreSQL]** do [!DNL Connections] lista, um [!DNL Object View] para o novo [!DNL PostgreSQL] é exibida.

### Definir as propriedades do controlador para a ligação {#properties}

No [!DNL PostgreSQL] guia exibição de objeto, selecione o **[!DNL Properties]** , seguido pela guia **[!DNL Driver Properties]** na barra lateral de navegação. Mais informações sobre [propriedades do driver](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties) pode ser encontrada na documentação oficial.

Em seguida, insira as propriedades do driver descritas na tabela abaixo.

>[!IMPORTANT]
>
>Para conectar o DBVisualizer ao Adobe Experience Platform, você deve habilitar o uso do SSL. Consulte a [Documentação dos modos SSL](./ssl-modes.md) para saber mais sobre o suporte SSL para conexões de terceiros com o Adobe Experience Platform Query Service e como se conectar usando `verify-full` Modo SSL.

| Propriedade | Descrição |
| ------ | ------ |
| `PGHOST` | O nome do host para o [!DNL PostgreSQL] servidor. Esse é o seu Experience Platform **[!UICONTROL Host] credencial**. |
| `ssl` | Definir o valor SSL `1` para ativar o uso de SSL. |
| `sslmode` | Isso controla o nível de proteção SSL. É recomendável usar o `require` Modo SSL ao conectar clientes de terceiros ao Adobe Experience Platform. O `require` O modo garante que a criptografia seja necessária em todas as comunicações e que a rede seja confiável para se conectar ao servidor correto. A validação do certificado SSL do servidor não é necessária. |
| `user` | O nome de usuário conectado ao banco de dados é a ID da organização. É uma sequência de caracteres alfanumérica que termina em `@Adobe.Org`. Esse é o seu Experience Platform **[!UICONTROL Nome do usuário] credencial**. |

Use a barra de pesquisa para localizar cada propriedade e, em seguida, selecione a célula correspondente para o valor do parâmetro. A célula será realçada em azul. Insira sua credencial da Platform no campo de valor e selecione **[!DNL Apply]** para adicionar a propriedade do driver.

>[!NOTE]
>
>Para adicionar um segundo `user` perfil, selecione `user` na coluna de parâmetro , selecione o ícone azul + (mais) para adicionar credenciais para cada usuário. Selecionar **[!DNL Apply]** para adicionar a propriedade do driver.

O [!DNL Edited] mostra uma marca de seleção para indicar que o valor do parâmetro foi atualizado.

### Credenciais do Serviço de Consulta de Entrada {#query-service-credentials}

Para encontrar as credenciais necessárias para conectar o BBVisualizer com o Serviço de query, faça logon na interface do usuário da plataforma e selecione **[!UICONTROL Queries]** no menu de navegação esquerdo, seguido por **[!UICONTROL Credenciais]**. Para obter mais informações sobre como encontrar seu **host**, **porta**, **banco de dados**, **username** e **senha** credenciais, leia a [guia de credenciais](../ui/credentials.md).

![A página Credenciais do espaço de trabalho Consultas do Experience Platform com Credenciais e as Credenciais de Expiração destacadas.](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] O também oferece credenciais que não estão expirando para permitir uma configuração única com clientes de terceiros. Consulte a documentação para [instruções completas sobre como gerar e usar credenciais que não estão expirando](../ui/credentials.md#non-expiring-credentials). É necessário concluir esse processo se você quiser conectar o BDVisualizer como uma configuração única. O `credential` e `technicalAccountId` os valores adquiridos incluem o valor do DBVisualizer `password` parâmetro.

## Autenticação {#authentication}

Para exigir uma ID de usuário e uma autenticação por senha sempre que uma conexão for estabelecida, navegue até a [!DNL Properties] e selecione **[!DNL Authentication]** na barra lateral de navegação abaixo [!DNL PostgreSQL].

No painel Autenticação de conexão, verifique as **[!DNL Require Userid]** e **[!DNL Require Password]** caixas de seleção e, em seguida, selecione **[!DNL Apply]**. Mais informações sobre [definição das opções de autenticação](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options) podem ser encontradas na documentação oficial.

## Conectar-se à plataforma

Você pode fazer uma conexão usando credenciais que estão expirando ou que não estão expirando. Para fazer uma conexão, selecione o **[!DNL Connection]** na guia do [!DNL PostgreSQL] guia exibição de objeto e insira suas credenciais de Experience Platform para as seguintes configurações. Instruções complementares para [configurar uma conexão manual](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually) estão disponíveis no sítio Web oficial do DBVisualizer.

>[!NOTE]
>
>Todas as credenciais exigidas pelo BDVisualizer na tabela abaixo são iguais para credenciais que expiram e não expiram, a menos que declarado na descrição do parâmetro.

| Parâmetro de conexão | Descrição |
|---|---|
| **[!UICONTROL Nome]** | Crie um nome para a sua conexão. É recomendável fornecer um nome amigável para reconhecer a conexão. |
| **[!UICONTROL Servidor de banco de dados]** | Este é o seu Experience Platform **[!UICONTROL Host]** credencial. |
| **[!UICONTROL Porta do Banco de Dados]** | A porta para [!DNL Query Service]. Você deve usar a porta **80º** ou **5432** para conectar-se com [!DNL Query Service]. |
| **[!UICONTROL Banco de dados]** | Use seu Experience Platform **[!UICONTROL Banco de dados]** valor da credencial: `prod:all`. |
| **[!UICONTROL Userid do Banco de Dados]** | Esta é a ID da organização da plataforma. Use seu Experience Platform **[!UICONTROL Nome do usuário]** valor da credencial. A ID estará no formato de `ORG_ID@AdobeOrg`. |
| **[!UICONTROL Senha do banco de dados]** | Esta sequência alfanumérica é o seu Experience Platform **[!UICONTROL Senha]** credencial. Se você quiser usar credenciais que não estejam expirando, esse valor será o argumento concatenado da variável `technicalAccountID` e `credential` baixado no arquivo JSON de configuração. O valor da senha assume o formulário: {technicalAccountId}:{credential}. O arquivo JSON de configuração para credenciais que não expiram é um download único durante a inicialização que o Adobe não mantém uma cópia. |

Depois de ter inserido todas as credenciais relevantes, selecione **[!DNL Connect]**.

O [!DNL Connect] será exibida na primeira ocasião da sessão. Digite sua ID de usuário e senha e selecione **[!DNL Connect]**. Uma mensagem é exibida no log para confirmar uma conexão bem-sucedida.

## Próximas etapas

Agora que você se conectou [!DNL DbVisualizer] com [!DNL Query Service], você pode usar [!DNL DbVisualizer] para gravar queries. Para obter mais informações sobre como gravar e executar consultas, leia o [guia sobre execução de query](../best-practices/writing-queries.md).
