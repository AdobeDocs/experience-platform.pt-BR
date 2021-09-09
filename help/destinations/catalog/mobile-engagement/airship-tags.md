---
keywords: etiquetas de aeróstato, destino de aeróstato
title: Ligação de Etiquetas de Avião
description: Transmita dados de público-alvo do Adobe para o Airship como tags de público-alvo para definição de metas dentro do Airship.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: a765f6829f08f36010e0e12a7186bf5552dfe843
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# [!DNL Airship Tags] conexão {#airship-tags-destination}

## Visão geral

[!DNL Airship] O é a principal plataforma de engajamento do cliente, ajudando você a fornecer mensagens omnicanais significativas e personalizadas para seus usuários em cada estágio do ciclo de vida do cliente.

Essa integração transmite os dados do segmento do Adobe Experience Platform para [!DNL Airship] como [Tags](https://docs.airship.com/guides/audience/tags/) para direcionamento ou acionamento.

Para saber mais sobre [!DNL Airship], consulte os [Documentos do Airship](https://docs.airship.com).


>[!TIP]
>
>Esta página de documentação foi criada pela equipe [!DNL Airship]. Para quaisquer consultas ou solicitações de atualização, entre em contato diretamente com o [support.airship.com](https://support.airship.com/).

## Pré-requisitos

Antes de enviar seus segmentos do Adobe Experience Platform para [!DNL Airship], você deve:

* Crie um grupo de tags no seu projeto [!DNL Airship].
* Gere um token portador para autenticação.

>[!TIP]
> 
>Crie uma conta [!DNL Airship] por meio de [este link de assinatura](https://go.airship.eu/accounts/register/plan/starter/), se ainda não tiver.

## Grupos de tags

O conceito de segmentos na Adobe Experience Platform é semelhante a [Tags](https://docs.airship.com/guides/audience/tags/) no Airship, com pequenas diferenças na implementação. Essa integração mapeia o status da associação de um usuário [em um Experience Platform segment](../../../xdm/field-groups/profile/segmentation.md) para a presença ou não presença de uma tag [!DNL Airship]. Por exemplo, em um segmento da Platform em que `xdm:status` muda para `realized`, a tag é adicionada ao canal [!DNL Airship] ou ao usuário nomeado para o qual esse perfil é mapeado. Se `xdm:status` for alterado para `exited`, a tag será removida.

Para habilitar essa integração, crie um *grupo de tags* em [!DNL Airship] chamado `adobe-segments`.

>[!IMPORTANT]
>
>Ao criar seu novo grupo de tags **Não marque** o botão de opção que diz &quot;[!DNL Allow these tags to be set only from your server]&quot;. Isso fará com que a integração de tags Adobe falhe.

Consulte [Gerenciar grupos de tags](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) para obter instruções sobre como criar o grupo de tags.

## Gerar token portador

Vá para **[!UICONTROL Settings]**&quot; **[!UICONTROL APIs &amp; Integrations]** no [Airship dashboard](https://go.airship.com) e selecione **[!UICONTROL Tokens]** no menu à esquerda.

Clique em **[!UICONTROL Criar token]**.

Forneça um nome amigável para o token, por exemplo, &quot;Destino de tags de Adobe&quot; e selecione &quot;Todo acesso&quot; para a função.

Clique em **[!UICONTROL Criar token]** e salve os detalhes como confidenciais.

## Casos de uso

Para ajudá-lo a entender melhor como e quando você deve usar o destino [!DNL Airship Tags], aqui estão exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso nº 1

Varejistas ou plataformas de entretenimento podem criar perfis de usuário em seus clientes de fidelidade e transmitir esses segmentos para [!DNL Airship] para direcionamento de mensagens em campanhas móveis.

### Caso de uso nº 2

Acione mensagens um para um em tempo real quando os usuários caírem em ou saírem de segmentos específicos no Adobe Experience Platform.

Por exemplo, um varejista configura um segmento específico de marca jeans na Platform. Esse varejista agora pode acionar uma mensagem móvel assim que alguém definir sua preferência de jeans para uma marca específica.

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configurar](../../ui/connect-destination.md) esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Token]** portador: o token portador gerado pelo  [!DNL Airship] painel.
* **[!UICONTROL Nome]**: insira um nome que ajudará a identificar esse destino.
* **[!UICONTROL Descrição]**: insira uma descrição para este destino.
* **[!UICONTROL Domínio]**: selecione um data center dos EUA ou da UE, dependendo de qual data center se aplica a esse destino.  [!DNL Airship] 


## Ativar segmentos para este destino {#activate}

Consulte [Ativar os dados do público-alvo para os destinos de exportação de segmentos de fluxo](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino.

## Considerações de mapeamento {#mapping-considerations}

[!DNL Airship] As tags podem ser definidas em um canal, que representa a instância do dispositivo, por exemplo, iPhone ou um usuário nomeado, que mapeia todos os dispositivos de um usuário para um identificador comum, como uma ID do cliente. Se você tiver endereços de email de texto simples (sem hash) como identidade primária em seu esquema, selecione o campo de email em seus **[!UICONTROL Atributos de origem]** e mapeie para o usuário nomeado [!DNL Airship] na coluna à direita em **[!UICONTROL Identidades do Target]**, conforme mostrado abaixo.

![Mapeamento de usuário nomeado](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Para identificadores que devem ser mapeados para um canal, ou seja, um dispositivo, mapeie para o canal apropriado com base na fonte. As imagens a seguir mostram como mapear uma ID de anúncio do Google para um canal [!DNL Airship] Android.

![Conectar-se a ](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Tags de aeróstatoConectar-se a Mapeamento de ](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Tags de AirshipChannel](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Uso e governança de dados {#data-usage-governance}

Todos os destinos [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](../../../data-governance/home.md).
