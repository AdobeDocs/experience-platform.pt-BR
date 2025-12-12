---
title: Notas de versão da extensão do Adobe Target v2
description: As mais recentes notas de versão de extensão de tag do Adobe Target v2 na Adobe Experience Platform.
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 41%

---

# Notas de versão da extensão Adobe Target v2

## v0.20.3 (23 de janeiro de 2024)

- Atualizado para oferecer suporte ao `at.js` 2.11.4
- Correção de um erro para impedir que dados geográficos inválidos fossem enviados para a API de entrega.

## v0.20.2 (29 de novembro de 2023)

- Atualizado para oferecer suporte a `at.js` 2.11.3
- Correção de um bug que impedia o envio de tokens de resposta em eventos at-content-rendering-failed.

## v0.20.1 (3 de novembro de 2023)

- Atualizado para oferecer suporte ao `at.js` 2.11.2.
- Correção de um bug que causava inconsistências nos tokens de resposta enviados em eventos personalizados.

## v0.20.0 (9 de outubro de 2023)

- Atualizado para oferecer suporte a `at.js` 2.11.0.
- Adição de suporte para configuração de sandboxId e sandboxName Adobe Experience Platform personalizados em targetGlobalSettings, que serão passados para a API de entrega nas chamadas getOffer/getOffers.
- Correção de DOM de sombra para encadeamento :eq() no seletor.

## v0.19.3 (18 de setembro de 2023)

- Atualizado para oferecer suporte ao `at.js` v2.10.3.
- Correção de um problema que acionava incorretamente o evento personalizado at-content-rendering-succeeded quando nenhuma oferta era renderizada. O evento correto, at-content-rendering-no-offers, agora é acionado.
- Adição de eventToken e responseTokens ao objeto de erro para o evento personalizado at-content-rendering-failed.

## v0.19.2 (14 de fevereiro de 2023)

- Correção de um problema que permitia que o tempo limite fosse definido como um elemento de dados.

## v0.19.1 (3 de fevereiro de 2023)

- Atualizado para oferecer suporte ao `at.js` v2.10.1
- Os parâmetros personalizados da mbox do cliente agora oferecem suporte à notação de pontos corretamente
- As chamadas de entrega não são mais feitas no VEC

## v0.19.0 (19 de setembro de 2022)

- Atualizado para oferecer suporte ao `at.js` v2.10.0
- Adição de suporte ao rastreamento entre domínios.

## v0.18.0 (1 de junho de 2022)

- Atualizado para oferecer suporte ao `at.js` v2.9.0
- Foi adicionado suporte a User Agent Client Hints.

## v0.17.1 (28 de janeiro de 2022)

- Atualizado para oferecer suporte ao `at.js` v2.8.1
- Correção de `pageLoad` que não estava sendo mapeado para `target-global-mbox` no modo de execução híbrido ODD
- Correção de um problema com detalhes de análise para a solicitação `mbox`
- As dependências de desenvolvimento foram atualizadas para corrigir vulnerabilidades de segurança

## v0.17.0 (7 de janeiro de 2022)

- Atualização de suporte para `at.js` v2.8.0, que agora está coletando dados de uso de recursos e de telemetria de desempenho.  Os dados pessoais não são coletados. Para recusar esse recurso, defina `telemetryEnabled` como `false` em `targetGlobalSettings`.

## v0.16.0 (28 de outubro de 2021)

- Atualizado para oferecer suporte ao `at.js` v2.7.0, agora disponível para download na Adobe Target.

## v0.15.2 (16 de agosto de 2021)

- Atualizado para oferecer suporte ao `at.js` 2.6.1.
- Inicialize a Decisão no dispositivo na inicialização independentemente do evento de Carregamento de página.
- A decisão no dispositivo agora pode ser usada na primeira visita após o download do artefato.

## v0.15.1 (20 de julho de 2021)

- Correção de um problema com um conflito de nome de função `stringify`, que resultava na geração de valores UUID incorretos para `sessionId`, `requestId` e assim por diante.

## v0.15.0 (16 de julho de 2021)

- Adicionar atributo seguro aos cookies sempre que `at.js` configurações secureOnly estiver definida como true
- Os tokens de resposta agora estão disponíveis ao usar o `triggerView()`
- Correção de um erro relacionado ao evento `CONTENT_RENDERING_NO_OFFERS`. Agora é acionado corretamente sempre que não há conteúdo retornado do Target
- Os detalhes das métricas de clique do A4T são retornados corretamente ao serem usadas solicitações de pré-busca
- A geração UUID não usa mais `Math.random()`, mas depende de `window.crypto`
- A expiração do cookie `sessionId` é estendida corretamente em cada chamada de rede
- A inicialização do cache de visualização de SPA agora é realizada corretamente e atende às configurações `viewsEnable`

## v0.14.2 (2 de junho de 2021)

- Correção de um erro em que o pacote final contém duas versões do `at.js`, uma com a Decisão no dispositivo e outra sem.

## v0.14.1 (19 de maio de 2021)

- Corrigir regressão introduzida com a versão v0.14, em que a ação Carregar Target disparava chamadas de mbox globais

## v0.14 (14 de maio de 2021)

- Adição de uma nova ação Carregar Destino com [Decisão no Dispositivo](./overview.md#load-target-with-on-device-decisioning), que carrega `at.js` 2.5 com recursos da Decisão no Dispositivo
- Atualizado de `at.js` para 2.5


## v0.13.7 (25 de março de 2021)

- Correção de um problema em que `targetPageParams` era incluído nas solicitações da mBox. `targetPageParams` deve ser incluído somente em solicitações `pageLoad`.
- Correção de um problema em documentos e objetos globais de janela na extensão de tag substituindo as dependências de objetos globais por referências diretas a eles.
- Atualizado `at.js` para 2.4.1.

## v0.13.6 (25 de janeiro de 2021)

- Adiciona suporte à ID unificada de perfil/plataforma ao customerIds da API de entrega
- Corrige a injeção de tag de estilo inválida
- Atualização do at.s para 2.4.0.
- Solução de um problema em que parâmetros indefinidos podem resultar em solicitações de entrega incorretas

## v0.13.4 (25 de novembro de 2020)

- Correção de um erro em que os parâmetros da mBox não eram exibidos na interface
- Atualizações de marca
- Atualização da versão `at.js` para 2.3.3

## v0.13.3 (24 de julho de 2020)

- Correção de um erro que fazia com que os links do modo de QA não funcionassem para atividades inativas
- Correção de um erro quando a extensão falhava se um script ou código adicionasse uma propriedade `default` ao `window` ou `document`

## v0.13.2 (15 de junho de 2020)

- Correção de um problema ao usar a substituição de CNAME e borda, em que o `at.js` 1.x poderia criar incorretamente o domínio do servidor, resultando na falha da solicitação do Target
- Correção de um problema em que, ao ser usada a extensão de tag v2 para a extensão de tag do Target e do Adobe Analytics, o Target atrasava a chamada de sendBeacon do Analytics.
- Aprimoramento da configuração `deviceIdLifetime` ao torná-la substituível via `targetGlobalSettings`.

## v0.13.0 (25 de março de 2020)

- Atualizado `at.js` para v2.3.
- Adição de suporte à Mbox global do Target na API adobe.target.getOffer.
- Correção de um problema em que os parâmetros e os parâmetros de carregamento de página não eram processados corretamente.

## v0.12.0 (10 de outubro de 2019)

- Atualizado `at.js` para v2.2.
- Desempenho aprimorado para integrações entre a biblioteca da Experience Cloud ID (ECID) v4.4 e o `at.js` 2.2.
- Anteriormente, a biblioteca ECID fez duas chamadas de bloqueio antes que `at.js` pudesse buscar experiências. Isso foi reduzido a uma única chamada, o que melhora significativamente o desempenho.

>[!NOTE]
>Atualize sua extensão de tag do ECID para v4.4.1 para aproveitar esse aprimoramento de desempenho.

## v0.11.1 (31 de julho de 2019)

- Versão de extensão atualizada para usar `at.js` 2.1.1
- Adição de uma correção para manipulação de parâmetros.

## v0.11.0 (3 de junho de 2019)

- Nova extensão de tag para oferecer suporte a `at.js` 2.1
