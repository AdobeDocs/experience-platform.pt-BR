---
keywords: Google ads;google ads;google adwords;Google AdWords;Google Adwords
title: Conexão do Google Ads
description: O Google Ads, anteriormente conhecido como Google AdWords, é um serviço de publicidade on-line que permite que as empresas façam anúncios pagos por clique em pesquisas baseadas em texto, exibições gráficas, vídeos do YouTube e exibições móveis no aplicativo.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 3%

---

# Conexão com o [!DNL Google Ads]

## Visão geral {#overview}

[!DNL Google Ads], anteriormente conhecido como [!DNL Google AdWords], é um serviço de publicidade on-line que permite que as empresas façam publicidade paga por clique em pesquisas baseadas em texto e em exibições gráficas, [!DNL YouTube] vídeos e exibições móveis no aplicativo.

## Especificações do destino {#specifics}

Observe os seguintes detalhes, específicos do [!DNL Google Ads] Destinos:

* Os públicos ativados são criados programaticamente no [!DNL Google] plataforma.
* [!DNL Platform] no momento, o não inclui uma métrica de medição para validar a ativação bem-sucedida. Consulte as contagens de público no Google para validar a integração e entender o tamanho do direcionamento de público.

>[!IMPORTANT]
>
>Se você deseja criar seu primeiro destino com o [!DNL Google Ads] e não ativaram o [Funcionalidade de sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) no Serviço de ID de Experience Cloud anterior (com Audience Manager ou outros aplicativos), entre em contato com a Consultoria de Adobe ou com o Atendimento ao cliente para ativar as sincronizações de ID. Se você tiver configurado anteriormente as integrações do Google no Audience Manager, as sincronizações de ID configuradas serão transferidas para a Platform.

## Identidades suportadas {#supported-identities}

[!DNL Google Ad Manager] O oferece suporte à ativação das identidades descritas na tabela abaixo.

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Selecione essa identidade de destino quando a identidade de origem for um namespace GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Selecione essa identidade de destino quando sua identidade de origem for um namespace IDFA. |
| UUID AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), também conhecido como [!DNL Device ID]. Uma ID numérica de dispositivo de 38 dígitos que o Audience Manager associa a cada dispositivo com o qual interage. | O Google usa [UUID AAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) para direcionar usuários na Califórnia e a Google Cookie ID para todos os outros usuários. |
| [!DNL Google] ID do cookie | [!DNL Google] ID do cookie | [!DNL Google] O usa essa ID para direcionar usuários fora da Califórnia. |
| RIDA | ID do Roku para publicidade. Essa ID identifica exclusivamente dispositivos Roku. |  |
| EMPREGADA | ID de publicidade da Microsoft. Esta ID identifica exclusivamente os dispositivos que executam o Windows 10. |  |
| ID do Amazon Fire TV | Esta ID identifica exclusivamente as TVs Amazon Fire. |  |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve que tipo de público-alvo você pode exportar para esse destino.

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

{style="table-layout:auto"}

## Pré-requisitos {#prerequisites}

### Existente [!DNL Google Ads] account

>[!IMPORTANT]
>
> [!DNL Google] substituiu o novo [!DNL Google Ads] integrações de cookies com fornecedores de terceiros. Para executar as etapas de lista de permissões na próxima seção, é necessário ter uma integração existente com [!DNL Google Ads]. Em consequência, a abordagem recomendada para [!DNL Google Ads] está configurando um [!DNL Google Customer Match] integração. Para obter mais detalhes sobre como criar uma [!DNL Google Customer Match] integração, leia o tutorial sobre como criar uma [[!DNL Google Customer Match]](./google-customer-match.md) conexão.

### Incluir na lista de permissões {#allow-listing}

>[!NOTE]
>
>A inclusão na lista de permissões é obrigatória antes de configurar o primeiro [!DNL Google Ads] destino na Platform. Certifique-se de que o processo de inclusão na lista de permissões descrito abaixo foi concluído até [!DNL Google] antes de criar um destino.
>A exceção a essa regra é para [Audience Manager](https://docs.adobe.com/content/help/pt-BR/experience-cloud/user-guides/home.translate.html) clientes. Se você já tiver criado uma conexão com esse destino Google no Audience Manager, não será necessário passar pelo processo de inclusão na lista de permissões novamente e você poderá prosseguir para as próximas etapas.

Antes de criar o [!DNL Google Ads] destino na Platform, você deve entrar em contato com o [!DNL Google] para que o Adobe seja incluído na lista de provedores de dados permitidos e para que sua conta seja adicionada à lista de permissões. Contato [!DNL Google] e fornecer as seguintes informações:

* **ID da conta**: ID da conta do Adobe com o Google. ID da conta: 87933855.
* **ID do cliente**: ID da conta do cliente Adobe com o Google. ID do cliente: 89690775.
* Seu tipo de conta: **AdWord**
* **ID do Google AdWords**: esta é a sua ID com [!DNL Google]. Normalmente, o formato de ID é 123-456-7890.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configuração](../../ui/connect-destination.md) Para esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Tipo de conta]**: AdWords é a única opção disponível.
* **[!UICONTROL ID da conta]**: preencha a ID da conta com [!DNL Google Ads]. Normalmente, o formato de ID é 123-456-7890.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados do público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

## Dados exportados

Para verificar se os dados foram exportados com êxito para o [!DNL Google Ads] destino, verifique seu [!DNL Google Ads] conta. Se a ativação for bem-sucedida, os públicos-alvo serão preenchidos na conta.

## Solução de problemas {#troubleshooting}

### 400 Mensagem de erro de solicitação incorreta {#bad-request}

Ao configurar esse destino, você pode receber o seguinte erro:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Esse erro ocorre quando as contas do cliente não estão em conformidade com os [pré-requisitos](#prerequisites) ou quando os clientes tentam configurar o destino sem uma interface existente [!DNL Google Ads] conta.

[!DNL Google] substituiu o novo [!DNL Google Ads] integrações de cookies com fornecedores de terceiros. Para executar a [incluir na lista de permissões](#allow-listing) , você deve ter uma integração existente com [!DNL Google Ads].

A abordagem recomendada para usar o [!DNL Google Ads] está configurando um [[!DNL Google Customer Match]](google-customer-match.md) integração.
