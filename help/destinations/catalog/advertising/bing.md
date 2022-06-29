---
keywords: 'publicidade; bing; '
title: Conexão Microsoft Bing
description: Com o destino de conexão do Microsoft Bing, você pode executar redirecionamento e campanhas digitais direcionadas ao público-alvo através do Microsoft Display Advertising.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: cffd689363e71f27a554df31beaf763f9bad37f4
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 2%

---

# [!DNL Microsoft Bing] conexão {#bing-destination}

## Visão geral {#overview}

O [!DNL Microsoft Bing] O destino ajuda a enviar dados de perfil para o [!DNL Microsoft Display Advertising].

Para enviar dados de perfil para o [!DNL Microsoft Bing], primeiro você deve se conectar ao destino.

## Casos de uso {#use-cases}

Como profissional de marketing, desejo poder usar segmentos criados [!DNL Microsoft Advertising IDs] para direcionar usuários por meio da exibição de publicidade em [!DNL Microsoft Advertising] canais.

## Identidades suportadas {#supported-identities}

[!DNL Microsoft Bing] O suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição |
|---|---|
| MAID | Microsoft Advertising ID |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequência de exportação {#export-type-frequency}

**[!DNL Segment Export]** - você está exportando todos os membros de um segmento (público-alvo) para a [!DNL Microsoft Bing] destino.

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) para a [!DNL Microsoft Bing] destino. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Pré-requisitos {#prerequisites}

>[!IMPORTANT]
>
>Se você deseja criar seu primeiro destino com [!DNL Microsoft Bing] e não ativou a variável [Funcionalidade de sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) no Serviço de Experience Cloud ID no passado (com o Adobe Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para ativar as sincronizações de ID. Se você já havia configurado [!DNL Microsoft Bing] integrações no Audience Manager, as sincronizações de ID que você configurou continuam para a Platform.

Ao configurar o destino, você deve fornecer as seguintes informações:

* [!UICONTROL ID da conta]: este é o seu [!DNL Bing Ads CID], em formato inteiro.

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID da conta]**: Seu [!DNL Bing Ads CID].

## Ativar segmentos para este destino {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="ID de mapeamento"
>abstract="Insira a ID de segmento numérica do Bing para a qual deseja mapear o segmento selecionado. Se o [!UICONTROL ID de mapeamento] não corresponde a uma ID de segmento no destino do Bing, você não verá os dados de público-alvo esperados em sua conta do Bing."

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar os dados do público-alvo para os destinos de exportação do segmento de fluxo](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

No [Agendamento do segmento](../../ui/activate-segment-streaming-destinations.md#scheduling) , você deve mapear manualmente seus segmentos para a ID de segmento numérico correspondente na variável [!DNL Bing] destino. Preencha a ID de segmento numérico de [!DNL Bing] no [!UICONTROL ID de mapeamento] campo.

![Imagem da interface do usuário que mostra a tela de mapeamento de segmento com um exemplo de ID de mapeamento do Bing](../../assets/catalog/advertising/bing/mapping-id.png)

Se o [!UICONTROL ID de mapeamento] não corresponde a uma ID de segmento no destino do Bing, você não verá os dados de público-alvo esperados em sua conta do Bing.

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para a [!DNL Microsoft Bing] destino, verifique seu [!DNL Microsoft Bing Ads] conta. Se a ativação foi bem-sucedida, os públicos-alvo são preenchidos na sua conta.
