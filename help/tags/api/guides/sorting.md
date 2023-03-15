---
title: Classificação de respostas na API do Reactor
description: Saiba como filtrar resultados ao listar recursos na API do Reactor.
exl-id: 49dcf0b6-4ce8-41d9-9e3a-e44f5c0ff905
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 100%

---

# Classificação de respostas na API do Reactor

A listagem de endpoints na API do Reactor permite classificar recursos retornados com base em atributos especificados. É possível configurar a ordem de classificação da resposta fornecendo um parâmetro `sort` no caminho da solicitação.

## Classificação crescente

Para classificar os recursos por um atributo em ordem crescente, especifique o
atributo pelo qual classificar e adicione como prefixo a ele um `+`:

`GET /companies/:company_id/properties?sort=+name`

## Classificação decrescente

Para classificar os recursos por um atributo em ordem decrescente, especifique o
atributo pelo qual classificar e adicione como prefixo a ele um `-`:

`GET /companies/:company_id/properties?sort=-name`

## Várias classificações

Para classificar por vários valores, forneça as diretivas de classificação como uma 
lista separada por vírgulas:

`GET /companies/:company_id/properties?sort=+name,-org_id`
