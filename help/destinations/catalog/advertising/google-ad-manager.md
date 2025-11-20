---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager; DFP
title: Conexão com o Google Ad Manager
description: O Google Ad Manager, anteriormente conhecido como DoubleClick for Publishers ou DoubleClick AdX, é uma plataforma de veiculação de anúncios da Google que fornece aos editores os meios para gerenciar a exibição de anúncios em seus sites, por meio de vídeos e aplicativos móveis.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 4%

---

# [!DNL Google Ad Manager] conexão

>[!IMPORTANT]
>
> A Google está lançando alterações na [API do Google Ads](https://developers.google.com/google-ads/api/docs/start), na [Correspondência do Cliente](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) e na [API de Exibição e Vídeo 360](https://developers.google.com/display-video/api/guides/getting-started/overview) para oferecer suporte aos requisitos de conformidade e consentimento definidos na [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) da União Europeia ([Política de Consentimento do Usuário](https://www.google.com/about/company/user-consent-policy/) da UE). A aplicação dessas alterações aos requisitos de consentimento estará em vigor a partir de 6 de março de 2024.
><br/>
>Para aderir à política de consentimento do usuário da UE e continuar criando listas de públicos-alvo para usuários no Espaço Econômico Europeu (EEE), anunciantes e parceiros devem garantir que eles transmitem o consentimento do usuário final ao fazer upload dos dados de público-alvo. Como parceiro da Google, a Adobe fornece as ferramentas necessárias para cumprir esses requisitos de consentimento de acordo com a DMA na União Europeia.
><br/>
>Os clientes que compraram o Adobe Privacy &amp; Security Shield e configuraram uma [política de consentimento](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para filtrar perfis não consentidos não precisam tomar nenhuma ação.
><br/>
>Os clientes que não compraram o Adobe Privacy &amp; Security Shield devem usar os recursos de [definição de segmento](../../../segmentation/home.md#segment-definitions) no [Construtor de segmentos](../../../segmentation/ui/segment-builder.md) para filtrar perfis não consentidos, a fim de continuar usando os Destinos do Real-Time CDP Google existentes sem interrupção.


O [!DNL Google Ad Manager], anteriormente conhecido como [!DNL DoubleClick for Publishers] (DFP) ou [!DNL DoubleClick AdX], é uma plataforma de veiculação de anúncios do [!DNL Google] que fornece aos editores os meios para gerenciar a exibição de anúncios em seus sites, por meio de vídeos e aplicativos móveis.

## Especificações do destino {#specifics}

Observe os seguintes detalhes que são específicos para destinos [!DNL Google Ad Manager]:

* Os públicos ativados são criados programaticamente na plataforma [!DNL Google].
* [!DNL Experience Platform] atualmente não inclui uma métrica de medição para validar a ativação bem-sucedida. Consulte as contagens de público no Google para validar a integração e entender o tamanho do direcionamento de público.
* Após mapear um público-alvo para um destino [!DNL Google Ad Manager], o nome do público-alvo aparece imediatamente na interface do usuário [!DNL Google Ad Manager].
* A população do segmento precisa de 24 a 48 horas para aparecer em [!DNL Google Ad Manager]. Além disso, os públicos-alvo devem ter um tamanho de público de pelo menos 50 perfis para serem exibidos em [!DNL Google Ad Manager]. Públicos com tamanhos menores que 50 perfis não serão preenchidos em [!DNL Google Ad Manager].

## Identidades suportadas {#supported-identities}

O [!DNL Google Ad Manager] dá suporte à ativação de públicos com base nas identidades mostradas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade | Descrição | Considerações |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| UUID do AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=pt-BR), também conhecido como [!DNL Device ID]. Uma ID numérica de dispositivo de 38 dígitos que o Audience Manager associa a cada dispositivo com o qual interage. | O Google usa o [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=pt-BR) para direcionar usuários na Califórnia, e a Google Cookie ID para todos os outros usuários. |
| ID do cookie [!DNL Google] | ID do cookie [!DNL Google] | [!DNL Google] usa essa ID para direcionar usuários fora da Califórnia. |
| RIDA | ID do Roku para Advertising. Essa ID identifica exclusivamente dispositivos Roku. |  |
| EMPREGADA | Microsoft Advertising ID. Esta ID identifica exclusivamente os dispositivos que executam o Windows 10. |  |
| ID do Amazon Fire TV | Esta ID identifica exclusivamente as TVs Amazon Fire. |  |

{style="table-layout:auto"}

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
| Tipo de exportação | **[!UICONTROL Audience export]** | Você está exportando todos os membros de um público para o destino do Google. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Pré-requisitos {#prerequisites}

Se você deseja criar seu primeiro destino com o [!DNL Google Ad Manager] e não habilitou a [funcionalidade de sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=pt-BR) no Serviço da Experience Cloud ID no passado (com o Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para habilitar as sincronizações de ID. Se você tiver configurado anteriormente as integrações do [!DNL Google] no Audience Manager, as sincronizações de ID configuradas serão transferidas para o Experience Platform.

### Incluir na lista de permissões {#allow-listing}

A inclusão na lista de permissões é obrigatória antes de configurar seu primeiro destino do [!DNL Google Ad Manager] no Experience Platform. Conclua o processo de inclusão na lista de permissões descrito abaixo antes de criar seu destino.

1. Siga as etapas descritas na [documentação do Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=en) para adicionar o Adobe as a linked Data Management Platform (DMP).
2. Na interface [!DNL Google Ad Manager], vá para **[!UICONTROL Admin]** > **[!UICONTROL Global Settings]** > **[!UICONTROL Network Settings]** e habilite o controle deslizante **[!UICONTROL API Access]**.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="Anexar ID de público-alvo ao nome do público-alvo"
>abstract="Selecione essa opção para que o nome do público-alvo no Google Ad Manager inclua a ID do público-alvo da Experience Platform, assim: `Audience Name (Audience ID)`"

Ao [configurar](../../ui/connect-destination.md) este destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Name]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Description]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Account ID]**: Digite seu [!DNL Audience Link ID] da conta [!DNL Google]. Este é um identificador específico associado à rede do [!DNL Google Ad Manager] (não ao [!DNL Network code]). Você pode encontrar isso em **[!UICONTROL Admin > Global settings]** na interface [!DNL Google Ad Manager].
* **[!UICONTROL Account Type]**: Selecione uma opção, dependendo da sua conta com o Google:
   * Usar `DFP by Google` para [!DNL DoubleClick] para editores
   * Usar `AdX buyer` para [!DNL Google AdX]
* **[!UICONTROL Append audience ID to audience name]**: Selecione esta opção para que o nome do público-alvo no Google Ad Manager inclua a ID de público-alvo do Experience Platform, desta forma: `Audience Name (Audience ID)`.

>[!NOTE]
>
>Ao configurar um destino do [!DNL Google Ad Manager], entre em contato com seu representante do [!DNL Google Account Manager] ou da Adobe para saber qual é o seu tipo de conta.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados de público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para o destino [!DNL Google Ad Manager], verifique sua conta [!DNL Google Ad Manager]. Se a ativação for bem-sucedida, os públicos-alvo serão preenchidos na conta.

## Solução de problemas {#troubleshooting}

Caso encontre erros ao usar esse destino e precise entrar em contato com o Adobe ou o Google, mantenha as seguintes IDs à mão.

Estas são as IDs de conta da Google da Adobe:

* **[!UICONTROL Account ID]**: 87933855
* **[!UICONTROL Customer ID]**: 89690775