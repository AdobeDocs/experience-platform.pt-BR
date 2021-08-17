---
keywords: atributos do dirigível, destino do dirigível
title: Conexão de atributos de aeróstato
description: Transmita dados de público-alvo do Adobe diretamente para o Airship como atributos de público-alvo para direcionamento dentro do Airship.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 1%

---

# (Beta) [!DNL Airship Attributes] conexão {#airship-attributes-destination}

>[!IMPORTANT]
>
>O destino [!DNL Airship Attributes] no Adobe Experience Platform está atualmente na versão beta. A documentação e a funcionalidade estão sujeitas a alterações.

## Visão geral {#overview}

[!DNL Airship] O é a principal plataforma de engajamento do cliente, ajudando você a fornecer mensagens omnicanais significativas e personalizadas para seus usuários em cada estágio do ciclo de vida do cliente.

Essa integração transmite os dados do perfil do Adobe para [!DNL Airship] como [Atributos](https://docs.airship.com/guides/audience/attributes/) para direcionamento ou acionamento.

Para saber mais sobre [!DNL Airship], consulte os [Documentos do Airship](https://docs.airship.com).

>[!TIP]
>
>Esta página de documentação foi criada pela equipe [!DNL Airship]. Para quaisquer consultas ou solicitações de atualização, entre em contato diretamente com o [support.airship.com](https://support.airship.com/).

## Pré-requisitos {#prerequisites}

Antes de enviar seus segmentos de público-alvo para [!DNL Airship], você deve:

* Ative os atributos no seu projeto [!DNL Airship].
* Gere um token portador para autenticação.

>[!TIP]
>
>Crie uma conta [!DNL Airship] por meio de [este link de assinatura](https://go.airship.eu/accounts/register/plan/starter/), se ainda não tiver.

## Ativar atributos {#enable-attributes}

Os atributos de perfil do Adobe Experience Platform são semelhantes a [!DNL Airship] atributos e podem ser facilmente mapeados uns para os outros na Plataforma usando a ferramenta de mapeamento demonstrada mais abaixo nesta página.

[!DNL Airship] Os projetos têm vários atributos predefinidos e padrão. Se você tiver um atributo personalizado, deverá defini-lo em [!DNL Airship] primeiro. Consulte [Configurar e gerenciar atributos](https://docs.airship.com/tutorials/audience/attributes/) para obter detalhes.

## Gerar token portador {#bearer-token}

Vá para **[!UICONTROL Settings]**&quot; **[!UICONTROL APIs &amp; Integrations]** no [Airship dashboard](https://go.airship.com) e selecione **[!UICONTROL Tokens]** no menu à esquerda.

Clique em **[!UICONTROL Criar token]**.

Forneça um nome amigável para o token, por exemplo, &quot;Destino de atributos do Adobe&quot; e selecione &quot;Todo acesso&quot; para a função.

Clique em **[!UICONTROL Criar token]** e salve os detalhes como confidenciais.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino [!DNL Airship Attributes], aqui estão exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso nº 1

Aproveite os dados de perfil coletados no Adobe Experience Platform para personalização da mensagem e conteúdo avançado em qualquer canal de [!DNL Airship]. Por exemplo, aproveite os dados do perfil [!DNL Experience Platform] para definir atributos de localização em [!DNL Airship]. Isso permitirá que uma marca de hotel exiba uma imagem para o local de hotel mais próximo para cada usuário.

### Caso de uso nº 2

Aproveite os atributos do Adobe Experience Platform para enriquecer ainda mais os perfis [!DNL Airship] e combiná-los com o SDK ou [!DNL Airship] dados preditivos. Por exemplo, um varejista pode criar um segmento com status de fidelidade e dados de localização (atributos da plataforma) e [!DNL Airship] com previsão de rotatividade de dados para enviar mensagens altamente direcionadas aos usuários no status de fidelidade gold que vivem em Las Vegas, NV, e têm uma alta probabilidade de rotatividade.

## Conecte-se ao destino {#connect}

Consulte [Ativar os dados do público-alvo para os destinos de exportação de segmentos de fluxo](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino.

### Parâmetros de conexão {#parameters}

Enquanto [configurar](../../ui/connect-destination.md) esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Token]** portador: o token portador gerado pelo  [!DNL Airship] painel.
* **[!UICONTROL Nome]**: insira um nome que ajudará a identificar esse destino.
* **[!UICONTROL Descrição]**: insira uma descrição para este destino.
* **[!UICONTROL Domínio]**: selecione um data center dos EUA ou da UE, dependendo de qual data center se aplica a esse destino.  [!DNL Airship] 

## Ativar segmentos para este destino {#activate}

Consulte [Ativar os dados do público-alvo para os destinos de exportação de segmentos de fluxo](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino.

## Considerações de mapeamento {#mapping-considerations}

[!DNL Airship] os atributos podem ser definidos em um canal, que representa a instância do dispositivo, por exemplo, iPhone ou um usuário nomeado, que mapeia todos os dispositivos de um usuário para um identificador comum, como uma ID do cliente. Se você tiver endereços de email de texto simples (sem hash) como identidade primária em seu esquema, selecione o campo de email em seus **[!UICONTROL Atributos de origem]** e mapeie para o usuário nomeado [!DNL Airship] na coluna à direita em **[!UICONTROL Identidades do Target]**, conforme mostrado abaixo.

![Mapeamento de usuário nomeado](../../assets/catalog/mobile-engagement/airship/mapping.png)

Para identificadores que devem ser mapeados para um canal, ou seja, um dispositivo, mapeie para o canal apropriado com base na fonte. As imagens a seguir mostram como dois mapeamentos são criados:

* ID de publicidade do iOS IDFA para um canal [!DNL Airship] iOS
* Atributo Adobe `fullName` para [!DNL Airship] &quot;Nome Completo&quot;

>[!NOTE]
>
>Use o nome amigável que aparece no painel [!DNL Airship] ao selecionar o campo de destino para o mapeamento de atributo.

**Mapear identidade**

Selecionar campo de origem:

![Conectar-se aos Atributos de Aeronave](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Selecione o campo de destino:

![Conectar-se aos Atributos de Aeronave](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**Atributo do mapa**

Selecione o atributo de origem:

![Selecionar campo de origem](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Selecione o atributo de meta:

![Selecionar campo de destino](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Verificar mapeamento:

![Mapeamento de canal](../../assets/catalog/mobile-engagement/airship/mapping.png)


## Uso e governança de dados {#data-usage-governance}

Todos os destinos [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte a [Visão geral da governança de dados](../../../data-governance/home.md).
