---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Avaliar um segmento
topic: tutorial
translation-type: tm+mt
source-git-commit: c0eacfba2feea66803e63ed55ad9d0a97e9ae47c
workflow-type: tm+mt
source-wordcount: '1543'
ht-degree: 0%

---


# Avaliar e acessar os resultados do segmento

Este documento fornece um tutorial para avaliar segmentos e acessar resultados de segmentos usando o [!DNL Segmentation API](../api/getting-started.md).

## Introdução

Este tutorial requer uma compreensão funcional dos vários [!DNL Adobe Experience Platform] serviços envolvidos na criação de segmentos de audiência. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [!DNL Real-time Customer Profile](../../profile/home.md): Fornece um perfil unificado e em tempo real para o cliente, com base em dados agregados de várias fontes.
- [!DNL Adobe Experience Platform Segmentation Service](../home.md): Permite que você crie segmentos de audiência a partir de [!DNL Real-time Customer Profile] dados.
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
- [Caixas de proteção](../../sandboxes/home.md): [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

### Cabeçalhos obrigatórios

Este tutorial também exige que você tenha concluído o tutorial [de](../../tutorials/authentication.md) autenticação para fazer chamadas com êxito para [!DNL Platform] APIs. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. As solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

Todas as solicitações POST, PUT e PATCH exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Avaliar um segmento

Depois de desenvolver, testar e salvar sua definição de segmento, você pode avaliar o segmento por meio de avaliação programada ou por demanda.

[A avaliação](#scheduled-evaluation) programada (também conhecida como &quot;segmentação programada&quot;) permite criar uma programação recorrente para executar uma tarefa de exportação em um horário específico, enquanto a avaliação [](#on-demand-evaluation) sob demanda envolve a criação de uma tarefa de segmento para criar a audiência imediatamente. As etapas para cada um são descritas abaixo.

Se você ainda não concluiu a [criação de um segmento usando o tutorial da API](./create-a-segment.md) de segmentação ou criou uma definição de segmento usando o Construtor [de](../ui/overview.md)segmentos, faça isso antes de prosseguir com este tutorial.

## Avaliação programada {#scheduled-evaluation}

Por meio da avaliação programada, sua Organização IMS pode criar uma programação recorrente para executar automaticamente as tarefas de exportação.

>[!NOTE]
>
>A avaliação agendada pode ser ativada para caixas de proteção com um máximo de cinco (5) políticas de mesclagem para o Perfil individual XDM. Se sua organização tiver mais de cinco políticas de mesclagem para o Perfil individual XDM em um único ambiente de caixa de proteção, você não poderá usar a avaliação programada.

### Criar um agendamento

Ao fazer uma solicitação POST para o `/config/schedules` ponto de extremidade, você pode criar um agendamento e incluir o horário específico em que o agendamento deve ser acionado.

Informações mais detalhadas sobre o uso desse terminal podem ser encontradas no guia de ponto de extremidade de [agendamentos](../api/schedules.md#create)

### Ativar um agendamento

Por padrão, uma programação fica inativa quando criada, a menos que a `state` propriedade esteja definida como `active` no corpo da solicitação de criação (POST). Você pode ativar uma programação (definir como `state` ) fazendo uma solicitação PATCH para o `active``/config/schedules` ponto final e incluindo a ID da programação no caminho.

Informações mais detalhadas sobre o uso desse terminal podem ser encontradas no guia de ponto de extremidade de [agendamentos](../api/schedules.md#update-state)

### Atualizar a hora agendada

O cronograma pode ser atualizado fazendo uma solicitação PATCH para o `/config/schedules` endpoint e incluindo a ID da programação no caminho.

Informações mais detalhadas sobre o uso desse terminal podem ser encontradas no guia de ponto de extremidade de [agendamentos](../api/schedules.md#update-schedule)

## Avaliação a pedido

A avaliação sob demanda permite criar um trabalho de segmento para gerar um segmento de audiência sempre que necessário. Ao contrário da avaliação agendada, isso ocorrerá somente quando solicitado e não é recorrente.

### Criar um trabalho de segmento

Um trabalho de segmento é um processo assíncrono que cria um novo segmento de audiência. Ele faz referência a uma definição de segmento, bem como a quaisquer políticas de mesclagem que controlam como [!DNL Real-time Customer Profile] mescla atributos sobrepostos em seus fragmentos de perfil. Quando uma tarefa de segmento é concluída com êxito, você pode coletar várias informações sobre o segmento, como quaisquer erros que possam ter ocorrido durante o processamento e o tamanho final da sua audiência.

Você pode criar um novo trabalho de segmento, fazendo uma solicitação POST para o `/segment/jobs` terminal na [!DNL Real-time Customer Profile] API.

Informações mais detalhadas sobre o uso desse endpoint podem ser encontradas no guia do endpoint jobs de [segmento](../api/segment-jobs.md#create)


### Pesquisar o status do trabalho do segmento

Você pode usar o `id` para um trabalho de segmento específico para executar uma solicitação de pesquisa (GET) para visualização do status atual do trabalho.

Informações mais detalhadas sobre o uso desse endpoint podem ser encontradas no guia do endpoint jobs de [segmento](../api/segment-jobs.md#get)

## Interpretar os resultados do segmento

Quando os trabalhos de segmento são executados com êxito, o `segmentMembership` mapa é atualizado para cada perfil incluído no segmento. `segmentMembership` também armazena quaisquer segmentos de audiência pré-avaliados que sejam ingeridos [!DNL Platform], permitindo a integração com outras soluções como [!DNL Adobe Audience Manager].

O exemplo a seguir mostra a aparência do `segmentMembership` atributo para cada registro de perfil individual:

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| Propriedade | Descrição |
| -------- | ----------- |
| `lastQualificationTime` | O carimbo de data e hora quando a asserção de associação de segmento foi feita e o perfil entrou ou saiu do segmento. |
| `status` | O status da participação do segmento como parte da solicitação atual. Deve ser igual a um dos seguintes valores conhecidos: <ul><li>`existing`: A entidade continua a estar no segmento.</li><li>`realized`: A entidade está inserindo o segmento.</li><li>`exited`: A entidade está saindo do segmento.</li></ul> |

## Acessar resultados do segmento

Os resultados de um trabalho de segmento podem ser acessados de uma das duas maneiras: você pode acessar perfis individuais ou exportar uma audiência inteira para um conjunto de dados.

As seções a seguir descrevem essas opções com mais detalhes.

## Procure um perfil

Se você souber o perfil específico que gostaria de acessar, poderá fazê-lo usando a [!DNL Real-time Customer Profile] API. As etapas completas para acessar perfis individuais estão disponíveis nos dados do Perfil do cliente em tempo real [Acessar usando o tutorial da API](../../profile/api/entities.md) do Perfil.

## Exportar um segmento {#export}

Depois que um trabalho de segmentação for concluído com êxito (o valor do `status` atributo é &quot;SUCEDIDO&quot;), você poderá exportar sua audiência para um conjunto de dados no qual ele possa ser acessado e executado.

As etapas a seguir são necessárias para exportar sua audiência:

- [Criar um conjunto de dados](#create-a-target-dataset) de público alvo - Crie o conjunto de dados para manter membros de audiência.
- [Gerar perfis de audiência no conjunto de dados](#generate-profiles-for-audience-members) - Preencha o conjunto de dados com Perfis individuais XDM com base nos resultados de um trabalho de segmento.
- [Monitorar o progresso](#monitor-export-progress) da exportação - Verifique o andamento atual do processo de exportação.
- [Ler dados](#next-steps) de audiência - Recupere os Perfis individuais XDM resultantes que representam os membros da audiência.

### Criar um conjunto de dados de público alvo

Ao exportar uma audiência, um conjunto de dados de público alvo deve ser criado primeiro. É importante que o conjunto de dados seja configurado corretamente para garantir que a exportação seja bem-sucedida.

Uma das principais considerações é o schema no qual o conjunto de dados se baseia (`schemaRef.id` na solicitação de amostra de API abaixo). Para exportar um segmento, o conjunto de dados deve ser baseado no Schema de União de Perfil individual (`https://ns.adobe.com/xdm/context/profile__union`) do XDM. Um schema união é um schema gerado pelo sistema e somente leitura que agregação os campos de schemas que compartilham a mesma classe, neste caso, que é a classe de Perfil Individual XDM. Para obter mais informações sobre schemas de visualização de união, consulte a seção Perfil do cliente em tempo [real do guia](../../xdm/api/getting-started.md)do desenvolvedor do Registro de Schemas.

Há duas maneiras de criar o conjunto de dados necessário:

- **Uso de APIs:** As etapas a seguir neste tutorial descrevem como criar um conjunto de dados que faz referência ao Schema de União de Perfil individual XDM usando a API de catálogo.
- **Usando a interface do usuário:** Para usar a interface do [!DNL Adobe Experience Platform] usuário para criar um conjunto de dados que faça referência ao schema da união, siga as etapas no tutorial [da](../ui/overview.md) interface do usuário e retorne a este tutorial para prosseguir com as etapas de [geração de perfis](#generate-xdm-profiles-for-audience-members)da audiência.

Se você já tiver um conjunto de dados compatível e souber sua ID, poderá prosseguir diretamente para a etapa de [geração de perfis](#generate-xdm-profiles-for-audience-members)audiências.

**Formato da API**

```http
POST /dataSets
```

**Solicitação**

A solicitação a seguir cria um novo conjunto de dados, fornecendo parâmetros de configuração na carga.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | Um nome descritivo para o conjunto de dados. |
| `schemaRef.id` | A ID da visualização de união (schema) à qual o conjunto de dados será associado. |
| `fileDescription.persisted` | Um valor booliano que, quando definido como `true`, permite que o conjunto de dados persista na visualização da união. |

**Resposta**

Uma resposta bem-sucedida retorna uma matriz contendo a ID exclusiva somente leitura gerada pelo sistema do conjunto de dados recém-criado. Uma ID de conjunto de dados configurada corretamente é necessária para exportar membros da audiência com êxito.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Gerar perfis para membros da audiência {#generate-profiles}

Depois de ter um conjunto de dados que persiste na união, você pode criar um trabalho de exportação para persistir os membros da audiência no conjunto de dados, fazendo uma solicitação POST para o `/export/jobs` ponto final na [!DNL Real-time Customer Profile] API e fornecendo a ID do conjunto de dados e as informações do segmento para os segmentos que você deseja exportar.

Informações mais detalhadas sobre o uso desse endpoint podem ser encontradas no guia de endpoint [de jobs de exportação](../api/export-jobs.md#create)

### Monitorar progresso de exportação

Como um trabalho de exportação processa, você pode monitorar seu status fazendo uma solicitação GET para o ponto de extremidade `/export/jobs` e incluindo o da tarefa `id` de exportação no caminho. A tarefa de exportação é concluída assim que o `status` campo retorna o valor &quot;SUCEDIDO&quot;.

Informações mais detalhadas sobre o uso desse endpoint podem ser encontradas no guia de endpoint [de jobs de exportação](../api/export-jobs.md#get)

## Próximas etapas

Quando a exportação for concluída com êxito, seus dados estarão disponíveis no Data Lake em [!DNL Experience Platform]. Em seguida, você pode usar a API [de acesso a](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) dados para acessar os dados usando a API `batchId` associada à exportação. Dependendo do tamanho do segmento, os dados podem estar em partes e o lote pode consistir em vários arquivos.

Para obter instruções passo a passo sobre como usar a [!DNL Data Access] API para acessar e baixar arquivos em lote, siga o tutorial [Acesso a](../../data-access/tutorials/dataset-data.md)dados.

Você também pode acessar dados de segmento exportados com êxito usando [!DNL Adobe Experience Platform Query Service]. Usando a interface do usuário ou a RESTful API, [!DNL Query Service] você pode gravar, validar e executar query em dados dentro do Data Lake.

Para obter mais informações sobre como query dados de audiência, consulte a documentação em [!DNL Query Service](../../query-service/home.md).
