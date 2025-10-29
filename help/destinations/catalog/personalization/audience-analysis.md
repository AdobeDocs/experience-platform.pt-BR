---
title: Destino da Análise de público-alvo
description: Visualize públicos para os quais os clientes se qualificam no Customer Journey Analytics.
badgeLimitedAvailability: label="Disponibilidade limitada" type="Informative"
exl-id: 81437237-d746-4ce9-b938-7d2541f0ed32
hide: true
hidefromtoc: true
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 3%

---

# Destino da Análise de público-alvo

O destino [!UICONTROL Audience Analysis] permite enriquecer os dados de público-alvo do Adobe Experience Platform no [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=pt-BR). Você pode selecionar quais públicos-alvo deseja incluir nos dados enriquecidos resultantes. As qualificações de público-alvo estão disponíveis como dimensões nos relatórios do [Analysis Workspace](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/home.html?lang=pt-BR).

>[!AVAILABILITY]
>
>Esse destino está em uma fase de teste limitada. Se estiver interessado em usar esse destino, entre em contato com a equipe de conta da Adobe.

## Pré-requisitos

São necessários os seguintes itens antes de usar este destino:

* Você deve estar provisionado para usar o destino da Análise de público-alvo. Se você ainda não tiver sido provisionado para usar esse destino, entre em contato com a equipe de conta da Adobe.
* Você deve ser provisionado para usar o Customer Journey Analytics.
* Você deve ter pelo menos um público-alvo criado no Adobe Experience Platform.

## Identidades suportadas

A Análise de público-alvo é compatível com a ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md). A Experience Cloud ID (ECID) geralmente é usada.

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Selecione a identidade de destino GAID quando a identidade de origem for um namespace GAID. |
| IDFA | Apple ID para anunciantes | Selecione a identidade de destino do IDFA quando a identidade de origem for um namespace do IDFA. |
| ECID | Experience Cloud ID | Um namespace que representa a ECID. Esse namespace também pode ser referenciado pelos seguintes aliases: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte o seguinte documento no [ECID](/help/identity-service/features/ecid.md) para obter mais informações. |
| phone_sha256 | Números de telefone com hash com o algoritmo SHA256 | Os números de telefone com hash SHA256 e texto sem formatação são compatíveis com o Adobe Experience Platform. Quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Apply transformation]** para que o [!DNL Experience Platform] coloque os dados em hash automaticamente durante a ativação. |
| email_lc_sha256 | Endereços de email com hash com o algoritmo SHA256 | O Adobe Experience Platform oferece suporte tanto para texto simples quanto para endereços de email com hash SHA256. Quando o campo de origem contiver atributos sem hash, marque a opção **[!UICONTROL Apply transformation]** para que o [!DNL Experience Platform] coloque os dados em hash automaticamente durante a ativação. |
| extern_id | IDs de usuário personalizadas | Selecione esta identidade de destino quando sua identidade de origem for um namespace personalizado. |

{style="table-layout:auto"}

## Públicos-alvo compatíveis

Os seguintes tipos de público-alvo são compatíveis ao usar esse destino:

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Uploads personalizados | ✓ | Públicos [importados](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Audience export]** | Você está exportando todos os membros de um público-alvo com os identificadores (nome, número de telefone ou outros) usados no destino da Análise de público-alvo. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Quando um perfil é atualizado no Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Configurar novo destino

>[!IMPORTANT]
> 
>Para criar um destino, você precisa da **[!UICONTROL View Destinations]** e da **[!UICONTROL Manage Destinations]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para criar esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Detalhes do destino

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Name]**: O nome do destino.
* **[!UICONTROL Description]**: a descrição do destino.
* **[!UICONTROL Datastream ID]**: a ID da sequência de dados que você deseja enriquecer com públicos qualificados. Você pode obter essa ID no [gerenciador de fluxos de dados](/help/datastreams/overview.md).
* **[!UICONTROL Integration alias]**: o alias de integração.

### Alertas

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

* **[!UICONTROL Activation Skipped Rate Exceed]**: Ser notificado quando a taxa de ativação ignorada exceder um limite.

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

### Política de governação e medidas de aplicação

Esta seção opcional permite definir suas políticas de governança de dados e garantir que os dados usados estejam em conformidade quando os públicos-alvo forem enviados e estiverem ativos.

Quando terminar de selecionar as ações de marketing desejadas para o destino, selecione **[!UICONTROL Create]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Depois que o destino for criado, você poderá ativar os públicos-alvo desejados para o destino.

1. Se você ainda não estiver no destino criado, poderá localizá-lo novamente navegando até **[!UICONTROL Destinations]** > **[!UICONTROL Browse]**.
1. Selecione **[!UICONTROL Activate audiences]**.
1. Selecione os públicos-alvo desejados para os quais deseja analisar qualificações. Quando terminar, selecione **[!UICONTROL Next]**.
1. Revise a configuração de destino e as configurações de público e selecione **[!UICONTROL Finish]**.

Você pode adicionar mais públicos para analisar no futuro navegando de volta para a página **[!UICONTROL Activate audiences]**. Não é possível remover públicos-alvo depois de ativados.
