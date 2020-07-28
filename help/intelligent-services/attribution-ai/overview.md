---
keywords: Experience Platform;attribution ai;overview;popular topics
solution: Experience Platform
title: Visão geral do Attribution AI
topic: Attribution AI
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---


# Visão geral do Attribution AI

Attribution AI, como parte dos Serviços inteligentes, é um serviço de atribuição de vários canais, algorítmico, que calcula a influência e o impacto incremental das interações do cliente em relação aos resultados especificados. Com o Attribution AI, os profissionais de marketing podem medir e otimizar os gastos com marketing e publicidade, entendendo o impacto de cada interação individual do cliente em cada fase das viagens do cliente.

## Como entender o Attribution AI

O Attribution AI é usado para atribuir créditos a pontos de contato que levam a eventos de conversão. Isso pode ser usado pelos comerciantes para ajudar a quantificar o impacto de marketing de cada ponto de contato de marketing individual em viagens de clientes. Exemplos de pontos de contato incluem impressões de anúncio de exibição, envios por email, aberturas de email e cliques de pesquisa pagos.

As saídas de Attribution AI podem ser segregadas em várias dimensões e podem ser utilizadas em diferentes estágios da jornada do cliente. Isso é feito sem a necessidade de traduzir as necessidades de negócios para problemas de aprendizado em máquinas, escolher algoritmos, treinamento ou implantar modelos.

Os dados do Attribution AI podem ser de Adobe (por exemplo, [!DNL Analytics]) ou fontes de dados não Adobe.

O Attribution AI suporta duas categorias de pontuações, algorítmicas e baseadas em regras. As pontuações algorítmicas incluem pontuações incrementais e influenciadas. As pontuações baseadas em regras incluem Primeiro toque, Último toque, Linear, em forma de U e Decaimento de tempo.

O vídeo a seguir foi projetado para oferecer suporte à sua compreensão do Attribution AI.

>[!VIDEO](https://video.tv.adobe.com/v/32667?learn=on&quality=12)

## Pontuações algorítmicas do Attribution AI

O Attribution AI suporta duas categorias de pontuações de atribuição, pontuações algorítmicas e baseadas em regras.

O Attribution AI produz dois tipos diferentes de pontuações algorítmicas, incrementais e influenciadas. Uma pontuação influenciada é a fração da conversão pela qual cada ponto de contato de marketing é responsável. Uma pontuação incremental é a quantidade de impacto marginal causado diretamente pelo ponto de contato de marketing. A principal diferença entre a pontuação incremental e a pontuação influenciada é que a pontuação incremental leva o efeito da linha de base em consideração. Não presume que a conversão seja causada apenas pelos pontos de contato de marketing anteriores.

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

O Attribution AI pode ser usado para auxiliar nos seguintes casos de uso de exemplo:

- **relatórios** executivo: Permita que os executivos compreendam o verdadeiro impacto incremental do marketing, tanto por canal, região, SKU etc.
- **Dotação** orçamental: Informe as decisões de alocação de orçamento no canal de marketing.
- **Otimização** da Campanha: Dentro de cada canal, entenda quais campanhas, criações e palavras-chave estão funcionando melhor para quais SKUs ou Geos. Isso permite que você veja cada canal para que a equipe de marketing possa otimizar suas táticas.
- **Atribuição** de funil completo: Entenda o impacto do marketing em toda a jornada do cliente. Por exemplo, assinatura de conta gratuita para conversão paga e além.
- **Avaliações** do parceiro: Avaliar a eficácia das agências e dos parceiros, com base nos resultados da atribuição.

### Recursos adicionais

O Attribution AI também oferta a integração com outras soluções Adobe como [!DNL Adobe Analytics]. Isso permite que você use essas soluções para utilizar o modelo algorítmico personalizável para avaliar o desempenho da mídia e fornecer insights analíticos.

## Próximas etapas

Você pode começar seguindo o guia de [introdução](./getting-started.md) . Este guia o orienta a configurar todas as pré-solicitações necessárias para o Attribution AI. Se você já tiver suas credenciais e dados prontos, visite o guia [do usuário do](./user-guide.md)Attribution AI. Este guia aborda a criação de uma instância e o envio para treinamento e pontuação.