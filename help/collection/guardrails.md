---
title: Contratos e alvos de nível de serviço
description: Saiba como configurar a autenticação para a API do Servidor de Rede de Borda
seo-description: Learn how to configure authentication for the Edge Network Server API
keywords: coleta de dados, coleta, rede de borda, api, sla, slt, níveis de serviço
hide: true
hidefromtoc: true
source-git-commit: 92b3a7bff576f72edc8628a850a2cdb9b43cb1c4
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---


# Medidas de proteção

## Visão geral {#overview}

A Adobe usará esforços comercialmente razoáveis para fazer com que a [!DNL Server API] disponível dentro de uma percentagem mensal de tempo de atividade de pelo menos 99,9% para cada região, durante qualquer ciclo de faturação mensal.

## Definições

* **Disponibilidade** é calculada para cada intervalo de cinco minutos como a porcentagem de solicitações processadas pela rede de borda da Experience Adobe Experience Platform que não falham com erros e estão relacionadas apenas às APIs de rede de borda da Adobe Experience Platform provisionadas. Se um locatário não fez solicitações em um intervalo de cinco minutos específico, esse intervalo é considerado como 100% disponível.
* **Porcentagem de tempo de atividade mensal** para uma determinada região é calculada como a média da disponibilidade para todos os intervalos de cinco minutos em um mês.
* Um **upstream** é um serviço por trás da Rede Adobe Edge, habilitado para um armazenamento de dados específico, como o Adobe Server Side Forwarding, Adobe Edge Segmentation ou Adobe Target.
* A **solicitação** enviada para a API do servidor é definida como uma ou mais unidades de solicitação.
* A **unidade de solicitação** corresponde a um fragmento de 8 KB de uma solicitação e um upstream configurado para um armazenamento de dados.
* Um **erro** é qualquer solicitação que falha devido a uma rede de borda Adobe Experience Platform [erro de serviço interno](error-handling.md).

## Objetivos internos

As equipes de engenharia de Adobe implantam praticamente os procedimentos de telemetria, monitoramento e dimensionamento em tempo real para garantir os seguintes alvos:

* Menos de 1% das solicitações HTTP retornam `5xx` erros nos últimos cinco minutos
* Menos de 1% das conexões upstream retornam um erro nos últimos cinco minutos
* Qualquer capacidade do locatário é dobrada em menos de 10 minutos a partir do momento em que um limite é atingido.

## Exclusões de contrato de nível de serviço

O compromisso de nível de serviço descrito acima não se aplica a problemas de indisponibilidade ou desempenho causados pelos seguintes eventos:

* Fatores fora do nosso controlo razoável, incluindo o acesso à Internet ou problemas conexos para além da infraestrutura de Adobe.
* Qualquer uso indevido da [!DNL Server API], conforme definido pelos limites descritos abaixo.

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

