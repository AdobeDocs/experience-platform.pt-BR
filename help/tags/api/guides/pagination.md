---
title: Paginação de respostas na API do reator
description: Saiba como paginar resultados ao listar recursos na API de reator.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# Paginação de respostas na API do reator

As respostas retornadas pela API do Reator são paginadas. O tamanho padrão da página é de 25 elementos. Detalhes sobre a paginação são relatados na seção `meta.pagination `do objeto de resposta da API:

```json
"meta": {
  "pagination": {
      "current_page": 1,
      "next_page": 2,
      "prev_page": null,
      "total_pages": 4,
      "total_count": 90
  }
}
```

É possível obter uma página específica e modificar o tamanho de uma página incluindo um parâmetro de consulta `page` no caminho da solicitação.

## Recuperar uma página específica

Para obter uma página específica:

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[number]={PAGE_NUMBER}
```

## Alterar o tamanho da página

Para alterar o tamanho da página:

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}
```

Opções diferentes podem ser combinadas:

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}&page[number]={PAGE_NUMBER}
```
