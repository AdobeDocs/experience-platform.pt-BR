---
keywords: Gerenciador de lances DoubleClick, Gerenciador de lances DoubleClick, DoubleClick, Display & Video 360, display 360, video 360, Video 360, Display 360, exibição e vídeo
title: Conexão Google Display & Video 360
description: Display & Video 360, anteriormente conhecido como DoubleClick Bid Manager, é uma ferramenta usada para executar campanhas digitais direcionadas para o público-alvo em fontes de inventário de Exibição, Vídeo e Dispositivo móvel.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: d0112cb26fcb85ad91ba403f81ee7f11d0889046
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 2%

---

# [!DNL Google Display & Video 360] conexão

## Visão geral {#overview}

[!DNL Display & Video 360], anteriormente conhecida como  [!DNL DoubleClick Bid Manager], é uma ferramenta usada para executar o redirecionamento e campanhas digitais direcionadas ao público-alvo em fontes de inventário de Exibição, Vídeo e Móvel.

## Especificações do destino {#specifics}

Observe os seguintes detalhes que são específicos para os destinos [!DNL Google Display & Video 360]:

* Públicos ativados são criados programaticamente na plataforma do Google.
* [!DNL Platform] atualmente não inclui uma métrica de medição para validar a ativação bem-sucedida. Consulte as contagens de público-alvo no Google para validar a integração e entender o tamanho do direcionamento de público-alvo.

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

## Pré-requisitos {#prerequisites}

### Lista de permissões

>[!NOTE]
>
>A lista de permissões é obrigatória antes de configurar seu primeiro destino [!DNL Google Display & Video 360] na Plataforma. Certifique-se de que o processo de lista de permissões descrito abaixo foi concluído pelo Google antes de criar um destino.

Antes de criar o destino [!DNL Google Display & Video 360] na Plataforma, você deve entrar em contato com o Google solicitando que o Adobe seja colocado na lista de provedores de dados permitidos e que sua conta seja adicionada à lista de permissões. Entre em contato com o Google e forneça as seguintes informações:

* **ID** da conta: ID da conta do Adobe com o Google. ID da conta: 87933855.
* **ID** do cliente: ID da conta do cliente do Adobe com o Google. ID do cliente: 89690775.
* **Seu tipo** de conta: use  **[!DNL Invite advertiser]** para permitir que os públicos-alvo sejam compartilhados somente com uma marca específica em sua conta do Display &amp; Video 360 ou use  **[!DNL Invite partner]** para permitir que os públicos-alvo sejam compartilhados com todas as marcas em sua conta do Display &amp; Video 360 .

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configurar](../../ui/connect-destination.md) esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Preencha o nome preferencial para esse destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL Tipo]** de conta: Selecione uma opção, dependendo de sua conta com o Google:
   * Use `Invite Advertiser` para permitir que os públicos-alvo sejam compartilhados somente com uma marca específica em sua conta do Display &amp; Video 360 .
   * Use `Invite Partner` para permitir que os públicos-alvo sejam compartilhados com todas as marcas em sua conta do Display &amp; Video 360.
* **[!UICONTROL ID]** da conta: Preencha a ID da  **[!DNL Invite partner]** conta do  **[!DNL Invite advertiser]** ou com o Google. Normalmente, essa é uma ID de seis ou sete dígitos.

>[!NOTE]
>
>Ao configurar um destino [!DNL Google Display & Video 360], trabalhe com seu [!DNL Google Account Manager] ou representante do Adobe para entender qual tipo de conta você tem.

## Ativar segmentos para este destino {#activate}

Consulte [Ativar os dados do público-alvo para os destinos de exportação de segmentos de fluxo](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino.

## Dados exportados

Para verificar se os dados foram exportados com êxito para o destino [!DNL Google Display & Video 360], verifique sua conta [!DNL Google Display & Video 360]. Se a ativação foi bem-sucedida, os públicos-alvo são preenchidos na sua conta.

## Solução de problemas {#troubleshooting}

### 400 Mensagem de erro de solicitação incorreta {#bad-request}

Ao configurar esse destino, você pode receber o seguinte erro:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Esse erro ocorre quando as contas do cliente não estão em conformidade com os [pré-requisitos](#prerequisites). Para corrigir esse problema, entre em contato com o Google e verifique se sua conta está incluída na lista de permissões.