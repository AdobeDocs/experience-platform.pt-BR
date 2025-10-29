---
title: Conexão Snap Inc
description: Saiba como se conectar à plataforma Snapchat Ads e exportar seus públicos do Experience Platform.
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 2%

---

# Conexão Snap Inc

## Visão geral {#overview}

[Anúncios do Snapchat](https://forbusiness.snapchat.com/) são feitos para todas as empresas, independentemente do tamanho ou setor. Torne-se parte das conversas diárias do Snapchatters com anúncios digitais em tela cheia que inspiram a ação das pessoas mais importantes para sua empresa.

>[!IMPORTANT]
>
>Este conector de destino e a página de documentação são criados e mantidos pela equipe do *Snap Inc*. Para qualquer consulta ou solicitação de atualização, contate-os diretamente em *dev-support@snap.com*

## Casos de uso {#use-cases}

Esse destino permite que os profissionais de marketing importem públicos-alvo de usuários criados no Experience Platform para o Snapchat Ads e os usem para direcionar seus anúncios.

## Pré-requisitos {#prerequisites}

Para usar este destino, você precisa ter uma conta do Snapchat Ads. Consulte esta documentação para obter informações sobre como criar um:

[Introdução ao Snapchat Advertising](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## Limitações {#limitations}

* A Snap Inc não oferece suporte a várias identidades para um determinado segmento de público-alvo. Mapeie apenas uma identidade ao ativar um segmento.
* O Snap Inc não oferece suporte à renomeação de segmentos. Para renomear um segmento, você deve desativá-lo, renomeá-lo e ativá-lo.
* Não é possível definir um período de retenção para os membros de um segmento de público-alvo. Todos os membros têm retenção de duração e estarão no público-alvo até serem removidos.

## Identidades suportadas {#supported-identities}

O destino *Snap Inc* dá suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

Todos os identificadores enviados para o destino *Snap Inc* devem ter hash no formato SHA-256. Para aplicar hash a identificadores de texto sem formatação antes de enviá-los ao destino, marque a opção **[!UICONTROL Apply transformation]** ao mapear identificadores de destino para o destino.

>[!WARNING]
> 
> Identificadores sem hash não serão aceitos pelo destino Snap Inc e enviá-los pode causar erros.


>[!IMPORTANT]
> 
> O destino Snap Inc não é compatível com várias identidades. Selecione apenas uma identidade.

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| Endereço de e-mail | Endereço de email com hash SHA-256 | Mapeie endereços de email para o campo de identidade de destino *emailAddress*. |
| Número de telefone | Número de telefone com hash SHA-256 | Mapeie endereços de email para o campo de identidade de destino *phoneNumber*. |
| GAID | ID de Advertising do Google com hash SHA-256 | Mapeie as IDs do Google Advertising no campo de identidade de destino *gaid*. |
| IDFA | ID de Advertising do Apple com hash SHA-256 | Mapeie as IDs do Apple Advertising no campo de identidade de destino *idfa*. |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Uploads personalizados | ✓ | Públicos [importados](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |
| [!DNL Federated Audience Composition] | ✓ | Públicos importados para o Experience Platform por meio da [Federated Audience Composition](https://experienceleague.adobe.com/pt-br/docs/federated-audience-composition/using/start/audiences). |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Audience export]** | Você está exportando todos os membros de um público-alvo com os identificadores (nome, número de telefone ou outros) usados no destino Snap Inc. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexão com a Snap Inc {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, siga estas etapas:

1. Localize o destino *Snap Inc* no Catálogo de Destino da Adobe Experience Platform e selecione **Configurar**.
2. Selecione **[!UICONTROL Connect to destination]**. Você será redirecionado para a seguinte tela:
   ![Tela de Autenticação 1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. Insira suas credenciais do Snapchat e selecione **Fazer Logon**.
4. Você verá os dados do Snapchat que o Adobe Experience Platform poderá acessar. Selecione **Continuar** para continuar com o processo de conexão.

![Tela de Autenticação 2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

Depois de selecionar continuar, aguarde até ser redirecionado de volta para o Adobe Experience Platform.

### Preencher detalhes do destino {#destination-details}

![Detalhes do destino](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

Para configurar detalhes para o destino, preencha os campos obrigatórios e selecione **[!UICONTROL Next]**.

* **[!UICONTROL Name]**: Um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Description]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL Account ID]**: a ID da conta de anúncio associada à conta de anúncio para a qual você gostaria de importar seus públicos. Para obter mais informações sobre como encontrar, consulte [esta documentação no Centro de Ajuda Comercial do Snapchat](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>Inserir uma ID de conta de anúncio do Snapchat incorreta ou inválida causará falha na ativação do público-alvo. Verifique se você inseriu a ID da conta de anúncio correta.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar perfis e públicos-alvo para destinos de exportação de público-alvo de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

## Validar exportação de dados {#exported-data}

Depois de ativar os públicos-alvo para o destino *Snap Inc*, você poderá ver os públicos-alvo na seção [**Públicos-alvo** do Gerenciador de Snap Ads](https://businesshelp.snapchat.com/s/article/audience-sharing). Para navegar até esta seção, siga estas etapas:

1. Faça logon no [Gerenciador de Snap Ads](https://ads.snapchat.com/)
2. Selecione **Públicos-alvo** no menu suspenso no canto superior esquerdo da tela. Você verá os públicos ativados no Adobe Experience Platform na Biblioteca de público-alvo:

![Públicos-alvo](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

Observe que, quando um público-alvo do Adobe é ativado pela primeira vez para a Snap Inc, você o verá inicialmente como um público-alvo vazio. Isso ocorre porque a Adobe Experience Platform não exporta dados de membros para a Snap Inc até avaliar o público-alvo. Para obter mais informações sobre como os públicos-alvo são avaliados no Experience Platform, consulte a [visão geral do Serviço de segmentação](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=pt-BR#evaluate-segments).

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] impõe a governança de dados, consulte a [visão geral da Governança de Dados](/help/data-governance/home.md).
