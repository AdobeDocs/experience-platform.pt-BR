---
keywords: destinos de crm;CRM;crm destinos;destino de crm do Microsoft Dynamics 365;Microsoft Dynamics 365
title: Conexão com o Microsoft Dynamics 365
description: O destino do Microsoft Dynamics 365 permite exportar os dados da conta e ativá-los no Microsoft Dynamics 365 para atender às suas necessidades comerciais.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 49bb5c95-f4b7-42e1-9aae-45143bbb1d73
source-git-commit: 416f4ff28ae5ca7ee3235f020ce012352d6002c7
workflow-type: tm+mt
source-wordcount: '1927'
ht-degree: 0%

---

# [!DNL Microsoft Dynamics 365] conexão

## Visão geral {#overview}

[[!DNL Microsoft Dynamics 365]](https://dynamics.microsoft.com/en-us/) O é uma plataforma de aplicativos de negócios baseada em nuvem que combina ERP (Enterprise Resource Planning, planejamento de recursos corporativos) e CRM (Customer Relationship Management, gerenciamento de relacionamento com o cliente), além de aplicativos de produtividade e ferramentas de IA, para oferecer operações completas, mais perfeitas e controladas, melhor potencial de crescimento e custos reduzidos.

Este [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) utiliza o [[!DNL Contact Entity Reference API]](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1), que permite atualizar as identidades em um público-alvo para [!DNL Dynamics 365].

[!DNL Dynamics 365] O usa o OAuth 2 com concessão de autorização como mecanismo de autenticação para se comunicar com o [!DNL Contact Entity Reference API]. Instruções para autenticar em seu [!DNL Dynamics 365] exemplo, são apresentados mais abaixo, no [Autenticar para destino](#authenticate) seção.

## Casos de uso {#use-cases}

Como profissional de marketing, você pode fornecer experiências personalizadas aos seus usuários com base em atributos de seus perfis do Adobe Experience Platform. Você pode criar públicos-alvo com base nos dados offline e enviá-los para [!DNL Dynamics 365], para ser exibido nos feeds dos usuários assim que os públicos-alvo e os perfis forem atualizados no Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

### Pré-requisitos do Experience Platform {#prerequisites-in-experience-platform}

Antes de ativar os dados para o [!DNL Dynamics 365] destino, você deve ter um [schema](/help/xdm/schema/composition.md), um [conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), e [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) criado em [!DNL Experience Platform].

Consulte a documentação do Adobe para [Grupo de campos de esquema Detalhes da associação do segmento](/help/xdm/field-groups/profile/segmentation.md) se precisar de orientação sobre os status do público-alvo.

### [!DNL Microsoft Dynamics 365] pré-requisitos {#prerequisites-destination}

Observe os seguintes pré-requisitos em [!DNL Dynamics 365], para exportar dados da Platform para o seu [!DNL Dynamics 365] conta:

#### Você precisa ter um [!DNL Microsoft Dynamics 365] account {#prerequisites-account}

Vá para a [!DNL Dynamics 365] [avaliação](https://dynamics.microsoft.com/en-us/dynamics-365-free-trial/) para registrar e criar uma conta, se ainda não tiver uma.

#### Criar campo dentro de [!DNL Dynamics 365] {#prerequisites-custom-field}

Criar o campo personalizado do tipo `Simple` com tipo de dados de campo como `Single Line of Text` qual Experience Platform usará para atualizar o status do público-alvo no [!DNL Dynamics 365].
Consulte a [!DNL Dynamics 365] documentação para [criar um campo (atributo)](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) se precisar de orientação adicional.

Um exemplo de configuração em [!DNL Dynamics 365] é mostrado abaixo:
![Captura de tela da interface do usuário do Dynamics 365 mostrando os campos personalizados.](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-fields.png)

#### Registrar um aplicativo e um usuário de aplicativo no Azure Ative Diretory {#prerequisites-app-user}

Para habilitar [!DNL Dynamics 365] para acessar os recursos, é necessário fazer logon com a [!DNL Azure Account] para [[!DNL Azure Active Directory]](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#register-an-application-with-azure-ad-and-create-a-service-principal) e crie o seguinte:
* Um [!DNL Azure Active Directory] aplicativo
* Uma Entidade de serviço
* Um segredo de aplicativo

Você também precisará [criar um usuário do aplicativo](https://docs.microsoft.com/en-us/power-platform/admin/manage-application-users#create-an-application-user) in [!DNL Azure Active Directory] e associá-lo ao aplicativo recém-criado.

#### Coletar [!DNL Dynamics 365] credenciais {#gather-credentials}

Anote os itens abaixo antes de autenticar na [!DNL Dynamics 365] Destino do CRM:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| `Client ID` | A variável [!DNL Dynamics 365] ID do cliente para o seu [!DNL Azure Active Directory] aplicação. Consulte a [[!DNL Dynamics 365] documentação](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) para obter orientação. | `ababbaba-abab-baba-acac-acacacacacac` |
| `Client Secret` | A variável [!DNL Dynamics 365] Segredo do cliente para o seu [!DNL Azure Active Directory] aplicação. Você usaria a opção #2 dentro do [[!DNL Dynamics 365] documentação](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#authentication-two-options). | `abcde~abcdefghijklmnopqrstuvwxyz12345678` para obter orientação. |
| `Tenant ID` | A variável [!DNL Dynamics 365] ID de locatário para o seu [!DNL Azure Active Directory] aplicação. Consulte a [[!DNL Dynamics 365] documentação](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) para obter orientação. | `1234567-aaaa-12ab-ba21-1234567890` |
| `Region` | A região do Microsoft associada ao URL do ambiente.<br> Consulte a [[!DNL Dynamics 365] documentação](https://learn.microsoft.com/en-us/power-platform/admin/new-datacenter-regions) para obter orientação. | Se o seu domínio for como abaixo, você precisará fornecer o valor destacado para o campo CRM no seletor suspenso ao autenticar para o [destino](#authenticate).<br> *org57771b33`crm`.dynamics.com*<br>  Por exemplo: se sua empresa for provisionada na região da América do Norte (NAM), seu URL será `crm.dynamics.com` e você precisa selecionar `crm`. Se sua empresa for provisionada na região do Canadá (CAN), o URL será `crm3.dynamics.com` e você precisa selecionar `crm3`. |
| `Environment URL` | Consulte a [[!DNL Dynamics 365] documentação](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/org-service/discover-url-organization-organization-service?view=op-9-1) para obter orientação. | Se o seu [!DNL Dynamics 365] for conforme abaixo, você precisará do valor realçado.<br> *`org57771b33`.crm.dynamics.com* |

{style="table-layout:auto"}

## Medidas de proteção {#guardrails}

A variável [Limites de solicitações e alocações](https://docs.microsoft.com/en-us/power-platform/admin/api-request-limits-allocations) detalhes da página o [!DNL Dynamics 365] Limites de API associados ao seu [!DNL Dynamics 365] licença. Você precisa garantir que seus dados e carga estejam dentro dessas restrições.

## Identidades suportadas {#supported-identities}

[!DNL Dynamics 365] O oferece suporte à atualização de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade de destino | Exemplo | Descrição | Considerações |
|---|---|---|---|
| `contactId` | 7eb682f1-ca75-e511-80d4-00155d2a68d1 | Identificador exclusivo de um contato. | **Obrigatório**. Consulte a [[!DNL Dynamics 365] documentação](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1) para obter mais detalhes. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | <ul><li>Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados *(por exemplo: endereço de email, número de telefone, sobrenome)*, de acordo com o mapeamento de campo.</li><li> Cada status de público-alvo no [!DNL Dynamics 365] é atualizado com o status de público-alvo correspondente na Platform, com base no **[!UICONTROL ID do mapeamento]** valor fornecido durante o [agendamento de público](#schedule-segment-export-example) etapa.</li></ul> |
| Frequência de exportação | **[!UICONTROL Streaming]** | <ul><li>Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

Dentro de **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** pesquisar [!DNL Dynamics 365]. Como alternativa, você pode localizá-lo na **[!UICONTROL CRM]** categoria.

### Autenticar para destino {#authenticate}

Para autenticar no destino, selecione **[!UICONTROL Conectar ao destino]**.
![Captura de tela da interface do usuário da plataforma mostrando como autenticar.](../../assets/catalog/crm/microsoft-dynamics-365/authenticate-destination.png)

Preencha os campos obrigatórios abaixo. Consulte a [Coletar credenciais do Dynamics 365](#gather-credentials) para obter orientação.
* **[!UICONTROL ID do cliente]**: A variável [!DNL Dynamics 365] ID do cliente para o seu [!DNL Azure Active Directory] aplicação.
* **[!UICONTROL ID do inquilino]**: A variável [!DNL Dynamics 365] ID de locatário para o seu [!DNL Azure Active Directory] aplicação.
* **[!UICONTROL Segredo do cliente]**: A variável [!DNL Dynamics 365] Segredo do cliente para o seu [!DNL Azure Active Directory] aplicação.
* **[!UICONTROL Região]**: Seu [[!DNL Dynamics 365]](https://learn.microsoft.com/en-us/power-platform/admin/new-datacenter-regions) Região. Por exemplo: se sua empresa for provisionada na região da América do Norte (NAM), seu URL será `crm.dynamics.com` e você precisa selecionar `crm`. Se sua empresa for provisionada na região do Canadá (CAN), o URL será `crm3.dynamics.com` e você precisa selecionar `crm3`.
* **[!UICONTROL URL do ambiente]**: Seu [!DNL Dynamics 365] URL do ambiente.

Se os detalhes fornecidos forem válidos, a interface exibirá uma **[!UICONTROL Conectado]** com uma marca de seleção verde. Você pode prosseguir para a próxima etapa.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.
![Captura de tela da interface do usuário da plataforma mostrando os detalhes do destino.](../../assets/catalog/crm/microsoft-dynamics-365/destination-details.png)

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos para este destino {#activate}

>[!IMPORTANT]
>
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e públicos para destinos de exportação de público de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Considerações e exemplo de mapeamento {#mapping-considerations-example}

Para enviar corretamente os dados do público-alvo do Adobe Experience Platform para a [!DNL Dynamics 365] destino, é necessário passar pela etapa de mapeamento de campos. O mapeamento consiste em criar um link entre os campos do esquema do Experience Data Model (XDM) na sua conta da Platform e seus equivalentes correspondentes no destino. Para mapear corretamente os campos XDM para o [!DNL Dynamics 365] campos de destino, siga estas etapas:

1. No **[!UICONTROL Mapeamento]** etapa, selecione **[!UICONTROL Adicionar novo mapeamento]**. Você verá uma nova linha de mapeamento na tela.
   ![Exemplo de captura de tela da interface do Platform para Adicionar novo mapeamento.](../../assets/catalog/crm/microsoft-dynamics-365/add-new-mapping.png)

1. No **[!UICONTROL Selecionar campo de origem]** escolha a **[!UICONTROL Selecionar namespace de identidade]** categoria e selecione `contactId`.
   ![Exemplo de captura de tela da interface do Platform para mapeamento de origem.](../../assets/catalog/crm/microsoft-dynamics-365/source-mapping.png)

1. No **[!UICONTROL Selecionar campo de destino]** selecione o tipo de campo de destino para o qual deseja mapear seu campo de origem.
   * **[!UICONTROL Selecionar namespace de identidade]**: selecione esta opção para mapear o campo de origem para um namespace de identidade da lista.
     ![Captura de tela da interface do usuário da plataforma mostrando o Target mapping para contactId.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-contactid.png)

   * Adicione o mapeamento a seguir entre o esquema de perfil XDM e o [!DNL Dynamics 365] instância: |Esquema do perfil XDM|[!DNL Dynamics 365] Instância| Obrigatório| |—|—|—| |`contactId`|`contactId`| Sim |

   * **[!UICONTROL Selecionar atributos personalizados]**: selecione esta opção para mapear o campo de origem para um atributo personalizado definido na variável **[!UICONTROL Nome do atributo]** campo. Consulte [[!DNL Dynamics 365] documentação](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1#entity-properties) para obter uma lista abrangente dos atributos suportados.
     ![Captura de tela da interface do usuário da plataforma mostrando o Target mapping para LastName.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-lastname.png)

     >[!IMPORTANT]
     >
     >Se você tiver um campo de origem de data ou carimbo de data e hora mapeado para um [!DNL Dynamics 365] [data ou carimbo de data e hora](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/reference/timestampdatemapping?view=dataverse-latest) campo de destino, certifique-se de que o valor mapeado que está sendo não esteja vazio. Se o valor transmitido estiver vazio, você encontrará um *`Bad request reported while pushing events to the destination. Please contact the administrator and try again.`* mensagem de erro e os dados não serão atualizados. Este é um [!DNL Dynamics 365] limitação.

   * Por exemplo, dependendo dos valores que você deseja atualizar, adicione o seguinte mapeamento entre o esquema de perfil XDM e o [!DNL Dynamics 365] instância: |Esquema do perfil XDM|[!DNL Dynamics 365] Instância| |—|—| |`person.name.firstName`|`FirstName`| |`person.name.lastName`|`LastName`| |`personalEmail.address`|`Email`|

   * Um exemplo usando esses mapeamentos é mostrado abaixo:
     ![Exemplo de captura de tela da interface do Platform mostrando os mapeamentos do Target.](../../assets/catalog/crm/microsoft-dynamics-365/mappings.png)

### Agendar exportação de público e exemplo {#schedule-segment-export-example}

No [[!UICONTROL Agendar exportação de público]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) do fluxo de trabalho de ativação, você deve mapear manualmente os públicos-alvo da Platform para o atributo de campo personalizado em [!DNL Dynamics 365].

Para fazer isso, selecione cada segmento e insira o atributo de campo personalizado correspondente em [!DNL Dynamics 365] no **[!UICONTROL ID do mapeamento]** campo.

>[!IMPORTANT]
>
>O valor usado para a variável **[!UICONTROL ID do mapeamento]** deve corresponder exatamente ao nome do atributo de campo personalizado criado em [!DNL Dynamics 365]. Consulte [[!DNL Dynamics 365] documentação](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) se precisar de orientação sobre como encontrar os atributos de campo personalizado.

Um exemplo é mostrado abaixo:
![Exemplo de captura de tela da interface do Platform mostrando Programar exportação de público-alvo.](../../assets/catalog/crm/microsoft-dynamics-365/schedule-segment-export.png)

## Validar exportação de dados {#exported-data}

Para validar se você configurou o destino corretamente, siga as etapas abaixo:

1. Selecionar **[!UICONTROL Destinos]** > **[!UICONTROL Procurar]** para navegar até a lista de destinos.
   ![Captura de tela da interface do usuário da plataforma mostrando os destinos de navegação.](../../assets/catalog/crm/microsoft-dynamics-365/browse-destinations.png)

1. Selecionar o destino e validar se o status é **[!UICONTROL habilitado]**.
   ![Captura de tela da interface do usuário da plataforma mostrando a execução do fluxo de dados de destinos.](../../assets/catalog/crm/microsoft-dynamics-365/destination-dataflow-run.png)

1. Alterne para a **[!DNL Activation data]** e selecione um nome de público-alvo.
   ![Exemplo de captura de tela da interface do Platform mostrando Dados de ativação de destinos.](../../assets/catalog/crm/microsoft-dynamics-365/destinations-activation-data.png)

1. Monitore o resumo do público-alvo e verifique se a contagem de perfis corresponde à contagem criada no segmento.
   ![Exemplo de captura de tela da interface do Platform mostrando o segmento.](../../assets/catalog/crm/microsoft-dynamics-365/segment.png)

1. Faça logon no [!DNL Dynamics 365] site e, em seguida, navegue até o [!DNL Customers] > [!DNL Contacts] e verifique se os perfis do público-alvo foram adicionados. Você pode ver que cada status de público-alvo em [!DNL Dynamics 365] foi atualizado com o status de público-alvo correspondente na Platform, com base na **[!UICONTROL ID do mapeamento]** valor fornecido durante o [agendamento de público](#schedule-segment-export-example) etapa.
   ![Captura de tela da interface do usuário do Dynamics 365 mostrando a página Contatos com status de público atualizado.](../../assets/catalog/crm/microsoft-dynamics-365/contacts.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte o [Visão geral da governança de dados](/help/data-governance/home.md).

## Erros e solução de problemas {#errors-and-troubleshooting}

### Erros desconhecidos encontrados ao enviar eventos para o destino {#unknown-errors}

Ao verificar uma execução de fluxo de dados, se você obter a seguinte mensagem de erro: `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![Captura de tela da interface do usuário do Platform mostrando o erro de solicitação incorreta.](../../assets/catalog/crm/microsoft-dynamics-365/error.png)

Para corrigir esse erro, verifique se **[!UICONTROL ID do mapeamento]** você forneceu em [!DNL Dynamics 365] para seu público-alvo da Platform é válido e existe em [!DNL Dynamics 365].

## Recursos adicionais {#additional-resources}

Informações adicionais úteis do [[!DNL Dynamics 365] documentação](https://docs.microsoft.com/en-us/dynamics365/) está abaixo:
* [Método IOrganizationService.Update(Entity)](https://docs.microsoft.com/en-us/dotnet/api/microsoft.xrm.sdk.iorganizationservice.update?view=dataverse-sdk-latest)
* [Atualizar e excluir linhas de tabela usando a API da Web](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/update-delete-entities-using-web-api#basic-update)
