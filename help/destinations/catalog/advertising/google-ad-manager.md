---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager; DFP
title: Conexão com o Google Ad Manager
description: O Google Ad Manager, anteriormente conhecido como DoubleClick for Publishers ou DoubleClick AdX, é uma plataforma de veiculação de anúncios da Google que fornece aos editores os meios para gerenciar a exibição de anúncios em seus sites, por meio de vídeos e aplicativos móveis.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: c4169d9371d329e445db7c83820b870ccbba238b
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 5%

---

# [!DNL Google Ad Manager] conexão

## Visão geral {#overview}

[!DNL Google Ad Manager], anteriormente conhecido como [!DNL DoubleClick for Publishers] (DFP) [!DNL DoubleClick AdX], é uma plataforma de veiculação de anúncios do [!DNL Google] que oferece aos editores os meios para gerenciar a exibição de anúncios em seus sites, por meio de vídeo e em aplicativos móveis.

## Especificações do destino {#specifics}

Observe os seguintes detalhes, específicos do [!DNL Google Ad Manager] Destinos:

* Os públicos ativados são criados programaticamente no [!DNL Google] plataforma.
* [!DNL Platform] no momento, o não inclui uma métrica de medição para validar a ativação bem-sucedida. Consulte as contagens de público no Google para validar a integração e entender o tamanho do direcionamento de público.
* Depois de mapear um público-alvo para um [!DNL Google Ad Manager] destino, o nome do público-alvo aparece imediatamente no campo [!DNL Google Ad Manager] interface do usuário.
* A população do segmento precisa de 24 a 48 horas para ser exibida no [!DNL Google Ad Manager]. Além disso, para serem exibidos no [!DNL Google Ad Manager]. Públicos-alvo com tamanhos menores do que 50 perfis não serão preenchidos em [!DNL Google Ad Manager].

## Identidades suportadas {#supported-identities}

[!DNL Google Ad Manager] O oferece suporte à ativação de públicos com base nas identidades mostradas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade | Descrição | Considerações |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| UUID AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), também conhecido como [!DNL Device ID]. Uma ID numérica de dispositivo de 38 dígitos que o Audience Manager associa a cada dispositivo com o qual interage. | O Google usa [UUID AAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) para direcionar usuários na Califórnia e a Google Cookie ID para todos os outros usuários. |
| [!DNL Google] ID do cookie | [!DNL Google] ID do cookie | [!DNL Google] O usa essa ID para direcionar usuários fora da Califórnia. |
| RIDA | ID do Roku para publicidade. Essa ID identifica exclusivamente dispositivos Roku. |  |
| EMPREGADA | ID de publicidade da Microsoft. Esta ID identifica exclusivamente os dispositivos que executam o Windows 10. |  |
| ID do Amazon Fire TV | Esta ID identifica exclusivamente as TVs Amazon Fire. |  |

{style="table-layout:auto"}

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

{style="table-layout:auto"}

## Pré-requisitos {#prerequisites}

Se você deseja criar seu primeiro destino com o [!DNL Google Ad Manager] e não ativaram o [Funcionalidade de sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) no Serviço de ID de Experience Cloud anterior (com Audience Manager ou outros aplicativos), entre em contato com a Consultoria de Adobe ou com o Atendimento ao cliente para ativar as sincronizações de ID. Se você já configurou o [!DNL Google] integrações no Audience Manager, as sincronizações de ID configuradas para serem transferidas para a Platform.

### Incluir na lista de permissões {#allow-listing}

A inclusão na lista de permissões é obrigatória antes de configurar o primeiro [!DNL Google Ad Manager] destino na Platform. Conclua o processo de inclusão na lista de permissões descrito abaixo antes de criar seu destino.

1. Siga as etapas descritas na seção [Documentação do Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=en) para adicionar o Adobe como uma Plataforma de gerenciamento de dados (DMP) vinculada.
2. No [!DNL Google Ad Manager] , vá para **[!UICONTROL Admin]** > **[!UICONTROL Configurações globais]** > **[!UICONTROL Configurações de rede]** e habilite o **[!UICONTROL Acesso à API]** controle deslizante.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="Anexar ID de público-alvo ao nome do público-alvo"
>abstract="Selecione essa opção para que o nome do público-alvo no Google Ad Manager inclua a ID do público-alvo da Experience Platform, assim: `Audience Name (Audience ID)`"

Enquanto [configuração](../../ui/connect-destination.md) Para esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: Preencha o nome preferencial para este destino.
* **[!UICONTROL Descrição]**: Opcional. Por exemplo, você pode mencionar para qual campanha está usando esse destino.
* **[!UICONTROL ID da conta]**: Insira seu [!DNL Audience Link ID] do seu [!DNL Google] conta. Esse é um identificador específico associado à [!DNL Google Ad Manager] rede (não a sua [!DNL Network code]). Você pode encontrar isso em **[!UICONTROL Administração > Configurações globais]** no [!DNL Google Ad Manager] interface.
* **[!UICONTROL Tipo de conta]**: selecione uma opção, dependendo da sua conta com o Google:
   * Uso `DFP by Google` para [!DNL DoubleClick] para editores
   * Uso `AdX buyer` para [!DNL Google AdX]
* **[!UICONTROL Anexar ID de público-alvo ao nome do público-alvo]**: selecione esta opção para que o nome do público-alvo no Google Ad Manager inclua a ID de público-alvo do Experience Platform, desta forma: `Audience Name (Audience ID)`.

>[!NOTE]
>
>Ao configurar um [!DNL Google Ad Manager] destino, trabalhe com seu [!DNL Google Account Manager] ou representante da Adobe para saber qual tipo de conta você tem.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados do público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para o [!DNL Google Ad Manager] destino, verifique seu [!DNL Google Ad Manager] conta. Se a ativação for bem-sucedida, os públicos-alvo serão preenchidos na conta.

## Solução de problemas {#troubleshooting}

Caso encontre erros ao usar esse destino e precise entrar em contato com o Adobe ou o Google, mantenha as seguintes IDs à mão.

Estas são as IDs de conta do Adobe Google:

* **[!UICONTROL ID da conta]**: 87933855
* **[!UICONTROL ID do cliente]**: 89690775