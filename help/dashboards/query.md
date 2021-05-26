---
solution: Experience Platform
title: Explore e processe conjuntos de dados brutos alimentando painéis de Experience Platform
type: Documentation
description: Saiba como usar o Serviço de query para explorar e processar conjuntos de dados brutos que alimentam perfis, segmentos e painéis de destino no Experience Platform.
source-git-commit: 743367431144e9714a967b0340c755bf2120559c
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 1%

---


# Explorar, verificar e processar conjuntos de dados de painéis usando o Serviço de query

A Adobe Experience Platform fornece informações importantes sobre o perfil, o segmento e os dados de destinos de sua organização por meio de painéis disponíveis na interface do usuário do Experience Platform. Em seguida, você pode usar o Serviço de query da Adobe Experience Platform para explorar, verificar e processar os conjuntos de dados brutos que alimentam esses painéis no lago de dados.

## Introdução ao Serviço de query

O Adobe Experience Platform Query Service oferece suporte aos profissionais de marketing para obter insights de seus dados, permitindo o uso do SQL padrão para consultar dados no lago de dados. O Serviço de query oferece uma interface de usuário e uma API que pode ser usada para unir qualquer conjunto de dados no lago de dados e capturar os resultados da query como novos conjuntos de dados para uso em relatórios, aprendizado de máquina ou para assimilação no Perfil do cliente em tempo real.

Para saber mais sobre o Serviço de query e sua função no Experience Platform, comece lendo a [Visão geral do Serviço de query](../query-service/home.md).

## Conjuntos de dados disponíveis

Você pode usar o Serviço de query para consultar conjuntos de dados brutos para painéis de perfil, segmento e destinos. As seções a seguir descrevem os conjuntos de dados brutos que podem ser encontrados no lago de dados.

### Conjuntos de dados do atributo de perfil

Para cada política de mesclagem ativa no Perfil do cliente em tempo real, há um conjunto de dados de atributo de perfil disponível no lago de dados.

A convenção de nomenclatura desse conjunto de dados é **Profile Attribute** seguida de um valor alfanumérico. Por exemplo: `Profile Attribute 14adf268-2a20-4dee-bee6-a6b0e34616a9`

Para entender o esquema completo do conjunto de dados, você pode visualizar e explorar o esquema usando o visualizador de conjunto de dados na interface do usuário do Experience Platform.

### Conjunto de dados de metadados do segmento

Há um conjunto de dados de metadados de segmento disponível no lago de dados para cada um dos segmentos da organização.

A convenção de nomenclatura desse conjunto de dados é **Profile Segment Definition** seguida de um valor alfanumérico. Por exemplo: `Profile Segment Definition 6591ba8f-1422-499d-822a-543b2f7613a3`

A imagem a seguir mostra o esquema do conjunto de dados de metadados do segmento.

![](images/query/segment-metadata.png)

### Conjunto de dados de metadados de destino

Os metadados para seus destinos ativados estão disponíveis como um conjunto de dados bruto no lago de dados.

A convenção de nomenclatura desse conjunto de dados é **DIM_Destination**.

A imagem a seguir mostra o esquema do conjunto de dados de metadados de destino.

![](images/query/destinations-metadata.png)

## Exemplo de consultas

As consultas de exemplo a seguir incluem amostras de SQL que podem ser usadas no Serviço de query para explorar, verificar e processar os conjuntos de dados brutos que alimentam seus painéis.

### Contagem de perfis por identidade

Esse insight de perfil fornece um detalhamento de identidades em todos os perfis mesclados no conjunto de dados. O número total de perfis por identidade (em outras palavras, adicionar os valores mostrados para cada namespace) pode ser maior que o número total de perfis mesclados, pois um perfil pode ter vários namespaces associados a ele. Por exemplo, se um cliente interagir com sua marca em mais de um canal, vários namespaces serão associados a esse cliente individual.

**Query**

```sql
Select
        Key namespace,
        count(1) count_of_profiles
     from
        (
           Select
               explode(identitymap)
           from
              profile_attribute_14adf268-2a20-4dee-bee6-a6b0e34616a9
        )
     group by
        namespace;
```

### Contagem de perfis por segmento

Esse insight de público-alvo fornece o número total de perfis mesclados em cada segmento no conjunto de dados. Esse número é o resultado da aplicação da política de mesclagem de segmentos aos seus dados de Perfil para unir fragmentos de perfil para formar um único perfil para cada indivíduo no segmento.

```sql
Select          
        concat_ws('-', key, source_namespace) segment_id,
        count(1) count_of_profiles
      from
        (
            Select
              Upper(key) as source_namespace,
              explode(value)
            from
              (
                  Select
                    explode(Segmentmembership)
                  from
                    profile_attribute_14adf268-2a20-4dee-bee6-a6b0e34616a9
              )
        )
      group by
      segment_id
```

### Contagem de segmentos ativados por destino para todos os destinos

## Próximas etapas

Ao ler este guia, agora você pode usar o Serviço de query para realizar várias consultas para explorar e processar os conjuntos de dados brutos que alimentam seus painéis de perfil, segmento e destinos.

Para saber mais sobre cada painel e suas métricas, selecione um painel na lista de painéis disponíveis na navegação da documentação.
