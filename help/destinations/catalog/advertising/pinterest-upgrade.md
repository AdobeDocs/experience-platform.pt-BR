---
title: Migração de destino do pinterest para a nova API. Ação do cliente necessária.
description: O pinterest está descontinuando a API do anunciante v4 usada atualmente pelo destino do Pinterest no Real-Time CDP. Entenda seus itens de ação para fazer a transição perfeita para a nova API sem interromper as campanhas do Pinterest.
hide: true
hidefromtoc: true
exl-id: c965235c-4208-4c28-9ac5-eb4c0061515d
source-git-commit: e3341ec6f62844858ecda7dd4db70d085f0bf217
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Atualização de destino do pinterest para a nova API. Ação do cliente necessária até 18 de janeiro de 2024.

>[!IMPORTANT]
>
>Os itens de ação do cliente nesta página se aplicam se sua organização tiver configurado fluxos de dados para exportar dados para o Pinterest antes de 16 de novembro de 2023, data em que o novo destino **[!UICONTROL Pinterest]**, usando a API mais recente do Pinterest, foi adicionado ao catálogo de destinos.

## O que está acontecendo?

O pinterest substituiu a API v4 do anunciante que foi usada pelo [destino do Pinterest](/help/destinations/catalog/advertising/pinterest.md) no Real-Time CDP. O Adobe atualizou o destino para usar a [v5 API do anunciante](https://developers.pinterest.com/docs/getting-started/migration/). Leia esta página para entender seus itens de ação e fazer a transição para a nova API sem interrupção das campanhas do Pinterest.

## Por que estou sendo notificado?

Identificamos sua organização como tendo fluxos de dados ativos para ativar públicos para o Pinterest.

## Qual é o plano?

O Adobe lançou uma nova placa de destino do Pinterest que aproveita a API v5 da Pinterest e preservará seus fluxos de dados existentes na nova conexão.

## Preciso fazer algo para manter meus públicos ativados funcionando?

Sim, antes de 18 de janeiro de 2024, é necessário autenticar no novo destino do Pinterest com sua conta de anunciante do Pinterest no Real-Time CDP. Consulte as instruções detalhadas abaixo.

### Reautenticar no Pinterest {#reauthenticate}

1. Vá para **[!UICONTROL Destinos > Contas]** e use o filtro na tela para filtrar somente o destino do Pinterest.
   ![Filtrar apenas contas do Pinterest](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. No destino **Pinterest**, selecione o símbolo de três pontos ... e selecione **[!UICONTROL Editar detalhes]**.
   ![Selecione Editar detalhes](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. Selecione **[!UICONTROL Reconectar OAuth]** e faça logon em sua conta da Pinterest.
   ![Selecionar Reconectar OAuth](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. Vá para o item de ação na seção abaixo

### Habilitar fluxos para novo destino {#disable-old-enable-new-flows}

Em seguida, é necessário habilitar os fluxos de dados para o novo cartão **[!UICONTROL Pinterest]**.

1. Vá para **[!UICONTROL Destinos > Procurar]** e use o filtro na tela para filtrar somente o destino **[!UICONTROL Pinterest]**.
   ![Filtrar fluxos de dados do Pinterest somente na guia Procurar](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. Selecione o nome da conexão com hiperlink (Campanha de fidelidade no exemplo da captura de tela acima) para o destino **[!UICONTROL Pinterest]** e alterne a opção **[!UICONTROL Habilitar]** para **em**.
   ![Ativar para novas conexões e desativar para conexões antigas](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-new-destination.png)

<!--

While no disruption to your campaigns is expected, remember to check in the Pinterest UI that everything works as expected.

-->

## Você pode compartilhar cronogramas de alto nível?

Sim, veja abaixo:

**Até 16 de novembro de 2023**: o novo destino está pronto, e você deve ver dois cartões Pinterest lado a lado no catálogo até que o Pinterest pare de oferecer suporte à antiga API v4. Todos os fluxos de dados existentes no cartão Pinterest atual são copiados para o novo destino.

![Destino antigo e novo do Pinterest lado a lado](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

<!--

>[!IMPORTANT]
>
>After November 16th, 2023 the legacy Pinterest destination is marked **[!UICONTROL Deprecating]**. <span class="preview">Any changes that you make to dataflows to the (Deprecating) Pinterest destination after November 16th will *not* be automatically carried over to the new Pinterest destination. </span>
>For example, we *do not recommend* that you activate new audiences to the old destination after November 16th. If you do that, you will then have to follow the [regular activation steps](/help/destinations/ui/activate-segment-streaming-destinations.md) to add the audience to the new destination once the customer actions are taken.

-->

**Até 15 de dezembro de 2023**: <span class="preview">Ação do cliente 1</span>. É necessário autenticar novamente no Pinterest para que o novo cartão seja conectado ao Pinterest. Exibir instruções completas em [esta seção](#reauthenticate).

<span class="preview">Ação do cliente 2</span>.Em seguida, é necessário habilitar os fluxos de dados no novo cartão. Exibir instruções completas em [esta seção](#disable-old-enable-new-flows).

<!--

>[!IMPORTANT]
>
>After December 15th, 2023, Adobe does not guarantee the integrity of dataflows to the old **[!UICONTROL (Deprecating) Pinterest]** destination.

-->

**Após 18 de janeiro de 2024**: <span class="preview">o Pinterest desativou o acesso à API do anunciante V4. Todos os clientes do Real-Time CDP que não atualizaram para o novo destino agora encontrarão falhas nos fluxos de dados para o destino do Pinterest. [Refaça a autenticação no Pinterest](#reauthenticate) e [habilite os fluxos de dados](#disable-old-enable-new-flows) para o destino atualizado para retomar suas campanhas no Pinterest.</span>

<!--

## Other items to note

After you enable the dataflows on the new destination card and disable the dataflows on the old destination cards, you should see no disruption in your campaigns or in the numbers of qualified profiles in the audiences coming in from Adobe Real-Time CDP.

-->
