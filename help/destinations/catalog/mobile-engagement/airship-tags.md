---
keywords: etiquetas de aeróstato, destino de aeróstato
title: Ligação de Etiquetas de Avião
description: Transmita dados de público-alvo do Adobe para o Airship como tags de público-alvo para definição de metas dentro do Airship.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 1%

---

# [!DNL Airship Tags] conexão {#airship-tags-destination}

## Visão geral

[!DNL Airship] O é a principal plataforma de engajamento do cliente, ajudando você a fornecer mensagens omnicanais significativas e personalizadas para seus usuários em cada estágio do ciclo de vida do cliente.

Essa integração passa os dados de segmento do Adobe Experience Platform para [!DNL Airship] as [Tags](https://docs.airship.com/guides/audience/tags/) para direcionamento ou acionamento.

Para saber mais sobre [!DNL Airship], consulte o [Documentos de aeróstato](https://docs.airship.com).


>[!TIP]
>
>Esta página de documentação foi criada pela [!DNL Airship] equipe. Para quaisquer consultas ou pedidos de atualização, contacte-os diretamente em [support.airship.com](https://support.airship.com/).

## Pré-requisitos

Antes de enviar os segmentos do Adobe Experience Platform para o [!DNL Airship], você deve:

* Crie um grupo de tags no [!DNL Airship] projeto.
* Gere um token portador para autenticação.

>[!TIP]
> 
>Crie um [!DNL Airship] conta via [este link de inscrição](https://go.airship.eu/accounts/register/plan/starter/) se você ainda não tiver.

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores usados no destino Tags de nave. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Grupos de tags

O conceito de segmentos na Adobe Experience Platform é semelhante ao [Tags](https://docs.airship.com/guides/audience/tags/) no Airship, com pequenas diferenças na implementação. Essa integração mapeia o status do [associação em um segmento de Experience Platform](../../../xdm/field-groups/profile/segmentation.md) à presença ou não de um [!DNL Airship] . Por exemplo, em um segmento da plataforma em que a variável `xdm:status` alterações em `realized`, a tag é adicionada ao [!DNL Airship] canal ou usuário nomeado para o qual este perfil está mapeado. Se a variável `xdm:status` alterações em `exited`, a tag será removida.

Para habilitar essa integração, crie um *grupo de tags* em [!DNL Airship] nomeado `adobe-segments`.

>[!IMPORTANT]
>
>Ao criar seu novo grupo de tags **Não verificar** o botão de opção que diz &quot;[!DNL Allow these tags to be set only from your server]&quot;. Isso fará com que a integração de tags Adobe falhe.

Consulte [Gerenciar grupos de tags](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) para obter instruções sobre como criar o grupo de tags.

## Gerar token portador

Ir para **[!UICONTROL Configurações]** &quot; **[!UICONTROL APIs e integrações]** no [Painel de bordo](https://go.airship.com) e selecione **[!UICONTROL Tokens]** no menu à esquerda.

Clique em **[!UICONTROL Criar token]**.

Forneça um nome amigável para o token, por exemplo, &quot;Destino de tags de Adobe&quot; e selecione &quot;Todo acesso&quot; para a função.

Clique em **[!UICONTROL Criar token]** e guarde os detalhes como confidenciais.

## Casos de uso

Para ajudá-lo a entender melhor como e quando você deve usar a variável [!DNL Airship Tags] destino, aqui estão casos de uso de exemplo que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso nº 1

Varejistas ou plataformas de entretenimento podem criar perfis de usuário em seus clientes de fidelidade e transmitir esses segmentos para [!DNL Airship] para o direcionamento de mensagens em campanhas móveis.

### Caso de uso nº 2

Acione mensagens um para um em tempo real quando os usuários caírem em ou saírem de segmentos específicos no Adobe Experience Platform.

Por exemplo, um varejista configura um segmento específico de marca jeans na Platform. Esse varejista agora pode acionar uma mensagem móvel assim que alguém definir sua preferência de jeans para uma marca específica.

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Token de portador]**: o token portador gerado pelo [!DNL Airship] painel.
* **[!UICONTROL Nome]**: insira um nome que ajudará a identificar esse destino.
* **[!UICONTROL Descrição]**: insira uma descrição para este destino.
* **[!UICONTROL Domínio]**: selecione um data center dos EUA ou da UE, dependendo de qual [!DNL Airship] o data center se aplica a esse destino.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar os dados do público-alvo para os destinos de exportação do segmento de fluxo](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Considerações de mapeamento {#mapping-considerations}

[!DNL Airship] As tags podem ser definidas em um canal, que representa a instância do dispositivo, por exemplo, iPhone ou um usuário nomeado, que mapeia todos os dispositivos de um usuário para um identificador comum, como uma ID do cliente. Se você tiver endereços de email de texto simples (sem hash) como identidade primária no esquema, selecione o campo de email em seu **[!UICONTROL Atributos de origem]** e mapear para [!DNL Airship] usuário nomeado na coluna direita em **[!UICONTROL Identidades do Target]**, conforme mostrado abaixo.

![Mapeamento de usuário nomeado](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Para identificadores que devem ser mapeados para um canal, ou seja, um dispositivo, mapeie para o canal apropriado com base na fonte. As imagens a seguir mostram como mapear uma ID de anúncio do Google para um [!DNL Airship] Canal Android.

![Conectar-se às Tags de nave](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Conectar-se às Tags de nave](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Mapeamento de canal](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](../../../data-governance/home.md).
