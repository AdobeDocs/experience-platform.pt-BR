---
keywords: crm; CRM; destinos crm; Microsoft Dynamics 365; destino do Microsoft Dynamics 365 crm
title: Conexão Microsoft Dynamics 365
description: O destino Microsoft Dynamics 365 permite exportar seus dados de conta e ativá-los no Microsoft Dynamics 365 para suas necessidades comerciais.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 49bb5c95-f4b7-42e1-9aae-45143bbb1d73
source-git-commit: 83778bc5d643f69e0393c0a7767fef8a4e8f66e9
workflow-type: tm+mt
source-wordcount: '1790'
ht-degree: 1%

---

# [!DNL Microsoft Dynamics 365] conexão

## Visão geral {#overview}

[[!DNL Microsoft Dynamics 365]](https://dynamics.microsoft.com/en-us/) O é uma plataforma de aplicativos de negócios baseada em nuvem que combina o Enterprise Resource Planning (ERP) e o Customer Relationship Management (CRM), além de aplicativos de produtividade e ferramentas de IA, para oferecer operações completas e mais controladas, melhor potencial de crescimento e custos reduzidos.

Essa [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) utiliza o [[!DNL Contact Entity Reference API]](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1), que permite atualizar identidades em um segmento para [!DNL Dynamics 365].

[!DNL Dynamics 365] O usa o OAuth 2 com a concessão de autorização como mecanismo de autenticação para se comunicar com o [!DNL Contact Entity Reference API]. Instruções para autenticação em seu [!DNL Dynamics 365] são mais abaixo, na variável [Autenticar para destino](#authenticate) seção.

## Casos de uso {#use-cases}

Como profissional de marketing, você pode fornecer experiências personalizadas para seus usuários, com base em atributos de seus perfis do Adobe Experience Platform. Você pode criar segmentos a partir de seus dados offline e enviar esses segmentos para [!DNL Dynamics 365], para exibir nos feeds dos usuários assim que os segmentos e os perfis forem atualizados no Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

### Pré-requisitos do Experience Platform {#prerequisites-in-experience-platform}

Antes de ativar os dados para o [!DNL Dynamics 365] destino, você deve ter um [schema](/help/xdm/schema/composition.md), a [conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)e [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) criado em [!DNL Experience Platform].

Consulte a documentação do Adobe para obter [Grupo de campos Detalhes da associação ao segmento](/help/xdm/field-groups/profile/segmentation.md) se você precisar de orientação sobre os status do segmento.

### [!DNL Microsoft Dynamics 365] pré-requisitos {#prerequisites-destination}

Observe os seguintes pré-requisitos em [!DNL Dynamics 365]para exportar dados da Platform para seu [!DNL Dynamics 365] conta:

#### Você precisa ter um [!DNL Microsoft Dynamics 365] account {#prerequisites-account}

Vá para o [!DNL Dynamics 365] [avaliação](https://dynamics.microsoft.com/en-us/dynamics-365-free-trial/) para registrar e criar uma conta, se você ainda não tiver uma.

#### Criar campo dentro de [!DNL Dynamics 365] {#prerequisites-custom-field}

Criar o campo personalizado do tipo `Simple` com tipo de dados de campo como `Single Line of Text` qual Experience Platform usará para atualizar o status do segmento em [!DNL Dynamics 365].
Consulte a [!DNL Dynamics 365] documentação para [criar um campo (atributo)](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) se precisar de orientação adicional.

Uma configuração de exemplo em [!DNL Dynamics 365] é mostrado abaixo:
![Captura de tela do Dynamics 365 UI mostrando os campos personalizados.](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-fields.png)

#### Registrar um aplicativo e um usuário de aplicativo no Azure Ative Diretory {#prerequisites-app-user}

Para ativar [!DNL Dynamics 365] para acessar recursos, você precisará fazer logon com sua [!DNL Azure Account] para [[!DNL Azure Active Directory]](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#register-an-application-with-azure-ad-and-create-a-service-principal) e crie o seguinte:
* Um [!DNL Azure Active Directory] aplicativo
* Um Principal de Serviço
* Um segredo de aplicativo

Você também precisará [criar um usuário do aplicativo](https://docs.microsoft.com/en-us/power-platform/admin/manage-application-users#create-an-application-user) em [!DNL Azure Active Directory] e associá-lo ao aplicativo recém-criado.

#### Colete [!DNL Dynamics 365] credenciais {#gather-credentials}

Anote os itens abaixo antes de autenticar para o [!DNL Dynamics 365] Destino do CRM:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| `Client ID` | O [!DNL Dynamics 365] ID do cliente para seu [!DNL Azure Active Directory] aplicativo. Consulte a [[!DNL Dynamics 365] documentação](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) para orientação. | `ababbaba-abab-baba-acac-acacacacacac` |
| `Client Secret` | O [!DNL Dynamics 365] Segredo do cliente para seu [!DNL Azure Active Directory] aplicativo. Você usaria a opção 2 na variável [[!DNL Dynamics 365] documentação](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#authentication-two-options). | `abcde~abcdefghijklmnopqrstuvwxyz12345678` para orientação. |
| `Tenant ID` | O [!DNL Dynamics 365] ID do locatário para sua [!DNL Azure Active Directory] aplicativo. Consulte a [[!DNL Dynamics 365] documentação](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) para orientação. | `1234567-aaaa-12ab-ba21-1234567890` |
| `Environment URL` | Consulte a [[!DNL Dynamics 365] documentação](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/org-service/discover-url-organization-organization-service?view=op-9-1) para orientação. | Se o seu [!DNL Dynamics 365] for o domínio , você precisará do valor destacado.<br> *`org57771b33`.crm.dynamics.com* |

## Medidas de proteção {#guardrails}

O [Limites de solicitações e alocações](https://docs.microsoft.com/en-us/power-platform/admin/api-request-limits-allocations) detalha a página [!DNL Dynamics 365] Limites de API associados a [!DNL Dynamics 365] licença. Você precisa garantir que seus dados e carga estejam dentro dessas restrições.

## Identidades suportadas {#supported-identities}

[!DNL Dynamics 365] O suporta a atualização de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Exemplo | Descrição | Considerações |
|---|---|---|---|
| `contactId` | 7eb682f1-ca75-e511-80d4-00155d2a68d1 | Identificador exclusivo para um contato. | **Obrigatório**. Consulte a [[!DNL Dynamics 365] documentação](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1) para obter mais detalhes. |

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | <ul><li>Você está exportando todos os membros de um segmento, junto com os campos de esquema desejados *(por exemplo: endereço de email, número de telefone, sobrenome)*, de acordo com o mapeamento de campo.</li><li> Cada status de segmento em [!DNL Dynamics 365] é atualizado com o status de segmento correspondente da Platform, com base no **[!UICONTROL ID de mapeamento]** valor fornecido durante a [agendamento de segmento](#schedule-segment-export-example) etapa.</li></ul> |
| Frequência de exportação | **[!UICONTROL Streaming]** | <ul><li>Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow para configurar destino , preencha os campos listados nas duas seções abaixo.

Within **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** pesquisar por [!DNL Dynamics 365]. Como alternativa, você pode localizá-lo sob a variável **[!UICONTROL CRM]** categoria .

### Autenticar para destino {#authenticate}

Para autenticar para o destino, selecione **[!UICONTROL Ligar ao destino]**.
![Captura de tela da interface do usuário da plataforma que mostra como autenticar.](../../assets/catalog/crm/microsoft-dynamics-365/authenticate-destination.png)

Preencha os campos obrigatórios abaixo. Consulte a [Obter credenciais do Dynamics 365](#gather-credentials) para quaisquer orientações.
* **[!UICONTROL ID do cliente]**: O [!DNL Dynamics 365] ID do cliente para seu [!DNL Azure Active Directory] aplicativo.
* **[!UICONTROL ID do locatário]**: O [!DNL Dynamics 365] ID do locatário para sua [!DNL Azure Active Directory] aplicativo.
* **[!UICONTROL Segredo do cliente]**: O [!DNL Dynamics 365] Segredo do cliente para seu [!DNL Azure Active Directory] aplicativo.
* **[!UICONTROL URL do ambiente]**: Seu [!DNL Dynamics 365] URL do ambiente.

Se os detalhes fornecidos forem válidos, a interface do usuário exibirá uma **[!UICONTROL Conectado]** status com uma marca de seleção verde. Você pode prosseguir para a próxima etapa.

### Preencha os detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.
![Captura de tela da interface do usuário da plataforma que mostra os detalhes do destino.](../../assets/catalog/crm/microsoft-dynamics-365/destination-details.png)

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
>
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmentos de fluxo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Considerações e exemplo de mapeamento {#mapping-considerations-example}

Para enviar corretamente os dados de público-alvo do Adobe Experience Platform para a [!DNL Dynamics 365] , é necessário percorrer a etapa de mapeamento de campo . O mapeamento consiste em criar um link entre os campos do esquema do Modelo de dados de experiência (XDM) na conta da plataforma e os equivalentes correspondentes do destino. Para mapear corretamente os campos XDM para a variável [!DNL Dynamics 365] campos de destino, siga estas etapas:

1. No **[!UICONTROL Mapeamento]** etapa , selecione **[!UICONTROL Adicionar novo mapeamento]**. Você verá uma nova linha de mapeamento na tela.
   ![Exemplo de captura de tela da interface do usuário da plataforma para Adicionar novo mapeamento.](../../assets/catalog/crm/microsoft-dynamics-365/add-new-mapping.png)

1. No **[!UICONTROL Selecionar campo de origem]** escolha a **[!UICONTROL Selecionar namespace de identidade]** categoria e selecione `contactId`.
   ![Exemplo de captura de tela da interface do usuário da plataforma para o mapeamento da fonte.](../../assets/catalog/crm/microsoft-dynamics-365/source-mapping.png)

1. No **[!UICONTROL Selecionar campo de destino]** selecione o tipo de campo de destino para o qual deseja mapear o campo de origem.
   * **[!UICONTROL Selecionar namespace de identidade]**: selecione essa opção para mapear o campo de origem para um namespace de identidade da lista.
      ![Captura de tela da interface do usuário da plataforma que mostra o mapeamento do Target para contactId.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-contactid.png)

   * Adicione o seguinte mapeamento entre o esquema de perfil XDM e o [!DNL Dynamics 365] instância: |Esquema de Perfil XDM|[!DNL Dynamics 365] Instância| Obrigatória| |—|—| |`contactId`|`contactId`| Sim |

   * **[!UICONTROL Selecionar atributos personalizados]**: selecione essa opção para mapear o campo de origem para um atributo personalizado definido na variável **[!UICONTROL Nome do atributo]** campo. Consulte [[!DNL Dynamics 365] documentação](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1#entity-properties) para obter uma lista abrangente dos atributos suportados.
      ![Captura de tela da interface do usuário da plataforma que mostra o mapeamento do Target para LastName.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-lastname.png)

      >[!IMPORTANT]
      >
      >Se você tiver um campo de origem de data ou carimbo de data e hora mapeado para um [!DNL Dynamics 365] [data ou carimbo de data e hora](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/reference/timestampdatemapping?view=dataverse-latest) no campo de destino, verifique se o valor mapeado que está sendo não está vazio. Se o valor passado estiver vazio, você encontrará um *`Bad request reported while pushing events to the destination. Please contact the administrator and try again.`* e os dados não serão atualizados. Isso é uma [!DNL Dynamics 365] limitação.

   * Por exemplo, dependendo dos valores que deseja atualizar, adicione o seguinte mapeamento entre o esquema de perfil XDM e o [!DNL Dynamics 365] instância: |Esquema de Perfil XDM|[!DNL Dynamics 365] Instância| |—|—| |`person.name.firstName`|`FirstName`| |`person.name.lastName`|`LastName`| |`personalEmail.address`|`Email`|

   * Um exemplo de uso desses mapeamentos é mostrado abaixo:
      ![Exemplo de captura de tela da interface do usuário da plataforma que mostra os mapeamentos do Target.](../../assets/catalog/crm/microsoft-dynamics-365/mappings.png)

### Programar exportação de segmento e exemplo {#schedule-segment-export-example}

No [[!UICONTROL Agendar exportação de segmentos]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) etapa do fluxo de trabalho de ativação, você deve mapear manualmente os segmentos da Platform para o atributo de campo personalizado em [!DNL Dynamics 365].

Para fazer isso, selecione cada segmento e insira o atributo de campo personalizado correspondente de [!DNL Dynamics 365] no **[!UICONTROL ID de mapeamento]** campo.

>[!IMPORTANT]
>
>O valor usado para a variável **[!UICONTROL ID de mapeamento]** deve corresponder exatamente ao nome do atributo de campo personalizado criado em [!DNL Dynamics 365]. Consulte [[!DNL Dynamics 365] documentação](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) se precisar de orientação para encontrar atributos de campo personalizados.

Um exemplo é mostrado abaixo:
![Exemplo de captura de tela da interface do usuário da plataforma que mostra a exportação do segmento de Programação.](../../assets/catalog/crm/microsoft-dynamics-365/schedule-segment-export.png)

## Validar exportação de dados {#exported-data}

Para validar se você configurou o destino corretamente, siga as etapas abaixo:

1. Selecionar **[!UICONTROL Destinos]** > **[!UICONTROL Procurar]** para navegar até a lista de destinos.
   ![Captura de tela da interface do usuário da plataforma que mostra os Destinos de navegação.](../../assets/catalog/crm/microsoft-dynamics-365/browse-destinations.png)

1. Selecione o destino e valide se o status é **[!UICONTROL ativado]**.
   ![Captura de tela da interface do usuário da plataforma que mostra a Execução do fluxo de dados de destinos.](../../assets/catalog/crm/microsoft-dynamics-365/destination-dataflow-run.png)

1. Alterne para **[!DNL Activation data]** e selecione um nome de segmento.
   ![Exemplo de captura de tela da interface do usuário da plataforma que mostra os Dados de ativação de destinos.](../../assets/catalog/crm/microsoft-dynamics-365/destinations-activation-data.png)

1. Monitore o resumo do segmento e garanta que a contagem de perfis corresponda à contagem criada no segmento.
   ![Exemplo de captura de tela da interface do usuário da plataforma que mostra o Segmento.](../../assets/catalog/crm/microsoft-dynamics-365/segment.png)

1. Faça logon no [!DNL Dynamics 365] e navegue até o [!DNL Customers] > [!DNL Contacts] e verificar se os perfis do segmento foram adicionados. Você pode ver que cada status de segmento em [!DNL Dynamics 365] foi atualizado com o status de segmento correspondente da Platform, com base no **[!UICONTROL ID de mapeamento]** valor fornecido durante a [agendamento de segmento](#schedule-segment-export-example) etapa.
   ![Captura de tela da interface do usuário do Dynamics 365 mostrando a página Contatos com status de segmento atualizados.](../../assets/catalog/crm/microsoft-dynamics-365/contacts.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](/help/data-governance/home.md).

## Erros e solução de problemas {#errors-and-troubleshooting}

### Erros desconhecidos encontrados ao enviar eventos para o destino {#unknown-errors}

Ao verificar uma execução de fluxo de dados, se você obter a seguinte mensagem de erro: `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![Captura de tela da interface do usuário da plataforma que mostra erro de solicitação incorreta.](../../assets/catalog/crm/microsoft-dynamics-365/error.png)

Para corrigir esse erro, verifique se a variável **[!UICONTROL ID de mapeamento]** você forneceu [!DNL Dynamics 365] para seu segmento da Platform é válido e existe em [!DNL Dynamics 365].

## Recursos adicionais {#additional-resources}

Informações úteis adicionais da [[!DNL Dynamics 365] documentação](https://docs.microsoft.com/en-us/dynamics365/) está abaixo:
* [Método IOrganizationService.Update(Entity)](https://docs.microsoft.com/en-us/dotnet/api/microsoft.xrm.sdk.iorganizationservice.update?view=dataverse-sdk-latest)
* [Atualizar e excluir linhas de tabela usando a API da Web](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/update-delete-entities-using-web-api#basic-update)
