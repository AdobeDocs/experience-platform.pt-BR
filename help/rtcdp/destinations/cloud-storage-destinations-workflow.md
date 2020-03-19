---
title: Fluxo de trabalho de destinos de armazenamento em nuvem
seo-title: Fluxo de trabalho de destinos de armazenamento em nuvem
description: Instruções para conectar-se aos locais de armazenamento na nuvem
seo-description: Instruções para conectar-se aos locais de armazenamento na nuvem
translation-type: tm+mt
source-git-commit: 225f18bd0d092bdae7b4cc99c278e850be9cfd56

---


# Fluxo de trabalho para criar destinos de armazenamento em nuvem

## Visão geral

Esta página explica como você pode se conectar a locais de armazenamento em nuvem na Adobe Real-time Customer Data Platform.

1. Em **[!UICONTROL Conexões > Destinos]**, selecione seu destino de armazenamento em nuvem preferencial e selecione o destino **[!UICONTROL do]** Connect.

   ![Conectar-se ao destino de armazenamento na nuvem](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. Na etapa **Autenticação** , se você já tiver configurado uma conexão com o destino de armazenamento na nuvem, selecione Conta **** existente e selecione a conexão existente. Ou você pode selecionar **[!UICONTROL Nova conta]** para configurar uma nova conexão com o destino de armazenamento na nuvem. Preencha as credenciais de autenticação de sua conta e selecione **[!UICONTROL Conectar ao destino]**.

   >[!NOTE]
   >
   >O Adobe Real-time CDP oferece suporte à validação de credenciais no processo de autenticação e exibe uma mensagem de erro se você inserir credenciais incorretas no local de armazenamento na nuvem. Isso garante que você não conclua o fluxo de trabalho com credenciais incorretas.

   ![Conectar-se ao destino do armazenamento na nuvem - etapa de autenticação](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. Na etapa **[!UICONTROL Configuração]** , digite um **[!UICONTROL Nome]** e um **[!UICONTROL Destino]** para o fluxo de ativação e insira o caminho **[!UICONTROL da]** Pasta no destino de armazenamento na nuvem onde os arquivos serão entregues. Selecione **[!UICONTROL Criar destino]** depois de preencher os campos acima.

   ![Conectar-se ao destino do armazenamento na nuvem - etapa de autenticação](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

4. Seu destino agora é criado. Você pode selecionar **[!UICONTROL Salvar e sair]** se quiser ativar segmentos posteriormente ou selecionar **[!UICONTROL Próximo]** para continuar o fluxo de trabalho e selecionar segmentos para ativar. Em qualquer caso, consulte a próxima seção, [Ativar segmentos](#activate-segments), para o restante do fluxo de trabalho,

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](/help/rtcdp/destinations/activate-destinations.md) para obter informações sobre o fluxo de trabalho de ativação do segmento.