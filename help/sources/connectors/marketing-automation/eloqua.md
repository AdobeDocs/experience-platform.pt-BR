---
title: Visão Geral Do Oracle Eloqua (V2) Source
description: Saiba como conectar o Oracle Eloqua ao Adobe Experience Platform.
source-git-commit: 180754969d4ae8dbd1308dfc85dae73baf64f759
workflow-type: tm+mt
source-wordcount: '1824'
ht-degree: 1%

---

# Visão geral da origem de [!DNL Oracle Eloqua] (V2)

>[!IMPORTANT]
>
>A origem [[!DNL Oracle Eloqua] (V1)](oracle-eloqua.md) original foi descontinuada em janeiro de 2026. Não há migrações disponíveis para esta fonte obsoleta e você deve reimplementar seus dados usando a nova fonte [!DNL Oracle Eloqua] (V2).

O [!DNL Oracle Eloqua] é uma poderosa plataforma de automação de marketing de nível empresarial projetada para ajudar as organizações, principalmente no setor B2B, a automatizar e personalizar o complexo processo de gerenciamento de clientes potenciais e de orquestração de jornadas dos compradores. Ele serve como um hub central onde as equipes de marketing podem definir, implantar e medir campanhas sofisticadas em vários canais digitais, garantindo que os clientes potenciais recebam o conteúdo certo no momento exato em que estão mais envolvidos. Os objetos com suporte para assimilação por meio de [!DNL Eloqua] são **Contatos**, **Contas**, **Campanhas** e **Atividades**. Quando a assimilação inicial for concluída, todos os dados alterados serão importados usando um processo incremental programado.

Você pode usar a origem [!DNL Eloqua] para conectar sua conta do [!DNL Eloqua] à Adobe Experience Platform. Leia a documentação abaixo para saber como começar.

## Exemplos de caso de uso {#use-case-examples}

A tabela abaixo descreve os objetos de marketing aos quais a integração [!DNL Eloqua] (V2) com o Adobe Experience Platform oferece suporte. Para cada objeto, você encontrará uma descrição, juntamente com casos de uso de exemplo, para ilustrar como a integração de dados do [!DNL Eloqua] com o Real-Time CDP pode aumentar a eficácia do marketing e os resultados da campanha.

| Objeto | Descrição | Exemplos de caso de uso |
| --- | --- | --- |
| Contatos | Insira dados de contato (como nome, email, número de telefone, cargo) no Real-Time CDP para criar perfis de clientes detalhados e unificados que consolidem todas as interações e compromissos com cada contato individual. | **Otimização de Campanha:** ao integrar dados de contato do [!DNL Eloqua], sua equipe de marketing pode identificar prospetos de alta prioridade com base em atividades recentes, como aberturas de email, envios de formulários e registros de eventos. O Real-Time CDP fornece uma visualização de 360° do comportamento de cada contato por email, site e outros pontos de contato de marketing, permitindo que as equipes de marketing personalizem campanhas e otimizem as mensagens para melhorar o engajamento e a conversão. |
| Contas | Assimile dados a nível de conta (como nome da empresa, setor, tamanho da empresa, receita, localização) para desenvolver estratégias de marketing baseado em conta (ABM) no Real-Time CDP e permitir que sua equipe direcione e envolva as organizações certas com mensagens relevantes. | **Campanhas ABM:** a integração de dados de conta de [!DNL Eloqua] ajuda a criar campanhas ABM direcionadas. Por exemplo, uma empresa de software poderia usar os dados da conta para segmentar e enviar campanhas de email personalizadas para tomadores de decisão em empresas do setor financeiro, promovendo novas soluções personalizadas para seu setor. |
| Campanhas | Assimilar dados de campanha (como nomes de campanha, tipos, metas, métricas de desempenho como taxas de abertura, CTRs) na Real-Time CDP para rastrear e otimizar o desempenho da campanha em vários canais. Use esses dados para medir o ROI e refinar suas estratégias. | **Atribuição entre canais:** se [!DNL Eloqua] enviar dados de campanha para a Real-Time CDP, as equipes de marketing poderão ver o desempenho das campanhas em vários canais (email, redes sociais, anúncios, etc.), atribuindo conversões aos pontos de contato corretos e refinando estratégias futuras com base nessa insight. |
| Atividades | Assimilar dados de atividade (como aberturas de email, cliques, visitas a sites, envios de formulários, participação em webinários) para rastrear o comportamento e os contatos em tempo real em diferentes canais, criando oportunidades para o envolvimento personalizado em tempo real. | **Alimentação em Tempo Real**: ao integrar os dados de atividade do [!DNL Eloqua], a Real-Time CDP pode disparar emails personalizados ou notificações para equipes de vendas quando um contato se envolver com conteúdo (como baixar um whitepaper ou clicar em um link de email), permitindo um acompanhamento oportuno e melhores oportunidades de conversão. |

{style="table-layout:auto"}

## Pré-requisitos {#prerequisites}

Leia as seções abaixo para obter a configuração de pré-requisitos que você deve concluir antes de poder conectar sua origem ao Experience Platform.

### Configurar aplicativo para autenticação

Siga as etapas abaixo para saber como configurar sua conta do [!DNL Eloqua] e conectar-se ao Experience Platform usando a autenticação básica.

Para começar, faça logon na instância do [!DNL Eloqua] como administrador (ou como um usuário que tem acesso para criar usuários, grupos de segurança e aplicativos).

![O Meu Painel Eloqua.](../../images/tutorials/create/eloqua/admin.png)

Navegue até **Configurações** > **Extensões da Plataforma** > **Desenvolvedor da App Cloud** > **Criar Aplicativo**. Forneça detalhes do aplicativo, incluindo nome, descrição, ícone e URL de retorno de chamada OAuth. Selecione **Salvar** ao concluir.

![O painel Desenvolvedor de Aplicativos e o botão Criar Aplicativo no painel Eloqua.](../../images/tutorials/create/eloqua/create-app.png)

| Propriedade | Descrição |
| --- | --- |
| Nome | O nome do seu aplicativo. |
| Descrição | Uma breve descrição do aplicativo. |
| Ícone | O URL do ícone. |
| URL de retorno de chamada OAuth | A URL à qual os usuários devem ser redirecionados após instalar o aplicativo e autenticar com [!DNL Eloqua]. |

![A janela de criação de aplicativos em Eloqua.](../../images/tutorials/create/eloqua/new-app.png)

Com seu aplicativo criado, navegue até [!DNL Authentication to Eloqua] e recupere a **ID do cliente** e o **segredo do cliente** do aplicativo recém-criado. Esses valores serão usados posteriormente ao se conectar ao Experience Platform.

![A ID do cliente e o segredo do cliente em Eloqua.](../../images/tutorials/create/eloqua/credentials.png)

Os grupos de segurança permitem que os administradores controlem quais níveis de acesso os usuários têm aos ativos, recursos, interfaces e assim por diante. Para criar um grupo de segurança, navegue até **Configurações** > **Usuários**. Em seguida, selecione a guia **Grupo** no painel esquerdo e selecione **Criar novo Grupo de Segurança**.

![O painel de gerenciamento de usuários em Eloqua.](../../images/tutorials/create/eloqua/user-management.png)

Use a janela **[!DNL Security Group Overview]** para fornecer um nome e um acrônimo para seu grupo de segurança. Depois de criada, navegue até [!DNL Action Permissions], adicione a permissão de API [!DNL Consume] na lista e selecione **Salvar**.

![A janela de visão geral do grupo de segurança em Eloqua.](../../images/tutorials/create/eloqua/security-group-overview.png)

![A janela de seleção da API de consumo](../../images/tutorials/create/eloqua/consume-api.png)

>[!NOTE]
>
>A API [!DNL Consume] é uma permissão necessária, mas você pode adicionar mais permissões dependendo do uso do aplicativo.

Para assimilar dados da campanha, navegue até a interface do **Editar Usuário** e adicione [!DNL Guided Campaigns] ao grupo de segurança selecionado.

![Grupo de segurança com campanhas guiadas adicionado.](../../images/tutorials/create/eloqua/add-guided-campaigns.png)

Opcionalmente, é possível criar um usuário adicional e adicioná-lo a um grupo de segurança. Para obter etapas detalhadas, leia a documentação do [!DNL Eloqua] sobre [criação de um usuário](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/UserManagement/Tasks/CreatingIndividualUsers.htm) e [atribuição de um usuário a um grupo de segurança](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityGroups/Tasks/AddingUsersToSecurityGroups.htm).

### Coletar credenciais necessárias

Você deve fornecer valores para as credenciais a seguir para conectar [!DNL Eloqua] ao Experience Platform.

| Credencial | Descrição |
| --- | --- |
| ID de cliente | O identificador exposto publicamente usado por [!DNL Eloqua] para identificar sua conta ao autorizar a Experience Platform. |
| Segredo do cliente | A chave confidencial conhecida apenas pelo aplicativo cliente e pelo servidor de autorização. Essa chave é necessária junto com a ID do cliente para autenticar sua conta. |
| Nome de usuário | O nome de usuário associado à sua conta [!DNL Eloqua]. Isso é usado para verificar e autorizar seu acesso. O nome de usuário segue o formato de `CompanyName\Username`. |
| Senha | A senha associada à sua conta [!DNL Eloqua]. Junto com seu nome de usuário, ele concede acesso ao seu ambiente Eloqua. |
| Endpoint base | O prefixo do URI da base de autenticação para [!DNL Eloqua]. O ponto de extremidade base não deve incluir `http://` ou `https://` durante a autenticação. |

## Guia de mapeamento de [!DNL Eloqua]

>[!NOTE]
>
>A seguir estão os campos delta usados internamente para carregamento de dados incrementais:
>
>- **Contatos:** `C_DateModified`
>- **Contas:** `M_DateModified`
>- **Atividade:** `CreatedAt`
>- **Objetos Personalizados:** `UpdatedAt`
>- **Campanha:** `updatedAt`

As tabelas a seguir fornecem mapeamentos detalhados entre os campos de origem [!DNL Eloqua] e seus campos de destino correspondentes do Experience Data Model (XDM) no Experience Platform. Cada linha descreve a lógica de transformação, se o campo é imutável e fornece observações adicionais para ajudar você a entender como os dados do [!DNL Eloqua] serão assimilados e estruturados no Experience Platform.

### Contas

| Coluna Source Eloqua | Caminho de destino XDM | Notas |
| --- | --- | --- |
| `"Eloqua"` | accountKey.sourceType | Esse campo é sempre definido como o valor fixo &quot;Eloqua&quot;. |
| `"${SOURCE_INSTANCE_ID}"` | accountKey.sourceInstanceID | O `SOURCE_INSTANCE_ID` será substituído automaticamente pelo conector. |
| `Id` | accountKey.sourceID | |
| `concat(Id, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | accountKey.sourceKey | O `SOURCE_INSTANCE_ID` será substituído automaticamente pelo conector. |
| `M_CompanyName` | accountName | |
| `M_Country` | accountPhysicalAddress.country | |
| `M_Address1` | accountPhysicalAddress.street1 | |
| `M_City` | accountPhysicalAddress.city | |
| `M_State_Prov` | accountPhysicalAddress.stateProvince | |
| `M_Zip_Postal` | accountPhysicalAddress.postalCode | |
| `M_BusPhone` | accountPhone.number | |
| `M_Fax1` | accountFax.number | |
| `M_Account_Engagement_Score` | accountScore | |
| `M_Account_Type1` | accountType | |
| `M_Wesbsite1` | accountOrganization.website | |
| `M_Employees1` | accountOrganization.numberOfEmployees | |
| `to_decimal(M_Annual_Revenue1)` | accountOrganization.annualRevenue.amount | |
| `M_DateModified` | extSourceSystemAudit.lastUpdatedDate | |
| `M_DateCreated` | extSourceSystemAudit.createdDate | |
| `M_Industry1` | accountOrganization.industry | |
| `iif(M_SFDCAccountID != null && M_SFDCAccountID != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", M_SFDCAccountID, "sourceKey", concat(M_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(M_MSCRMAccountID != null && M_MSCRMAccountID != "", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", M_MSCRMAccountID, "sourceKey", concat(M_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | extSourceSystemAudit.externalKey | O conector não pode detectar a ID da instância do CRM automaticamente. Você deve substituir manualmente o `${CRM_INSTANCE_ID}` pela ID real da instância do CRM, que é a ID da instância do Salesforce ou do Dynamics. Durante a assimilação, se `M_SFDCAccountID` estiver presente, o conector gerará a chave externa usando esse valor e anexará `\@CRM_INSTANCE_ID.Salesforce`. Se esse campo estiver vazio, o conector usará `M_MSCRMAccountID` e, em vez disso, anexará `\@CRM_INSTANCE_ID.Dynamics`. Se ambos os campos estiverem vazios, este campo será definido como nulo. |

{style="table-layout:auto"}

### Atividades

| Coluna Source Eloqua | Caminho de destino XDM | Notas |
| --- | --- | --- |
| `"Eloqua"` | personKey.sourceType | Esse campo é sempre definido como o valor fixo &quot;Eloqua&quot;. |
| `"${SOURCE_INSTANCE_ID}"` | personKey.sourceInstanceID | O `SOURCE_INSTANCE_ID` será substituído automaticamente pelo conector. |
| `ContactId` | personKey.sourceID |  |
| `concat(ContactId, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | personKey.sourceKey | O `SOURCE_INSTANCE_ID` será substituído automaticamente pelo conector. |
| `ExternalId` | _id |  |
| `iif(ActivityType!=null && ActivityType!="", iif(ActivityType=="EmailSend", "directMarketing.emailSent", iif(ActivityType=="EmailOpen", "directMarketing.emailOpened", iif(ActivityType=="EmailClickthrough", "directMarketing.emailClicked", iif(ActivityType=="Unsubscribe", "directMarketing.emailUnsubscribed", iif(ActivityType=="Bounceback", "directMarketing.emailBounced", iif(ActivityType=="FormSubmit", "web.formFilledOut", iif(ActivityType=="PageView", "web.webpagedetails.pageViews", ActivityType))))))), null)` | eventType | Com base no ActivityType, o valor eventType do Experience Platform correspondente será preenchido. Para ExternalActivities, não há eventType no Experience Platform. Você pode modificar esse mapeamento para manipular mais tipos. |
| `ActivityDate` | carimbo de data e hora | |
| `iif(AssetType == "Email", AssetName, null)` | directMarketing.mailingName | |
| `iif(AssetType == "Email", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | directMarketing.mailingKey | O `SOURCE_INSTANCE_ID` será substituído automaticamente pelo conector. |
| `iif(AssetType == "Email", EmailAddress, null)` | directMarketing.email | |
| `iif(ActivityType == "Bounceback", SmtpStatusCode, null)` | directMarketing.emailBouncedCode | |
| `iif(AssetType == "Email", SmtpMessage, null)` | directMarketing.emailBouncedDetails | |
| `iif(AssetType == "Email", EmailWebLink, null)` | directMarketing.linkURL | |
| `iif(ActivityType == "FormSubmit", AssetName, null)` | web.fillOutForm.webFormName | |
| `iif(ActivityType == "FormSubmit", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | web.fillOutForm.webFormKey | O `SOURCE_INSTANCE_ID` será substituído automaticamente pelo conector. |
| `iif(ActivityType == "PageView", AssetName, null)` | web.webPageDetails.name | |
| `iif(ActivityType == "PageView", to_object("sourceType", "Eloqua", "sourceInstanceID", "${SOURCE_INSTANCE_ID}","sourceID",${AssetId}, "sourceKey", concat(${AssetId},"\\@${SOURCE_INSTANCE_ID}.Eloqua")), null)` | web.webPageDetails.webPageKey | O `SOURCE_INSTANCE_ID` será substituído automaticamente pelo conector. |
| `iif(ActivityType == "PageView", Url, null)` | web.webPageDetails.URL | |

{style="table-layout:auto"}

### Campanhas

| Coluna Source Eloqua | Caminho de destino XDM | Notas |
| --- | --- | --- |
| `"Eloqua"` | campaignKey.sourceType | Esse campo é sempre definido como o valor fixo &quot;Eloqua&quot;. |
| `"${SOURCE_INSTANCE_ID}"` | campaignKey.sourceInstanceID | O `SOURCE_INSTANCE_ID` será substituído automaticamente pelo conector. |
| `id` | campaignKey.sourceID | |
| `concat(id, "\\@${SOURCE_INSTANCE_ID}.Eloqua")` | campaignKey.sourceKey | O `SOURCE_INSTANCE_ID` será substituído automaticamente pelo conector. |
| `name` | campaignName | |
| `endAt` | campaignEndDate | |
| `startAt` | campaignStartDate | |
| `actualCost` | actualCost.amount | |
| `budgetedCost` | budgetedCost.amount | |
| `description` | campaignDescription | |
| `currentStatus` | campaignStatus | |
| `campaignType` | campaignType | |
| `createdAt` | extSourceSystemAudit.createdDate | |
| `updatedAt` | extSourceSystemAudit.lastUpdatedDate | |

{style="table-layout:auto"}

### Contatos

| Coluna Source Eloqua | Caminho de destino XDM | Notas |
| --- | --- | --- |
| `"Eloqua"` | b2b.personKey.sourceType | Esse campo é sempre definido como o valor fixo &quot;Eloqua&quot;. |
| `"${SOURCE_INSTANCE_ID}"` | b2b.personKey.sourceInstanceID | O `SOURCE_INSTANCE_ID` será substituído automaticamente pelo conector. |
| `Id` | b2b.personKey.sourceID |  |
| `concat(Id, "\\@${SOURCE_INSTANCE_ID}.Eloqua"` | b2b.personKey.sourceKey | O `SOURCE_INSTANCE_ID` será substituído automaticamente pelo conector. |
| `C_Company` | b2b.companyName |  |
| `C_Website1` | b2b.companyWebsite |  |
| `C_Job_Title1` | extendedWorkDetails.jobTitle |  |
| `C_Fax` | faxPhone.number |  |
| `C_MobilePhone` | mobilePhone.number |  |
| `iif(C_SFDCLeadID != null && C_SFDCLeadID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCLeadID, "sourceKey", concat(C_SFDCLeadID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_SFDCContactID != null && C_SFDCContactID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCContactID, "sourceKey", concat(C_SFDCContactID, "\\@${CRM_INSTANCE_ID}.Salesforce")), null))` | personComponents.sourceExternalKey | Se a instância [!DNL Eloqua] estiver sincronizada com o Salesforce, mantenha esse mapeamento. Caso contrário, remova-o. O conector não tem uma maneira de determinar o CRM_INSTANCE_ID, portanto, você deve substituir ${CRM_INSTANCE_ID} pela ID de instância do Salesforce sincronizada. Esse mesmo mapeamento se aplica a personComponents e extSourceSystemAudit, portanto, mantenha ambos. |
| `iif(C_MSCRMLeadID != null && C_MSCRMLeadID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMLeadID, "sourceKey", concat(C_MSCRMLeadID, "\\@${CRM_INSTANCE_ID}.Dynamics")), iif(C_MSCRMContactID != null && C_MSCRMContactID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMContactID, "sourceKey", concat(C_MSCRMContactID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))"` | personComponents.sourceExternalKey | Se a instância [!DNL Eloqua] estiver sincronizada com o Dynamics, mantenha esse mapeamento. Caso contrário, remova-o. O conector não tem uma maneira de determinar o CRM_INSTANCE_ID, portanto, você deve substituir ${CRM_INSTANCE_ID} pela ID de instância sincronizada do Dynamics. Esse mesmo mapeamento se aplica a personComponents e extSourceSystemAudit, portanto, mantenha ambos. |
| `iif(C_SFDCLeadID != null && C_SFDCLeadID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCLeadID, "sourceKey", concat(C_SFDCLeadID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_SFDCContactID != null && C_SFDCContactID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCContactID, "sourceKey", concat(C_SFDCContactID, "\\@${CRM_INSTANCE_ID}.Salesforce")), null))"` | extSourceSystemAudit.externalKey | Se a instância [!DNL Eloqua] estiver sincronizada com o Salesforce, mantenha esse mapeamento. Caso contrário, remova-o. O conector não tem uma maneira de determinar o CRM_INSTANCE_ID, portanto, você deve substituir ${CRM_INSTANCE_ID} pela ID de instância do Salesforce sincronizada. Esse mesmo mapeamento se aplica a personComponents e extSourceSystemAudit, portanto, mantenha ambos. |
| `iif(C_MSCRMLeadID != null && C_MSCRMLeadID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMLeadID, "sourceKey", concat(C_MSCRMLeadID, "\\@${CRM_INSTANCE_ID}.Dynamics")), iif(C_MSCRMContactID != null && C_MSCRMContactID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMContactID, "sourceKey", concat(C_MSCRMContactID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | extSourceSystemAudit.externalKey | Se a instância [!DNL Eloqua] estiver sincronizada com o Dynamics, mantenha esse mapeamento. Caso contrário, remova-o. O conector não tem uma maneira de determinar o CRM_INSTANCE_ID, portanto, você deve substituir ${CRM_INSTANCE_ID} pela ID de instância sincronizada do Dynamics. Esse mesmo mapeamento se aplica a personComponents e extSourceSystemAudit, portanto, mantenha ambos. |
| `C_DateCreated` | extSourceSystemAudit.createdDate |  |
| `C_DateModified` | extSourceSystemAudit.lastUpdatedDate |  |
| `iif(C_SFDCAccountID != null && C_SFDCAccountID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCAccountID, "sourceKey", concat(C_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_MSCRMAccountID != null && C_MSCRMAccountID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMAccountID, "sourceKey", concat(C_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | b2b.accountKey | O conector não tem como determinar a CRM_INSTANCE_ID, portanto, você deve substituir ${CRM_INSTANCE_ID} pela ID de instância do CRM sincronizada, seja a ID de instância do Salesforce ou a ID de instância do Dynamics. Esse mesmo mapeamento se aplica a b2b.accountKey e personComponents.sourceAccountKey, portanto, mantenha ambos. |
| `iif(C_SFDCAccountID != null && C_SFDCAccountID != "\\", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_SFDCAccountID, "sourceKey", concat(C_SFDCAccountID, "\\@${CRM_INSTANCE_ID}.Salesforce")), iif(C_MSCRMAccountID != null && C_MSCRMAccountID != "\\", to_object("sourceType", "Dynamics", "sourceInstanceID", "${CRM_INSTANCE_ID}", "sourceID", C_MSCRMAccountID, "sourceKey", concat(C_MSCRMAccountID, "\\@${CRM_INSTANCE_ID}.Dynamics")), null))` | personComponents.sourceAccountKey | O conector não tem como determinar a CRM_INSTANCE_ID, portanto, você deve substituir ${CRM_INSTANCE_ID} pela ID de instância do CRM sincronizada, seja a ID de instância do Salesforce ou a ID de instância do Dynamics. Esse mesmo mapeamento se aplica a b2b.accountKey e personComponents.sourceAccountKey, portanto, mantenha ambos. |
| `C_Lead_Source___Original1` | b2b.personSource | |
| `C_Lead_Source___Original1` | personComponents.personSource | |
| `C_Lead_Status1` | b2b.personStatus | |
| `C_Lead_Status1` | personComponents.personStatus | |
| `C_FirstName` | person.name.firstName | |
| `C_LastName` | person.name.lastName | |
| `C_Middle_Name1` | person.name.middleName | |
| `C_Salutation` | person.name.courtesyTitle | |
| `C_City` | workAddress.city | |
| `C_Country` | workAddress.country | |
| `C_Zip_Postal` | workAddress.postalCode | |
| `C_State_Prov` | workAddress.state | |

{style="table-layout:auto"}

### Referência de mapeamento do tipo de atividade

| Eloqua ActivityType | eventType XDM |
| -------------------- | --------------- |
| `EmailSend` | directMarketing.emailSent |
| `EmailOpen` | directMarketing.emailOpened |
| `EmailClickthrough` | directMarketing.emailClicked |
| `Unsubscribe` | directMarketing.emailUnsubscribed |
| `Bounceback` | directMarketing.emailBounced |
| `FormSubmit` | web.formFilledOut |
| `PageView` | web.webpagedetails.pageViews |
| `Other` | passar como está |

{style="table-layout:auto"}

### Espaços reservados de variáveis

Os modelos de mapeamento usam os seguintes espaços reservados para variáveis, que são substituídos quando um fluxo de dados é executado:

| Espaço reservado | Descrição | Uso |
| ----------- | ----------- | ----- |
| `${SOURCE_INSTANCE_ID}` | ID exclusiva da instância de origem do Eloqua | Usado em chaves de origem |
| `${CRM_INSTANCE_ID}` | Identificador exclusivo do sistema CRM (Salesforce/Dynamics) | Usado em chaves externas |

## Conectar [!DNL Eloqua] ao Experience Platform

Continue a configurar sua conexão de origem do [!DNL Eloqua] no Experience Platform. Para obter um guia passo a passo sobre como configurar a conexão através da interface do usuário, consulte o [tutorial aqui](../../tutorials/ui/create/marketing-automation/eloqua.md). Leia este tutorial para saber mais sobre como conectar sua conta do [!DNL Eloqua], selecionar dados, mapear campos, agendar assimilações e monitorar seus fluxos de dados.

