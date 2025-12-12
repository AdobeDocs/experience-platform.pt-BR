---
title: Notas
description: Saiba como adicionar anotações textuais a determinados recursos de tag na Adobe Experience Platform.
exl-id: 14d6b6a1-3bd0-4181-8181-e6b35c197a44
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 100%

---

# Notas

Notas são anotações textuais que podem ser adicionadas a determinados recursos de tags na Adobe Experience Platform. As notas podem ser anexadas aos seguintes recursos:

* Extensões
* Elementos de dados
* Regras
* Componentes da regra
* Bibliotecas
* Propriedades

As observações podem conter até 512 caracteres Unicode.

Observações são comentários que não têm impacto no comportamento dos recursos a que estão associados. Eles não estão incluídos em bibliotecas construídas. Você pode usar observações para:

* Fornecer informações de fundo sobre um recurso
* Função como uma lista de itens a fazer para aprimoramentos futuros
* Enviar recomendações de uso de recursos para outros usuários
* Dar instruções aos outros membros da equipe
* Registrar contexto histórico
* Lembre-se do que um recurso faz, por que ele é construído da maneira que ele é, ou onde ele é usado

## Criar notas

Os recursos notáveis exibem um trilho estreito no lado direito da tela. O painel inclui um ícone para notas. Este ícone exibe o número atual de notas anexadas ao recurso.

Selecione **[!UICONTROL Notes]** para expandir o painel direito e exibir as notas, com as mais recentes na parte superior.  Para adicionar uma nova nota, digite o texto da nota na caixa na parte superior e selecione **[!UICONTROL Add Note]**.

## Outras

* As notas nos recursos de tags correspondem ao comportamento das notas no DTM, pois são imutáveis e não podem ser editadas nem excluídas.
* Ao exibir revisões anteriores de um recurso, somente as notas que foram criadas antes da `created_at` data dessa revisão são exibidas.
* Quando você exclui um recurso, todas as notas anexadas ao recurso também são excluídas.
