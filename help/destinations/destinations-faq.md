---
keywords: Destinos; perguntas; perguntas frequentes; perguntas frequentes; perguntas frequentes sobre destinos
title: Perguntas frequentes
seo-title: Frequently asked questions
description: Respostas às perguntas mais frequentes sobre os destinos do Adobe Experience Platform
seo-description: Answers to the most frequently asked questions about Adobe Experience Platform destinations
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: 69fc8e8ec3211495056be73c2e49c6aecfc569ea
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 4%

---

# Perguntas frequentes {#faq}

## Visão geral {#overview}

Este documento fornece respostas a perguntas frequentes sobre destinos do Adobe Experience Platform. Para perguntas e solução de problemas relacionados a outros [!DNL Platform] , incluindo os encontrados em todos [!DNL Platform] APIs, consulte o [Guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

## Perguntas gerais sobre destinos {#general}

**Por que vejo contagens de perfil diferentes na interface do usuário do Experience Platform e nos arquivos CSV exportados?**

Esse é um comportamento normal devido ao modo como o Experience Platform executa a segmentação.

A segmentação de streaming atualiza a contagem de perfis para segmentos de streaming ao longo do dia, enquanto a segmentação em lote atualiza a contagem de perfis para segmentos em lote uma vez a cada 24 horas.

Quando o agendamento de exportação do segmento difere do agendamento de segmentação, o perfil conta entre a interface do usuário e o [!DNL CSV] será diferente, especialmente quando se tratar de segmentos de streaming.

Consulte a [Documentação do Serviço de segmentação](../segmentation/home.md) para obter mais detalhes.

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**O que preciso fazer antes de ativar públicos-alvo em [!DNL Facebook Custom Audiences]?**

Antes de enviar segmentos de público-alvo para o [!DNL Facebook], certifique-se de atender aos seguintes requisitos:

* Seu [!DNL Facebook] a conta do usuário deve ter o **[!DNL Manage campaigns]** permissão ativada para a conta do anúncio que você planeja usar.
* O **Adobe Experience Cloud** A conta comercial deve ser adicionada como um parceiro de publicidade em seu [!DNL Facebook Ad Account]. Use `business ID=206617933627973`. Consulte [Adicionar parceiros ao seu gerente de negócios](https://www.facebook.com/business/help/1717412048538897) na documentação do Facebook para obter detalhes.
   >[!IMPORTANT]
   >
   > Ao configurar as permissões para o Adobe Experience Cloud, você deve ativar o **Gerenciar campanhas** permissão. Isso é necessário para a integração de [!DNL Adobe Experience Platform].
* Leia e assine o [!DNL Facebook Custom Audiences] Termos de serviço. Para fazer isso, acesse `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, onde `accountID` é a sua [!DNL Facebook Ad Account ID].

**Preciso adicionar qualquer aplicativo ou pixel ao meu [!DNL Facebook] conta do anunciante?**

Não. Como essa não é uma integração baseada em pixel, não há necessidade de adicionar pixels à conta do anunciante.

**Quanto tempo o Facebook leva para processar informações do Adobe Experience Platform?**

A partir de março de 2021, [!DNL Facebook Custom Audiences] precisa de até uma hora para processar as informações recebidas de [!DNL Platform].

**Posso usar [!DNL Facebook Custom Audiences] para direcionamento de público-alvo em outros [!DNL Facebook] aplicativos, como [!DNL Instagram]?**

Você pode usar o [!DNL Facebook Custom Audiences] destino para segmentação de público-alvo em toda a família de aplicativos do Facebook que são compatíveis com [!DNL Facebook Custom Audiences], incluindo [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network]e [!DNL Messenger]. A seleção do aplicativo no qual os anunciantes desejam executar campanhas é indicada no nível de posicionamento em [!DNL Facebook Ads Manager].

**Qual é a diferença entre as [!DNL Facebook Custom Audiences] ligação e [!DNL Facebook Pixel] extensão?**

O [!DNL Facebook Custom Audiences] uso da conexão [!DNL Platform] identidades ao enviar públicos para [!DNL Facebook], enquanto a variável [[!DNL Facebook Pixel] conexão](../destinations/catalog/advertising/facebook-pixel.md) usa a variável [!DNL Facebook] pixel integrado em um site.

Estas duas integrações são complementares; você pode usar ambas para garantir uma melhor cobertura do público-alvo. Como exemplo, você pode usar a variável [!DNL Facebook Pixel] extensão para visitantes do site de prospecção que não criaram uma conta, enquanto [!DNL Facebook Custom Audiences] pode ajudar você a direcionar clientes existentes, com base em [!DNL Platform] identidades.

**A integração do Adobe Experience Platform com o [!DNL Facebook Custom Audiences] oferecer suporte para usuários desqualificados de um público-alvo quando não estiverem mais qualificados para ele?**

Sim, a integração oferece suporte à remoção de usuários do [!DNL Facebook Custom Audiences] quando deixarem de se qualificar.

**Como devo fazer hash nos dados do público-alvo antes de enviá-los para [!DNL Facebook]?**

[!DNL Facebook] exige que nenhuma informação pessoal identificável (PII) seja enviada de forma clara. Portanto, os públicos-alvo ativados para [!DNL Facebook] pode ser desligado *hash* identificadores, como endereços de email ou números de telefone.

Para obter explicações detalhadas sobre os requisitos de correspondência de ID, consulte [Requisitos de correspondência de ID](catalog/social/facebook.md#id-matching-requirements).

**Que tipo de identidade posso ativar no [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] O suporta a ativação das seguintes identidades: emails com hash, números de telefone com hash, [!DNL GAID], [!DNL IDFA]e IDs externas personalizadas.

**Posso criar vários destinos do Facebook na interface do usuário da plataforma para contas Facebook separadas?**

Sim. Um destino Facebook no Experience Platform é 1:1 para uma conta de anúncio no Facebook. Você pode criar um destino Facebook separado para cada conta de anúncio do Facebook em sua empresa. Siga as [tutorial de conexão de destino](/help/destinations/ui/connect-destination.md) e conecte-se a uma conta Facebook separada para cada novo destino do Facebook na interface do usuário da plataforma. Não há limite para o número de contas de anúncio do Facebook às quais você pode se conectar.

## Públicos-alvo correspondentes ao linkedIn {#linkedin}

**Preciso adicionar qualquer aplicativo ou pixel ao meu [!DNL LinkedIn] conta do anunciante?**

Não. Como essa não é uma integração baseada em pixel, não há necessidade de adicionar pixels à conta do anunciante.

**O que preciso fazer antes de ativar públicos-alvo em [!DNL LinkedIn Matched Audiences]?**

Antes de usar a variável [!UICONTROL Público-alvo correspondente do linkedIn] de destino, verifique se [!DNL LinkedIn Campaign Manager] tem a [!DNL Creative Manager] nível de permissão ou superior.

Para saber como editar seu [!DNL LinkedIn Campaign Manager] permissões do usuário, consulte [Adicionar, editar e remover permissões de usuário em contas publicitárias](https://www.linkedin.com/help/lms/answer/5753) na documentação do LinkedIn.

**Como devo fazer hash nos dados do público-alvo antes de enviá-los para [!DNL LinkedIn]?**

[!DNL LinkedIn] exige que nenhuma informação pessoal identificável (PII) seja enviada de forma clara. Portanto, os públicos-alvo ativados para [!DNL LinkedIn] pode ser desligado *hash* identificadores, como endereços de email ou números de telefone.

Para obter explicações detalhadas sobre os requisitos de correspondência de ID, consulte [Requisitos de correspondência de ID](catalog/social/linkedin.md#id-matching-requirements).

**Que tipo de identidade posso ativar no [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] O suporta a ativação das seguintes identidades: emails com hash, [!DNL GAID]e [!DNL IDFA].
