---
solution: Experience Platform
title: Explorar, verificar e processar conjuntos de dados do painel usando o serviço de query
type: Documentation
description: Saiba como usar o Serviço de query para explorar e processar conjuntos de dados brutos que alimentam perfis, segmentos e painéis de destino no Experience Platform.
exl-id: 0087dcab-d5fe-4a24-85f6-587e9ae74fb8
source-git-commit: fe2d9e60dd641e1f03f7dde72e64e2892ae7c1a2
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# Explorar, verificar e processar conjuntos de dados de painel usando [!DNL Query Service]

A Adobe Experience Platform fornece informações importantes sobre o perfil, o segmento e os dados de destinos de sua organização por meio de painéis disponíveis na interface do usuário do Experience Platform. Em seguida, você pode usar o Adobe Experience Platform [!DNL Query Service] para explorar, verificar e processar os conjuntos de dados brutos que alimentam esses painéis no lago de dados.

## Introdução ao [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] O oferece suporte a profissionais de marketing para obter insights de seus dados, permitindo o uso de SQL padrão para consultar dados no lago de dados. [!DNL Query Service] O oferece uma interface de usuário e uma API que pode ser usada para unir qualquer conjunto de dados no lago de dados e capturar os resultados da consulta como novos conjuntos de dados para uso em relatórios, aprendizado de máquina ou para assimilação no Perfil do cliente em tempo real.

Para saber mais sobre [!DNL Query Service] e o seu papel no Experience Platform, por favor comece por ler [[!DNL Query Service] visão geral](../query-service/home.md).

## Acesso aos conjuntos de dados disponíveis

Você pode usar [!DNL Query Service] para consultar conjuntos de dados brutos para painéis de perfil, segmento e destinos. Para exibir seus conjuntos de dados disponíveis, na interface do usuário do Experience Platform, selecione **Conjuntos de dados** na navegação à esquerda para abrir o painel Conjuntos de dados . O painel lista todos os conjuntos de dados disponíveis para sua organização. Os detalhes são exibidos para cada conjunto de dados listado, incluindo seu nome, o esquema ao qual o conjunto de dados adere e o status da execução de assimilação mais recente.

![O painel Navegação do conjunto de dados com a guia Conjuntos de dados realçada na navegação à esquerda.](./images/query/browse-datasets.png)

### Conjuntos de dados gerados pelo sistema

>[!IMPORTANT]
>
>Os conjuntos de dados gerados pelo sistema ficam ocultos por padrão. Por padrão, a variável [!UICONTROL Procurar] A guia mostra somente os conjuntos de dados nos quais você assimilou dados.

Para exibir conjuntos de dados gerados pelo sistema, selecione o ícone de filtro (![Um ícone de filtro.](./images/query/filter.png)) localizado à esquerda da barra de pesquisa.

![A guia Navegação dos conjuntos de dados com o ícone de filtro realçado.](./images/query/filter-datasets.png)

Uma barra lateral aparece contendo dois botões, [!UICONTROL Incluído em Perfil] e [!UICONTROL Mostrar conjuntos de dados do sistema]. Selecione a opção de alternância para [!UICONTROL Mostrar conjuntos de dados do sistema] para incluir conjuntos de dados gerados pelo sistema na lista de conjuntos de dados navegáveis.

![A guia Navegação dos conjuntos de dados com o botão Mostrar conjuntos de dados do sistema é realçada.](./images/query/show-system-datasets.png)

### Conjuntos de dados do atributo de perfil

Os insights do painel de perfis são vinculados às políticas de mesclagem que foram definidas pela sua organização. Para cada política de mesclagem ativa, há um conjunto de dados de atributo de perfil disponível no lago de dados.

A convenção de nomenclatura desses conjuntos de dados é **Exportação de Instantâneo do Perfil** seguido por um valor alfanumérico aleatório gerado pelo sistema. Por exemplo: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

Para entender o esquema completo de cada conjunto de dados de exportação de instantâneo de perfil, você pode visualizar e explorar os conjuntos de dados [uso do visualizador de conjunto de dados](../catalog/datasets/user-guide.md) na interface do usuário do Experience Platform.

![](images/query/profile-attribute.png)

#### Mapeamento de conjuntos de dados de atributos de perfil para mesclar IDs de política

O valor alfanumérico atribuído a cada conjunto de dados de atributo de perfil gerado pelo sistema é uma sequência de caracteres aleatória que mapeia para uma ID de política de mesclagem de uma das políticas de mesclagem criadas pela organização. O mapeamento de cada ID de política de mesclagem para sua string de conjunto de dados de atributo de perfil relacionada é mantido na variável `adwh_dim_merge_policies` conjunto de dados.

O `adwh_dim_merge_policies` o conjunto de dados contém os seguintes campos:

* `merge_policy_name`
* `merge_policy_id`
* `merge_policy`
* `dataset_id`

Esse conjunto de dados pode ser explorado usando a interface do Editor de consultas no Experience Platform. Para saber mais sobre como usar o Editor de consultas, consulte [Guia da interface do usuário do Editor de consultas](../query-service/ui/user-guide.md).

### Conjunto de dados de metadados do segmento

Há um conjunto de dados de metadados de segmento disponível no lago de dados que contém metadados para cada um dos segmentos da organização.

A convenção de nomenclatura desse conjunto de dados é **Segmentdefinition-Snapshot-Export** seguido por um valor alfanumérico. Por exemplo: `Segmentdefinition-Snapshot-Export-acf28952-2b6c-47ed-8f7f-016ac3c6b4e7`

Para entender o esquema completo de cada conjunto de dados de exportação de instantâneo de definição de segmento, você pode visualizar e explorar os conjuntos de dados [uso do visualizador de conjunto de dados](../catalog/datasets/user-guide.md) na interface do usuário do Experience Platform.

![](images/query/segment-metadata.png)

### Conjunto de dados de metadados de destino

Os metadados para todos os destinos ativados de sua organização estão disponíveis como um conjunto de dados bruto no lago de dados.

A convenção de nomenclatura desse conjunto de dados é **DIM_Destination**.

Para entender o esquema completo do conjunto de dados de destino DIM, você pode visualizar e explorar o conjunto de dados [uso do visualizador de conjunto de dados](../catalog/datasets/user-guide.md) na interface do usuário do Experience Platform.

![](images/query/destinations-metadata.png)

## Exemplo de consultas

Os exemplos de consultas a seguir incluem amostras de SQL que podem ser usadas em [!DNL Query Service] para explorar, verificar e processar os conjuntos de dados brutos que alimentam seus painéis.

### Contagem de perfis por identidade

Esse insight de perfil fornece um detalhamento de identidades em todos os perfis mesclados no conjunto de dados.

>[!NOTE]
>
>O número total de perfis por identidade (em outras palavras, adicionar os valores mostrados para cada namespace) pode ser maior que o número total de perfis mesclados, pois um perfil pode ter vários namespaces associados a ele. Por exemplo, se um cliente interagir com sua marca em mais de um canal, vários namespaces serão associados a esse cliente individual.

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
              Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
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
                    Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
              )
        )
      group by
      segment_id
```

## Próximas etapas

Ao ler este guia, agora você pode usar [!DNL Query Service] para realizar várias consultas para explorar e processar os conjuntos de dados brutos que alimentam seu perfil, segmento e painéis de destinos.

Para saber mais sobre cada painel e suas métricas, selecione um painel na lista de painéis disponíveis na navegação da documentação.
