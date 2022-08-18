---
keywords: google ad manager, google ad, doubleclick, DoubleClick AdX, DoubleClick, Google Ad Manager, Google ad manager; DFP
title: Conexão com o Google Ad Manager
description: O Google Ad Manager, anteriormente conhecido como DoubleClick for Publishers ou DoubleClick AdX, é uma plataforma de veiculação de anúncios da Google que oferece aos editores os meios de gerenciar a exibição de anúncios em seus sites, por meio de vídeos e aplicativos móveis.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 7d32499bec8d7248472ae60b07893dbb5496d984
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 3%

---

# [!DNL Google Ad Manager] conexão

## Visão geral {#overview}

[!DNL Google Ad Manager], anteriormente conhecida como [!DNL DoubleClick for Publishers] (DFP) ou [!DNL DoubleClick AdX], é uma plataforma de veiculação de anúncios do [!DNL Google] que oferece aos editores os meios de gerenciar a exibição de anúncios em seus sites, por meio de vídeos e aplicativos móveis.

## Especificações do destino {#specifics}

Observe os detalhes a seguir que são específicos para [!DNL Google Ad Manager] Destinos:

* Os públicos-alvo ativados são criados de forma programática no [!DNL Google] plataforma.
* [!DNL Platform] atualmente não inclui uma métrica de medição para validar a ativação bem-sucedida. Consulte as contagens de público-alvo no Google para validar a integração e entender o tamanho do direcionamento de público-alvo.

## Identidades suportadas {#supported-identities}

[!DNL Google Ad Manager] O suporta a ativação de identidades descritas na tabela abaixo.

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Selecione essa identidade de destino quando sua identidade de origem for um namespace GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Selecione essa identidade de destino quando sua identidade de origem for um namespace IDFA. |
| UUID do AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)também conhecido como [!DNL Device ID]. Uma ID de dispositivo numérica de 38 dígitos que o Audience Manager associa a cada dispositivo com o qual ele interage. | O Google usa [UUID do AAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) para direcionar usuários na Califórnia e a ID do cookie da Google para todos os outros usuários. |
| [!DNL Google] ID do cookie | [!DNL Google] ID do cookie | [!DNL Google] O usa essa ID para direcionar usuários fora da Califórnia. |
| RIDA | ID do Roku para publicidade. Essa ID identifica exclusivamente dispositivos Roku. |  |
| MAID | Microsoft Advertising ID. Esta ID identifica exclusivamente dispositivos que executam o Windows 10. |  |
| Amazon Fire TV ID | Essa ID identifica exclusivamente Amazon Fire TVs. |  |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) para o destino do Google. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Pré-requisitos {#prerequisites}

Se você deseja criar seu primeiro destino com [!DNL Google Ad Manager] e não ativou a variável [Funcionalidade de sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) no Serviço de Experience Cloud ID no passado (com o Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para ativar as sincronizações de ID. Se você já havia configurado [!DNL Google] integrações no Audience Manager, as sincronizações de ID que você configurou continuam para a Platform.

### Lista de permissões {#allow-listing}

>[!NOTE]
>
>A lista de permissões é obrigatória antes da configuração da primeira [!DNL Google Ad Manager] no Platform. Certifique-se de que o processo de inclusão na lista de permissões descrito abaixo foi concluído por [!DNL Google] antes de criar um destino.
>A exceção a esta regra é para [Audience Manager](https://docs.adobe.com/content/help/pt-BR/experience-cloud/user-guides/home.translate.html) clientes. Se você já criou uma conexão com esse destino Google no Audience Manager, não é necessário passar pelo processo de lista de permissões novamente e prosseguir para as próximas etapas.

Antes de criar a [!DNL Google Ad Manager] no Platform, você deve entrar em contato com [!DNL Google] para que o Adobe seja colocado na lista de provedores de dados permitidos e para que sua conta seja adicionada à lista de permissões. Contato [!DNL Google] e fornecer as seguintes informações:

* **ID da conta**: ID da conta do Adobe com Google. ID da conta: 87933855.
* **Customer ID**: ID da conta do cliente do Adobe com Google. ID do cliente: 89690775.
* **Código de rede**: Este é o seu [!DNL Google Ad Manager] identificador de rede, encontrado em **[!UICONTROL Administração > Configurações globais]** na interface do Google, bem como no URL.
* **ID do link de público-alvo**: Esse é um identificador específico associado ao [!DNL Google Ad Manager] rede (não sua [!DNL Network code]), também encontrado em **[!UICONTROL Administração > Configurações globais]** na interface do Google.
* Seu tipo de conta. DFP por Google ou comprador AdX.

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
   * Use `DFP by Google` para [!DNL DoubleClick] para editores
   * Use `AdX buyer` para [!DNL Google AdX]
* **[!UICONTROL ID da conta]**: Preencha a ID do link de público-alvo com [!DNL Google].

>[!NOTE]
>
>Ao configurar um [!DNL Google Ad Manager] destino, trabalhe com seu [!DNL Google Account Manager] ou representante de Adobe para entender qual tipo de conta você tem.

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar os dados do público-alvo para os destinos de exportação do segmento de fluxo](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para a [!DNL Google Ad Manager] destino, verifique seu [!DNL Google Ad Manager] conta. Se a ativação foi bem-sucedida, os públicos-alvo são preenchidos na sua conta.
