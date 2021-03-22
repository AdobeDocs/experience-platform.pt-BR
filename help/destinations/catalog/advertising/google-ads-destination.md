---
keywords: Google ads, google ads, google adwords, Google AdWords, Google Adwords
title: Conexão com o Google Ads
description: O Google Ads, anteriormente conhecido como Google AdWords, é um serviço de publicidade online que permite que as empresas paguem anúncios por clique em pesquisas baseadas em texto, exibições gráficas, vídeos do YouTube e exibições móveis no aplicativo.
translation-type: tm+mt
source-git-commit: 24e0a274e61fcf6311c647067920686e4f25e840
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 0%

---


# [!DNL Google Ads] conexão

## Visão geral {#overview}

[!DNL Google Ads], anteriormente conhecido como  [!DNL Google AdWords], é um serviço de anúncios online que permite que as empresas paguem anúncios por clique em pesquisas baseadas em texto, exibições gráficas,  [!DNL YouTube] vídeos e exibições móveis no aplicativo.

## Especificações de destino {#specifics}

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

* **ID**  da conta: essa é a ID da conta do Adobe com  [!DNL Google]. Entre em contato com o Atendimento ao cliente do Adobe ou seu representante do Adobe para obter essa ID.
* **ID**  do cliente: esta é a ID da conta do cliente Adobe com  [!DNL Google]. Entre em contato com o Atendimento ao cliente do Adobe ou seu representante do Adobe para obter essa ID.
* Seu tipo de conta: **AdWords**
* **ID do Google AdWords** : Essa é a sua ID com  [!DNL Google]. Normalmente, o formato da ID é 123-456-7890.

## Configurar destino

Em **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selecione [!DNL Google Ads] e selecione **[!UICONTROL Configure]**.

![Conectar destino do Google Ads](../../assets/catalog/advertising/google-ads-destination/catalog.png)

>[!NOTE]
>
>Se uma conexão com esse destino já existir, você poderá ver um botão **[!UICONTROL Activate]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consulte a seção [Catálogo](../../ui/destinations-workspace.md#catalog) da documentação do espaço de trabalho de destino.

Na etapa **Configurar** do fluxo de trabalho criar destino, preencha o [!UICONTROL Basic Information] para o destino.

![Informações básicas sobre o Google Ads](../../assets/catalog/advertising/google-ads-destination/setup.png)

* **[!UICONTROL Name]**: Preencha o nome preferencial para esse destino.
* **[!UICONTROL Description]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Account Type]**: O AdWords é a única opção disponível.
* **[!UICONTROL Account ID]**: Preencha a ID da conta com  [!DNL Google Ads]. Normalmente, o formato da ID é 123-456-7890.
* **[!UICONTROL Marketing action]**: As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte a [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

## Ativar segmentos para [!DNL Google Ads]

Para obter instruções sobre como ativar segmentos para [!DNL Google Ads], consulte [Ativar dados para destinos](../../ui/activate-destinations.md).

## Dados exportados

Para verificar se os dados foram exportados com êxito para o destino [!DNL Google Ads], verifique sua conta [!DNL Google Ads]. Se a ativação foi bem-sucedida, os públicos-alvo são preenchidos na sua conta.