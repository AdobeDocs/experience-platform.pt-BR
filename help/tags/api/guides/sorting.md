---
title: Classificação de respostas na API do reator
description: Saiba como filtrar resultados ao listar recursos na API de reator.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# Classificação de respostas na API do reator

A listagem de endpoints na API do Reator permite classificar recursos retornados com base em atributos especificados. Você pode configurar a ordem de classificação da resposta fornecendo um parâmetro `sort` no caminho da solicitação.

## Classificação crescente

Os recursos podem ser classificados por um atributo em ordem crescente especificando a variável
atributo pelo qual classificar e prefixando com um `+`:

`GET /companies/:company_id/properties?sort=+name`

## Classificar decrescente

Os recursos podem ser classificados por um atributo em ordem decrescente especificando a variável
atributo pelo qual classificar e prefixando com um `-`:

`GET /companies/:company_id/properties?sort=-name`

## Várias classificações

Para classificar por vários valores, forneça as diretivas de classificação como separadas por vírgulas
lista:

`GET /companies/:company_id/properties?sort=+name,-org_id`
