---
solution: Experience Platform
title: Importação e uso de públicos externos
description: Siga este tutorial para saber como usar públicos externos com o Adobe Experience Platform.
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
hide: true
hidefromtoc: true
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '1720'
ht-degree: 0%

---

# Importação e uso de públicos externos

>[!IMPORTANT]
>
>Esta documentação contém informações de uma versão anterior da documentação de Públicos-alvo e, como resultado, está desatualizada.

O Adobe Experience Platform oferece suporte à capacidade de importar público externo, que pode ser usado posteriormente como componentes para um novo público. Este documento fornece um tutorial para configurar o Experience Platform para importar e usar públicos externos.

## Introdução

Este tutorial requer um entendimento prático dos vários [!DNL Adobe Experience Platform] serviços envolvidos na criação de públicos. Antes de iniciar este tutorial, revise a documentação dos seguintes serviços:

- [Serviço de segmentação](../home.md): permite criar públicos-alvo a partir dos dados do Perfil do cliente em tempo real.
- [Perfil do cliente em tempo real](../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
- [Experience Data Model (XDM)](../../xdm/home.md): a estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente. Para melhor usar a segmentação, verifique se seus dados são assimilados como perfis e eventos de acordo com a [práticas recomendadas para modelagem de dados](../../xdm/schema/best-practices.md).
- [Conjuntos de dados](../../catalog/datasets/overview.md): a construção de armazenamento e gerenciamento para a persistência de dados no Experience Platform.
- [Assimilação por transmissão](../../ingestion/streaming-ingestion/overview.md): como o Experience Platform assimila e armazena dados de dispositivos do lado do cliente e do lado do servidor em tempo real.

### Definições de públicos versus segmentos

Antes de começar a importar e usar públicos externos, é importante entender a diferença entre públicos e definições de segmento.

Os públicos-alvo se referem ao grupo de perfis no qual você está tentando filtrar. Ao usar definições de segmento, você pode criar um público-alvo criando uma definição de segmento que filtre seus perfis para o subconjunto que atende aos critérios de qualificação de segmento.

As definições de segmento incluem informações como nome, descrição, expressão (se aplicável), data de criação, data da última modificação e uma ID. A ID vincula os metadados do segmento aos perfis individuais que atendem à qualificação do segmento e fazem parte do público-alvo resultante.

| Públicos-alvo | Definição de segmento |
| --------- | ---------------- |
| O grupo de perfis que você está tentando encontrar. Ao usar definições de segmento, significa que será o grupo de perfis que atenderá à qualificação de segmento. | O grupo de regras usado para segmentar o público que você está procurando. |

## Criar um namespace de identidade para o público externo

A primeira etapa para usar públicos-alvo externos é criar um namespace de identidade. Os namespaces de identidade permitem que a Platform associe de onde um público-alvo se origina.

Para criar um namespace de identidade, siga as instruções na [guia de namespace de identidade](../../identity-service/namespaces.md#manage-namespaces). Ao criar o namespace de identidade, adicione os detalhes de origem ao namespace de identidade e marque sua [!UICONTROL Tipo] as a **[!UICONTROL Identificador não pessoal]**.

![O identificador não pessoal é realçado no modal Criar namespace de identidade.](../images/tutorials/external-audiences/identity-namespace-info.png)

## Criar um esquema para os metadados do segmento

Depois de criar um namespace de identidade, é necessário criar um novo esquema para o segmento que você criará.

Para começar a compor um esquema, primeiro selecione **[!UICONTROL Esquemas]** na barra de navegação à esquerda, seguido pelo botão **[!UICONTROL Criar esquema]** no canto superior direito do espaço de trabalho Esquemas. Aqui, selecione **[!UICONTROL Procurar]** para ver uma seleção completa dos Tipos de esquema disponíveis.

![Criar esquema e Procurar são realçados.](../images/tutorials/external-audiences/create-schema-browse.png)

Como você está criando uma definição de segmento, que é uma classe predefinida, selecione **[!UICONTROL Usar classe existente]**. Agora, selecione a variável **[!UICONTROL Definição de segmento]** classe, seguida por **[!UICONTROL Atribuir classe]**.

![A classe de definição de segmento é destacada.](../images/tutorials/external-audiences/assign-class.png)

Agora que o esquema foi criado, será necessário especificar qual campo conterá a ID do segmento. Este campo deve ser marcado como a identidade primária e atribuído aos namespaces criados anteriormente.

![As caixas de seleção para marcar o campo selecionado como a identidade principal são realçadas no Editor de esquemas.](../images/tutorials/external-audiences/mark-primary-identifier.png)

Depois de marcar o `_id` como a identidade primária, selecione o título do esquema, seguido da alternância rotulada como **[!UICONTROL Perfil]**. Selecionar **[!UICONTROL Ativar]** para ativar o esquema para [!DNL Real-Time Customer Profile].

![A opção para ativar o esquema para Perfil é realçada no Editor de esquemas.](../images/tutorials/external-audiences/schema-profile.png)

Agora, esse esquema é ativado para Perfil, com a identificação principal atribuída ao namespace de identidade que não é de pessoa que você criou. Como resultado, isso significa que os metadados de segmento importados para a Platform usando esse esquema serão assimilados no Perfil sem serem mesclados com outros dados de perfil relacionados às pessoas.

## Criar um conjunto de dados para o esquema

Depois de configurar o esquema, será necessário criar um conjunto de dados para os metadados do segmento.

Para criar um conjunto de dados, siga as instruções na [guia do usuário do conjunto de dados](../../catalog/datasets/user-guide.md#create). Você deve seguir o **[!UICONTROL Criar conjunto de dados a partir do esquema]** opção, usando o schema criado anteriormente.

![O esquema no qual você deseja basear seu conjunto de dados é realçado.](../images/tutorials/external-audiences/select-schema.png)

Depois de criar o conjunto de dados, continue seguindo as instruções na [guia do usuário do conjunto de dados](../../catalog/datasets/user-guide.md#enable-profile) para ativar esse conjunto de dados para o Perfil de cliente em tempo real.

![A opção para ativar o esquema para Perfil é realçada na página de atividade do conjunto de dados.](../images/tutorials/external-audiences/dataset-profile.png)

## Configurar e importar dados de público

Com o conjunto de dados ativado, os dados agora podem ser enviados para a Platform por meio da interface do usuário ou usando as APIs de Experience Platform. Você pode assimilar esses dados por meio de uma conexão em lote ou de transmissão.

### Assimilar dados usando uma conexão em lote

Para criar uma conexão em lote, siga as instruções na guia genérica [guia da interface do usuário de upload de arquivo local](../../sources/tutorials/ui/create/local-system/local-file-upload.md). Para obter uma lista completa de fontes disponíveis com as quais você pode usar a assimilação de dados, leia a [visão geral das origens](../../sources/home.md).

### Assimilar dados usando uma conexão de transmissão

Para criar uma conexão de transmissão, siga as instruções em [Tutorial de API](../../sources/tutorials/api/create/streaming/http.md) ou o [Tutorial de interface do usuário](../../sources/tutorials/ui/create/streaming/http.md).

Depois de criar a conexão de streaming, você terá acesso ao terminal de streaming exclusivo para o qual poderá enviar seus dados. Para saber como enviar dados para esses endpoints, leia o [tutorial sobre transmissão de dados de registro](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![O ponto final de transmissão da conexão de transmissão é realçado na página de detalhes da origem.](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Estrutura de metadados de público

Depois de criar uma conexão, você pode assimilar seus dados na Platform.

Uma amostra dos metadados da carga do público-alvo externo pode ser vista abaixo:

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample External Audience"
        }
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "_id": "{SEGMENT_ID}",
            "description": "Sample description",
            "identityMap": {
                "{IDENTITY_NAMESPACE}": [{
                    "id": "{}"
                }]
            },
            "segmentName" : "{SEGMENT_NAME}",
            "segmentStatus": "ACTIVE",
            "version": "1.0"
        }
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `schemaRef` | O schema **deve** consulte o schema criado anteriormente para obter os metadados do segmento. |
| `datasetId` | A ID do conjunto de dados **deve** consulte o conjunto de dados criado anteriormente para o esquema que você acabou de criar. |
| `xdmEntity._id` | A ID **deve** consulte a mesma ID de segmento que você está usando como público-alvo externo. |
| `xdmEntity.identityMap` | Esta seção **deve** contém o rótulo de identidade usado ao criar o namespace criado anteriormente. |
| `{IDENTITY_NAMESPACE}` | Este é o rótulo do namespace de identidade criado anteriormente. Assim, por exemplo, se você chamasse o namespace de identidade de &quot;externalAudience&quot;, usaria isso como a chave da matriz. |
| `segmentName` | O nome do segmento pelo qual você deseja segmentar o público externo. |

## Criação de segmentos usando públicos importados

Após configurar os públicos-alvo importados, eles podem ser usados como parte do processo de segmentação. Para encontrar públicos externos, acesse o Construtor de segmentos e selecione **[!UICONTROL Públicos-alvo]** na guia **[!UICONTROL Campos]** seção.

![O seletor de públicos-alvo externos no Construtor de segmentos é realçado.](../images/tutorials/external-audiences/external-audiences.png)

## Próximas etapas

Agora que você pode usar públicos-alvo externos nos segmentos, pode usar o Construtor de segmentos para criar segmentos. Para saber como criar segmentos, leia o [tutorial sobre a criação de segmentos](./create-a-segment.md).

## Apêndice

Além de usar metadados de público-alvo externo importados e usá-los para criar segmentos, você também pode importar associações de segmento externo para a Platform.

### Configurar um esquema de destino de associação de segmento externo

Para começar a compor um esquema, primeiro selecione **[!UICONTROL Esquemas]** na barra de navegação à esquerda, seguido pelo botão **[!UICONTROL Criar esquema]** no canto superior direito do espaço de trabalho Esquemas. Aqui, selecione **[!UICONTROL Perfil individual XDM]**.

![A área Perfil individual XDM é realçada.](../images/tutorials/external-audiences/create-schema-profile.png)

Agora que o esquema foi criado, será necessário adicionar o grupo de campos de associação de segmento como parte do esquema. Para fazer isso, selecione [!UICONTROL Detalhes da associação do segmento], seguido por [!UICONTROL Adicionar grupos de campos].

![O grupo de campos Detalhes da associação do segmento é destacado.](../images/tutorials/external-audiences/segment-membership-details.png)

Além disso, verifique se o esquema está marcado para **[!UICONTROL Perfil]**. Para fazer isso, será necessário marcar um campo como a identidade principal.

![A opção para ativar o esquema para Perfil é realçada no Editor de esquemas.](../images/tutorials/external-audiences/external-segment-profile.png)

### Configurar o conjunto de dados

Depois de criar seu esquema, será necessário criar um conjunto de dados.

Para criar um conjunto de dados, siga as instruções na [guia do usuário do conjunto de dados](../../catalog/datasets/user-guide.md#create). Você deve seguir o **[!UICONTROL Criar conjunto de dados a partir do esquema]** opção, usando o schema criado anteriormente.

![O schema que você está usando para criar o banco de dados é realçado.](../images/tutorials/external-audiences/select-schema.png)

Depois de criar o conjunto de dados, continue seguindo as instruções na [guia do usuário do conjunto de dados](../../catalog/datasets/user-guide.md#enable-profile) para ativar esse conjunto de dados para o Perfil de cliente em tempo real.

![A opção para ativar o esquema para Perfil é realçada no fluxo de trabalho Criar conjuntos de dados.](../images/tutorials/external-audiences/dataset-profile.png)

## Configurar e importar dados de associação de público externo

Com o conjunto de dados ativado, os dados agora podem ser enviados para a Platform por meio da interface do usuário ou usando as APIs de Experience Platform. Você pode assimilar esses dados por meio de uma conexão em lote ou de transmissão.

### Assimilar dados usando uma conexão em lote

Para criar uma conexão em lote, siga as instruções na guia genérica [guia da interface do usuário de upload de arquivo local](../../sources/tutorials/ui/create/local-system/local-file-upload.md). Para obter uma lista completa de fontes disponíveis com as quais você pode usar a assimilação de dados, leia a [visão geral das origens](../../sources/home.md).

### Assimilar dados usando uma conexão de transmissão

Para criar uma conexão de transmissão, siga as instruções em [Tutorial de API](../../sources/tutorials/api/create/streaming/http.md) ou o [Tutorial de interface do usuário](../../sources/tutorials/ui/create/streaming/http.md).

Depois de criar a conexão de streaming, você terá acesso ao terminal de streaming exclusivo para o qual poderá enviar seus dados. Para saber como enviar dados para esses endpoints, leia o [tutorial sobre transmissão de dados de registro](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![O ponto final de transmissão da conexão de transmissão é realçado na página de detalhes da origem.](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Estrutura de associação de segmento

Depois de criar uma conexão, você pode assimilar seus dados na Platform.

Um exemplo da carga de associação do público-alvo externo pode ser visto abaixo:

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample External Audience Membership"
        }
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "_id": "{UNIQUE_ID}",
            "description": "Sample description",
            "{TENANT_NAME}": {
                "identities": {
                    "{SCHEMA_IDENTITY}": "sample-id"
                }
            },
            "personId" : "sample-name",
            "segmentMembership": {
                "{IDENTITY_NAMESPACE}": {
                    "{EXTERNAL_IDENTITY}": {
                        "status": "realized",
                        "lastQualificationTime": "2022-03-14T:00:00:00Z"
                    }
                }
            }
        }
    }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `schemaRef` | O schema **deve** consulte o schema criado anteriormente para obter os dados de associação do segmento. |
| `datasetId` | A ID do conjunto de dados **deve** consulte o conjunto de dados criado anteriormente para o schema de associação que você acabou de criar. |
| `xdmEntity._id` | Uma ID adequada usada para identificar exclusivamente o registro no conjunto de dados. |
| `{TENANT_NAME}.identities` | Esta seção é usada para conectar o grupo de campos das identidades personalizadas com os usuários importados anteriormente. |
| `segmentMembership.{IDENTITY_NAMESPACE}` | Este é o rótulo do namespace de identidade personalizado criado anteriormente. Assim, por exemplo, se você chamasse o namespace de identidade de &quot;externalAudience&quot;, usaria isso como a chave da matriz. |

>[!NOTE]
>
>Por padrão, as associações de público-alvo externo são retidas apenas por 30 dias. Para retê-los por mais de 30 dias, use o `validUntil` ao assimilar os dados do público-alvo. Para obter mais informações sobre esse campo, leia o guia em [Grupos de campos de esquema Detalhes da associação do segmento](../../xdm/field-groups/profile/segmentation.md).