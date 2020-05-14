---
title: start rápido com o Launch
seo-title: start rápido do SDK da Web do Adobe Experience Platform com Launch
description: Guia de start rápido para usar a extensão do SDK da Web da Experience Platform para coletar dados
seo-description: Guia de start rápido para usar a extensão do SDK da Web da Experience Platform para coletar dados
translation-type: tm+mt
source-git-commit: 2ccb2c17590780f7f1bd5e553164209763ab9e24
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 3%

---


# Boas-vindas

Este guia o orientará pelas diferentes formas de configurar o SDK da Web da plataforma Adobe Experience no Launch. Para poder usar este recurso, é necessário ter uma lista de permissões. Se você quiser entrar na lista de espera, entre em contato com seu CSM.

- Ter um domínio [próprio (CNAME)](https://docs.adobe.com/content/help/pt-BR/core-services/interface/ec-cookies/cookies-first-party.html) habilitado. Se você já tiver um CNAME para o Analytics, use esse. O teste no desenvolvimento funcionará sem um CNAME, mas você precisará de um antes de ir para a produção
- Esteja qualificado para a Plataforma de dados da plataforma Adobe Experience. Se você não tiver adquirido a plataforma, forneceremos à Experience Platform Data Services Foundation para uso limitado com o SDK, sem custos adicionais.
- Usar a versão mais recente do serviço de ID de Visitante

## Criar uma ID de configuração

Você pode criar uma ID de configuração usando a ferramenta [de configuração de](../fundamentals/edge-configuration.md) borda na inicialização. Isso permitirá que você ative a rede Edge para enviar dados para as várias soluções. Detalhes sobre como localizar cada opção são encontrados na Página da Ferramenta [de Configuração de](../fundamentals/edge-configuration.md) Borda.

>[!NOTE]
>
>Sua organização deve estar na lista de permissões do recurso. Entre em contato com o seu CSM para ser colocado na lista para uma eventual lista de permissões.

## Preparar um Schema

A Experience Platform Edge Network utiliza os dados como XDM. O XDM é um formato de dados que permite definir schemas. O schema define como o Edge Network espera que os dados sejam formatados. Para enviar dados, você precisará definir seu schema.

- [Criar um schema](../../xdm/tutorials/create-schema-ui.md)
- Adicionar a combinação do SDK da Web da plataforma Adobe Experience ao schema criado

## Instalar o SDK no Launch

Efetue login em Iniciar e instale a `AEP Web SDK` extensão. Como parte da instalação do SDK, você será solicitado a configurar a extensão. Insira a ID de configuração solicitada acima. A extensão preenche automaticamente a ID da empresa.

Para obter mais detalhes sobre diferentes opções de configuração, consulte [Configuração do SDK](../fundamentals/configuring-the-sdk.md).

## Criar uma base de elementos de dados em seu Schema

Na inicialização, crie um Elemento de dados que faça referência ao schema alterando a extensão para AEP Web SDK e definindo o tipo como Objeto XDM. Isso carregará seu schema e permitirá que você mapeie os elementos de dados em diferentes partes do schema.

![Elemento de data na inicialização](../../assets/edge_data_element.png)

## Enviar um evento

Depois que a extensão é instalada, o start envia eventos adicionando uma ação &quot;sendEvent&quot; da extensão AEP Web SDK a uma regra. Certifique-se de adicionar o elemento de dados que você acabou de criar ao evento como os dados XDM. Recomendamos que você envie pelo menos um evento sempre que uma página for carregada.

Para obter mais detalhes sobre como rastrear eventos, consulte [Rastreamento de Eventos](../fundamentals/tracking-events.md).

## Próximas etapas

Depois que os dados estiverem fluindo, você poderá fazer o seguinte.

- [Crie seu schema](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)
- [Saiba mais sobre como depurar](../fundamentals/debugging.md)
- Saiba como [personalizar a experiência](../fundamentals/rendering-personalization-content.md)
- Saiba mais sobre como enviar dados para várias soluções
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
