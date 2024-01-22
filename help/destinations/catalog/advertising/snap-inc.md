---
title: Conexão Snap Inc
description: Saiba como se conectar à plataforma Snapchat Ads e exportar seus públicos do Experience Platform.
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 2%

---

# Conexão Snap Inc

## Visão geral {#overview}

[Anúncios do Snapchat](https://forbusiness.snapchat.com/) são feitos para cada empresa, independentemente do tamanho ou setor. Torne-se parte das conversas diárias do Snapchatters com anúncios digitais em tela cheia que inspiram a ação das pessoas mais importantes para sua empresa.

>[!IMPORTANT]
>
>Esse conector de destino e a página de documentação são criados e mantidos pelo *Snap Inc* equipe. Para qualquer consulta ou solicitação de atualização, entre em contato diretamente em *dev-support@snap.com*

## Casos de uso {#use-cases}

Esse destino permite que os profissionais de marketing importem públicos-alvo de usuários criados no Experience Platform para o Snapchat Ads e os usem para direcionar seus anúncios.

## Pré-requisitos {#prerequisites}

Para usar este destino, você precisa ter uma conta do Snapchat Ads. Consulte esta documentação para obter informações sobre como criar um:

[Introdução à Snapchat Advertising](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## Limitações {#limitations}

* A Snap Inc não oferece suporte a várias identidades para um determinado segmento de público-alvo. Mapeie apenas uma identidade ao ativar um segmento.
* O Snap Inc não oferece suporte à renomeação de segmentos. Para renomear um segmento, você deve desativá-lo, renomeá-lo e ativá-lo.
* Não é possível definir um período de retenção para os membros de um segmento de público-alvo. Todos os membros têm retenção de duração e estarão no público-alvo até serem removidos.

## Identidades suportadas {#supported-identities}

A variável *Snap Inc* o destino oferece suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

Todos os identificadores enviados para o *Snap Inc* o destino deve ter hash no formato SHA-256. Para aplicar hash a identificadores de texto sem formatação antes de enviá-los para o destino, verifique **[!UICONTROL Aplicar transformação]** ao mapear identificadores de destino para o destino.

>[!WARNING]
> 
> Identificadores sem hash não serão aceitos pelo destino Snap Inc e enviá-los pode causar erros.


>[!IMPORTANT]
> 
> O destino Snap Inc não é compatível com várias identidades. Selecione apenas uma identidade.

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| Endereço de email | Endereço de email com hash SHA-256 | Mapear endereços de email no campo de identidade de destino *emailAddress*. |
| Número de telefone | Número de telefone com hash SHA-256 | Mapear endereços de email no campo de identidade de destino *phoneNumber*. |
| GAID | ID de publicidade do Google com hash SHA-256 | Mapear IDs de publicidade do Google no campo de identidade de destino *gaid*. |
| IDFA | ID de publicidade do Apple com hash SHA-256 | Mapear IDs de publicidade do Apple no campo de identidade de destino *idfa*. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportação de público]** | Você está exportando todos os membros de um público-alvo com os identificadores (nome, número de telefone ou outros) usados no *SEUDESTINO* destino. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexão com a Snap Inc {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Exibir destinos]** e **[!UICONTROL Gerenciar destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, siga estas etapas:

1. Localize o *Snap Inc* destino no Catálogo de destino do Adobe Experience Platform e selecione **Configurar**.
2. Selecionar **[!UICONTROL Conectar ao destino]**. Você será redirecionado para a seguinte tela:
   ![Tela de Autenticação 1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. Insira suas credenciais do Snapchat e selecione **Fazer logon**.
4. Você verá os dados do Snapchat que o Adobe Experience Platform poderá acessar. Selecionar **Continuar** para continuar com o processo de conexão.

![Tela de Autenticação 2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

Depois de selecionar continuar, aguarde até ser redirecionado de volta para o Adobe Experience Platform.

### Preencher detalhes do destino {#destination-details}

![Detalhes do destino](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

Para configurar detalhes para o destino, preencha os campos obrigatórios e selecione **[!UICONTROL Próxima]**.

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL ID da conta]**: a ID da conta de anúncio associada à conta de anúncio para a qual você desejará importar os públicos. Para obter mais informações sobre como encontrar isso, consulte [esta documentação está disponível no Snapchat Business Help Center](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>Inserir uma ID de conta de anúncio do Snapchat incorreta ou inválida causará falha na ativação do público-alvo. Verifique se você inseriu a ID da conta de anúncio correta.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar os dados, é necessário **[!UICONTROL Exibir destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}

Ler [Ativar perfis e públicos para destinos de exportação de público de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

## Validar exportação de dados {#exported-data}

Depois de ativar os públicos-alvo para a variável *Snap Inc* destino, você poderá ver os públicos-alvo no Gerenciador de anúncios do Snap [**Públicos-alvo** seção](https://businesshelp.snapchat.com/s/article/audience-sharing). Para navegar até esta seção, siga estas etapas:

1. Faça logon na [Gerenciador de anúncios instantâneos](https://ads.snapchat.com/)
2. Selecionar **Públicos-alvo** no menu suspenso no canto superior esquerdo da tela. Você verá os públicos ativados no Adobe Experience Platform na Biblioteca de público-alvo:

![Públicos-alvo](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

Observe que, quando um público-alvo Adobe é ativado pela primeira vez para a Snap Inc, você o verá inicialmente como um público-alvo vazio. Isso ocorre porque a Adobe Experience Platform não exporta dados de membros para a Snap Inc até avaliar o público-alvo. Para obter mais informações sobre como os públicos-alvo são avaliados em Experience Platform, consulte [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html#evaluate-segments).

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte o [Visão geral da governança de dados](/help/data-governance/home.md).
