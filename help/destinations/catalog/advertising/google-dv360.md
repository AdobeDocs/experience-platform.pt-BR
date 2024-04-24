---
title: Conexão do Google Display & Video 360
description: O Display & Video 360, anteriormente conhecido como DoubleClick Bid Manager, é uma ferramenta usada para executar campanhas digitais direcionadas por redirecionamento e público-alvo em fontes de inventário de vídeo, dispositivos móveis e exibição.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: 0db22ba2993012357cf65daaeffb5676193fba23
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 2%

---

# [!DNL Google Display & Video 360] conexão

>[!IMPORTANT]
>
> A Google está lançando alterações no [API do Google Ads](https://developers.google.com/google-ads/api/docs/start), [Correspondência de Cliente](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html), e o [API de vídeo e exibição 360](https://developers.google.com/display-video/api/guides/getting-started/overview) a fim de apoiar os requisitos de conformidade e consentimento definidos no [Lei dos Mercados Digitais](https://digital-markets-act.ec.europa.eu/index_en) (DMA) na União Europeia ([Política de consentimento do usuário da UE](https://www.google.com/about/company/user-consent-policy/)). A aplicação dessas alterações aos requisitos de consentimento estará em vigor a partir de 6 de março de 2024.
><br/>
>Para aderir à política de consentimento do usuário da UE e continuar criando listas de públicos-alvo para usuários no Espaço Econômico Europeu (EEE), anunciantes e parceiros devem garantir que eles transmitem o consentimento do usuário final ao fazer upload dos dados de público-alvo. Como Parceiro da Google, o Adobe fornece as ferramentas necessárias para cumprir esses requisitos de consentimento de acordo com a DMA na União Europeia.
><br/>
>Clientes que compraram o Adobe Privacy &amp; Security Shield e configuraram um [política de consentimento](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para filtrar perfis não consentidos, não é necessário tomar nenhuma ação.
><br/>
>Os clientes que não compraram o Adobe Privacy &amp; Security Shield devem usar o [definição de segmento](../../../segmentation/home.md#segment-definitions) recursos no [Construtor de segmentos](../../../segmentation/ui/segment-builder.md) para filtrar perfis não consentidos, a fim de continuar usando os Destinos existentes do Real-Time CDP Google sem interrupção.

[!DNL Display & Video 360], anteriormente conhecido como [!DNL DoubleClick Bid Manager], é uma ferramenta usada para executar campanhas digitais direcionadas por público e redirecionamento em fontes de inventário para exibição, vídeo e dispositivos móveis.

## Especificações do destino {#specifics}

Observe os seguintes detalhes, específicos do [!DNL Google Display & Video 360] Destinos:

* Os públicos ativados são criados programaticamente na plataforma do Google.
* A ativação de preenchimentos retroativos de público para o [!DNL Google Display & Video 360] o destino está programado para ocorrer de 24 a 48 horas depois que um público-alvo é mapeado pela primeira vez para uma conexão de destino. Essa atualização é uma resposta à política da Google de aguardar 24 horas até a assimilação de dados e tem como objetivo melhorar as taxas de correspondência entre o Real-Time CDP e o [!DNL Google Display & Video 360]. Essa é uma configuração de backend aplicável somente a esse destino e não está relacionada a nenhuma opção de agendamento configurável pelo cliente na interface do usuário do.

>[!IMPORTANT]
>
>Se você deseja criar seu primeiro destino com o Google Display &amp; Video 360 e não ativou o [Funcionalidade de sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) no Serviço de ID de Experience Cloud no passado (com o Adobe Audience Manager ou outros aplicativos), entre em contato com a Consultoria de Adobe ou com o Atendimento ao cliente para ativar as sincronizações de ID. Se você tiver configurado anteriormente as integrações do Google no Audience Manager, as sincronizações de ID configuradas serão transferidas para a Platform.

## Identidades suportadas {#supported-identities}

[!DNL Google Display & Video 360] O oferece suporte à ativação de públicos com base nas identidades mostradas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade | Descrição | Considerações |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| UUID AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), também conhecido como [!DNL Device ID]. Uma ID numérica de dispositivo de 38 dígitos que o Audience Manager associa a cada dispositivo com o qual interage. | O Google usa [UUID AAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) para direcionar usuários na Califórnia e a Google Cookie ID para todos os outros usuários. |
| [!DNL Google] ID do cookie | [!DNL Google] ID do cookie | [!DNL Google] O usa essa ID para direcionar usuários fora da Califórnia. |
| RIDA | ID do Roku para publicidade. Essa ID identifica exclusivamente dispositivos Roku. |  |
| EMPREGADA | ID de publicidade da Microsoft. Esta ID identifica exclusivamente os dispositivos que executam o Windows 10. |  |
| ID do Amazon Fire TV | Esta ID identifica exclusivamente as TVs Amazon Fire. |  |

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
| Tipo de exportação | **[!UICONTROL Exportação de público]** | Você está exportando todos os membros de um público para o destino do Google. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

## Pré-requisitos {#prerequisites}

### Incluir na lista de permissões {#allow-listing}

>[!NOTE]
>
>A inclusão na lista de permissões é obrigatória antes de configurar o primeiro [!DNL Google Display & Video 360] destino na Platform. Verifique se o processo de inclusão na lista de permissões descrito abaixo foi concluído até [!DNL Google] antes de criar um destino.
>A exceção a essa regra é para [Audience Manager](https://docs.adobe.com/content/help/pt-BR/experience-cloud/user-guides/home.translate.html) clientes. Se você já tiver criado uma conexão com esse destino Google no Audience Manager, não será necessário passar pelo processo de inclusão na lista de permissões novamente e você poderá prosseguir para as próximas etapas.

Antes de criar o [!DNL Google Display & Video 360] destino na Platform, você deve entrar em contato com a Google solicitando que o Adobe seja incluído na lista de provedores de dados permitidos e que sua conta seja adicionada ao incluo na lista de permissões. Entre em contato com a Google e forneça as seguintes informações:

* **ID da conta**: ID da conta do Adobe com o Google. ID da conta: 87933855.
* **ID do cliente**: ID da conta do cliente Adobe com o Google. ID do cliente: 89690775.
* **Seu tipo de conta**: uso **[!DNL Invite advertiser]** para permitir que os públicos sejam compartilhados somente com uma marca específica em sua conta de Vídeo e exibição 360 ou no uso **[!DNL Invite partner]** para permitir que os públicos sejam compartilhados com todas as marcas em sua conta Display &amp; Video 360.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Exibir destinos]** e **[!UICONTROL Gerenciar destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configuração](../../ui/connect-destination.md) Para esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Tipo de conta]**: selecione uma opção, dependendo da sua conta com o Google:
   * Uso `Invite Advertiser` para permitir que os públicos sejam compartilhados somente com uma marca específica em sua conta de Vídeo e exibição 360.
   * Uso `Invite Partner` para permitir que os públicos sejam compartilhados com todas as marcas em sua conta Display &amp; Video 360.
* **[!UICONTROL ID da conta]**: Preencha o **[!DNL Invite partner]** ou **[!DNL Invite advertiser]** ID da conta com o Google. Normalmente, é uma ID de seis ou sete dígitos.

>[!NOTE]
>
>Ao configurar um [!DNL Google Display & Video 360] destino, trabalhe com seu [!DNL Google Account Manager] ou representante da Adobe para saber qual tipo de conta você tem.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Exibir destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados do público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

## Dados exportados

Para verificar se os dados foram exportados com êxito para o [!DNL Google Display & Video 360] destino, verifique seu [!DNL Google Display & Video 360] conta. Se a ativação for bem-sucedida, os públicos-alvo serão preenchidos na conta.

## Solução de problemas {#troubleshooting}

### 400 Mensagem de erro de solicitação incorreta {#bad-request}

Ao configurar esse destino, você pode receber o seguinte erro:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Esse erro ocorre quando as contas do cliente não estão em conformidade com os [pré-requisitos](#prerequisites). Para corrigir esse problema, entre em contato com a Google e verifique se sua conta está incluída na lista de permissões.