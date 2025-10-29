---
title: Conexão do Google Ads
description: O Google Ads, anteriormente conhecido como Google AdWords, é um serviço de publicidade on-line que permite que as empresas façam anúncios pagos por clique em pesquisas baseadas em texto, exibições gráficas, vídeos do YouTube e exibições móveis no aplicativo.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 2%

---

# [!DNL Google Ads] conexão

## Visão geral {#overview}

O [!DNL Google Ads], anteriormente conhecido como [!DNL Google AdWords], é um serviço de publicidade online que permite que as empresas publiquem anúncios pagos por clique em pesquisas baseadas em texto, exibições gráficas, vídeos do [!DNL YouTube] e exibições móveis no aplicativo.

## Especificações do destino {#specifics}

Observe os seguintes detalhes que são específicos para destinos [!DNL Google Ads]:

* Os públicos ativados são criados programaticamente na plataforma [!DNL Google].
* [!DNL Experience Platform] atualmente não inclui uma métrica de medição para validar a ativação bem-sucedida. Consulte as contagens de público no Google para validar a integração e entender o tamanho do direcionamento de público.

>[!IMPORTANT]
>
>Se você deseja criar seu primeiro destino com o [!DNL Google Ads] e não habilitou a [funcionalidade de sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) no Serviço da Experience Cloud ID no passado (com o Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para habilitar as sincronizações de ID. Se você tiver configurado anteriormente as integrações do Google no Audience Manager, as sincronizações de ID configuradas serão transferidas para o Experience Platform.

## Identidades suportadas {#supported-identities}

[!DNL Google Ads] dá suporte à ativação das identidades descritas na tabela abaixo.

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Selecione essa identidade de destino quando a identidade de origem for um namespace GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Selecione essa identidade de destino quando sua identidade de origem for um namespace IDFA. |
| UUID do AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), também conhecido como [!DNL Device ID]. Uma ID numérica de dispositivo de 38 dígitos que o Audience Manager associa a cada dispositivo com o qual interage. | O Google usa o [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) para direcionar usuários na Califórnia, e a Google Cookie ID para todos os outros usuários. |
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

### Conta [!DNL Google Ads] existente

>[!IMPORTANT]
>
> [!DNL Google] substituiu novas [!DNL Google Ads] integrações de cookies com fornecedores de terceiros. Para executar as etapas de inclui na lista de permissões na próxima seção, você deve ter uma integração existente com o [!DNL Google Ads]. Como resultado, a abordagem recomendada para o uso do [!DNL Google Ads] é configurar uma integração do [!DNL Google Customer Match]. Para obter mais detalhes sobre como criar uma integração [!DNL Google Customer Match], leia o tutorial sobre como criar uma conexão [[!DNL Google Customer Match]](./google-customer-match.md).

### Incluir na lista de permissões {#allow-listing}

>[!NOTE]
>
>A inclusão na lista de permissões é obrigatória antes de configurar seu primeiro destino do [!DNL Google Ads] no Experience Platform. Verifique se o processo de inclusão na lista de permissões descrito abaixo foi concluído por [!DNL Google] antes de criar um destino.
>&#x200B;>A exceção a esta regra é para clientes do [Audience Manager](https://docs.adobe.com/content/help/pt-BR/experience-cloud/user-guides/home.translate.html). Se você já tiver criado uma conexão com esse destino do Google no Audience Manager, não será necessário passar pelo processo de inclusão na lista de permissões novamente e você poderá prosseguir para as próximas etapas.

Antes de criar o destino [!DNL Google Ads] no Experience Platform, contate [!DNL Google] para que o Adobe seja colocado na lista de provedores de dados permitidos e para que sua conta seja adicionada ao incluo na lista de permissões. Contate [!DNL Google] e forneça as seguintes informações:

* **ID da conta**: ID da conta da Adobe com a Google. ID da conta: 87933855.
* **ID do cliente**: ID da conta de cliente da Adobe com a Google. ID do cliente: 89690775.
* Seu tipo de conta: **AdWords**
* **ID do Google AdWords**: esta é sua ID com [!DNL Google]. Normalmente, o formato de ID é 123-456-7890.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configurar](../../ui/connect-destination.md) este destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Name]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Description]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Account Type]**: AdWords é a única opção disponível.
* **[!UICONTROL Account ID]**: preencha sua ID de conta com [!DNL Google Ads]. Normalmente, o formato de ID é 123-456-7890.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados de público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

## Dados exportados

Para verificar se os dados foram exportados com êxito para o destino [!DNL Google Ads], verifique sua conta [!DNL Google Ads]. Se a ativação for bem-sucedida, os públicos-alvo serão preenchidos na conta.

## Resolução de problemas {#troubleshooting}

### 400 Mensagem de erro de solicitação incorreta {#bad-request}

Ao configurar esse destino, você pode receber o seguinte erro:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Este erro ocorre quando as contas de clientes não atendem aos [pré-requisitos](#prerequisites) ou quando os clientes tentam configurar o destino sem uma conta existente do [!DNL Google Ads].

[!DNL Google] substituiu novas [!DNL Google Ads] integrações de cookies com fornecedores de terceiros. Para executar as etapas [incluir na lista de permissões](#allow-listing), é necessário ter uma integração existente com [!DNL Google Ads].

A abordagem recomendada para o uso do [!DNL Google Ads] é configurar uma integração do [[!DNL Google Customer Match]](google-customer-match.md).
