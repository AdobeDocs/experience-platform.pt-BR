---
title: Medidas de proteção de desempenho para a API do servidor de Edge Network
description: Saiba como usar a API do servidor em medidas de proteção de desempenho ideais.
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: 5d6b70e397a252e037589c3200053ebcb7eb8291
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 2%

---


# Medidas de proteção de desempenho para a API do servidor de Edge Network

## Visão geral {#overview}

As medidas de proteção de desempenho definem limites de uso relacionados aos casos de uso da API do servidor. Ultrapassar as medidas de proteção de desempenho descritas neste artigo pode resultar em degradação do desempenho.

O Adobe não é responsável pela degradação do desempenho causada por limites de uso excedidos. Os clientes que excederem consistentemente as medidas de proteção de desempenho podem solicitar capacidade de processamento adicional para evitar a degradação do desempenho.

>[!IMPORTANT]
>
>Verifique os direitos de licença em sua Ordem de venda e a correspondência [Descrição do produto](https://helpx.adobe.com/legal/product-descriptions.html?lang=pt-BR) sobre os limites de uso reais, além desta página de medidas de proteção.

## Definições

* **Disponibilidade** é calculado para cada intervalo de cinco minutos como a porcentagem de solicitações processadas pelo Edge Network Experience Platform que não falham com erros e se relacionam apenas às APIs de Edge Network provisionadas. Se um locatário não fizer solicitações em um determinado intervalo de cinco minutos, esse intervalo será considerado 100% disponível.
* **Porcentagem mensal de tempo de atividade** para uma determinada região é calculada como a média da disponibilidade para todos os intervalos de cinco minutos em um mês.
* Um **upstream** é um serviço por trás do Edge Network, habilitado para um fluxo de dados específico, como o encaminhamento pelo lado do servidor do Adobe, a segmentação do Adobe Edge ou o Adobe Target.
* A **unidade de solicitação** corresponde a um fragmento de 8 KB de uma solicitação e um upstream configurado para um fluxo de dados.
* A **solicitação** é uma única mensagem enviada por um aplicativo de propriedade do cliente para o [!DNL Server API]. Uma solicitação pode conter uma ou mais unidades de solicitação.
* Um **erro** é qualquer solicitação que falha devido a um Edge Network [erro de serviço interno](error-handling.md).

## Limites de serviço

Todos os fluxos de dados impõem determinados limites de uso, que controlam principalmente quantos eventos podem ser enviados simultaneamente, seu tamanho e o número de serviços upstream para os quais essas solicitações são roteadas.

### Unidades de solicitação

Todos os limites são aplicados e normalizados durante um período **unidade de solicitação (RU)**, definido como um **Fragmento de 8 KB** de uma solicitação indo para um serviço upstream configurado em um fluxo de dados.

#### Exemplos

| Upstreams configurados por sequência de dados | Tamanho médio de solicitação | Unidades de solicitação |
| --- | --- | --- |
| 1 (Plataforma Adobe) | 8 KB (1 fragmento) | 1 |
| 2 (Plataforma Adobe, Adobe Target) | 8 KB (1 fragmento) | 2 |
| 2 (Plataforma Adobe, Adobe Target) | 16 KB (2 fragmentos) | 4 |
| 2 (Plataforma Adobe, Adobe Target) | 64 KB (8 fragmentos) | 16 |

### Limites de unidades de solicitação

A tabela abaixo mostra os valores de limite padrão. Se precisar de limites de unidade de solicitação mais altos, entre em contato com o representante de conta.

| Endpoint | Unidades de solicitações por segundo |
| --- | --- |
| `/v2/interact` | 4000 |
| `/v2/collect` | 6000 |


### Limite de tamanho de solicitação HTTP

| Formato da carga útil | Tamanho máximo para uma solicitação | Máximo de 8 KB de fragmentos de solicitação |
| --- | --- | --- |
| Texto sem formatação JSON | 64 KB | 8 |


>[!NOTE]
>
>Dependendo do conteúdo em si, os formatos binários geralmente são 20 a 40% mais compactos, permitindo que você envie mais dados do que em JSON de texto simples. Entre em contato com o representante do Atendimento ao cliente se precisar de uma capacidade maior para seus fluxos de dados.

## Próximas etapas

Consulte a documentação a seguir para obter mais informações sobre outras medidas de proteção dos serviços de Experience Platform, informações de latência de ponta a ponta e informações de licenciamento dos documentos Descrição do produto Real-Time CDP:

* [Medidas de proteção do Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagramas de latência de ponta a ponta](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) para vários serviços de Experience Platform.
* [Real-time Customer Data Platform (B2C Edition - Pacotes Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Pacotes Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Pacotes Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
