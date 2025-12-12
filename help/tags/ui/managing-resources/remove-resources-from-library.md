---
title: Remover recursos de uma biblioteca
description: Saiba como remover recursos de uma biblioteca de tags.
exl-id: ad1dd093-962c-4f6d-85eb-c5ed1b644927
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 100%

---

# Remover recursos de uma biblioteca

Caso não deseje mais que um recurso tenha um efeito em uma build, remova-o da biblioteca que contém esse recurso e crie uma nova build.

>[!IMPORTANT]
>
>Os recursos nas bibliotecas são interdependentes. Remover um recurso de uma build pode alterar o comportamento de outros recursos na build.

O processo de remoção funciona de forma um pouco diferente, dependendo do estado em que a biblioteca está.

## Bibliotecas de desenvolvimento

Os recursos em bibliotecas de desenvolvimento podem ser manipulados diretamente.

1. Abra a biblioteca.
1. Remova o recurso.
1. Salve a biblioteca.
1. Crie a biblioteca.

## Bibliotecas enviadas e aprovadas

Os recursos que estão nas bibliotecas enviadas ou aprovadas não podem ser manipulados diretamente. Você precisará mover a biblioteca de volta para o estado de desenvolvimento.

1. Rejeitar a biblioteca (move a biblioteca de volta para o desenvolvimento).
1. Siga as etapas em “Bibliotecas de desenvolvimento” acima, para remover recursos das bibliotecas de desenvolvimento.

## Bibliotecas de produção

Remover recursos de uma biblioteca de produção é o caso mais complexo. Não é possível manipular os recursos da biblioteca nesse estado e você também não pode mover essas bibliotecas de volta para o estado de desenvolvimento.

Em vez disso, você deve desabilitar o recurso. Desabilitar é uma alteração que você depois adiciona a uma biblioteca de desenvolvimento como qualquer outra alteração. Quando essa alteração é colocada em produção, o recurso é movido da biblioteca de produção.

1. Desabilite o recurso.
   1. Selecione o recurso na exibição em lista.
   1. Selecione **[!UICONTROL Disable]**.
1. Crie uma nova biblioteca de desenvolvimento.
1. Adicione `latest` a versão do recurso desabilitado.
1. Salve e crie.
1. Siga o processo normal para a promoção de bibliotecas para produção.
1. Publique para produção para remover o recurso.
