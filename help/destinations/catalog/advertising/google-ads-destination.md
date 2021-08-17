---
keywords: Google ads, google ads, google adwords, Google AdWords, Google Adwords
title: Conexão com o Google Ads
description: O Google Ads, anteriormente conhecido como Google AdWords, é um serviço de publicidade online que permite que as empresas paguem anúncios por clique em pesquisas baseadas em texto, exibições gráficas, vídeos YouTube e exibições móveis no aplicativo.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# [!DNL Google Ads] conexão

## Visão geral {#overview}

[!DNL Google Ads], anteriormente conhecido como  [!DNL Google AdWords], é um serviço de anúncios online que permite que as empresas paguem anúncios por clique em pesquisas baseadas em texto, exibições gráficas,  [!DNL YouTube] vídeos e exibições móveis no aplicativo.

## Especificações do destino {#specifics}

Observe os seguintes detalhes que são específicos para os destinos [!DNL Google Ads]:

* Os públicos-alvo ativados são criados programaticamente na plataforma [!DNL Google] .
* [!DNL Platform] atualmente não inclui uma métrica de medição para validar a ativação bem-sucedida. Consulte as contagens de público-alvo no Google para validar a integração e entender o tamanho do direcionamento de público-alvo.

>[!IMPORTANT]
>
>Se você deseja criar seu primeiro destino com [!DNL Google Ads] e não ativou a [funcionalidade de sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) no Serviço de Experience Cloud ID no passado (com o Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para ativar as sincronizações de ID. Se você tinha configurado anteriormente as integrações do Google no Audience Manager, as sincronizações de ID que você havia configurado eram transferidas para a Platform.

## Identidades suportadas {#supported-identities}

[!DNL Google Ad Manager] O suporta a ativação de identidades descritas na tabela abaixo.

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Selecione essa identidade de destino quando sua identidade de origem for um namespace GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Selecione essa identidade de destino quando sua identidade de origem for um namespace IDFA. |
| UUID do AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), também conhecida como  [!DNL Device ID]. Uma ID de dispositivo numérica de 38 dígitos que o Audience Manager associa a cada dispositivo com o qual ele interage. | O Google usa [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) para direcionar usuários na Califórnia e a ID de cookie do Google para todos os outros usuários. |
| [!DNL Google] ID do cookie | [!DNL Google] ID do cookie | [!DNL Google] O usa essa ID para direcionar usuários fora da Califórnia. |
| RIDA | ID do Roku para publicidade. Essa ID identifica exclusivamente dispositivos Roku. |  |
| MAID | ID de publicidade da Microsoft. Esta ID identifica exclusivamente dispositivos que executam o Windows 10. |  |
| Amazon Fire TV ID | Essa ID identifica exclusivamente Amazon Fire TVs. |  |

## Tipo de exportação {#export-type}

**Exportar segmento**  - você está exportando todos os membros de um segmento (público-alvo) para o destino do Google.

## Pré-requisitos

### Conta [!DNL Google Ads] existente

>[!IMPORTANT]
>
> [!DNL Google] O substituiu as novas integrações  [!DNL Google Ads] de cookies por fornecedores terceirizados. Para executar as etapas do lista de permissões na próxima seção, você deve ter uma integração existente com [!DNL Google Ads]. Como resultado, a abordagem recomendada para usar [!DNL Google Ads] é configurar uma integração [!DNL Google Customer Match]. Para obter mais detalhes sobre como criar uma integração [!DNL Google Customer Match], leia o tutorial sobre como criar uma conexão [[!DNL Google Customer Match]](./google-customer-match.md).

### Lista de permissões

>[!NOTE]
>
>A lista de permissões é obrigatória antes de configurar seu primeiro destino [!DNL Google Ads] na Plataforma. Verifique se o processo de lista de permissões descrito abaixo foi concluído por [!DNL Google] antes de criar um destino.

Antes de criar o destino [!DNL Google Ads] na Plataforma, você deve entrar em contato com [!DNL Google] para que o Adobe seja colocado na lista de provedores de dados permitidos e para que sua conta seja adicionada à lista de permissões. Entre em contato com [!DNL Google] e forneça as seguintes informações:

* **ID** da conta: ID da conta do Adobe com o Google. ID da conta: 87933855.
* **ID** do cliente: ID da conta do cliente do Adobe com o Google. ID do cliente: 89690775.
* Seu tipo de conta: **AdWords**
* **ID do Google AdWords**: Essa é a sua ID com  [!DNL Google]. Normalmente, o formato da ID é 123-456-7890.

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configurar](../../ui/connect-destination.md) esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Preencha o nome preferencial para esse destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Tipo]** de conta: O AdWords é a única opção disponível.
* **[!UICONTROL ID]** da conta: Preencha a ID da conta com  [!DNL Google Ads]. Normalmente, o formato da ID é 123-456-7890.

## Ativar segmentos para este destino {#activate}

Consulte [Ativar os dados do público-alvo para os destinos de exportação de segmentos de fluxo](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino.


## Dados exportados

Para verificar se os dados foram exportados com êxito para o destino [!DNL Google Ads], verifique sua conta [!DNL Google Ads]. Se a ativação foi bem-sucedida, os públicos-alvo são preenchidos na sua conta.
