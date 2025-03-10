---
solution: Experience Platform
title: Explorar, verificar e processar conjuntos de dados do painel usando o serviço de consulta
type: Documentation
description: Saiba como usar o Serviço de consulta para explorar e processar conjuntos de dados brutos que potencializam o perfil, o público-alvo e os painéis de destino no Experience Platform.
exl-id: 0087dcab-d5fe-4a24-85f6-587e9ae74fb8
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 1%

---

# Explorar, verificar e processar conjuntos de dados de painel usando o [!DNL Query Service]

A Adobe Experience Platform fornece informações importantes sobre os dados de perfil, público-alvo e destinos de sua organização por meio dos painéis disponíveis na interface do usuário do Experience Platform. Em seguida, você pode usar o Adobe Experience Platform [!DNL Query Service] para explorar, verificar e processar os conjuntos de dados brutos que alimentam esses painéis no data lake.

## Introdução ao [!DNL Query Service]

O Adobe Experience Platform [!DNL Query Service] oferece suporte aos profissionais de marketing para obter informações de seus dados, permitindo o uso do SQL padrão para consultar dados no data lake. O [!DNL Query Service] oferece uma interface de usuário e uma API que podem ser usadas para ingressar em qualquer conjunto de dados no data lake e capturar os resultados da consulta como novos conjuntos de dados para usar em relatórios, aprendizado de máquina ou para assimilação no Perfil do cliente em tempo real.

Para saber mais sobre [!DNL Query Service] e sua função no Experience Platform, comece lendo a [[!DNL Query Service] visão geral](../query-service/home.md).

## Acesso aos conjuntos de dados disponíveis

Você pode usar o [!DNL Query Service] para consultar conjuntos de dados brutos para painéis de perfil, público-alvo e destinos. Para exibir seus conjuntos de dados disponíveis, na interface do usuário do Experience Platform, selecione **Conjuntos de dados** no menu de navegação esquerdo para abrir o painel Conjuntos de dados. O painel lista todos os conjuntos de dados disponíveis para sua organização. Os detalhes são exibidos para cada conjunto de dados listado, incluindo o nome, o esquema ao qual o conjunto de dados pertence e o status da execução de assimilação mais recente.

![O painel de Navegação do Conjunto de Dados com a guia Conjuntos de Dados realçada na navegação à esquerda.](./images/query/browse-datasets.png)

### Conjuntos de dados gerados pelo sistema {#system-generated-datasets}

>[!IMPORTANT]
>
>Os conjuntos de dados gerados pelo sistema ficam ocultos por padrão. Por padrão, a guia [!UICONTROL Procurar] mostra apenas conjuntos de dados nos quais você assimilou dados.

Para exibir conjuntos de dados gerados pelo sistema, selecione o ícone de filtro (![Um ícone de filtro.](/help/images/icons/filter.png)) localizado à esquerda da barra de pesquisa.

![A guia Procurar Conjuntos de Dados com o ícone de filtro realçado.](./images/query/filter-datasets.png)

Uma barra lateral é exibida contendo dois alternadores, [!UICONTROL Incluídos no Perfil] e [!UICONTROL Mostrar conjuntos de dados do sistema]. Selecione a opção para [!UICONTROL Mostrar conjuntos de dados do sistema] para incluir conjuntos de dados gerados pelo sistema na lista navegável de conjuntos de dados.

![A guia Procurar Conjuntos de Dados com a opção Mostrar conjuntos de dados do sistema foi realçada.](./images/query/show-system-datasets.png)

### Conjuntos de dados do atributo de perfil {#profile-attribute-datasets}

Os insights do painel de perfil estão ligados às políticas de mesclagem que foram definidas por sua organização. Para cada política de mesclagem ativa, há um conjunto de dados de atributo de perfil disponível no data lake.

A convenção de nomenclatura desses conjuntos de dados é **Profile-Snapshot-Export** seguida de um valor alfanumérico aleatório gerado pelo sistema. Por exemplo: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

Para entender o esquema completo de cada conjunto de dados de exportação de instantâneo de perfil, você pode visualizar e explorar os conjuntos de dados [usando o visualizador de conjunto de dados](../catalog/datasets/user-guide.md) na interface do usuário do Experience Platform.

![Uma visualização do conjunto de dados Profile-Snapshot-Export.](images/query/profile-attribute.png)

#### Mapeamento de conjuntos de dados do atributo de perfil para IDs de política de mesclagem

O valor alfanumérico atribuído a cada conjunto de dados de atributo de perfil gerado pelo sistema é uma sequência aleatória que mapeia para uma ID de política de mesclagem de uma das políticas de mesclagem criadas pela organização. O mapeamento de cada ID de política de mesclagem para sua cadeia de caracteres de conjunto de dados de atributo de perfil relacionada é mantido no conjunto de dados `adwh_dim_merge_policies`.

O conjunto de dados `adwh_dim_merge_policies` contém os seguintes campos:

* `merge_policy_name`
* `merge_policy_id`
* `merge_policy`
* `dataset_id`

Esse conjunto de dados pode ser explorado usando a interface do Editor de consultas no Experience Platform. Para saber mais sobre o uso do Editor de Consultas, consulte o [guia da interface do Editor de Consultas](../query-service/ui/user-guide.md).

### Conjunto de dados de metadados de público

Há um conjunto de dados de metadados de público-alvo disponível no data lake que contém metadados para cada um dos públicos-alvo de sua organização.

A convenção de nomenclatura deste conjunto de dados é **Segmentdefinition-Snapshot-Export** seguido de um valor alfanumérico. Por exemplo: `Segmentdefinition-Snapshot-Export-acf28952-2b6c-47ed-8f7f-016ac3c6b4e7`

Para entender o esquema completo de cada conjunto de dados de exportação de instantâneo de definição de segmento, você pode visualizar e explorar os conjuntos de dados [usando o visualizador de conjunto de dados](../catalog/datasets/user-guide.md) na interface do usuário do Experience Platform.

### Conjunto de dados de metadados de destino

Os metadados de todos os destinos ativados de sua organização estão disponíveis como um conjunto de dados bruto no data lake.

A convenção de nomenclatura deste conjunto de dados é **DIM_Destination**.

Para entender o esquema completo do conjunto de dados de destino DIM, você pode visualizar e explorar o conjunto de dados [usando o visualizador de conjunto de dados](../catalog/datasets/user-guide.md) na interface do usuário do Experience Platform.

![Uma visualização do conjunto de dados DIM_Destination.](images/query/destinations-metadata.png)

## Relatórios de insights da Plataforma de dados do cliente (CDP)

O recurso Modelos de dados de insights da CDP expõe o SQL que habilita os insights para vários widgets de perfil, destino e segmentação. Você pode personalizar esses modelos de consulta SQL para criar relatórios CDP para seus casos de uso de marketing e KPI.

Os relatórios da CDP fornecem insights sobre os dados do perfil e sua relação com públicos-alvo e destinos. Consulte a documentação do Modelo de dados dos insights da CDP para obter informações detalhadas sobre como [aplicar os Modelos de dados dos insights da CDP a seus casos de uso de KPI específicos](./data-models/cdp-insights-data-model-b2c.md).

## Exemplo de consultas

Os exemplos de consultas a seguir incluem SQL de exemplo que pode ser usado no [!DNL Query Service] para explorar, verificar e processar os conjuntos de dados brutos que alimentam seus painéis.

### Contagem de perfis por identidade

Esse insight do perfil fornece um detalhamento das identidades em todos os perfis mesclados no conjunto de dados.

>[!NOTE]
>
>O número total de perfis por identidade (em outras palavras, somando os valores mostrados para cada namespace) pode ser maior que o número total de perfis mesclados, pois um perfil pode ter vários namespaces associados a ele. Por exemplo, se um cliente interagir com sua marca em mais de um canal, vários namespaces serão associados a esse cliente individual.

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

### Contagem de perfis por público

Este insight de público-alvo fornece o número total de perfis mesclados em cada público-alvo no conjunto de dados. Esse número é o resultado da aplicação da política de mesclagem de público-alvo aos dados do seu Perfil para mesclar fragmentos de perfil e formar um único perfil para cada indivíduo no público-alvo.

```sql
Select          
        concat_ws('-', key, source_namespace) audience_id,
        count(1) count_of_profiles
      from
        (
            Select
              Upper(key) as source_namespace,
              explode(value)
            from
              (
                  Select
                    explode(Audiencemembership)
                  from
                    Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
              )
        )
      group by
      audience_id
```

## Próximas etapas

Ao ler este guia, agora é possível usar o [!DNL Query Service] para executar várias consultas para explorar e processar os conjuntos de dados brutos que alimentam seu perfil, público-alvo e painéis de destinos.

Para saber mais sobre cada painel e suas métricas, selecione um painel na lista de painéis disponíveis na navegação da documentação.
