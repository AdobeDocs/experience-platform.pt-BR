---
title: Conexão do Google Display & Video 360
description: O Display & Video 360, anteriormente conhecido como DoubleClick Bid Manager, é uma ferramenta usada para executar campanhas digitais direcionadas por redirecionamento e público-alvo em fontes de inventário de vídeo, dispositivos móveis e exibição.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1134'
ht-degree: 2%

---

# [!DNL Google Display & Video 360] conexão

>[!IMPORTANT]
>
> A Google está lançando alterações na [API do Google Ads](https://developers.google.com/google-ads/api/docs/start), na [Correspondência do Cliente](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) e na [API de Exibição e Vídeo 360](https://developers.google.com/display-video/api/guides/getting-started/overview) para oferecer suporte aos requisitos de conformidade e consentimento definidos na [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) da União Europeia ([Política de Consentimento do Usuário](https://www.google.com/about/company/user-consent-policy/) da UE). A aplicação dessas alterações aos requisitos de consentimento estará em vigor a partir de 6 de março de 2024.
> &#x200B;><br/>
> &#x200B;>Para aderir à política de consentimento do usuário da UE e continuar criando listas de públicos-alvo para usuários no Espaço Econômico Europeu (EEE), anunciantes e parceiros devem garantir que eles transmitem o consentimento do usuário final ao fazer upload dos dados de público-alvo. Como parceiro da Google, a Adobe fornece as ferramentas necessárias para cumprir esses requisitos de consentimento de acordo com a DMA na União Europeia.
> &#x200B;><br/>
> &#x200B;>Os clientes que compraram o Adobe Privacy &amp; Security Shield e configuraram uma [política de consentimento](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para filtrar perfis não consentidos não precisam tomar nenhuma ação.
> &#x200B;><br/>
> &#x200B;>Os clientes que não compraram o Adobe Privacy &amp; Security Shield devem usar os recursos de [definição de segmento](../../../segmentation/home.md#segment-definitions) no [Construtor de segmentos](../../../segmentation/ui/segment-builder.md) para filtrar perfis não consentidos, a fim de continuar usando os Destinos do Real-Time CDP Google existentes sem interrupção.

O [!DNL Display & Video 360], anteriormente conhecido como [!DNL DoubleClick Bid Manager], é uma ferramenta usada para executar campanhas digitais com direcionamento de público e redirecionamento em fontes de inventário de vídeo, dispositivos móveis e exibição.

## Especificações do destino {#specifics}

Observe os seguintes detalhes que são específicos para destinos [!DNL Google Display & Video 360]:

* Os públicos ativados são criados programaticamente na plataforma do Google.
* A ativação de preenchimentos retroativos de público para o destino [!DNL Google Display & Video 360] está agendada para ocorrer de 24 a 48 horas depois que um público é mapeado pela primeira vez para uma conexão de destino. Esta atualização é uma resposta à política da Google de aguardar 24 horas até assimilar dados e tem como objetivo melhorar as taxas de correspondência entre o Real-Time CDP e o [!DNL Google Display & Video 360]. Essa é uma configuração de backend aplicável somente a esse destino e não está relacionada a nenhuma opção de agendamento configurável pelo cliente na interface do usuário do.

>[!IMPORTANT]
>
>Se você deseja criar seu primeiro destino com o Google Display &amp; Video 360 e não habilitou a [funcionalidade de sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) no Serviço da Experience Cloud ID no passado (com o Adobe Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para habilitar as sincronizações de ID. Se você tiver configurado anteriormente as integrações do Google no Audience Manager, as sincronizações de ID configuradas serão transferidas para o Experience Platform.

## Identidades suportadas {#supported-identities}

O [!DNL Google Display & Video 360] dá suporte à ativação de públicos com base nas identidades mostradas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade | Descrição | Considerações |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| UUID do AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), também conhecido como [!DNL Device ID]. Uma ID numérica de dispositivo de 38 dígitos que o Audience Manager associa a cada dispositivo com o qual interage. | O Google usa o [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) para direcionar usuários na Califórnia, e a Google Cookie ID para todos os outros usuários. |
| ID do cookie [!DNL Google] | ID do cookie [!DNL Google] | [!DNL Google] usa essa ID para direcionar usuários fora da Califórnia. |
| RIDA | ID do Roku para Advertising. Essa ID identifica exclusivamente dispositivos Roku. |  |
| EMPREGADA | Microsoft Advertising ID. Esta ID identifica exclusivamente os dispositivos que executam o Windows 10. |  |
| ID do Amazon Fire TV | Esta ID identifica exclusivamente as TVs Amazon Fire. |  |

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

## Pré-requisitos {#prerequisites}

### Incluir na lista de permissões {#allow-listing}

>[!NOTE]
>
>A inclusão na lista de permissões é obrigatória antes de configurar seu primeiro destino do [!DNL Google Display & Video 360] no Experience Platform. Verifique se o processo de inclusão na lista de permissões descrito abaixo foi concluído por [!DNL Google] antes de criar um destino.
>&#x200B;>A exceção a esta regra é para clientes do [Audience Manager](https://docs.adobe.com/content/help/pt-BR/experience-cloud/user-guides/home.translate.html). Se você já tiver criado uma conexão com esse destino do Google no Audience Manager, não será necessário passar pelo processo de inclusão na lista de permissões novamente e você poderá prosseguir para as próximas etapas.

Antes de criar o destino [!DNL Google Display & Video 360] no Experience Platform, você deve contatar a Google, solicitando que o Adobe seja colocado na lista de provedores de dados permitidos e que sua conta seja adicionada ao incluo na lista de permissões. Entre em contato com a Google e forneça as seguintes informações:

* **ID da conta**: ID da conta da Adobe com a Google. ID da conta: 87933855.
* **ID do cliente**: ID da conta de cliente da Adobe com a Google. ID do cliente: 89690775.
* **Tipo de conta**: use **[!DNL Invite advertiser]** para permitir que os públicos-alvo sejam compartilhados somente com uma marca específica na sua conta de Vídeo e Exibição 360 ou use **[!DNL Invite partner]** para permitir que os públicos-alvo sejam compartilhados com todas as marcas na sua conta de Vídeo e Exibição 360.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configurar](../../ui/connect-destination.md) este destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Name]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Description]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Account Type]**: Selecione uma opção, dependendo da sua conta com o Google:
   * Use o `Invite Advertiser` para permitir que os públicos-alvo sejam compartilhados somente com uma marca específica na sua conta de Vídeo e Exibição 360.
   * Use o `Invite Partner` para permitir que os públicos-alvo sejam compartilhados com todas as marcas em sua conta de Vídeo e Exibição 360.
* **[!UICONTROL Account ID]**: Preencha sua ID de conta do **[!DNL Invite partner]** ou **[!DNL Invite advertiser]** com o Google. Normalmente, é uma ID de seis ou sete dígitos.

>[!NOTE]
>
>Ao configurar um destino do [!DNL Google Display & Video 360], fale com seu representante da Adobe ou do [!DNL Google Account Manager] para saber qual é o seu tipo de conta.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados de público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

## Dados exportados

Para verificar se os dados foram exportados com êxito para o destino [!DNL Google Display & Video 360], verifique sua conta [!DNL Google Display & Video 360]. Se a ativação for bem-sucedida, os públicos-alvo serão preenchidos na conta.

## Resolução de problemas {#troubleshooting}

### 400 Mensagem de erro de solicitação incorreta {#bad-request}

Ao configurar esse destino, você pode receber o seguinte erro:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Este erro ocorre quando as contas de clientes não atendem aos [pré-requisitos](#prerequisites). Para corrigir esse problema, entre em contato com a Google e verifique se sua conta está incluída na lista de permissões.