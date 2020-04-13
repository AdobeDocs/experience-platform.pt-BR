---
title: Destino do Facebook
seo-title: Destino do Facebook
description: Ative perfis para suas campanhas do Facebook para definição de metas, personalização e supressão de audiências com base em emails com hash.
seo-description: Ative perfis para suas campanhas do Facebook para definição de metas, personalização e supressão de audiências com base em emails com hash.
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# (Beta) Destino do Facebook

>[!IMPORTANT]
>
>O destino do Facebook no Adobe Real-time CDP está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

## Visão geral

Ative perfis para suas campanhas do Facebook para definição de metas, personalização e supressão de audiências com base em emails com hash.

## Especificações de destino

### Tipo de Ativação

Exportação de segmento - você está exportando todos os membros de um segmento (audiência) com seus identificadores (nome, número de telefone etc.) usado no destino do Facebook

## Pré-requisitos

Antes de enviar os segmentos de audiência para [!DNL Facebook], verifique se você atende aos seguintes requisitos:

1. Sua conta [!DNL Facebook] de usuário deve ter a permissão **Gerenciar campanha** ativada para a conta de anúncio que você planeja usar.
2. Adicione a conta comercial da **Adobe Experience Cloud** como um parceiro de publicidade em seu [!DNL Facebook Ad Account]site. Use `business ID=206617933627973`. Consulte [Adicionar parceiros ao seu gerente](https://www.facebook.com/business/help/1717412048538897) de negócios para obter detalhes.
   >[!IMPORTANT]
   > Ao configurar as permissões para a Adobe Experience Cloud, você deve ativar a permissão **Gerenciar campanha** . Isso é necessário para a [!DNL Adobe Real-time CDP] integração.
3. Leia e assine os [!DNL Facebook Custom Audiences] Termos de serviço. Para fazer isso, vá para `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, onde `accountID` está seu [!DNL Facebook Ad Account ID].


## Destino do Connect

Para conectar o destino do Facebook, consulte Fluxo de trabalho [de autenticação de destinos de rede](/help/rtcdp/destinations/social-network-destinations-workflow.md)Social.


## Ativar segmentos no Facebook

Para obter instruções sobre como ativar segmentos no Facebook, consulte [Ativar dados para destinos](/help/rtcdp/destinations/activate-destinations.md).