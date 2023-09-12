---
keywords: publicidade; bing;
title: Conexão com o Microsoft Bing
description: Com o destino da conexão do Microsoft Bing, você pode executar redirecionamento e campanhas digitais direcionadas por público em toda a Rede de publicidade da Microsoft, incluindo Publicidade de exibição, Pesquisa e Nativo.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 093ddd1651e15bebf73d007fb05042fbcf02c675
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 8%

---

# Conexão com o [!DNL Microsoft Bing] {#bing-destination}

## Visão geral {#overview}

Use o [!DNL Microsoft Bing] destino para enviar dados de perfil a todo o [!DNL Microsoft Advertising Network], incluindo [!DNL Display Advertising], [!DNL Search], e [!DNL Native].

A variável [!DNL Microsoft Bing] o destino cria *[!DNL Custom Audiences]* no Microsoft. Estes estão disponíveis tanto no [!DNL Microsoft Search Network] e [!DNL Audience Network] ([!DNL Native] /[!DNL Display] /[!DNL Programmatic]), conforme indicado na [Documentação da Microsoft Advertising](https://help.ads.microsoft.com/#apex/ads/en/56892/1-500).

Para enviar dados de perfil para [!DNL Microsoft Bing], você deve primeiro se conectar ao destino.

## Casos de uso {#use-cases}

Como profissional de marketing, quero poder usar públicos-alvo criados com o [!DNL Microsoft Advertising IDs] para direcionar usuários por meio de publicidade de exibição ou pesquisa em [!DNL Microsoft Advertising] canais.

## Identidades suportadas {#supported-identities}

[!DNL Microsoft Bing] O oferece suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade de destino | Descrição |
|---|---|
| EMPREGADA | ID de publicidade do Microsoft |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve que tipo de público-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md). |
| Uploads personalizados | ✓ | Públicos-alvo [importado](../../../segmentation/ui/overview.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

**[!DNL Audience Export]** - você estiver exportando todos os membros de um público-alvo para a [!DNL Microsoft Bing] destino.

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportação de público]** | Você está exportando todos os membros de um público-alvo para a [!DNL Microsoft Bing] destino. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Pré-requisitos {#prerequisites}

>[!IMPORTANT]
>
>Se você deseja criar seu primeiro destino com o [!DNL Microsoft Bing] e não ativaram o [Funcionalidade de sincronização de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) no Serviço de ID de Experience Cloud no passado (com o Adobe Audience Manager ou outros aplicativos), entre em contato com a Consultoria de Adobe ou com o Atendimento ao cliente para ativar as sincronizações de ID. Se você já configurou o [!DNL Microsoft Bing] integrações no Audience Manager, as sincronizações de ID configuradas para serem transferidas para a Platform.

Ao configurar o destino, você deve fornecer as seguintes informações:

* [!UICONTROL ID da conta]: este é o seu [!DNL Bing Ads CID], em formato inteiro.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Preencher detalhes do destino {#parameters}

Enquanto [configuração](../../ui/connect-destination.md) Para esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL ID da conta]**: Seu [!DNL Bing Ads Customer ID] (CID). Sua CID é um número inteiro, encontrado no URL quando você faz logon no [!DNL Microsoft Advertising].

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos para este destino {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="ID de mapeamento"
>abstract="Insira a ID de público-alvo numérica do Bing para a qual deseja mapear o segmento selecionado. Se a [!UICONTROL ID de mapeamento] fornecida não corresponder a uma ID de público-alvo no destino do Bing, você não verá os dados de público-alvo esperados na sua conta do Bing."

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados do público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

No [Programação de público](../../ui/activate-segment-streaming-destinations.md#scheduling) etapa, você deve mapear manualmente o nome do público-alvo na [!UICONTROL ID do mapeamento] campo. Isso garante que os metadados do público-alvo sejam transmitidos corretamente para o [!DNL Bing].

![Imagem da interface do usuário mostrando a tela de agendamento de público-alvo com um exemplo de como mapear o nome do público-alvo para a ID de mapeamento do Bing.](../../assets/catalog/advertising/bing/mapping-id.png)

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para o [!DNL Microsoft Bing] destino, verifique seu [!DNL Microsoft Bing Ads] conta. Se a ativação for bem-sucedida, os públicos-alvo serão preenchidos na conta.
