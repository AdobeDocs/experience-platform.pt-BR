---
title: Excluir recursos
description: Saiba como excluir recursos de tags no Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 84%

---

# Excluir recursos

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

A exclusão de um recurso é uma remoção permanente desse recurso do Adobe Experience Platform. Se você ainda quiser que o recurso apareça na interface do usuário da coleta de dados, mas não esteja na biblioteca de tags, consulte [Remover recursos de uma biblioteca](remove-resources-from-library.md).

É possível excluir elementos de dados, regras, extensões, hosts, ambientes e propriedades. Depois da exclusão, esses recursos não poderão ser recuperados.

Os recursos adicionados a bibliotecas (elementos de dados, regras e extensões) têm considerações especiais quando você os exclui.

## Preparar um recurso para exclusão

Há recursos em diferentes estados e eles dependem uns dos outros. Antes de excluir um recurso, verifique se ele está em um estado em que pode ser excluído.

A preparação de um recurso para exclusão consiste em duas etapas básicas:

1. Resolver dependências.
1. Remover das bibliotecas.

### Resolver dependências

As regras, os elementos de dados e as extensões são interdependentes, portanto, na maioria das vezes, ao excluir um, há um efeito em cascata e você tem outras coisas que precisa limpar.

#### Regras

As regras dependem de outros recursos (extensões e elementos de dados), mas não têm recursos que dependam delas. Excluir uma regra significa que não é mais possível usá-la em uma biblioteca ou nem mesmo visualizá-la, mas você não terá dependências para limpar depois.

#### Elementos de dados

Os elementos de dados dependem das extensões, mas diferentemente das regras, os elementos de dados podem ter regras e extensões que dependem deles. Se um elemento de dados for excluído, todas as regras ou extensões que dependerem desse elemento de dados serão afetadas.

Depois de excluído, o elemento de dados não retornará mais o valor correto no tempo de execução. Ele retornará uma string vazia ou o nome do elemento de dados excluído encurtado em % % (exemplo: `%data-element-name%`). Esse comportamento é configurável em Configurações de propriedade.

É possível resolver essas dependências antes ou depois de excluir o elemento de dados.

#### Extensões

Todos os outros recursos (regras, componentes de regras e elementos de dados) são fornecidos por extensões.

Os componentes de regras e os elementos de dados dependem das extensões para seu comportamento, mas também apenas para serem exibidos na interface do usuário da Coleta de dados. Se você excluir a extensão antes de resolver dependências, não será mais possível visualizar esses recursos órfãos. Esses recursos órfãos aparecem nas exibições de lista, mas você receberá um erro ao tentar abrir a visualização de detalhes.

Por isso, tenha muito cuidado ao excluir extensões e resolva as dependências, antes de excluí-las.

### Remover das bibliotecas

Antes de excluir um recurso, você deve removê-lo de qualquer biblioteca que o contenha. Esse processo é diferente, dependendo do estado da biblioteca.

#### Desenvolvimento

1. Abra a biblioteca.
1. Remova o recurso.
1. Salve a biblioteca.
1. Exclua o recurso.

#### Enviada para aprovação

1. Rejeitar a biblioteca (move a biblioteca de volta para o desenvolvimento).
1. Siga as etapas acima para remover um recurso de uma biblioteca de desenvolvimento.

#### Produção

1. Desative o recurso.
1. Publique o recurso desativado para produção.
1. Exclua o recurso.

## Excluir um recurso

Na visualização de lista apropriada, selecione o recurso que deseja excluir e selecione **[!UICONTROL Excluir]**.
