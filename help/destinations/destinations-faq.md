---
keywords: destinos, perguntas, perguntas frequentes, faq, perguntas frequentes sobre destinos
title: Perguntas frequentes
description: Respostas às perguntas mais frequentes sobre destinos do Adobe Experience Platform
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 4%

---

# Perguntas frequentes {#faq}

## Visão geral {#overview}

Este documento fornece respostas a perguntas frequentes sobre destinos do Adobe Experience Platform. Para perguntas e solução de problemas relacionados a outros [!DNL Platform] serviços, incluindo os encontrados em todos os [!DNL Platform] APIs, consulte o [guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

## Perguntas gerais sobre destinos {#general}

**Por que estou vendo diferentes contagens de perfis na interface do usuário do Experience Platform e nos arquivos CSV exportados?**

Esse é um comportamento normal devido à maneira como o Experience Platform executa a segmentação.

A segmentação de transmissão atualiza a contagem de perfis para segmentos de transmissão ao longo do dia, enquanto a segmentação em lote atualiza a contagem de perfis para segmentos em lote uma vez a cada 24 horas.

Quando a programação de exportação de segmento for diferente da programação de segmentação, o perfil será contado entre a interface do usuário e a exportada [!DNL CSV] O arquivo será diferente, especialmente quando se trata de segmentos de transmissão.

Consulte a [Documentação do Serviço de segmentação](../segmentation/home.md) para obter mais detalhes.

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**O que preciso fazer antes de ativar públicos no [!DNL Facebook Custom Audiences]?**

Antes de enviar os segmentos de público-alvo para [!DNL Facebook], certifique-se de atender aos seguintes requisitos:

* Seu [!DNL Facebook] a conta de usuário deve ter o **[!DNL Manage campaigns]** permissão ativada para a conta de anúncio que você planeja usar.
* A variável **Adobe Experience Cloud** conta comercial deve ser adicionada como um parceiro de publicidade em sua [!DNL Facebook Ad Account]. Use `business ID=206617933627973`. Consulte [Adicionar parceiros ao seu gerente de negócios](https://www.facebook.com/business/help/1717412048538897) na documentação do Facebook para obter detalhes.
   >[!IMPORTANT]
   >
   > Ao configurar as permissões para o Adobe Experience Cloud, você deve ativar o **Gerenciar campanhas** permissão. Isso é necessário para a integração de [!DNL Adobe Experience Platform].
* Leia e assine o [!DNL Facebook Custom Audiences] Termos de serviço. Para fazer isso, acesse `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, onde `accountID` é a sua [!DNL Facebook Ad Account ID].

**Preciso adicionar aplicativos ou pixels às [!DNL Facebook] conta de anunciante?**

Não. Como essa não é uma integração baseada em pixels, não há necessidade de adicionar pixels à conta do anunciante.

**Quanto tempo o Facebook leva para processar informações do Adobe Experience Platform?**

Em março de 2021, [!DNL Facebook Custom Audiences] precisa de até uma hora para processar informações recebidas do [!DNL Platform].

**Posso usar [!DNL Facebook Custom Audiences] para direcionamento de público em outros [!DNL Facebook] aplicativos, como [!DNL Instagram]?**

Você pode usar o [!DNL Facebook Custom Audiences] destino para direcionamento de público-alvo na família de aplicativos da Facebook compatíveis com [!DNL Facebook Custom Audiences], incluindo [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], e [!DNL Messenger]. A seleção do aplicativo no qual os anunciantes desejam executar campanhas é indicada no nível de posicionamento no [!DNL Facebook Ads Manager].

**Qual é a diferença entre as variáveis [!DNL Facebook Custom Audiences] conexão e [!DNL Facebook Pixel] extensão?**

A variável [!DNL Facebook Custom Audiences] usos da conexão [!DNL Platform] identidades ao enviar públicos para o [!DNL Facebook], enquanto a variável [[!DNL Facebook Pixel] conexão](../destinations/catalog/advertising/facebook-pixel.md) usa o [!DNL Facebook] pixel integrado em um site.

Estas duas integrações são complementares; você pode usar ambas para garantir uma melhor cobertura do público-alvo. Como exemplo, você pode usar a variável [!DNL Facebook Pixel] extensão para visitantes de sites de prospecção que não criaram uma conta, enquanto [!DNL Facebook Custom Audiences] podem ajudar você a direcionar clientes existentes, com base em [!DNL Platform] identidades.

**A integração do Adobe Experience Platform com o [!DNL Facebook Custom Audiences] oferecer suporte à desqualificação de usuários de um público-alvo quando eles não se qualificam mais para ele?**

Sim, a integração permite remover usuários do [!DNL Facebook Custom Audiences] quando eles não se qualificarem mais.

**Como devo aplicar hash aos dados do público-alvo antes de enviá-los para o [!DNL Facebook]?**

[!DNL Facebook] exige que nenhuma informação pessoal identificável (PII) seja enviada em claro. Portanto, os públicos-alvo foram ativados para [!DNL Facebook] pode ser desativado *com hash* identificadores, como endereços de email ou números de telefone.

Para obter explicações detalhadas sobre os requisitos de correspondência de ID, consulte [Requisitos de correspondência de ID](catalog/social/facebook.md#id-matching-requirements).

**Em que tipo de identidades posso ativar [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] O é compatível com a ativação das seguintes identidades: emails com hash, números de telefone com hash, [!DNL GAID], [!DNL IDFA]e IDs externas personalizadas.

**Posso criar vários destinos do Facebook na interface do usuário da Platform para contas separadas do Facebook?**

Sim. Um destino do Facebook no Experience Platform é 1:1 para uma conta de anúncio no Facebook. É possível criar um destino do Facebook separado para cada conta de anúncio do Facebook na empresa. Siga as [tutorial de conexão de destino](/help/destinations/ui/connect-destination.md) e conecte-se a uma conta do Facebook separada para cada novo destino do Facebook na interface do usuário da plataforma. Não há limite para o número de contas de anúncios do Facebook às quais você pode se conectar.

## Correspondência de cliente do Google {#google-customer-match}

**Ao exportar segmentos para a Correspondência de clientes do Google, por que vejo números extras anexados ao final dos nomes de segmentos na interface do Google?**

O Google exige que os nomes de segmento sejam exclusivos. Os números que você está vendo são [Carimbos de data e hora UNIX](https://www.unixtimestamp.com/) e são anexados para manter os nomes de segmento exclusivos, se você mapeou o mesmo segmento para vários destinos do Google.

## Públicos-alvo correspondentes do linkedIn {#linkedin}

**Preciso adicionar aplicativos ou pixels às [!DNL LinkedIn] conta de anunciante?**

Não. Como essa não é uma integração baseada em pixels, não há necessidade de adicionar pixels à conta do anunciante.

**O que preciso fazer antes de ativar públicos no [!DNL LinkedIn Matched Audiences]?**

Antes de poder usar o [!UICONTROL Público-alvo correspondente do linkedIn] destino, verifique se [!DNL LinkedIn Campaign Manager] a conta tem o [!DNL Creative Manager] nível de permissão ou superior.

Para saber como editar suas [!DNL LinkedIn Campaign Manager] permissões do usuário, consulte [Adicionar, editar e remover permissões de usuário em contas publicitárias](https://www.linkedin.com/help/lms/answer/5753) na documentação do LinkedIn.

**Como devo aplicar hash aos dados do público-alvo antes de enviá-los para o [!DNL LinkedIn]?**

[!DNL LinkedIn] exige que nenhuma informação pessoal identificável (PII) seja enviada em claro. Portanto, os públicos-alvo foram ativados para [!DNL LinkedIn] pode ser desativado *com hash* identificadores, como endereços de email ou números de telefone.

Para obter explicações detalhadas sobre os requisitos de correspondência de ID, consulte [Requisitos de correspondência de ID](catalog/social/linkedin.md#id-matching-requirements).

**Em que tipo de identidades posso ativar [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] O é compatível com a ativação das seguintes identidades: emails com hash, [!DNL GAID], e [!DNL IDFA].
