---
keywords: atributos do dirigível;destino do dirigível
title: Conexão com os atributos do dirigível
description: Transmita facilmente os dados de público-alvo da Adobe para o Airship como atributos de público-alvo para direcionamento no Airship.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 2%

---

# [!DNL Airship Attributes] conexão {#airship-attributes-destination}

## Visão geral {#overview}

O [!DNL Airship] é o principal Experience Platform de envolvimento com o cliente, ajudando você a fornecer mensagens omnicanais relevantes e personalizadas aos seus usuários em cada estágio do ciclo de vida do cliente.

Esta integração transmite dados de perfil do Adobe para [!DNL Airship] como [Atributos](https://docs.airship.com/guides/audience/attributes/) para direcionamento ou acionamento.

Para saber mais sobre [!DNL Airship], consulte os [Documentação de dirigível](https://docs.airship.com).

>[!TIP]
>
>Esse conector de destino e a página de documentação são criados e mantidos pela equipe [!DNL Airship]. Para quaisquer consultas ou solicitações de atualização, entre em contato diretamente em [support.airship.com](https://support.airship.com/).

## Pré-requisitos {#prerequisites}

Antes de enviar os públicos-alvo para [!DNL Airship], você deve:

* Habilite atributos em seu projeto [!DNL Airship].
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
| Tipo de exportação | **[!UICONTROL Profile-based]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome) e/ou identidades, de acordo com o mapeamento de campos. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Ativar atributos {#enable-attributes}

Os atributos de perfil do Adobe Experience Platform são semelhantes aos atributos do [!DNL Airship] e podem ser facilmente mapeados no Experience Platform usando a ferramenta de mapeamento demonstrada mais abaixo nesta página.

[!DNL Airship] projetos têm vários atributos predefinidos e padrão. Se você tiver um atributo personalizado, defina-o primeiro em [!DNL Airship]. Consulte [Configurar e gerenciar atributos](https://docs.airship.com/tutorials/audience/attributes/) para obter detalhes.

## Gerar token de portador {#bearer-token}

Vá para **[!UICONTROL Settings]**&quot; **[!UICONTROL APIs & Integrations]** no [Painel de dirigível](https://go.airship.com) e selecione **[!UICONTROL Tokens]** no menu à esquerda.

Clique em **[!UICONTROL Create Token]**.

Forneça um nome amigável para o token, por exemplo, &quot;Destino de atributos do Adobe&quot;, e selecione &quot;Todo acesso&quot; para a função.

Clique em **[!UICONTROL Create Token]** e salve os detalhes como confidenciais.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino [!DNL Airship Attributes], veja a seguir exemplos de casos de uso que os clientes da Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso #1

Aproveite os dados de perfil coletados no Adobe Experience Platform para personalização da mensagem e conteúdo avançado em qualquer um dos canais de [!DNL Airship]. Por exemplo, use os dados de perfil do [!DNL Experience Platform] para definir atributos de localização dentro de [!DNL Airship]. Isso permitirá que uma marca de hotel exiba uma imagem para a localização do hotel mais próxima para cada usuário.

### Caso de uso #2

Aproveite os Atributos do Adobe Experience Platform para enriquecer ainda mais [!DNL Airship] perfis e combiná-los com SDK ou dados preditivos [!DNL Airship]. Por exemplo, uma retailer pode criar um público-alvo com status de fidelidade e dados de localização (atributos da Experience Platform) e [!DNL Airship] com previsão de churn de dados para enviar mensagens altamente direcionadas aos usuários no status de fidelidade gold que vivem em Las Vegas, Nova York e têm uma alta probabilidade de churn.

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
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Consulte [Ativar dados de público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

## Considerações de mapeamento {#mapping-considerations}

Os atributos [!DNL Airship] podem ser definidos em um canal, que representa a instância do dispositivo, por exemplo, iPhone, ou em um usuário nomeado, que mapeia todos os dispositivos de um usuário para um identificador comum, como uma ID de cliente. Se você tiver endereços de email de texto sem formatação (sem hash) como identidade principal no esquema, selecione o campo de email em seu **[!UICONTROL Source Attributes]** e mapeie para o [!DNL Airship] usuário nomeado na coluna direita em **[!UICONTROL Target Identities]**, como mostrado abaixo.

![Mapeamento de Usuário Nomeado](../../assets/catalog/mobile-engagement/airship/mapping.png)

Para identificadores que devem ser mapeados para um canal, ou seja, um dispositivo, mapeie para o canal apropriado com base na origem. As imagens a seguir mostram como dois mapeamentos são criados:

* ID do iOS Advertising IDFA para um canal do iOS [!DNL Airship]
* Atributo `fullName` do Adobe para o atributo &quot;Full Name&quot; [!DNL Airship]

>[!NOTE]
>
>Use o nome amigável que aparece no painel do [!DNL Airship] ao selecionar o campo de destino para o mapeamento de atributos.

**Mapear identidade**

Selecionar campo de origem:

![Conectar-se aos Atributos da Aeronave](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Selecionar campo de destino:

![Conectar-se aos Atributos da Aeronave](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**Mapear atributo**

Selecionar atributo de origem:

![Selecionar campo de origem](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Selecionar atributo de destino:

![Selecionar campo de destino](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Verificar mapeamento:

![Mapeamento de canal](../../assets/catalog/mobile-engagement/airship/mapping.png)


## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] impõe a governança de dados, consulte a [visão geral da Governança de Dados](../../../data-governance/home.md).
