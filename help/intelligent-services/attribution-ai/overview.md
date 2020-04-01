---
keywords: Experience Platform;attribution ai;overview;popular topics
solution: Experience Platform
title: Visão geral do AI de atribuição
topic: Attribution AI
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# Visão geral do AI de atribuição

A Atribuição AI, como parte dos Serviços inteligentes, é um serviço de atribuição algorítmico e com vários canais que calcula a influência e o impacto incremental das interações do cliente em relação aos resultados especificados. Com a Atribuição AI, os profissionais de marketing podem medir e otimizar o gasto de marketing e publicidade ao compreender o impacto de cada interação individual do cliente em cada fase das viagens do cliente.

## Compreensão da IA de atribuição

O AI de atribuição é usado para atribuir créditos a pontos de contato que levam a eventos de conversão. Isso pode ser usado pelos comerciantes para ajudar a quantificar o impacto de marketing de cada ponto de contato de marketing individual em viagens de clientes. Exemplos de pontos de contato incluem impressões de anúncio de exibição, envios por email, aberturas de email e cliques de pesquisa pagos.

As saídas de IA de atribuição podem ser segregadas em várias dimensões e podem ser utilizadas em diferentes estágios da jornada do cliente. Isso é feito sem a necessidade de traduzir as necessidades de negócios para problemas de aprendizado em máquinas, escolher algoritmos, treinamento ou implantar modelos.

Os dados da AI de atribuição podem ser da Adobe (por exemplo, Analytics) ou de fontes de dados que não são da Adobe.

O AI de atribuição suporta duas categorias de pontuações, algorítmicas e baseadas em regras. As pontuações algorítmicas incluem pontuações incrementais e influenciadas. As pontuações baseadas em regras incluem Primeiro toque, Último toque, Linear, em forma de U e Decaimento de tempo.

## Pontuações algorítmicas de atribuição AI

O AI de atribuição suporta duas categorias de pontuações de atribuição, pontuações algorítmicas e baseadas em regras.

O AI de atribuição produz dois tipos diferentes de pontuações algorítmicas, incrementais e influenciadas. Uma pontuação influenciada é a fração da conversão pela qual cada ponto de contato de marketing é responsável. Uma pontuação incremental é a quantidade de impacto marginal causado diretamente pelo ponto de contato de marketing. A principal diferença entre a pontuação incremental e a pontuação influenciada é que a pontuação incremental leva o efeito da linha de base em consideração. Não presume que a conversão seja causada apenas pelos pontos de contato de marketing anteriores.

Consulte a tabela abaixo para obter mais detalhes sobre cada uma dessas pontuações de atribuição:

| Pontuações de atribuição | Descrição |
| ----- | ----------- |
| Primeiro contato | A pontuação de atribuição baseada em regras que atribui todos os créditos ao ponto de contato inicial em um caminho de conversão. |
| Último contato | A pontuação de atribuição baseada em regras que atribui todo o crédito ao ponto de contato mais próximo da conversão. |
| Linear | A pontuação de atribuição baseada em regras que atribui crédito igual a cada ponto de contato em um caminho de conversão. |
| Forma de U | Pontuação de atribuição baseada em regras que atribui 40% do crédito ao primeiro ponto de contato e 40% do crédito ao último ponto de contato, com os outros pontos de contato dividindo os restantes 20% igualmente. |
| Declínio de tempo | A pontuação de atribuição baseada em regras na qual os pontos de contato mais próximos da conversão recebem mais crédito do que os pontos de contato mais distantes no tempo da conversão. |
| Influenciado (algorítmico) | A pontuação influenciada é a fração da conversão pela qual cada ponto de contato de marketing é responsável. |
| Incremental (algorítmico) | A pontuação incremental é a quantidade de impacto marginal causado diretamente por um ponto de contato de marketing. |

## Exemplos de casos de uso comercial

A IA de atribuição pode ser usada para auxiliar nos seguintes casos de uso de exemplo:

- **relatórios** executivo: Permita que os executivos compreendam o verdadeiro impacto incremental do marketing, tanto por canal, região, SKU etc.
- **Dotação** orçamental: Informe as decisões de alocação de orçamento no canal de marketing.
- **Otimização** da Campanha: Dentro de cada canal, entenda quais campanhas, criações e palavras-chave estão funcionando melhor para quais SKUs ou Geos. Isso permite que você veja cada canal para que a equipe de marketing possa otimizar suas táticas.
- **Atribuição** de funil completo: Entenda o impacto do marketing em toda a jornada do cliente. Por exemplo, assinatura de conta gratuita para conversão paga e além.
- **Avaliações** do parceiro: Avaliar a eficácia das agências e dos parceiros, com base nos resultados da atribuição.

### Recursos adicionais

O AI de atribuição também oferta a integração com outras soluções da Adobe, como o Adobe Analytics. Isso permite que você use essas soluções para utilizar o modelo algorítmico personalizável para avaliar o desempenho da mídia e fornecer insights analíticos.

## Próximas etapas

Você pode começar seguindo o guia de [introdução](./getting-started.md) . Este guia o orienta a configurar todas as pré-solicitações necessárias para a Atribuição AI. Se você já tiver suas credenciais e dados prontos, visite o guia [do usuário da](./user-guide.md)Atribuição AI. Este guia aborda a criação de uma instância e o envio para treinamento e pontuação.