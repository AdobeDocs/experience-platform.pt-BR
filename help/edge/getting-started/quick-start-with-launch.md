---
title: start rápido com o Launch
seo-title: start rápido do Adobe Experience Platform Web SDK com o Launch
description: Guia de start rápido para usar a extensão do SDK Experience Platform Web para coletar dados
seo-description: Guia de start rápido para usar a extensão do SDK Experience Platform Web para coletar dados
translation-type: tm+mt
source-git-commit: 9b8bddf39301cdc39bfa5370ef98d99434fc64f8
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 4%

---


# Boas-vindas

Este guia o orientará pelas diferentes etapas sobre como configurar o SDK da Web do Adobe Experience Platform no Adobe Launch. Você precisa ter permissões e estar na lista de permissões para usar esse recurso. Se você quiser entrar na lista de espera, entre em contato com seu CSM. Além disso, para usar esse recurso, é necessário:

- Ter um domínio [próprio (CNAME)](https://docs.adobe.com/content/help/pt-BR/core-services/interface/ec-cookies/cookies-first-party.html) habilitado. Se você já tiver um CNAME para o Adobe Analytics, use esse. O teste no desenvolvimento funcionará sem um CNAME, mas você precisará de um antes de ir para a produção
- Usar a versão mais recente do serviço de ID de Visitante

## Criar uma ID de configuração

Você pode criar uma ID de configuração usando a ferramenta [de configuração de](../fundamentals/edge-configuration.md) borda no Adobe Launch. Isso permitirá que você ative a rede Edge para enviar dados para as várias soluções. Consulte a página Ferramenta [de configuração de](../fundamentals/edge-configuration.md) borda para obter detalhes sobre como localizar cada opção.

>[!NOTE]
>
>Sua organização deve estar na lista de permissões do recurso. Entre em contato com seu CSM para ser adicionado à lista de permissões.

## Preparar um Schema

A Experience Platform Edge Network utiliza dados como XDM. O XDM é um formato de dados que permite definir schemas. O schema define como o Edge Network espera que os dados sejam formatados. Para enviar dados, você precisará definir seu schema. Certifique-se de concluir o seguinte:

- [Criar um schema](../../xdm/tutorials/create-schema-ui.md)
- Adicione o mixin do SDK da Web para Adobe Experience Platform ao schema criado

O vídeo a seguir tem o objetivo de oferecer suporte à criação de um schema, conjunto de dados e conector de fonte de transmissão para seus dados do SDK da Web.

>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

## Instalar o SDK no Adobe Launch

Faça logon no Adobe Launch e instale a `AEP Web SDK` extensão. Como parte da instalação do SDK, você será solicitado a configurar a extensão. Digite a ID de configuração solicitada acima. A extensão preenche automaticamente a ID da empresa.

Para obter mais detalhes sobre diferentes opções de configuração, consulte [Configuração do SDK](../fundamentals/configuring-the-sdk.md).

## Criar uma base de elementos de dados em seu Schema

No Adobe Launch, crie um Elemento de dados que faça referência ao schema alterando a extensão para AEP Web SDK e definindo o tipo como Objeto XDM. Isso carregará seu schema e permitirá que você mapeie os elementos de dados em diferentes partes do schema.

![Elemento de data na inicialização](../../assets/edge_data_element.png)

## Enviar um evento

Depois que a extensão é instalada, o start envia eventos adicionando uma ação &quot;sendEvent&quot; da extensão AEP Web SDK a uma regra. Certifique-se de adicionar o elemento de dados que você acabou de criar ao evento como os dados XDM. Recomendamos que você envie pelo menos um evento sempre que uma página for carregada.

Para obter mais detalhes sobre como rastrear eventos, consulte [Rastreamento de Eventos](../fundamentals/tracking-events.md).

## Próximas etapas

Depois de ter os dados fluindo, você pode fazer o seguinte:

- [Crie seu schema](https://docs.adobe.com/content/help/pt-BR/experience-platform/xdm/schema/composition.html)
- [Saiba mais sobre como depurar](../fundamentals/debugging.md)
- Saiba como [personalizar a experiência](../fundamentals/rendering-personalization-content.md)
- Saiba mais sobre como enviar dados para várias soluções
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
