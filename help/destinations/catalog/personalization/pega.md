---
title: Conexão do Hub de decisão do cliente Pega
description: Use o destino do Pega Customer Decision Hub no Adobe Experience Platform para enviar atributos de perfil e dados de associação de público-alvo para o Pega Customer Decision Hub para a próxima melhor ação de decisão.
exl-id: 0546da5d-d50d-43ec-bbc2-9468a7db4d90
source-git-commit: 05e996f9e33e0d8be3d15a9ab3baaaf6d8152b5a
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 2%

---

# Conexão do Hub de decisão do cliente Pega

## Visão geral {#overview}

Use o [!DNL Pega Customer Decision Hub] destino no Adobe Experience Platform para enviar atributos de perfil e dados de associação de público para [!DNL Pega Customer Decision Hub] para a tomada de decisão da próxima melhor ação.

Associação de público-alvo de perfil do Adobe Experience Platform, quando carregado no [!DNL Pega Customer Decision Hub], podem ser usados como preditivo em modelos adaptáveis e ajudam a fornecer os dados contextuais e comportamentais certos para fins de decisão da próxima melhor ação.

>[!IMPORTANT]
>
>Esse conector de destino e a página de documentação são criados e mantidos pela Pegasystems. Para qualquer consulta ou pedido de atualização, entre em contato diretamente com Pega [aqui](mailto:support@pega.com).

## Casos de uso

Para ajudá-lo a entender melhor como e quando você deve usar o [!DNL Customer Decision Hub] destino, aqui estão exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Telecomunicações

Um profissional de marketing deseja aproveitar os insights da próxima melhor ação baseada em modelo de ciência de dados fornecida por [!DNL Pega Customer Decision Hub] para o envolvimento do cliente. [!DNL Pega Customer Decision Hub] O depende muito da intenção do cliente, por exemplo &quot;Interested_In_5G&quot;, &quot;Interested_in_Unlimited_Dataplan&quot; ou &quot;Interest_in_iPhone_Accessations&quot;.

### Serviços financeiros

Um profissional de marketing deseja otimizar as ofertas para clientes que assinaram ou cancelaram a assinatura dos boletins informativos de Plano de aposentadoria ou Plano de aposentadoria. As empresas de serviços financeiros podem assimilar várias IDs de clientes de seus próprios CRMs na Adobe Experience Platform, criar públicos a partir de seus próprios dados offline e enviar perfis que estão entrando e saindo dos públicos para [!DNL Pega Customer Decision Hub] para decisões de próxima melhor ação (NBA) em canais de saída.

## Pré-requisitos {#prerequisites}

Antes de usar esse destino para exportar dados do Adobe Experience Platform, conclua os seguintes pré-requisitos em [!DNL Pega Customer Decision Hub]:

* Configure o [Componente de integração de Perfil e Associação de público-alvo do Adobe Experience Platform](https://docs.pega.com/component/customer-decision-hub/adobe-experience-platform-profile-and-segment-membership-integration-component) no seu [!DNL Pega Customer Decision Hub] instância.
* Configurar o OAuth 2.0 [Registro do cliente usando credenciais do cliente](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) tipo de concessão no seu [!DNL Pega Customer Decision Hub] instância.
* Configurar [fluxo de dados de execução em tempo real](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) para o fluxo de dados de Associação de público-alvo do Adobe em seu [!DNL Pega Customer Decision Hub] instância.

## Identidades suportadas {#supported-identities}

[!DNL Pega Customer Decision Hub] O é compatível com a ativação de IDs de usuário personalizadas descritas na tabela abaixo. Para obter mais detalhes, consulte [identidades](/help/identity-service/namespaces.md).

| Identidade de destino | Descrição |
|---|---|
| *CustomerID* | Identificador de usuário comum que identifica exclusivamente um perfil no [!DNL Pega Customer Decision Hub] e ADOBE EXPERIENCE PLATFORM |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Exportar todos os membros de um público-alvo com o identificador (*CustomerID*), atributos (sobrenome, nome, localização etc.) e dados de Associação de público-alvo. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões sempre ativas baseadas em API. Assim que um perfil é atualizado no Experience Platform, com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Para obter mais informações, consulte [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

#### Autenticação de Credenciais de Cliente OAuth 2 {#oauth-2-client-credentials-authentication}

![Imagem da tela da interface do usuário na qual você pode se conectar ao destino do Pega CDH usando o OAuth 2 com autenticação de Credenciais de cliente](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

Preencha os campos abaixo e selecione **[!UICONTROL Conectar ao destino]**:

* **[!UICONTROL URL do token de acesso]**: o URL do token de acesso OAuth 2 no [!DNL Pega Customer Decision Hub] instância.
* **[!UICONTROL ID do cliente]**: o OAuth 2 [!DNL client ID] que você gerou no seu [!DNL Pega Customer Decision Hub] instância.
* **[!UICONTROL Segredo do cliente]**: o OAuth 2 [!DNL client secret] que você gerou no seu [!DNL Pega Customer Decision Hub] instância.

### Preencher detalhes do destino {#destination-details}

Depois de estabelecer a conexão de autenticação com o [!DNL Pega Customer Decision Hub], forneça as seguintes informações para o destino:

![Imagem da tela da interface do usuário mostrando campos preenchidos para detalhes de destino do Pega CDH](../../assets/catalog/personalization/pega/pega-connect-destination.png)

Para configurar detalhes para o destino, preencha os campos obrigatórios e selecione **[!UICONTROL Próxima]**.

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL Nome do host]**: o Nome de host do Pega Customer Decision Hub para o qual o perfil é exportado como dados json.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil de transmissão](../../ui/activate-streaming-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Atributos de destino {#attributes}

No [[!UICONTROL Selecionar atributos]](../../ui/activate-streaming-profile-destinations.md#select-attributes) etapa, o Adobe recomenda que você selecione um identificador exclusivo de sua [esquema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino.

### Exemplo de mapeamento: ativação de atualizações de perfil no [!DNL Pega Customer Decision Hub] {#mapping-example}

Veja abaixo um exemplo do mapeamento de identidade correto ao exportar perfis para o [!DNL Pega Customer Decision Hub].

Selecionar campos de origem:

* Selecione um identificador (por exemplo: CustomerID) como identidade de origem que identifica exclusivamente um perfil no Adobe Experience Platform e [!DNL Pega Customer Decision Hub].
* Selecionar alterações de atributo do perfil de origem XDM que precisam ser exportadas e atualizadas no [!DNL Pega Customer Decision Hub].

Selecionar campos de destino:

* Selecione o `CustomerID` namespace como identidade de destino.
* Selecione nomes de atributo de perfil de destino que precisam ser mapeados para atributos de perfil de origem XDM correspondentes.

![Mapeamento de identidade](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## Dados exportados / Validar exportação de dados {#exported-data}

Uma atualização bem-sucedida da associação de público-alvo de um perfil inseriria o identificador de público-alvo, o nome e os status no armazenamento de dados de associação de público de marketing da Pega. Os dados de associação são associados a um cliente usando o Designer de perfil do cliente no [!DNL Pega Customer Decision Hub], conforme mostrado abaixo.
![Imagem da tela da interface do usuário onde você pode associar dados de associação do público-alvo do Adobe ao cliente, usando o Designer de perfil do cliente](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

Os dados de associação de público-alvo são usados nas políticas de Envolvimento do Designer de próxima ação do Pega para a tomada de decisões de próxima ação, conforme mostrado abaixo.
![Imagem da tela da interface do usuário na qual você pode adicionar campos de associação de público-alvo como condições nas Políticas de envolvimento do Designer de próxima ação Pega](../../assets/catalog/personalization/pega/pega-profile-designer-engagment.png)

Os campos de dados de associação de público-alvo do cliente são adicionados como preditores em modelos adaptáveis, conforme mostrado abaixo.
![Imagem da tela da interface do usuário na qual você pode adicionar campos de associação de Público-alvo como predicadores em modelos adaptáveis, usando o Prediction Studio](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## Recursos adicionais {#additional-resources}

Consulte [Configuração de um registro de cliente OAuth 2.0](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) in [!DNL Pega Customer Decision Hub].

Consulte [Criação de uma execução em tempo real para fluxos de dados](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) in [!DNL Pega Customer Decision Hub].

Consulte [Gerenciar registros do cliente no Designer de Perfil do Cliente](https://docs.pega.com/whats-new-pega-platform/manage-customer-records-customer-profile-designer-86).

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte o [Visão geral da governança de dados](/help/data-governance/home.md).
