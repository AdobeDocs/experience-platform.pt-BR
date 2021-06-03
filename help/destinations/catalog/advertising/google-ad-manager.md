---
keywords: google ad manager; google ad; doubleclick; DoubleClick AdX; DoubleClick; Google Ad Manager; Google ad manager; Google ad manager; DFP
title: Conexão com o Google Ad Manager
description: O Google Ad Manager, anteriormente conhecido como DoubleClick for Publishers ou DoubleClick AdX, é uma plataforma de veiculação de anúncios do Google que oferece aos editores os meios de gerenciar a exibição de anúncios em seus sites, por meio de vídeos e aplicativos móveis.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 4df2e7ce9c7e94da4ea0be50ba21232c639e2587
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 0%

---

# [!DNL Google Ad Manager] conexão

## Visão geral {#overview}

[!DNL Google Ad Manager], anteriormente conhecida como  [!DNL DoubleClick for Publishers] (DFP) ou  [!DNL DoubleClick AdX], é uma plataforma de veiculação de anúncios da  [!DNL Google] que oferece aos editores os meios de gerenciar a exibição de anúncios em seus sites, por meio de vídeos e aplicativos móveis.

## Especificações do destino {#specifics}

Observe os seguintes detalhes que são específicos para os destinos [!DNL Google Ad Manager]:

* Os públicos-alvo ativados são criados programaticamente na plataforma [!DNL Google] .
* [!DNL Platform] atualmente não inclui uma métrica de medição para validar a ativação bem-sucedida. Consulte as contagens de público-alvo no Google para validar a integração e entender o tamanho do direcionamento de público-alvo.

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

Se você deseja criar seu primeiro destino com [!DNL Google Ad Manager] e não ativou a [funcionalidade de sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) no Serviço de Experience Cloud ID no passado (com o Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para ativar as sincronizações de ID. Se você já havia configurado [!DNL Google] integrações no Audience Manager, as sincronizações de ID que você havia configurado continuam para a Platform.

## Lista de permissões

>[!NOTE]
>
>A lista de permissões é obrigatória antes de configurar seu primeiro destino [!DNL Google Ad Manager] na Plataforma. Verifique se o processo de lista de permissões descrito abaixo foi concluído por [!DNL Google] antes de criar um destino.

Antes de criar o destino [!DNL Google Ad Manager] na Plataforma, você deve entrar em contato com [!DNL Google] para que o Adobe seja colocado na lista de provedores de dados permitidos e para que sua conta seja adicionada à lista de permissões. Entre em contato com [!DNL Google] e forneça as seguintes informações:

* **ID**  da conta: essa é a ID da conta do Adobe com  [!DNL Google]. Entre em contato com o Atendimento ao cliente do Adobe ou seu representante do Adobe para obter essa ID.
* **ID**  do cliente: esta é a ID da conta do cliente Adobe com  [!DNL Google]. Entre em contato com o Atendimento ao cliente do Adobe ou seu representante do Adobe para obter essa ID.
* **ID**  de rede: esta é a sua conta com  [!DNL Google Ad Manager]
* **ID**  do link de público-alvo: esta é a sua conta com  [!DNL Google Ad Manager]
* Seu tipo de conta. DFP por Google ou AdX comprador.

## Configurar destino

Em **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]**, selecione **[!DNL Google Ad Manager]** e selecione **[!UICONTROL Configurar]**.

![Conectar o destino do Google Ad Manager](../../assets/catalog/advertising/google-ad-manager/catalog.png)

>[!NOTE]
>
>Se uma conexão com esse destino já existir, você poderá ver um botão **[!UICONTROL Ativar]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Ativate]** e **[!UICONTROL Configure]**, consulte a seção [Catalog](../../ui/destinations-workspace.md#catalog) da documentação do espaço de trabalho de destino.

Na etapa **Configurar** do workflow criar destino, preencha o [!UICONTROL Informações básicas] para o destino.

![Informações básicas sobre o Google Ad Manager](../../assets/catalog/advertising/google-ad-manager/setup.png)

* **[!UICONTROL Nome]**: Preencha o nome preferencial para esse destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Tipo]** de conta: Selecione uma opção, dependendo de sua conta com o Google:
   * Use `DFP by Google` para [!DNL DoubleClick] para Editores
   * Use `AdX buyer` para [!DNL Google AdX]
* **[!UICONTROL ID]** da conta: Preencha a ID da conta com  [!DNL Google]. Pode ser a ID de rede ou a ID do link de público-alvo. Normalmente, essa é uma ID de oito dígitos.
* **[!UICONTROL Ação]** de marketing: As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte a [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

>[!NOTE]
>
>Ao configurar um destino [!DNL Google Ad Manager], trabalhe com seu [!DNL Google Account Manager] ou representante do Adobe para entender qual tipo de conta você tem.

## Ativar segmentos para [!DNL Google Ad Manager]

Para obter instruções sobre como ativar segmentos para [!DNL Google Ad Manager], consulte [Ativar dados para destinos](../../ui/activate-destinations.md).

## Dados exportados

Para verificar se os dados foram exportados com êxito para o destino [!DNL Google Ad Manager], verifique sua conta [!DNL Google Ad Manager]. Se a ativação foi bem-sucedida, os públicos-alvo são preenchidos na sua conta.
