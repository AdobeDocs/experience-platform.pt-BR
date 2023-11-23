---
title: Migração de destino do pinterest para a nova API. Ação do cliente necessária.
description: O pinterest está descontinuando a API do anunciante v4 usada atualmente pelo destino do Pinterest no Real-Time CDP. Entenda seus itens de ação para fazer a transição perfeita para a nova API sem interromper as campanhas do Pinterest.
hide: true
hidefromtoc: true
exl-id: c965235c-4208-4c28-9ac5-eb4c0061515d
source-git-commit: c2e308b5e743f07062be9a34e23c4bc700b27463
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# Atualização de destino do pinterest para a nova API. Ação do cliente necessária até 15 de dezembro de 2023

>[!IMPORTANT]
>
>Os itens de ação do cliente nessa página se aplicam se sua organização tiver configurado fluxos de dados para exportar dados para o Pinterest antes de 16 de novembro de 2023, data em que a **[!UICONTROL (Novo) Pinterest]** O destino, usando a API mais recente do Pinterest, foi adicionado ao catálogo de destinos.

## O que está acontecendo?

O pinterest está descontinuando a API do anunciante v4 usada atualmente pela [Destino do pinterest](/help/destinations/catalog/advertising/pinterest.md) no Real-Time CDP. O Adobe está trabalhando com o Pinterest e está atualizando o destino para usar o [API do anunciante v5](https://developers.pinterest.com/docs/getting-started/migration/). Leia esta página para entender seus itens de ação e fazer a transição para a nova API sem interrupção das campanhas do Pinterest.

## Por que estou sendo notificado?

Identificamos sua organização como tendo fluxos de dados ativos para ativar públicos para o Pinterest.

## Qual é o plano?

A Adobe está lançando uma nova placa de destino do Pinterest que aproveita a API v5 da Pinterest e preservará seus fluxos de dados existentes na nova conexão.

## Preciso fazer algo para manter meus públicos ativados funcionando?

Sim, depois de 16 de novembro de 2023, será necessário autenticar no novo destino do Pinterest com sua conta de anunciante do Pinterest no Real-Time CDP. Consulte as instruções detalhadas abaixo.

### Reautenticar no Pinterest {#reauthenticate}

1. Ir para **[!UICONTROL Destinos > Contas]** e use o filtro na tela para filtrar somente o destino do Pinterest.
   ![Filtrar somente contas do Pinterest](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. No **(Novo) Pinterest** , selecione o símbolo de três pontos ... e selecione **[!UICONTROL Editar detalhes]**.
   ![Selecione Editar detalhes](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. Selecionar **[!UICONTROL Reconectar OAuth]** e faça logon na sua conta da Pinterest.
   ![Selecione Reconectar OAuth](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. Vá para o item de ação na seção abaixo

### Desabilitar fluxos existentes para destino antigo e habilitar fluxos para novo destino {#disable-old-enable-new-flows}

Em seguida, é necessário desativar manualmente os fluxos existentes para o cartão de destino antigo **[!UICONTROL (Obsoleto) Pinterest]** e habilitar fluxos para o novo cartão **[!UICONTROL (Novo) Pinterest]**.

1. Ir para **[!UICONTROL Destinos > Navegar]** e use o filtro na tela para filtrar a variável **[!UICONTROL (Novo) Pinterest]** e **[!UICONTROL (Obsoleto) Pinterest]** somente destinos.
   ![Filtrar fluxos de dados do Pinterest somente na guia Procurar](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. Selecione o nome da conexão com hiperlink (Campanha de fidelidade no exemplo de captura de tela acima) para o **[!UICONTROL (Obsoleto) Pinterest]** destino e alterne o **[!UICONTROL Ativar]** alternar para **desligado**.
   ![Ativar para novas conexões e desativar para conexões antigas](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-old-destination.png)
3. Selecione o nome da conexão com hiperlink (Campanha de fidelidade no exemplo de captura de tela acima) para o **[!UICONTROL (Novo) Pinterest]** destino e alterne o **[!UICONTROL Ativar]** alternar para **em**.
   ![Ativar para novas conexões e desativar para conexões antigas](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-new-destination.png)
4. Compare a lista de públicos-alvo ativados no fluxo de dados antigo e novo e verifique se você não tem novos públicos-alvo nos fluxos antigos que estão ausentes nos novos fluxos.

Embora não seja esperada nenhuma interrupção em suas campanhas, lembre-se de verificar na interface do usuário do Pinterest se tudo funciona conforme esperado.

## Você pode compartilhar cronogramas de alto nível?

Sim, veja abaixo:

**Até 16 de novembro de 2023**: o novo destino está pronto, e você deve ver dois cartões Pinterest lado a lado no catálogo, e todos os fluxos de dados existentes para o cartão Pinterest atual são copiados para o novo destino.

![Destino antigo e novo do Pinterest lado a lado](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

>[!IMPORTANT]
>
>Depois de 16 de novembro de 2023, o destino do Pinterest herdado será marcado **[!UICONTROL Obsoleto]**. <span class="preview">Quaisquer alterações feitas nos fluxos de dados para o destino do Pinterest (obsoleto) após 16 de novembro resultarão *não* será automaticamente transferida para o novo destino do Pinterest. </span>
>Por exemplo, *não recomendar* que você ative novos públicos-alvo para o destino antigo após 16 de novembro. Se você fizer isso, terá que seguir as etapas [etapas de ativação regular](/help/destinations/ui/activate-segment-streaming-destinations.md) para adicionar o público-alvo ao novo destino depois que as ações do cliente forem executadas.

**Até 15 de dezembro de 2023**: <span class="preview">Ação do cliente 1</span>. É necessário autenticar novamente no Pinterest para que o novo cartão seja conectado ao Pinterest. Exibir instruções completas em [nesta seção](#reauthenticate).

<span class="preview">Ação do cliente 2</span>Em seguida, é necessário desativar os fluxos de dados para o Pinterest no cartão antigo e ativar os fluxos de dados no novo cartão. Exibir instruções completas em [nesta seção](#disable-old-enable-new-flows).

>[!IMPORTANT]
>
>Após 15 de dezembro de 2023, o Adobe não garante a integridade dos fluxos de dados para o antigo **[!UICONTROL (Obsoleto) Pinterest]** destino.

## Outros itens a serem observados

Depois de habilitar os fluxos de dados no novo cartão de destino e desabilitar os fluxos de dados nos cartões de destino antigos, você não deve ver interrupções em suas campanhas ou nos números de perfis qualificados nos públicos-alvo provenientes do Adobe Real-Time CDP.
