---
title: Notas
description: Saiba como adicionar anotações textuais a determinados recursos de tags no Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 78%

---

# Notas

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Notas são anotações textuais que podem ser adicionadas a determinados recursos de tags no Adobe Experience Platform. As notas podem ser anexadas aos seguintes recursos:

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

Selecione **[!UICONTROL Notas]** para expandir o painel direito e exibir as notas, com as mais recentes no topo. Para adicionar uma nova nota, digite o texto da nota na caixa na parte superior e selecione **[!UICONTROL Adicionar nota]**.

## Outras

* As notas nos recursos de tag correspondem ao comportamento das notas no DTM, na medida em que são imutáveis e não podem ser editadas ou excluídas.
* Ao exibir revisões anteriores de um recurso, somente as notas que foram criadas antes da `created_at` data dessa revisão são exibidas.
* Quando você exclui um recurso, todas as notas anexadas ao recurso também são excluídas.
