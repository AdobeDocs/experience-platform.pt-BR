---
title: (Beta) Conexão do Snap Inc
description: Saiba como se conectar à Plataforma de anúncios do Snapchat e exportar seus segmentos de público-alvo do Experience Platform.
source-git-commit: 734d66cc881ab1b691c13ef446331d0c51851cf9
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 2%

---


# (Beta) Snap Inc

## Visão geral {#overview}

[Anúncios de Snapchat](https://forbusiness.snapchat.com/) são feitas para todas as empresas, independentemente do tamanho ou da indústria. Torne-se parte das conversas diárias dos Snapchatters com anúncios digitais em tela inteira que inspiram ação das pessoas mais importantes para sua empresa.

>[!IMPORTANT]
>
>Esta página de documentação foi criada pela *Snap Inc* equipe. No momento, esse é um produto beta e a funcionalidade está sujeita a alterações. Para quaisquer consultas ou pedidos de atualização, contacte-os diretamente em *dev-support@snap.com*

## Casos de uso {#use-cases}

Esse destino permite que os profissionais de marketing importem segmentos de usuários criados no Experience Platform para Snapchat Ads e os usem para direcionar seus anúncios.

## Pré-requisitos {#prerequisites}

Para usar esse destino, você deve ter uma conta Snapchat Ads. Consulte esta documentação para obter informações sobre como criar uma:

[Introdução à Publicidade em Snapchat](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## Limitações {#limitations}

* A Snap Inc não oferece suporte a várias identidades para um determinado segmento de público-alvo. Mapeie apenas uma identidade ao ativar um segmento.
* A Snap Inc não oferece suporte para renomear segmentos. Para renomear um segmento, você deve desativá-lo, renomeá-lo e ativá-lo.
* Não é possível definir um período de retenção para os membros de um segmento de público-alvo. Todos os membros têm retenção vitalícia e estarão no segmento até serem removidos.

## Identidades suportadas {#supported-identities}

O *Snap Inc* O destino oferece suporte à ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

Todos os identificadores enviados para a *Snap Inc* o destino deve ter hash no formato SHA-256. Para fazer hash de identificadores de texto simples antes de enviá-los para o destino, verifique a **[!UICONTROL Aplicar transformação]** ao mapear identificadores de destino para o destino.

>[!WARNING]
> 
> Os identificadores sem hash não serão aceitos pelo destino do Snap Inc e o seu envio pode causar erros.


>[!IMPORTANT]
> 
> O destino Snap Inc não oferece suporte a várias identidades. Selecione apenas uma identidade.

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| Endereço de email | Endereço de email com hash SHA-256 | Mapear endereços de email para o campo de identidade de destino *emailAddress*. |
| Número de telefone | Número de telefone com hash SHA-256 | Mapear endereços de email para o campo de identidade de destino *phoneNumber*. |
| GAID | SHA-256 ID de publicidade Google com hash | Mapear IDs de publicidade do Google para o campo de identidade do target *gaid*. |
| IDFA | SHA-256 ID de publicidade Apple com hash | Mapear IDs de publicidade do Apple para o campo de identidade do target *idfa*. |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportar segmento]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores (nome, número de telefone ou outros) usados na *SEU DESTINO* destino. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Conexão com a Snap Inc {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

### Autenticar para destino {#authenticate}

Para autenticar para o destino, siga estas etapas:

1. Encontre a *Snap Inc* destino do Catálogo de Destino da Adobe Experience Platform e selecione **Configurar**.
2. Selecionar **[!UICONTROL Ligar ao destino]**. Você será redirecionado para a seguinte tela:
   ![Tela de autenticação 1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. Insira suas credenciais do Snapchat e selecione **Fazer logon**.
4. Você verá os dados do Snapchat que o Adobe Experience Platform poderá acessar. Selecionar **Continuar** para prosseguir com o processo de conexão.

![Tela de autenticação 2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

Depois de selecionar continuar, aguarde até que você seja redirecionado de volta para o Adobe Experience Platform.

### Preencha os detalhes do destino {#destination-details}

![Detalhes do destino](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

Para configurar detalhes para o destino, preencha os campos obrigatórios e selecione **[!UICONTROL Próximo]**.

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL ID da conta]**: A ID da conta do anúncio associada à conta do anúncio para a qual você deseja importar os segmentos. Para obter mais informações sobre como encontrar isso, consulte [esta documentação no Snapchat Business Help Center](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>Inserir uma ID de conta de anúncio de Snapchat incorreta ou inválida causará falha na ativação do segmento. Verifique novamente se você inseriu a ID de conta de anúncio adequada.

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmentos de fluxo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Validar exportação de dados {#exported-data}

Depois de ativar os segmentos na *Snap Inc* como destino, você poderá ver os segmentos no gerenciador de anúncios do Snap [**Públicos-alvo** seção](https://businesshelp.snapchat.com/s/article/audience-sharing). Para navegar até esta seção, siga estas etapas:

1. Faça logon no [Gerenciador de anúncios do Snap](https://ads.snapchat.com/)
2. Selecionar **Públicos-alvo** no menu suspenso no canto superior esquerdo da tela. Você verá os segmentos ativados no Adobe Experience Platform na Biblioteca de público-alvo:

![Públicos-alvo](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

Observe que, quando um segmento Adobe é ativado pela primeira vez no Snap Inc, você o verá inicialmente como um público-alvo vazio. Isso ocorre porque a Adobe Experience Platform não exporta dados dos membros para a Snap Inc até que avalie o segmento. Para obter mais informações sobre como os segmentos são avaliados no Experience Platform, consulte o [Visão geral do serviço de segmentação](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=en#evaluate-segments).

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](/help/data-governance/home.md).