---
title: Medidas de proteção de desempenho para a API do Servidor de Rede de Borda
description: Saiba como usar a API do servidor em medidas de proteção de desempenho ideais.
keywords: coleta de dados, coleta, rede de borda, api, sla, slt, níveis de serviço
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 2%

---

# Medidas de proteção de desempenho para a API do Servidor de Rede de Borda

## Visão geral {#overview}

As medidas de proteção de desempenho definem limites de uso relacionados aos casos de uso da API do servidor. Exceder as medidas de proteção de desempenho descritas neste artigo pode resultar em degradação do desempenho.

O Adobe não é responsável pela degradação do desempenho causada por limites de uso excedidos. Os clientes que excedem consistentemente as medidas de proteção de desempenho podem solicitar capacidade de processamento adicional para evitar a degradação do desempenho.

## Definições

* **Disponibilidade** é calculada para cada intervalo de cinco minutos como a porcentagem de solicitações processadas pela rede de borda do Experience Platform que não falham com erros e estão relacionadas apenas às APIs de rede de borda provisionadas. Se um locatário não fez solicitações em um intervalo de cinco minutos específico, esse intervalo é considerado como 100% disponível.
* **Porcentagem de tempo de atividade mensal** para uma determinada região é calculada como a média da disponibilidade para todos os intervalos de cinco minutos em um mês.
* Um **upstream** é um serviço atrás da Edge Network, habilitado para um armazenamento de dados específico, como o Adobe Server Side Forwarding, Adobe Edge Segmentation ou Adobe Target.
* A **unidade de solicitação** corresponde a um fragmento de 8 KB de uma solicitação e um upstream configurado para um armazenamento de dados.
* A **solicitação** é uma única mensagem enviada por um aplicativo de propriedade do cliente para o [!DNL Server API]. Uma solicitação pode conter uma ou mais unidades de solicitação.
* Um **erro** é qualquer solicitação que falha devido a uma rede de borda [erro de serviço interno](error-handling.md).

## Limites de serviço

Todos os conjuntos de dados impõem determinados limites de uso, que controlam principalmente quantos eventos podem ser enviados simultaneamente, seu tamanho e o número de serviços upstream para os quais essas solicitações são roteadas.

### Unidades de solicitação

Todos os limites são aplicados e normalizados ao longo de um **unidade de pedido (RU)**, definido como um **Fragmento de 8 KB** de uma solicitação que vai para um serviço upstream configurado em um armazenamento de dados.

#### Exemplos

| Upstreams configurados por armazenamento de dados | Tamanho médio da solicitação | Unidades de solicitação |
| --- | --- | --- |
| 1 (Plataforma Adobe) | 8 KB (1 fragmento) | 1 |
| 2 (Adobe Platform, Adobe Target) | 8 KB (1 fragmento) | 2 |
| 2 (Adobe Platform, Adobe Target) | 16 KB (2 fragmentos) | 4 |
| 2 (Adobe Platform, Adobe Target) | 64 KB (8 fragmentos) | 16 |

### Limites de unidades de solicitação

A tabela abaixo mostra os valores limite padrão. Se precisar de limites de unidade de solicitação mais altos, entre em contato com o representante de conta.

| Endpoint | Unidades de solicitação por segundo |
| --- | --- |
| `/v2/interact` | 4000 |
| `/v2/collect` | 6000 |


### Limite de tamanho da solicitação HTTP

| Formato de carga | Tamanho máximo de uma solicitação | Fragmentos de solicitação de no máximo 8 KB |
| --- | --- | --- |
| Texto simples JSON | 64 KB | 8 |


>[!NOTE]
>
>Dependendo da própria carga, os formatos binários geralmente são 20-40% mais compactos, permitindo que você envie mais dados do que faria no JSON de texto simples. Entre em contato com seu representante de Atendimento ao cliente se precisar de uma capacidade maior para seus conjuntos de dados.
