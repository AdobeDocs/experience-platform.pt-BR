---
title: Paginação de respostas na API do Reactor
description: Saiba como paginar resultados ao listar recursos na API do Reactor.
exl-id: bccb6e78-4ac8-4786-b398-6e55109d99dd
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 86%

---

# Paginação de respostas na API do Reactor

As respostas retornadas pela API do Reactor são paginadas. O tamanho de página padrão é de 25 elementos. Há detalhes sobre a paginação na seção `meta.pagination` do objeto de resposta da API:

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
