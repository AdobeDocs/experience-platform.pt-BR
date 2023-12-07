---
keywords: etiquetas do dirigível;destino do dirigível
title: Conexão com as Tags do Aeróstato
description: Transmita dados de público-alvo do Adobe para o dirigível sem interrupções como tags de público-alvo para direcionamento no dirigível.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: 34ae6f0f791a40584c2d476ed715bb7c5b733c42
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 2%

---

# [!DNL Airship Tags] conexão {#airship-tags-destination}

## Visão geral

[!DNL Airship] O é a principal plataforma de engajamento do cliente, ajudando você a fornecer mensagens omnicanais relevantes e personalizadas aos seus usuários em cada estágio do ciclo de vida do cliente.

Essa integração transmite os dados de público-alvo do Adobe Experience Platform para o [!DNL Airship] as [Tags](https://docs.airship.com/guides/audience/tags/) para direcionamento ou acionamento.

Para saber mais sobre [!DNL Airship], consulte o [Documentação do dirigível](https://docs.airship.com).


>[!TIP]
>
>Esse conector de destino e a página de documentação são criados e mantidos pelo [!DNL Airship] equipe. Para qualquer consulta ou solicitação de atualização, entre em contato diretamente em [support.airship.com](https://support.airship.com/).

## Pré-requisitos

Antes de enviar os públicos-alvo da Adobe Experience Platform para [!DNL Airship], você deve:

* Crie um grupo de tags na [!DNL Airship] projeto.
* Gerar um token de portador para autenticação.

>[!TIP]
> 
>Criar um [!DNL Airship] conta via [este link de inscrição](https://go.airship.eu/accounts/register/plan/starter/) caso ainda não o tenha feito.

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md). |
| Uploads personalizados | ✓ | Públicos-alvo [importado](../../../segmentation/ui/overview.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportação de público]** | Você está exportando todos os membros de um público-alvo com os identificadores usados no destino Tags de dirigível. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Grupos de tags

O conceito de públicos-alvo na Adobe Experience Platform é semelhante ao [Tags](https://docs.airship.com/guides/audience/tags/) em Aeróstatos, com ligeiras diferenças na implementação. Essa integração mapeia o status de um usuário [associação em um segmento Experience Platform](../../../xdm/field-groups/profile/segmentation.md) à presença ou não de uma [!DNL Airship] tag. Por exemplo, em um público-alvo da Platform em que a variável `xdm:status` alterações em `realized`, a tag é adicionada à [!DNL Airship] canal ou usuário nomeado para o qual este perfil está mapeado. Se a variável `xdm:status` alterações em `exited`, a tag do será removida.

Para habilitar essa integração, crie um *grupo de tags* in [!DNL Airship] nomeado `adobe-segments`.

>[!IMPORTANT]
>
>Ao criar seu novo grupo de tags **Não verificar** o botão de opção que diz &quot;[!DNL Allow these tags to be set only from your server]&quot;. Isso fará com que a integração das tags Adobe falhe.

Consulte [Gerenciar grupos de tags](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) para obter instruções sobre como criar o grupo de tags.

## Gerar token de portador

Ir para **[!UICONTROL Configurações]** &quot; **[!UICONTROL APIs e integrações]** no [Painel do dirigível](https://go.airship.com) e selecione **[!UICONTROL Tokens]** no menu à esquerda.

Clique em **[!UICONTROL Criar token]**.

Forneça um nome amigável para o token, por exemplo, &quot;Destino de tags Adobe&quot; e selecione &quot;Acesso integral&quot; para a função.

Clique em **[!UICONTROL Criar token]** e salve os detalhes como confidenciais.

## Casos de uso

Para ajudá-lo a entender melhor como e quando você deve usar o [!DNL Airship Tags] destino, aqui estão exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso #1

Os varejistas ou as plataformas de entretenimento podem criar perfis de usuário em seus clientes de fidelidade e transmitir esses públicos para [!DNL Airship] para direcionamento de mensagens em campanhas móveis.

### Caso de uso #2

Acione mensagens individuais em tempo real quando os usuários entrarem ou saírem de públicos específicos no Adobe Experience Platform.

Por exemplo, um varejista configura um público-alvo específico da marca jeans na Platform. Esse varejista agora pode acionar uma mensagem móvel assim que alguém definir sua preferência de jeans para uma marca específica.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Conectar ao destino]**.

* **[!UICONTROL Token de portador]**: o token do portador gerado pelo [!DNL Airship] painel.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: digite um nome que ajudará a identificar esse destino.
* **[!UICONTROL Descrição]**: digite uma descrição para esse destino.
* **[!UICONTROL Domínio]**: selecione um data center dos EUA ou da UE, dependendo de qual [!DNL Airship] o data center se aplica a esse destino.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados do público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

## Considerações de mapeamento {#mapping-considerations}

[!DNL Airship] as tags podem ser definidas em um canal, que representa a instância do dispositivo, por exemplo, iPhone, ou em um usuário nomeado, que mapeia todos os dispositivos de um usuário para um identificador comum, como uma ID de cliente. Se você tiver endereços de email de texto sem formatação (com hash) como identidade principal no esquema, selecione o campo de email no **[!UICONTROL Atributos de origem]** e mapear para o [!DNL Airship] usuário nomeado na coluna à direita em **[!UICONTROL Identidades do Target]**, conforme mostrado abaixo.

![Mapeamento de usuário nomeado](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Para identificadores que devem ser mapeados para um canal, ou seja, um dispositivo, mapeie para o canal apropriado com base na origem. As imagens a seguir mostram como mapear uma Google Advertising ID para uma [!DNL Airship] Canal Android.

![Conectar-se a etiquetas do dirigível](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![Conectar-se a etiquetas do dirigível](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![Mapeamento de canal](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte [Visão geral da governança de dados](../../../data-governance/home.md).
