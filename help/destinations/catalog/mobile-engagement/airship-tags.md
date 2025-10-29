---
keywords: etiquetas do dirigível;destino do dirigível
title: Conexão com as Tags do Aeróstato
description: Transmita continuamente os dados do público-alvo da Adobe para o Airship como tags de público-alvo para direcionamento no Airship.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 2%

---

# [!DNL Airship Tags] conexão {#airship-tags-destination}

## Visão geral

O [!DNL Airship] é a principal plataforma de engajamento do cliente, ajudando você a fornecer mensagens omnicanais relevantes e personalizadas aos seus usuários em cada estágio do ciclo de vida do cliente.

Esta integração transmite os dados de público-alvo do Adobe Experience Platform para [!DNL Airship] como [Marcas](https://docs.airship.com/guides/audience/tags/) para direcionamento ou acionamento.

Para saber mais sobre [!DNL Airship], consulte os [Documentação de dirigível](https://docs.airship.com).


>[!TIP]
>
>Esse conector de destino e a página de documentação são criados e mantidos pela equipe [!DNL Airship]. Para quaisquer consultas ou solicitações de atualização, entre em contato diretamente em [support.airship.com](https://support.airship.com/).

## Pré-requisitos

Antes de enviar os públicos-alvo da Adobe Experience Platform para o [!DNL Airship], você deve:

* Crie um grupo de marcas em seu projeto [!DNL Airship].
* Gerar um token de portador para autenticação.

>[!TIP]
> 
>Crie uma conta do [!DNL Airship] via [este link de inscrição](https://go.airship.eu/accounts/register/plan/starter/) se ainda não tiver feito isso.

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Uploads personalizados | ✓ | Públicos [importados](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Audience export]** | Você está exportando todos os membros de um público-alvo com os identificadores usados no destino Tags de dirigível. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Grupos de tags

O conceito de públicos-alvo na Adobe Experience Platform é semelhante a [Tags](https://docs.airship.com/guides/audience/tags/) em Aeróstato, com pequenas diferenças na implementação. Esta integração mapeia o status da [associação de um usuário em um segmento do Experience Platform](../../../xdm/field-groups/profile/segmentation.md) para a presença ou não de uma marca [!DNL Airship]. Por exemplo, em um público-alvo da Experience Platform em que `xdm:status` muda para `realized`, a marca é adicionada ao canal [!DNL Airship] ou usuário nomeado para o qual esse perfil está mapeado. Se o `xdm:status` for alterado para `exited`, a marca será removida.

Para habilitar esta integração, crie um *grupo de marcas* em [!DNL Airship] chamado `adobe-segments`.

>[!IMPORTANT]
>
>Ao criar seu novo grupo de marcas **Não marque** o botão de opção que diz &quot;[!DNL Allow these tags to be set only from your server]&quot;. Isso fará com que a integração de tags do Adobe falhe.

Consulte [Gerenciar grupos de marcas](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) para obter instruções sobre como criar o grupo de marcas.

## Gerar token de portador

Vá para **[!UICONTROL Settings]**&quot; **[!UICONTROL APIs & Integrations]** no [Painel de dirigível](https://go.airship.com) e selecione **[!UICONTROL Tokens]** no menu à esquerda.

Clique em **[!UICONTROL Create Token]**.

Forneça um nome amigável para o token, por exemplo, &quot;Destino de tags da Adobe&quot; e selecione &quot;Acesso integral&quot; para a função.

Clique em **[!UICONTROL Create Token]** e salve os detalhes como confidenciais.

## Casos de uso

Para ajudá-lo a entender melhor como e quando você deve usar o destino [!DNL Airship Tags], veja a seguir exemplos de casos de uso que os clientes da Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso #1

Varejistas ou plataformas de entretenimento podem criar perfis de usuário em seus clientes de fidelidade e transmitir esses públicos para o [!DNL Airship] para direcionamento de mensagens em campanhas móveis.

### Caso de uso #2

Acione mensagens individuais em tempo real quando os usuários entrarem ou saírem de públicos específicos no Adobe Experience Platform.

Por exemplo, uma retailer configura um público-alvo específico de uma marca jeans na Experience Platform. Esse retailer agora pode acionar uma mensagem móvel assim que alguém definir sua preferência de jeans para uma marca específica.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Bearer token]**: o token de portador gerado pelo painel [!DNL Airship].

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Name]**: digite um nome que o ajudará a identificar este destino.
* **[!UICONTROL Description]**: digite uma descrição para este destino.
* **[!UICONTROL Domain]**: selecione um data center dos EUA ou da UE, dependendo de qual data center [!DNL Airship] se aplica a esse destino.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados de público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

## Considerações de mapeamento {#mapping-considerations}

[!DNL Airship] marcas podem ser definidas em um canal, que representa a instância do dispositivo, por exemplo, iPhone, ou em um usuário nomeado, que mapeia todos os dispositivos de um usuário para um identificador comum, como uma ID de cliente. Se você tiver endereços de email de texto sem formatação (sem hash) como identidade principal no esquema, selecione o campo de email em seu **[!UICONTROL Source Attributes]** e mapeie para o [!DNL Airship] usuário nomeado na coluna direita em **[!UICONTROL Target Identities]**, como mostrado abaixo.

![Mapeamento de Usuário Nomeado](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Para identificadores que devem ser mapeados para um canal, ou seja, um dispositivo, mapeie para o canal apropriado com base na origem. As imagens a seguir mostram como mapear uma Google Advertising ID para um canal do Android [!DNL Airship].

![Conectar-se às Tags de Aeronave](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Conectar-se às Tags de Aeronave](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Mapeamento de canal](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] impõe a governança de dados, consulte [Visão geral da Governança de Dados](../../../data-governance/home.md).
