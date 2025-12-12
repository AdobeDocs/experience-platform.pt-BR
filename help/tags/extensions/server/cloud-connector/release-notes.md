---
title: Notas de versão da extensão do conector de nuvem da Adobe Experience Platform
description: As notas de versão mais recentes da extensão do conector de nuvem da Adobe Experience Platform.
exl-id: 5ee85d9f-71f4-46ee-9064-4ceee1cf90e7
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 100%

---

# Notas de versão da extensão do conector de nuvem da Adobe Experience Platform

## 17 de janeiro de 2023

v1.0.1

* Correção de um problema em que um JSON válido colado na área de texto bruto do corpo era salvo como uma string em vez de um JSON.
* Não permita que o corpo seja definido em solicitações GET ou HEAD.
* Correção de um erro em que salvar uma resposta com mais de 5 kb resultaria na falha da execução da regra.
