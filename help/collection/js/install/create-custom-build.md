---
title: Criar um build personalizado do Web SDK usando o pacote NPM
description: Crie uma build personalizada do Web SDK que contenha apenas os módulos necessários.
exl-id: 0ba5ae55-9ec0-41b6-9675-e76ade8ca4cd
source-git-commit: 60447ef6f881bf2a34f5502f2259328bf73d08c0
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 6%

---

# Criar um build personalizado do Web SDK

A biblioteca Experience Platform Web SDK inclui vários módulos para vários recursos, como personalização, identidade, rastreamento de links e muito mais. Dependendo dos casos de uso, talvez você só precise de recursos específicos em vez da biblioteca inteira. A criação de um build personalizado do Web SDK permite selecionar apenas os módulos necessários, reduzindo o tamanho da biblioteca e melhorando o desempenho.

## Casos de uso {#use-case}

A criação de um build personalizado do Web SDK ajuda a reduzir o tamanho da biblioteca e aumentar o desempenho. Veja alguns exemplos:

### Remoção do Media Analytics {#media-analytics-removal}

Se o site não tiver conteúdo de mídia, você poderá excluir os módulos [!DNL Media Analytics] e [!DNL Streaming Media] da compilação. Isso pode reduzir o tamanho de build do Web SDK em até 50% e melhorar a velocidade de carregamento.

### Remoção do Personalization {#personalization}

Se você precisar apenas coletar métricas do usuário e não planeja usar o Adobe Target ou Journey Optimizer para personalização, é possível excluir o módulo [!DNL Personalization]. Isso reduz o tamanho da biblioteca e permite que você colete as métricas necessárias.

## Pré-requisitos {#prerequisites}

Para criar uma build personalizada do Web SDK, é necessário o pacote NPM do Web SDK. Verifique se você tem o [Node.js](https://nodejs.org/en/download/package-manager/all) instalado em sua máquina. Consulte a documentação sobre como [instalar o Web SDK usando o pacote NPM](npm.md) para obter mais detalhes.

## Componentes e dependências {#components-dependencies}

Antes de criar um build personalizado do Web SDK, defina os componentes e comandos do Web SDK que você planeja usar. Alguns comandos dependem dos módulos específicos que estão sendo incluídos na build.

A tabela abaixo mostra a relação entre os módulos Web SDK e os comandos que eles incluem:

| Dependência de módulo | Parâmetros de configuração | Comandos | Categoria de tamanho |
|---------|----------|---------|---------|
| Coletor de atividades | [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) | N/D | Médio |
| Públicos-alvo | N/D | N/D | Pequeno |
| Contexto | [`context`](../commands/configure/context.md) | N/D | Pequeno |
| Mecanismo de regras | `personalizationStorageEnabled` | <ul><li>`evaluateRulesets`</li><li>[`subscribeRulesetItems`](../commands/subscriberulesetitems.md)</li></ul> | Médio |
| Mesclagem de eventos | N/D | `createEventMergeId` | Pequeno |
| Media Analytics Bridge | N/D | [`getMediaAnalyticsTracker`](../commands/getmediaanalyticstracker.md) | Grande |
| Personalização | <ul><li>[`prehidingStyle`](../commands/configure/prehidingstyle.md)</li><li>[`targetMigrationEnabled`](../commands/configure/targetmigrationenabled.md)</li><li>[`autoCollectPropositionInteractions`](../commands/configure/autocollectpropositioninteractions.md)</li></ul> | N/D | Grande |
| Consentimento | [`defaultConsent`](../commands/configure/defaultconsent.md) | [`setConsent`](../commands/setconsent.md) | Pequeno |
| Mídia de transmissão | [`streamingMedia`](../commands/configure/streamingmedia.md) | <ul><li>[`createMediaSession`](../commands/createmediasession.md)</li><li>[`sendMediaEvent`](../commands/sendmediaevent.md)</li></ul> | Grande |

## Criar um build personalizado do Web SDK usando o pacote NPM {#create-custom-build}

1. Abra o terminal e execute o `npx @adobe/alloy`. Você será solicitado a selecionar os componentes do Web SDK que deseja incluir na sua build personalizada.

   ![Imagem de um terminal mostrando a seleção do módulo de compilação personalizada.](../assets/custom-build/npx.png)

   Use as teclas de seta para mover para cima e para baixo na lista de módulos.

   * Pressione **Espaço** para habilitar ou desabilitar o módulo selecionado.
   * Pressione `A` para ativar ou desativar todos os módulos.
   * Pressione `I` para inverter sua seleção.
   * Pressione `Enter` para confirmar sua seleção e ir para a próxima etapa.

1. Depois de selecionar os módulos a serem incluídos na build personalizada, você pode escolher entre salvar uma versão minificada ou não da build da biblioteca personalizada do Web SDK. Selecione a opção desejada e pressione `Enter`.

   ![Imagem de um terminal mostrando a seleção de minificação de compilação personalizada.](../assets/custom-build/minify.png)

1. Em seguida, você será perguntado onde deseja salvar a criação no computador local. Pressione `Enter` para confirmar o local pré-selecionado ou insira um novo local.

   ![Imagem de um terminal mostrando a opção de salvamento de compilação personalizada.](../assets/custom-build/save.png)

1. Depois de confirmar o local, a build personalizada é gerada e salva.

   ![Imagem de um terminal mostrando o local salvo da compilação personalizada.](../assets/custom-build/saved.png)
