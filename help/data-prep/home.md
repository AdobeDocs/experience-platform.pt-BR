---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mapping;data prep;data preparation;preparing data;
solution: Experience Platform
title: Funções de mapeamento
topic: overview
description: Este documento apresenta a preparação de dados no Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: db38f0666f5c945461043ad08939ebda52c21855
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Preparo de dados

O Data Prep permite que os engenheiros de dados mapeiem, transformem e validem dados para e do Experience Data Model (XDM). A Prep. de dados aparece como uma etapa do &quot;Mapa&quot; nos processos de ingestão de dados, incluindo o fluxo de trabalho de ingestão de CSV. Os engenheiros de dados podem usar a Preparação de dados para executar a seguinte manipulação de dados durante a ingestão:

- Definir mapeamentos de pass-through simples para atribuir atributos de entrada aos atributos XDM
- Criar campos calculados para executar cálculos em linha que podem ser atribuídos a atributos XDM
- Transforme os dados aplicando funções de manipulação de string, numérica ou de data
- Construir hierarquias XDM usando funções hierárquicas
- Pré-visualização os dados conforme são manipulados na Preparação de dados

A Prep. de dados também aplica várias validações de dados intrínsecas para garantir que a integridade dos dados seja mantida à medida que for assimilada. Sempre que possível, o Data Prep mapeia automaticamente os schemas de dados recebidos para XDM. Os engenheiros de dados podem alterar, corrigir e excluir os mapeamentos sugeridos e substituí-los pelos mapeamentos, conforme apropriado.

## Mapeamento

Um mapeamento é uma associação de um atributo de entrada ou de um campo calculado a um atributo XDM. Um único atributo pode ser mapeado para vários atributos XDM criando mapeamentos individuais.

Para saber mais sobre as diferentes funções de mapeamento, leia o guia [de funções de](./functions.md)mapeamento.

## Conjunto de mapeamento

Um conjunto de mapeamentos que transformam um schema em outro é conhecido coletivamente como um conjunto de mapeamentos. Um único conjunto de mapeamentos é criado como parte de cada fluxo de dados. Um conjunto de mapeamentos é parte integrante dos fluxos de dados e é criado, editado e monitorado como parte dos fluxos de dados.

## Próximas etapas

Este documento cobriu as noções básicas sobre a preparação de dados no Adobe Experience Platform. Para saber mais sobre diferentes funções de mapeamento, leia o guia [de funções de](./functions.md)mapeamento. Para saber mais sobre as diferentes strings datetime, leia o guia [de strings de](./dates.md)data.