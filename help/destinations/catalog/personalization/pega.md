---
title: Conexão do Hub de decisão do cliente Pega
description: Use o destino do Hub de decisão do cliente Pega no Adobe Experience Platform para enviar atributos de perfil e dados de associação de segmento para o Hub de decisão do cliente Pega para a próxima melhor decisão.
exl-id: 0546da5d-d50d-43ec-bbc2-9468a7db4d90
source-git-commit: ae00b113308354e98f4448d2544e2a6e475c384e
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 1%

---

# Conexão do Hub de decisão do cliente Pega

## Visão geral {#overview}

Use o [!DNL Pega Customer Decision Hub] destino no Adobe Experience Platform para enviar atributos de perfil e dados de associação de segmento para o [!DNL Pega Customer Decision Hub] para a decisão da próxima melhor ação.

Associação de segmento de perfil do Adobe Experience Platform, quando carregada em [!DNL Pega Customer Decision Hub]O , pode ser usado como preditor em modelos adaptáveis e ajudar a fornecer os dados contextuais e comportamentais corretos para fins de decisão de próxima melhor ação.

>[!IMPORTANT]
>
>Esta página de documentação foi criada pelo Pegasystems. Para quaisquer consultas ou pedidos de atualização, contacte diretamente Pega [here](mailto:support@pega.com).

## Casos de uso

Para ajudá-lo a entender melhor como e quando você deve usar a variável [!DNL Customer Decision Hub] destino, aqui estão casos de uso de exemplo que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Telecomunicações

Um profissional de marketing deseja aproveitar os insights do modelo baseado em ciência de dados para a próxima melhor ação, conforme fornecido pelo [!DNL Pega Customer Decision Hub] para envolvimento do cliente. [!DNL Pega Customer Decision Hub] O depende muito da intenção do cliente - por exemplo, &quot;Interested_In_5G&quot;, &quot;Interested_in_Unlimited_Dataplan&quot; ou &quot;Interest_in_iPhone_acessórios&quot;.

### Serviços financeiros

Um comerciante deseja otimizar as ofertas para clientes que assinaram ou cancelaram a assinatura nos boletins informativos de Plano de Pensão ou Plano de Reforma. As empresas de serviços financeiros podem assimilar várias IDs de cliente de seus próprios CRMs no Adobe Experience Platform, criar segmentos a partir de seus próprios dados offline e enviar perfis que estão inserindo e saindo dos segmentos para o [!DNL Pega Customer Decision Hub] para decisão de próxima melhor ação (NBA) em canais de saída.

## Pré-requisitos {#prerequisites}

Antes de usar esse destino para exportar dados do Adobe Experience Platform, certifique-se de concluir os seguintes pré-requisitos em [!DNL Pega Customer Decision Hub]:

* Configure o [Componente de integração de associação de perfil e segmento do Adobe Experience Platform](https://docs.pega.com/component/customer-decision-hub/adobe-experience-platform-profile-and-segment-membership-integration-component) em seu [!DNL Pega Customer Decision Hub] instância.
* Configurar o OAuth 2.0 [Registro do cliente usando credenciais do cliente](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) tipo de concessão em seu [!DNL Pega Customer Decision Hub] instância.
* Configurar [fluxo de dados de execução em tempo real](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) para Fluxo de dados de associação de segmento de Adobe em seu [!DNL Pega Customer Decision Hub] instância.

## Identidades suportadas {#supported-identities}

[!DNL Pega Customer Decision Hub] O suporta a ativação de IDs de usuário personalizadas descritas na tabela abaixo. Para obter mais detalhes, consulte [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição |
|---|---|
| *CustomerID* | Identificador de usuário comum que identifica exclusivamente um perfil no [!DNL Pega Customer Decision Hub] e Adobe Experience Platform |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Exportar todos os membros de um segmento com identificador (*CustomerID*), atributos (sobrenome, nome, localização etc.) e Dados de associação ao segmento. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são sempre conexões baseadas em API. Assim que um perfil é atualizado no Experience Platform, com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Para obter mais informações, consulte [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow para configurar destino , preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

#### Autenticação de credenciais de cliente OAuth 2 {#oauth-2-client-credentials-authentication}

![Imagem da tela da interface do usuário na qual você pode se conectar ao destino Pega CDH, usando o OAuth 2 com autenticação de credenciais do cliente](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

Preencha os campos abaixo e selecione **[!UICONTROL Ligar ao destino]**:

* **[!UICONTROL URL do token de acesso]**: O URL do token de acesso OAuth 2 em seu [!DNL Pega Customer Decision Hub] instância.
* **[!UICONTROL ID do cliente]**: O OAuth 2 [!DNL client ID] que você gerou em seu [!DNL Pega Customer Decision Hub] instância.
* **[!UICONTROL Segredo do cliente]**: O OAuth 2 [!DNL client secret] que você gerou em seu [!DNL Pega Customer Decision Hub] instância.

### Preencha os detalhes do destino {#destination-details}

Depois de estabelecer a conexão de autenticação com o [!DNL Pega Customer Decision Hub], fornecer as seguintes informações para o destino:

![Imagem da tela da interface do usuário mostrando campos preenchidos para os detalhes de destino do Pega CDH](../../assets/catalog/personalization/pega/pega-connect-destination.png)

Para configurar detalhes para o destino, preencha os campos obrigatórios e selecione **[!UICONTROL Próximo]**.

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL Nome do host]**: O Nome do host do hub de decisão do cliente Pega para o qual o perfil é exportado como dados json.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil de fluxo](../../ui/activate-streaming-profile-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Atributos de destino {#attributes}

No [[!UICONTROL Selecionar atributos]](../../ui/activate-streaming-profile-destinations.md#select-attributes) , o Adobe recomenda selecionar um identificador exclusivo de [schema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que deseja exportar para o destino.

### Exemplo de mapeamento: ativação de atualizações de perfil em [!DNL Pega Customer Decision Hub] {#mapping-example}

Abaixo está um exemplo do mapeamento de identidade correto ao exportar perfis para o [!DNL Pega Customer Decision Hub].

Seleção de campos de origem:

* Selecione um identificador (por exemplo: CustomerID) como identidade de origem que identifica exclusivamente um perfil no Adobe Experience Platform e [!DNL Pega Customer Decision Hub].
* Selecione as alterações no atributo de perfil de origem XDM que precisam ser exportadas e atualizadas em [!DNL Pega Customer Decision Hub].

Seleção de campos de destino:

* Selecione o `CustomerID` namespace como identidade de destino.
* Selecione nomes de atributos de perfil de destino que precisam ser mapeados para atributos de perfil de origem XDM correspondentes.

![Mapeamento de identidade](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## Dados exportados / Validar exportação de dados {#exported-data}

Uma atualização de associação de segmento bem-sucedida para um perfil inseriria o identificador de segmento, o nome e os status no armazenamento de dados de associação de segmento de marketing Pega. Os dados de associação são associados a um cliente que usa o Customer Profile Designer em [!DNL Pega Customer Decision Hub], conforme mostrado abaixo.
![Imagem da tela da interface do usuário na qual você pode associar dados de associação de segmento do Adobe ao Cliente, usando o Designer de perfil do cliente](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

Os dados de associação do segmento são usados nas políticas de Envolvimento do Designer de Pega Next-Best-Action para a próxima melhor tomada de decisão, conforme mostrado abaixo.
![Imagem da tela da interface do usuário, onde é possível adicionar campos de associação de Segmento como condições nas Políticas de envolvimento do Pega Next-Best-Action Designer](../../assets/catalog/personalization/pega/pega-profile-designer-engagment.png)

Os campos de dados de associação do segmento do cliente são adicionados como indicadores nos modelos adaptáveis, como mostrado abaixo.
![Imagem da tela da interface do usuário, onde é possível adicionar campos de associação de Segmento como preditores em modelos adaptáveis, usando o Predição Studio](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## Recursos adicionais {#additional-resources}

Consulte [Configuração de um registro de cliente OAuth 2.0](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) em [!DNL Pega Customer Decision Hub].

Consulte [Criação de uma execução em tempo real para fluxos de dados](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) em [!DNL Pega Customer Decision Hub].

Consulte [Gerenciar registros do cliente no Customer Profile Designer](https://docs.pega.com/whats-new-pega-platform/manage-customer-records-customer-profile-designer-86).

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](/help/data-governance/home.md).
