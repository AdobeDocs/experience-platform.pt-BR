---
keywords: publicidade; bing;
title: Conexão com o Microsoft Bing
description: Com o destino da conexão do Microsoft Bing, você pode executar campanhas digitais direcionadas por público e redirecionamento em toda a Microsoft Advertising Network, incluindo Publicidade de exibição, Pesquisa e Nativo.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: b282dbae9131e0d2acdcd999d57f2e08b0bd7810
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 5%

---

# [!DNL Microsoft Bing] conexão {#bing-destination}

## Visão geral {#overview}


>[!IMPORTANT]
>
>Após uma atualização interna para o serviço de destinos a partir de agosto de 2025, você pode enfrentar uma **queda no número de perfis ativados** em seus fluxos de dados para [!DNL Microsoft Bing].
>
> Esta queda é causada pela introdução do **requisito de mapeamento ECID** para todas as ativações nesta plataforma de destino. Consulte a seção [mapeamento obrigatório](#mandatory-mappings) nesta página para obter informações detalhadas.
>
>**O que mudou:**
>
>* O mapeamento ECID (Experience Cloud ID) agora é **obrigatório** para todas as ativações de perfil.
>* Perfis sem mapeamento ECID serão **descartados** dos fluxos de dados de ativação existentes.
>
>**O que é necessário fazer:**
>
>* Analise seus dados de público-alvo para confirmar se os perfis têm valores ECID válidos.
>* Monitore suas métricas de ativação para verificar as contagens esperadas de perfis.

Use o destino [!DNL Microsoft Bing] para enviar dados de perfil para todo o [!DNL Microsoft Advertising Network], incluindo [!DNL Display Advertising], [!DNL Search] e [!DNL Native].

O destino [!DNL Microsoft Bing] cria *[!DNL Custom Audiences]* no Microsoft. Eles estão disponíveis no [!DNL Microsoft Search Network] e [!DNL Audience Network] ([!DNL Native] /[!DNL Display] /[!DNL Programmatic]), conforme listados na [documentação do Microsoft Advertising](https://help.ads.microsoft.com/#apex/ads/en/56892/1-500).

Para enviar dados de perfil para [!DNL Microsoft Bing], primeiro você deve se conectar ao destino.

## Casos de uso {#use-cases}

Como profissional de marketing, quero poder usar públicos criados a partir do [!DNL Microsoft Advertising IDs] para direcionar usuários por meio de publicidade de exibição ou pesquisa nos canais [!DNL Microsoft Advertising].

## Identidades suportadas {#supported-identities}

O [!DNL Microsoft Bing] dá suporte à ativação de públicos com base nas identidades mostradas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade | Descrição |
|---|---|
| EMPREGADA | MICROSOFT ADVERTISING ID |
| ECID | Experience Cloud ID. Essa identidade é obrigatória para que a integração funcione corretamente, mas não é usada para ativação de público-alvo. |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Uploads personalizados | ✓ | Públicos [importados](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

**[!DNL Audience Export]** - você está exportando todos os membros de um público para o destino [!DNL Microsoft Bing].

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Audience export]** | Você está exportando todos os membros de um público para o destino [!DNL Microsoft Bing]. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Pré-requisitos {#prerequisites}

>[!IMPORTANT]
>
>Se você deseja criar seu primeiro destino com o [!DNL Microsoft Bing] e não habilitou a [funcionalidade de sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) no Serviço da Experience Cloud ID no passado (com o Adobe Audience Manager ou outros aplicativos), entre em contato com a Adobe Consulting ou com o Atendimento ao cliente para habilitar as sincronizações de ID. Se você tiver configurado anteriormente as integrações do [!DNL Microsoft Bing] no Audience Manager, as sincronizações de ID configuradas serão transferidas para o Experience Platform.

Ao configurar o destino, você deve fornecer as seguintes informações:

* [!UICONTROL Account ID]: este é o seu [!DNL Bing Ads CID], em formato inteiro.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Preencher detalhes do destino {#parameters}

Ao [configurar](../../ui/connect-destination.md) este destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Name]**: Um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Description]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL Account ID]**: Seu [!DNL Bing Ads Customer ID] (CID). Sua CID é um número inteiro, encontrado na URL quando você faz login em [!DNL Microsoft Advertising].

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="ID de mapeamento"
>abstract="Insira a ID de público-alvo numérica do Bing para a qual deseja mapear o segmento selecionado. Se o [!UICONTROL Mapping ID] fornecido não corresponder a uma ID de público-alvo no destino do Bing, você não verá os dados do público-alvo esperados na sua conta do Bing."

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_bing"
>title="Conjuntos de mapeamento pré-configurados"
>abstract="Pré-configuramos esses dois conjuntos de mapeamento para você. Quando você ativa dados no Microsoft Bing, os perfis qualificados para os públicos ativados devem ter pelo menos uma identidade ECID associada ao perfil para serem exportados com êxito para o destino."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/advertising/bing#preconfigured-mappings" text="Leia mais sobre os mapeamentos pré-configurados"

>[!IMPORTANT]
> 
>Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados de público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

Na etapa [Agenda de público-alvo](../../ui/activate-segment-streaming-destinations.md#scheduling), mapeie manualmente o nome do público-alvo no campo [!UICONTROL Mapping ID]. Isso garante que os metadados de público sejam passados corretamente para [!DNL Bing].

![Imagem da interface do usuário mostrando a tela de agendamento de público-alvo com um exemplo de como mapear o nome do público-alvo para a ID de Mapeamento do Bing.](../../assets/catalog/advertising/bing/mapping-id.png)

### Mapeamentos obrigatórios {#mandatory-mappings}

Todas as identidades de destino descritas na seção [identidades com suporte](#supported-identities) são obrigatórias e devem ser mapeadas durante o processo de ativação do público-alvo. Isso inclui:

* **MULHER** (Microsoft Advertising ID)
* **ECID** (Experience Cloud ID)

A falha no mapeamento de todas as identidades necessárias impede a conclusão do fluxo de trabalho de ativação. Cada identidade serve a um propósito específico na integração e todas são necessárias para que o destino funcione corretamente.

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para o destino [!DNL Microsoft Bing], verifique sua conta [!DNL Microsoft Bing Ads]. Se a ativação for bem-sucedida, os públicos-alvo serão preenchidos na conta.
