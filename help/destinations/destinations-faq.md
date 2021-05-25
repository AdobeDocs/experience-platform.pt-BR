---
keywords: Destinos; perguntas; perguntas frequentes; perguntas frequentes; perguntas frequentes sobre destinos
title: Perguntas frequentes
seo-title: Perguntas frequentes
description: Respostas às perguntas mais frequentes sobre os destinos do Adobe Experience Platform
seo-description: Respostas às perguntas mais frequentes sobre os destinos do Adobe Experience Platform
source-git-commit: 47b3ef28281e3480e8b194486845f4fb4326b7d4
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 6%

---


# Perguntas frequentes {#faq}

## Visão geral {#overview}

Este documento fornece respostas a perguntas frequentes sobre destinos do Adobe Experience Platform. Para perguntas e solução de problemas relacionados a outros serviços [!DNL Platform], incluindo aqueles encontrados em todas as [!DNL Platform] APIs, consulte o [Guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**O que preciso fazer antes de ativar públicos-alvo no  [!DNL Facebook Custom Audiences]?**

Antes de enviar seus segmentos de público-alvo para [!DNL Facebook], verifique se você atende aos seguintes requisitos:

* Sua conta de usuário [!DNL Facebook] deve ter a permissão **[!DNL Manage campaigns]** ativada para a conta de anúncio que você planeja usar.
* A conta comercial **Adobe Experience Cloud** deve ser adicionada como um parceiro de publicidade em seu [!DNL Facebook Ad Account]. Use `business ID=206617933627973`. Consulte [Adicionar parceiros ao seu gerente de negócios](https://www.facebook.com/business/help/1717412048538897) na documentação do Facebook para obter detalhes.
   >[!IMPORTANT]
   >
   > Ao configurar as permissões para o Adobe Experience Cloud, você deve habilitar a permissão **Gerenciar campanhas**. Isso é necessário para a integração de [!DNL Adobe Experience Platform].
* Leia e assine os [!DNL Facebook Custom Audiences] Termos de serviço. Para fazer isso, acesse `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, onde `accountID` é a sua [!DNL Facebook Ad Account ID].

**Preciso adicionar algum aplicativo ou pixels à minha conta  [!DNL Facebook] de anunciante?**

Não. Como essa não é uma integração baseada em pixel, não há necessidade de adicionar pixels à conta do anunciante.

**Quanto tempo o Facebook leva para processar informações do Adobe Experience Platform?**

A partir de março de 2021, [!DNL Facebook Custom Audiences] precisa de até uma hora para processar as informações recebidas de [!DNL Platform].

**Posso usar  [!DNL Facebook Custom Audiences] para o direcionamento de público-alvo em outros  [!DNL Facebook] aplicativos, como o  [!DNL Instagram]?**

Você pode usar o destino [!DNL Facebook Custom Audiences] para o direcionamento de público-alvo em toda a família de aplicativos da Facebook compatíveis com [!DNL Facebook Custom Audiences], incluindo [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] e [!DNL Messenger]. A seleção do aplicativo no qual os anunciantes desejam executar campanhas é indicada no nível de posicionamento em [!DNL Facebook Ads Manager].

**Qual é a diferença entre a  [!DNL Facebook Custom Audiences] conexão e a  [!DNL Facebook Pixel] extensão?**

A conexão [!DNL Facebook Custom Audiences] usa [!DNL Platform] identidades ao enviar públicos para [!DNL Facebook], enquanto a [[!DNL Facebook Pixel] conexão](../destinations/catalog/advertising/facebook-pixel.md) usa o pixel [!DNL Facebook] integrado em um site.

Estas duas integrações são complementares; você pode usar ambas para garantir uma melhor cobertura do público-alvo. Como exemplo, você pode usar a extensão [!DNL Facebook Pixel] para visitantes de sites de prospecção que não criaram uma conta, enquanto [!DNL Facebook Custom Audiences] pode ajudar a direcionar clientes existentes, com base nas identidades [!DNL Platform].

**A integração do Adobe Experience Platform com o  [!DNL Facebook Custom Audiences] suporte desqualifica os usuários de um público-alvo quando eles não estão mais qualificados para isso?**

Sim, a integração oferece suporte à remoção de usuários de [!DNL Facebook Custom Audiences] quando não se qualificam mais.

**Como devo fazer o hash dos dados do público-alvo antes de enviá-los para o  [!DNL Facebook]?**

[!DNL Facebook] exige que nenhuma informação pessoal identificável (PII) seja enviada de forma clara. Portanto, os públicos-alvo ativados para [!DNL Facebook] podem ser desconectados dos identificadores com hash *como endereços de email ou números de telefone.*

Para obter explicações detalhadas sobre os requisitos de correspondência de ID, consulte [Requisitos de correspondência de ID](catalog/social/facebook.md#id-matching-requirements).

**Que tipo de identidade posso ativar no  [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] O suporta a ativação das seguintes identidades: emails com hash, números de telefone com hash  [!DNL GAID],  [!DNL IDFA]e IDs externas personalizadas.

## Públicos-alvo correspondentes ao linkedIn {#linkedin}

**Preciso adicionar algum aplicativo ou pixels à minha conta  [!DNL LinkedIn] de anunciante?**

Não. Como essa não é uma integração baseada em pixel, não há necessidade de adicionar pixels à conta do anunciante.

**O que preciso fazer antes de ativar públicos-alvo no  [!DNL LinkedIn Matched Audiences]?**

Antes de usar o destino [!UICONTROL LinkedIn Matched Audience], verifique se a conta [!DNL LinkedIn Campaign Manager] tem o nível de permissão [!DNL Creative Manager] ou superior.

Para saber como editar suas permissões de usuário [!DNL LinkedIn Campaign Manager], consulte [Adicionar, editar e remover permissões de usuário em contas publicitárias](https://www.linkedin.com/help/lms/answer/5753) na documentação do LinkedIn.

**Como devo fazer o hash dos dados do público-alvo antes de enviá-los para o  [!DNL LinkedIn]?**

[!DNL LinkedIn] exige que nenhuma informação pessoal identificável (PII) seja enviada de forma clara. Portanto, os públicos-alvo ativados para [!DNL LinkedIn] podem ser desconectados dos identificadores com hash *como endereços de email ou números de telefone.*

Para obter explicações detalhadas sobre os requisitos de correspondência de ID, consulte [Requisitos de correspondência de ID](catalog/social/linkedin.md#id-matching-requirements).

**Que tipo de identidade posso ativar no  [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] O suporta a ativação das seguintes identidades: emails com hash  [!DNL GAID], e  [!DNL IDFA].
