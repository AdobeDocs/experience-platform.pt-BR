---
title: Serviço de identidade e perfil do cliente em tempo real
description: Saiba mais sobre a relação entre o Serviço de identidade e o Perfil do cliente em tempo real
hide: true
hidefromtoc: true
badge: Alfa
source-git-commit: 03e4cd440f8627ad837a31e1c017d0b824cafb04
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 1%

---

# Compreender a relação entre o Serviço de identidade e o Perfil do cliente em tempo real

>[!IMPORTANT]
>
>* As regras de vinculação do gráfico de identidade estão atualmente em Alpha. O recurso e a documentação estão sujeitos a alterações.
>
>* Esta página supõe que a política de mesclagem está usando o gráfico de identidade. Para obter mais informações sobre políticas de mesclagem no Perfil do cliente em tempo real, leia a documentação em [políticas de mesclagem e compilação de identidade](../../profile/merge-policies/overview.md#identity-stitching).

Embora você possa usar o Serviço de identidade e o Perfil do cliente em tempo real em conjunto, os dois recursos do Adobe Experience Platform não são inerentemente os mesmos.

* Você pode usar o Serviço de identidade para gerar e manter o gráfico de identidade que reúne as identidades diferentes de um cliente individual.
* Você pode usar o Perfil do cliente em tempo real para reunir fragmentos de perfil diferentes e criar um perfil mesclado. Este processo requer o uso do gráfico de identidade.

Este documento descreve as semelhanças, diferenças e relacionamentos entre o Serviço de identidade e o Perfil do cliente em tempo real.

## Serviço de identidade versus Perfil do cliente em tempo real

As principais diferenças entre o Serviço de identidade e o Perfil do cliente em tempo real são as seguintes:

| | Identity Service | Perfil do cliente em tempo real |
| --- | --- |--- |
| **Propósito** | <ul><li>Você pode usar o Serviço de identidade para criar e gerenciar gráficos de identidade.</li></ul> | Você pode usar o Perfil de cliente em tempo real para: <ul><li>Crie uma exibição de 360 graus de um perfil de cliente.</li><li>Exibir e gerenciar perfis</li><li>Segmente perfis para criar públicos.</li></ul> |
| **Entrada** | <ul><li>Para usar o Serviço de identidade, você deve assimilar dados de registro ou eventos de série temporal que tenham pelo menos dois campos marcados como identidade. Os campos marcados como identidade são assimilados no Serviço de identidade.</li></ul> | **Para mesclar perfis, você deve fornecer**: <ul><li>Fragmentos de perfil: representam uma identidade principal exclusiva e os dados de registro ou evento correspondentes dessa ID em um determinado conjunto de dados.</li><li>Gráficos de identidade: o perfil faz referência ao gráfico de identidade de um determinado perfil do cliente, para identificar todos os fragmentos de perfil com as mesmas identidades principais.</li></ul> **Para qualificação de segmento, você deve fornecer**: <ul><li>Perfis mesclados: um perfil mesclado é uma única visualização de um cliente, em que fragmentos de perfil e identidades diferentes são coletados em uma visualização abrangente.</li></ul> |
| **Processo** | <ul><li>Depois de assimilar pelo menos duas identidades, o Serviço de identidade vincula essas identidades.</li></ul> | <ul><li>O Perfil do cliente em tempo real mescla fragmentos de perfil ao fazer referência aos gráficos de identidade correspondentes.</li><li>Qualificar perfis para segmentos com base nos critérios de segmentação</li></ul> |
| **Saída** | <ul><li>O resultado é um gráfico de identidade, que é um conjunto de identidades relacionadas a um indivíduo.</li></ul> | <ul><li>O resultado é um perfil mesclado, que é uma visualização única e abrangente de um determinado cliente.</li><li>Perfis com associações de segmento definidas</li></ul> |

{style="table-layout:auto"}

>[!BEGINSHADEBOX]

## Como um perfil mesclado é criado?

Leia as etapas abaixo para entender melhor o processo de criação de um perfil mesclado:

* Primeiro, o Perfil do cliente em tempo real faz referência a um gráfico de identidade e recupera todas as identidades.
* Em seguida, o Perfil recupera todos os fragmentos de perfil relacionados a cada identidade.
* Depois de bem-sucedido, o Perfil mescla todos os eventos e atributos existentes.
   * Se necessário, aplique regras de precedência para determinar qual atributo ou evento usar

![Um fluxograma detalhando como o Serviço de identidade e a Mesclagem de perfis funcionam.](../images/identity-settings/identity-and-profile.png)

>[!ENDSHADEBOX]

### O que significa marcar um campo como identidade?

Marcar ou designar um campo como identidade é uma instrução para o Experience Platform assimilar esse campo específico no Serviço de identidade. Essa designação permite que os fragmentos de perfil sejam mesclados no Perfil do cliente em tempo real. Se não houver fragmentos de perfil associados à identidade, não os designe como identidade.

#### Noções básicas sobre identidades primária e secundária

Depois de marcar os campos como identidades, eles podem ser definidos como identidades primárias ou secundárias. As identidades primária e secundária são conceitos que fazem parte do Perfil do cliente em tempo real.

* A identidade principal (às vezes chamada de &quot;chave primária&quot;) é a identidade na qual os fragmentos de perfil são armazenados.
* Se houver apenas uma identidade em uma determinada linha de dados, essa única identidade será designada como primária.
* Se houver duas ou mais identidades, uma será designada como primária e a restante será designada como secundária.

O Serviço de identidade assimila apenas campos designados como identidade. O Serviço de identidade não armazena informações sobre se uma identidade é primária ou secundária.

## Próximas etapas

Para obter mais informações sobre regras de vinculação de gráficos de identidade, leia a seguinte documentação:

* [Visão geral das regras de vinculação do gráfico de identidade](./overview.md)
* [Exemplos de cenários para configurar regras de vinculação de gráficos de identidade](./example-scenarios.md)
* [Lógica de vinculação de identidade](./identity-linking-logic.md)