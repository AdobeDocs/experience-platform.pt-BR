---
keywords: Gerenciador de lances DoubleClick, Gerenciador de lances DoubleClick, DoubleClick, Display & Video 360, display 360, video 360, Video 360, Display 360, exibição e vídeo
title: Conexão Google Display & Video 360
description: Display & Video 360, anteriormente conhecido como DoubleClick Bid Manager, é uma ferramenta usada para executar campanhas digitais direcionadas para o público-alvo em fontes de inventário de Exibição, Vídeo e Dispositivo móvel.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---


# [!DNL Google Display & Video 360] conexão

## Visão geral {#overview}

[!DNL Display & Video 360], anteriormente conhecida como  [!DNL DoubleClick Bid Manager], é uma ferramenta usada para executar o redirecionamento e campanhas digitais direcionadas ao público-alvo em fontes de inventário de Exibição, Vídeo e Móvel.

## Especificações de destino {#specifics}

Observe os seguintes detalhes que são específicos para os destinos [!DNL Google Display & Video 360]:

* Públicos ativados são criados programaticamente na plataforma do Google.
* No momento, a plataforma não inclui uma métrica de medição para validar a ativação bem-sucedida. Consulte as contagens de público-alvo no Google para validar a integração e entender o tamanho do direcionamento de público-alvo.

>[!IMPORTANT]
>
>Se você deseja criar seu primeiro destino com o Google Display &amp; Video 360 e não ativou a [funcionalidade de sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) no Serviço de ID do Experience Cloud no passado (com o Adobe Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para ativar as sincronizações de ID. Se você tinha configurado anteriormente as integrações do Google no Audience Manager, as sincronizações de ID que você havia configurado eram transferidas para a Platform.

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

### Lista de permissões

>[!NOTE]
>
>A lista de permissões é obrigatória antes de configurar seu primeiro destino [!DNL Google Display & Video 360] na Plataforma. Verifique se o processo de lista de permissões descrito abaixo foi concluído pelo Google antes de criar um destino.

Antes de criar o destino [!DNL Google Display & Video 360] na Plataforma, você deve entrar em contato com o Google solicitando que o Adobe seja colocado na lista de provedores de dados permitidos e que sua conta seja adicionada à lista de permissões. Entre em contato com o Google e forneça as seguintes informações:

* **ID**  da conta: esta é a ID da conta do Adobe com o Google. Entre em contato com o Atendimento ao cliente do Adobe ou seu representante do Adobe para obter essa ID.
* **ID**  do cliente: esta é a ID da conta do cliente Adobe com o Google. Entre em contato com o Atendimento ao cliente do Adobe ou seu representante do Adobe para obter essa ID.
* **Seu tipo** de conta: use  **[!DNL Invite advertiser]** para permitir que os públicos-alvo sejam compartilhados somente com uma marca específica em sua conta do Display &amp; Video 360 ou use  **[!DNL Invite partner]** para permitir que os públicos-alvo sejam compartilhados com todas as marcas em sua conta do Display &amp; Video 360 .

## Configurar destino

Em **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selecione [!DNL Google Display & Video 360] e selecione **[!UICONTROL Configure]**.

![Conecte o destino Google Display &amp; Video 360](../../assets/catalog/advertising/google-dv360/catalog.png)

>[!NOTE]
>
>Se uma conexão com esse destino já existir, você poderá ver um botão **[!UICONTROL Activate]** no cartão de destino. Para obter mais informações sobre a diferença entre [!UICONTROL Activate] e [!UICONTROL Configure], consulte a seção [Catálogo](../../ui/destinations-workspace.md#catalog) da documentação do espaço de trabalho de destino.

Na etapa **Setup** do workflow de criação de destino, preencha o [!UICONTROL Basic Information] para o destino, bem como as ações de marketing que devem se aplicar a esse destino.

![Informações básicas sobre Google Display &amp; Video 360](../../assets/catalog/advertising/google-dv360/setup.png)

* **[!UICONTROL Name]**: Preencha o nome preferencial para esse destino.
* **[!UICONTROL Description]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Account Type]**: Selecione uma opção, dependendo de sua conta com o Google:
   * Use `Invite Advertiser` para permitir que os públicos-alvo sejam compartilhados somente com uma marca específica em sua conta do Display &amp; Video 360 .
   * Use `Invite Partner` para permitir que os públicos-alvo sejam compartilhados com todas as marcas em sua conta do Display &amp; Video 360.
* **[!UICONTROL Account ID]**: Preencha a ID da  **[!DNL Invite partner]** conta do  **[!DNL Invite advertiser]** ou com o Google. Normalmente, essa é uma ID de seis ou sete dígitos.
* **[!UICONTROL Marketing action]**: As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte a [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

>[!NOTE]
>
>Ao configurar um destino [!DNL Google Display & Video 360], trabalhe com seu [!DNL Google Account Manager] ou representante do Adobe para entender qual tipo de conta você tem.

## Ativar segmentos para [!DNL Google Display & Video 360]

Para obter instruções sobre como ativar segmentos para [!DNL Google Display & Video 360], consulte [Ativar dados para destinos](../../ui/activate-destinations.md).

## Dados exportados

Para verificar se os dados foram exportados com êxito para o destino [!DNL Google Display & Video 360], verifique sua conta [!DNL Google Display & Video 360]. Se a ativação foi bem-sucedida, os públicos-alvo são preenchidos na sua conta.