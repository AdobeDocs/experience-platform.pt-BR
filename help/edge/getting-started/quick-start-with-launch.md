---
title: start rápido com o Launch
seo-title: start rápido do Adobe Experience Platform Web SDK com o Launch
description: Guia de start rápido para usar a extensão do SDK Experience Platform Web para coletar dados
seo-description: Guia de start rápido para usar a extensão do SDK Experience Platform Web para coletar dados
translation-type: tm+mt
source-git-commit: d958e323df2535c168edd3a35b878fcc4bb73370
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 5%

---


# Boas-vindas

Este guia o guia pelas diferentes maneiras de configurar o SDK da Web do Adobe Experience Platform no Launch. Para usar esse recurso, é necessário incluir uma lista de permissões. Se você quiser entrar na lista de espera, entre em contato com seu CSM.

- Ter um domínio [próprio (CNAME)](https://docs.adobe.com/content/help/pt-BR/core-services/interface/ec-cookies/cookies-first-party.html) habilitado. Se você já tiver um CNAME para Analytics, use esse. Testar no desenvolvimento funciona sem um CNAME, mas é necessário um antes de ir para a produção.
- Tenha direito ao Adobe Experience Platform. Se você não tiver comprado a Platform, a Adobe fornecerá a Experience Platform Data Services Foundation para uso limitado com o SDK, sem custos adicionais.
- Use a versão mais recente do serviço de ID de Visitante.

## Preparar um Schema

A Experience Platform Edge Network utiliza dados como XDM. O XDM é um formato de dados que permite definir schemas. O schema define como o Edge Network espera que os dados sejam formatados. Para enviar dados, você deve definir seu schema.

1. [Criar um schema](../../xdm/tutorials/create-schema-ui.md)
2. Adicione a combinação AEP [!DNL Web SDK ExperienceEvent] ao schema criado.
3. Crie um conjunto de dados a partir do schema que você criou.

O vídeo a seguir tem o objetivo de oferecer suporte para a criação de um schema, conjunto de dados e conector de fonte de streaming para seus [!DNL Web SDK] dados.

Efetue login em Iniciar e instale a `AEP Web SDK` extensão. Ao instalar o SDK, você será solicitado a configurar a extensão. Insira a ID de configuração solicitada acima. A extensão preenche automaticamente a ID da empresa.


Para obter mais detalhes sobre diferentes opções de configuração, consulte [Configuração do SDK](../fundamentals/configuring-the-sdk.md).

## Criar uma ID de configuração

Você pode criar uma ID de configuração usando a ferramenta [de configuração de](../fundamentals/edge-configuration.md) borda no Launch. Isso permite habilitar a Edge Network para enviar dados para as várias soluções. Detalhes sobre como localizar cada opção são encontrados na Página da Ferramenta [de Configuração de](../fundamentals/edge-configuration.md) Borda.

>[!NOTE]
>
>Sua organização deve estar na lista de permissões para este recurso. Entre em contato com o seu CSM para ser colocado na lista para uma eventual lista de permissões.

## Criar um elemento de dados com base no seu Schema

Em Iniciar, crie um Elemento de dados que faça referência ao schema alterando a extensão para AEP Web SDK e definindo o tipo como `XDM Object`. Isso carrega seu schema e permite mapear elementos de dados em diferentes partes do schema.

![Elemento de data na inicialização](../../assets/edge_data_element.png)

## Enviar um evento

Depois que a extensão é instalada, o start envia eventos adicionando uma `sendEvent` ação da extensão AEP Web SDK a uma regra. Adicione o elemento de dados que você acabou de criar ao evento como os dados XDM. O Adobe recomenda que você envie pelo menos um evento sempre que uma página for carregada.

Para obter mais detalhes sobre como rastrear eventos, consulte [Rastreamento de Eventos](../fundamentals/tracking-events.md).

## Próximas etapas

Depois de ter os dados fluindo, você pode fazer o seguinte.

- [Crie seu schema](https://docs.adobe.com/content/help/pt-BR/experience-platform/xdm/schema/composition.html)
- [Saiba mais sobre como depurar](../fundamentals/debugging.md)
- Saiba como [personalizar a experiência](../fundamentals/rendering-personalization-content.md)
- Saiba mais sobre como enviar dados para várias soluções
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
