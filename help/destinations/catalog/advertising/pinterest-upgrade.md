---
title: Migração de destino do pinterest para a nova API. Ação do cliente necessária.
description: O pinterest está descontinuando a API do anunciante v4 usada atualmente pelo destino do Pinterest no Real-Time CDP. Entenda seus itens de ação para fazer a transição perfeita para a nova API sem interromper as campanhas do Pinterest.
hide: true
hidefromtoc: true
source-git-commit: 10bf63677c66366c226d647b1174093c1704a8b9
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 0%

---

# Atualização de destino do pinterest para a nova API. Ação do cliente necessária até 15 de dezembro de 2023

## O que está acontecendo?

O pinterest está descontinuando a API do anunciante v4 usada atualmente pela [Destino do pinterest](/help/destinations/catalog/advertising/pinterest.md) no Real-Time CDP. O Adobe está trabalhando com o Pinterest e está atualizando o destino para usar o [API do anunciante v5](https://developers.pinterest.com/docs/getting-started/migration/). Leia esta página para entender seus itens de ação e fazer a transição para a nova API sem interrupção das campanhas do Pinterest.

## Por que estou sendo notificado?

Identificamos sua organização como tendo fluxos de dados ativos para ativar públicos para o Pinterest.

## Qual é o plano?

A Adobe está lançando uma nova placa de destino do Pinterest que aproveita a API v5 da Pinterest e preservará seus fluxos de dados existentes na nova conexão.

## Preciso fazer algo para manter meus públicos ativados funcionando?

Sim, depois que o Adobe concluir a atualização (direcionada para 16 de novembro), será necessário reautenticar no Pinterest com sua conta de anunciante do Pinterest no Adobe Experience Platform. Consulte as instruções detalhadas abaixo.

### Reautenticar no Pinterest {#reauthenticate}

1. Ir para **[!UICONTROL Destinos > Contas]** e use o filtro na tela para filtrar somente o destino do Pinterest.
   ![Filtrar somente contas do Pinterest](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. No **(Novo) Pinterest** , selecione o símbolo de três pontos ... e selecione **[!UICONTROL Editar detalhes]**.
   ![Selecione Editar detalhes](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. Selecionar **[!UICONTROL Reconectar OAuth]** e faça logon na sua conta da Pinterest.
   ![Selecione Reconectar OAuth](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. Informe ao Adobe que você foi reautenticado na **[!UICONTROL (Novo) Pinterest]** destino.

### Desabilitar fluxos existentes para destino antigo e habilitar fluxos para novo destino {#disable-old-enable-new-flows}

Em seguida, é necessário desativar manualmente os fluxos existentes para o cartão antigo e habilitar os fluxos para o novo cartão.

>[!IMPORTANT]
>
>Após a reautenticação, você pode entrar em contato com o Adobe e executaremos essa segunda etapa para você. Se preferir executar essa etapa manualmente, siga as etapas abaixo:

1. Ir para **[!UICONTROL Destinos > Navegar]** e use o filtro na tela para filtrar a variável **[!UICONTROL (Novo) Pinterest]** e **[!UICONTROL (Obsoleto) Pinterest]** somente destinos.
   ![Filtrar fluxos de dados do Pinterest somente na guia Procurar](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. Selecione o nome da conexão com hiperlink (Campanha de fidelidade no exemplo de captura de tela acima) e alterne a variável **[!UICONTROL Ativar]** alternar para **desligado** para a conexão antiga e para **em** para a nova conexão.
   ![Ativar para novas conexões e desativar para conexões antigas](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle.png)
3. Compare a lista de públicos-alvo ativados no fluxo de dados antigo e novo e verifique se você não tem novos públicos-alvo nos fluxos antigos que estão ausentes nos novos fluxos.

Embora não seja esperada nenhuma interrupção em suas campanhas, lembre-se de verificar na interface do usuário do Pinterest se tudo funciona conforme esperado.

## Você pode compartilhar cronogramas de alto nível?

Sim, veja abaixo:

**Até 16 de novembro**: o novo destino está pronto, e você deve ver dois cartões Pinterest lado a lado no catálogo, e todos os fluxos de dados existentes para o cartão Pinterest atual são copiados para o novo destino.

![Destino antigo e novo do Pinterest lado a lado](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

>[!IMPORTANT]
>
>Depois de 16 de novembro, o destino do Pinterest herdado é marcado **[!UICONTROL Obsoleto]**. <span class="preview">Quaisquer alterações feitas nos fluxos de dados para o destino do Pinterest (obsoleto) após 16 de novembro resultarão *não* será automaticamente transferida para o novo destino do Pinterest. </span>
>Por exemplo, *não recomendar* que você ative novos públicos-alvo para o destino antigo após 16 de novembro. Se você fizer isso, terá que seguir as etapas [etapas de ativação regular](/help/destinations/ui/activate-segment-streaming-destinations.md) para adicionar o público-alvo ao novo destino depois que as ações do cliente forem executadas.

**Até 15 de dezembro**: <span class="preview">Ação do cliente</span>. É necessário autenticar novamente no Pinterest para que o novo cartão seja conectado ao Pinterest (instruções mais acima). Depois de fazer isso, entre em contato conosco.

Os fluxos de dados para o Pinterest no cartão antigo precisam ser desativados e os do novo cartão precisam ser ativados. Você pode fazer isso manualmente na interface do usuário do, ou entre em contato com o Adobe e faremos isso para você.

## Outros itens a serem observados

Depois de habilitar os fluxos de dados no novo cartão de destino e desabilitar os fluxos de dados nos cartões de destino antigos, você não deve ver interrupções em suas campanhas ou nos números de perfis qualificados nos públicos-alvo provenientes do Adobe Real-Time CDP.
