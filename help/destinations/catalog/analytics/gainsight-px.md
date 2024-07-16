---
title: Conexão Gainsight PX
description: Use o destino do Gainsight PX para enviar informações de segmentação para a plataforma Gainsight PX.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 0ca0d34f-f866-4f59-80f8-60198fbb86be
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 3%

---

# Conexão Gainsight PX {#gainsight-px}

## Visão geral {#overview}

[[!DNL Gainsight PX]](https://www.gainsight.com/product-experience/) é uma plataforma de experiência de produto que permite que as equipes de produtos entendam como os usuários usam seus produtos, coletam comentários e criam envolvimentos no aplicativo, como apresentações de produtos, para impulsionar a integração de usuários e a adoção de produtos.

>[!IMPORTANT]
>
>O conector de destino e a página de documentação são criados e mantidos pela equipe do *Gainsight PX*. Para qualquer consulta ou solicitação de atualização, contate-os diretamente em *`pxsupport@gainsight.com`*.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino *Gainsight PX*, veja a seguir exemplos de casos de uso que os clientes da Adobe Experience Platform podem resolver usando esse destino.

### Direcionamento de envolvimentos no aplicativo {#targeting-in-app-engagements}

Uma empresa SaaS deseja envolver seus clientes por meio de um guia no aplicativo construído no Gainsight PX. Um público-alvo para receber este compromisso foi criado no Adobe Experience Platform. O destino PX do Gainsight recebe o público-alvo e o disponibiliza no ambiente PX do Gainsight.

## Pré-requisitos {#prerequisites}

* Contate a equipe de suporte do [!DNL Gainsight] e solicite a ativação de recursos de segmentos externos para sua assinatura.
* Gere um valor de Segredo OAuth para sua assinatura PX usando o botão **[!UICONTROL Gerar Novo Segredo]** na parte inferior da [página Detalhes da Empresa](https://app.aptrinsic.com/settings/subscription)
  ![Tela Detalhes da empresa no Gainsight PX mostrando o botão Gerar novo segredo](../../assets/catalog/analytics/gainsight-px/generate_oauth_secret.png)

## Identidades suportadas {#supported-identities}

O Gainsight PX é compatível com a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](../../../identity-service/features/namespaces.md).

| Identidade de destino | Descrição |
|---|----|
| IdentifyID | Identificador de usuário comum que identifica exclusivamente um usuário no Gainsight PX e no Adobe Experience Platform |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve que tipo de público-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---|---|---|
| [!DNL Segmentation Service] | ✓ | Públicos gerados por meio do [Serviço de segmentação](../../../segmentation/home.md) do Experience Platform. |
| Uploads personalizados | X | Públicos [importados](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---|---|---|
| Tipo de exportação | **[!UICONTROL Exportação de segmentos]** | Você está exportando todos os membros de um público com os identificadores (nome, número de telefone ou outros) usados no destino [!DNL Gainsight PX]. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Quando um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa da **[!UICONTROL Permissão de controle de acesso]** [Gerenciar Destinos](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow da configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Conectar ao destino]**.

![Captura de tela de autenticação](../../assets/catalog/analytics/gainsight-px/auth-screen.png)

* **[!UICONTROL Senha]**: a senha usada para fazer logon no [[!DNL Gainsight PX]](https://app.aptrinsic.com)
* **[!UICONTROL ID do cliente]**: a ID de assinatura do Gainsight PX na [página Detalhes da empresa](https://app.aptrinsic.com/settings/subscription)
* **[!UICONTROL Segredo do cliente]**: o segredo OAuth gerado na parte inferior da [página Detalhes da Empresa](https://app.aptrinsic.com/settings/subscription) na interface do usuário do [!DNL Gainsight PX].
* **[!UICONTROL Nome de usuário]**: o email usado para fazer logon na interface de usuário do [[!DNL Gainsight PX]](https://app.aptrinsic.com)

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Tela de detalhes do destino na interface do usuário do Experience Platform mostrando como preencher os campos Nome e Descrição](../../assets/catalog/analytics/gainsight-px/destination_details.png)

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar este destino no futuro.

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Avançar]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
>
>* Para ativar dados, você precisa de **[!UICONTROL Gerenciar Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar perfis e segmentos para destinos de exportação de segmento de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público para este destino.

### Mapear identidades {#map}

Esse destino oferece suporte ao mapeamento de atributos de perfil e namespaces de identidade. O target mapping deve sempre ser o namespace de identidade **[!UICONTROL IDENTIFY_ID]**.

Consulte os exemplos abaixo para entender melhor como configurar o mapeamento.

#### Mapear um atributo de perfil {#map-profile-attribute}

No exemplo mostrado abaixo, o campo de origem é um atributo de perfil XDM que é mapeado para o namespace de destino IDENTIFY_ID.

![Tela de mapeamento de exemplo de Namespace de Identidade mostrando como selecionar os valores de origem e de destino](../../assets/catalog/analytics/gainsight-px/mapping_attribute.png)

#### Mapear um namespace de identidade {#map-identity-namespace}

No exemplo mostrado abaixo, o campo de origem é um namespace de identidade (**[!UICONTROL ECID]**) que é mapeado para o namespace de destino **[!UICONTROL IDENTIFY_ID]**.

![Tela de mapeamento de exemplo de atributo mostrando como selecionar os valores de origem e de destino](../../assets/catalog/analytics/gainsight-px/mapping_identities.png)

## Dados exportados / Validar exportação de dados {#exported-data}

Os dados de segmentação são transmitidos do Experience Platform para o Gainsight PX.

Os metadados do segmento estão visíveis na tela Segmentos na interface do usuário do [!DNL Gainsight PX].

![Tela da lista de segmentos no Gainsight PX mostrando segmentos externos.](../../assets/catalog/analytics/gainsight-px/segment_metadata.png)

As informações de associação de segmento estão visíveis na guia Segmentos da tela do Audience Explorer da interface do usuário do [!DNL Gainsight PX].

![Tela do Audience Explorer no Gainsight PX mostrando segmentos associados para um usuário.](../../assets/catalog/analytics/gainsight-px/PX_Segments.png)

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia a [Visão geral da Governança de Dados](/help/data-governance/home.md).
