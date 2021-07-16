---
title: Notas de versão da extensão da camada de dados do cliente da Adobe
description: As notas de versão mais recentes da extensão de tag da Camada de dados do cliente da Adobe na Adobe Experience Platform.
source-git-commit: 8dfb7bdc16d0654ee1d76dc5f5af50938b122d33
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 100%

---

# Notas de versão da extensão da Camada de dados do cliente da Adobe

## Versão 2.0.2

* Carregamento da biblioteca principal ACDL (versão 2.0.2)
* A versão 2.0.0 da biblioteca principal ACDL removeu a capacidade de aproveitar event.beforeState e event.afterState. Dessa forma, modificamos esses objetos para sempre retornar objetos vazios. As implementações que dependem dessa funcionalidade precisarão ser atualizadas ao migrar para essa versão.

## Versão 1.1.3

* Carregamento da biblioteca principal ACDL (versão 1.1.3)

## Versão 1.1.2

A seguinte funcionalidade é fornecida pela extensão na versão inicial:

* Carregamento da biblioteca principal ACDL (versão 1.1.1)
* Renomear a camada de dados da Adobe
* Eventos:
   * Acompanhamento de todos os eventos
   * Acompanhamento de todos os dados enviados
   * Acompanhamento de um evento específico enviado
   * Todos os eventos podem ser acompanhados em escopos diferentes
* Elementos de dados:
   * Estado calculado: estado global ou específico
   * Tamanho da camada de dados
* Ações:
   * Redefinir o tamanho da camada de dados (mantendo o Estado calculado mais recente)
   * Enviar objeto para a camada de dados
