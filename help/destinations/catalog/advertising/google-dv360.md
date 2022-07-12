---
keywords: Gerenciador de lances DoubleClick, Gerenciador de lances DoubleClick, DoubleClick, Display & Video 360, display 360, video 360, Video 360, Display 360, exibição e vídeo
title: Conexão Google Display & Video 360
description: Display & Video 360, anteriormente conhecido como DoubleClick Bid Manager, é uma ferramenta usada para executar campanhas digitais direcionadas para o público-alvo em fontes de inventário de Exibição, Vídeo e Dispositivo móvel.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 2%

---

# [!DNL Google Display & Video 360] conexão

## Visão geral {#overview}

[!DNL Display & Video 360], anteriormente conhecida como [!DNL DoubleClick Bid Manager], é uma ferramenta usada para executar o redirecionamento e campanhas digitais direcionadas ao público-alvo em fontes de inventário de Exibição, Vídeo e Dispositivo móvel .

## Especificações do destino {#specifics}

Observe os detalhes a seguir que são específicos para [!DNL Google Display & Video 360] Destinos:

* Públicos ativados são criados de forma programática na plataforma Google.
* [!DNL Platform] atualmente não inclui uma métrica de medição para validar a ativação bem-sucedida. Consulte as contagens de público-alvo no Google para validar a integração e entender o tamanho do direcionamento de público-alvo.

>[!IMPORTANT]
>
>Se você deseja criar seu primeiro destino com o Google Display &amp; Video 360 e não ativou o [Funcionalidade de sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) no Serviço de Experience Cloud ID no passado (com o Adobe Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para ativar as sincronizações de ID. Se você tinha configurado anteriormente as integrações do Google no Audience Manager, as sincronizações de ID que você havia configurado eram transferidas para a Platform.

## Identidades suportadas {#supported-identities}

[!DNL Google Display & Video 360] O suporta a ativação de identidades descritas na tabela abaixo.

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Selecione essa identidade de destino quando sua identidade de origem for um namespace GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Selecione essa identidade de destino quando sua identidade de origem for um namespace IDFA. |
| UUID do AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)também conhecido como [!DNL Device ID]. Uma ID de dispositivo numérica de 38 dígitos que o Audience Manager associa a cada dispositivo com o qual ele interage. | O Google usa [UUID do AAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) para direcionar usuários na Califórnia e a ID do cookie da Google para todos os outros usuários. |
| [!DNL Google] ID do cookie | [!DNL Google] ID do cookie | [!DNL Google] O usa essa ID para direcionar usuários fora da Califórnia. |
| RIDA | ID do Roku para publicidade. Essa ID identifica exclusivamente dispositivos Roku. |  |
| MAID | Microsoft Advertising ID. Esta ID identifica exclusivamente dispositivos que executam o Windows 10. |  |
| Amazon Fire TV ID | Essa ID identifica exclusivamente Amazon Fire TVs. |  |

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) para o destino do Google. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

## Pré-requisitos {#prerequisites}

### Lista de permissões {#allow-listing}

>[!NOTE]
>
>A lista de permissões é obrigatória antes da configuração da primeira [!DNL Google Display & Video 360] no Platform. Certifique-se de que o processo de inclusão na lista de permissões descrito abaixo foi concluído pela Google antes de criar um destino.

Antes de criar a [!DNL Google Display & Video 360] no Platform, você deve entrar em contato com a Google solicitando que o Adobe seja incluído na lista de provedores de dados permitidos e que sua conta seja adicionada à lista de permissões. Entre em contato com a Google e forneça as seguintes informações:

* **ID da conta**: ID da conta do Adobe com Google. ID da conta: 87933855.
* **Customer ID**: ID da conta do cliente do Adobe com Google. ID do cliente: 89690775.
* **Seu tipo de conta**: use **[!DNL Invite advertiser]** para permitir que os públicos-alvo sejam compartilhados somente com uma marca específica em sua conta do Display &amp; Video 360 ou use **[!DNL Invite partner]** para permitir que os públicos-alvo sejam compartilhados com todas as marcas em sua conta do Display &amp; Video 360 .

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Preencha o nome preferencial para esse destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Tipo de conta]**: Selecione uma opção, dependendo da sua conta com o Google:
   * Use `Invite Advertiser` para permitir que os públicos-alvo sejam compartilhados somente com uma marca específica em sua conta do Display &amp; Video 360 .
   * Use `Invite Partner` para permitir que os públicos-alvo sejam compartilhados com todas as marcas em sua conta do Display &amp; Video 360 .
* **[!UICONTROL ID da conta]**: Preencha o **[!DNL Invite partner]** ou **[!DNL Invite advertiser]** ID da conta com o Google. Normalmente, essa é uma ID de seis ou sete dígitos.

>[!NOTE]
>
>Ao configurar um [!DNL Google Display & Video 360] destino, trabalhe com seu [!DNL Google Account Manager] ou representante de Adobe para entender qual tipo de conta você tem.

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar os dados do público-alvo para os destinos de exportação do segmento de fluxo](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Dados exportados

Para verificar se os dados foram exportados com êxito para a [!DNL Google Display & Video 360] destino, verifique seu [!DNL Google Display & Video 360] conta. Se a ativação foi bem-sucedida, os públicos-alvo são preenchidos na sua conta.

## Solução de problemas {#troubleshooting}

### 400 Mensagem de erro de solicitação incorreta {#bad-request}

Ao configurar esse destino, você pode receber o seguinte erro:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Esse erro ocorre quando as contas do cliente não estão em conformidade com a [pré-requisitos](#prerequisites). Para corrigir esse problema, entre em contato com a Google e verifique se sua conta está incluída na lista de permissões.