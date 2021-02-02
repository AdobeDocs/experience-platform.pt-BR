---
keywords: Experience Platform;home;popular topics;avaliação de segmento;Serviço de segmentação;segmentação;segmentação;avaliar um segmento;acessar resultados do segmento;avaliar e acessar segmento;
solution: Experience Platform
title: Avaliar um segmento
topic: tutorial
type: Tutorial
description: Este documento fornece um tutorial para avaliar segmentos e acessar resultados de segmentos usando a API de segmentação.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '1560'
ht-degree: 0%

---


# Avaliar e acessar os resultados do segmento

Este documento fornece um tutorial para avaliar segmentos e acessar resultados de segmentos usando [[!DNL Segmentation API]](../api/getting-started.md).

## Introdução

Este tutorial requer uma compreensão funcional dos vários [!DNL Adobe Experience Platform] serviços envolvidos na criação de segmentos de audiência. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil unificado e em tempo real para o cliente, com base em dados agregados de várias fontes.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Permite que você crie segmentos de audiência a partir de  [!DNL Real-time Customer Profile] dados.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual a Plataforma organiza os dados de experiência do cliente.
- [Caixas de proteção](../../sandboxes/home.md):  [!DNL Experience Platform] fornece caixas de proteção virtuais que particionam uma única  [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

### Cabeçalhos obrigatórios

Este tutorial também exige que você tenha concluído o tutorial de autenticação [](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para [!DNL Platform] APIs. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. As solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a [documentação de visão geral da caixa de proteção](../../sandboxes/home.md).

Todas as solicitações de POST, PUT e PATCH exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Avaliar um segmento

Depois de desenvolver, testar e salvar sua definição de segmento, você pode avaliar o segmento por meio de avaliação programada ou por demanda.

[A avaliação](#scheduled-evaluation)  agendada (também conhecida como &quot;segmentação agendada&quot;) permite criar uma programação recorrente para executar uma tarefa de exportação em um horário específico, enquanto a avaliação  [sob demanda ](#on-demand-evaluation) envolve a criação de uma tarefa de segmento para criar a audiência imediatamente. As etapas para cada um são descritas abaixo.

Se você ainda não concluiu o [crie um segmento usando o tutorial da API de segmentação](./create-a-segment.md) ou criou uma definição de segmento usando [Construtor de segmentos](../ui/overview.md), faça isso antes de prosseguir com este tutorial.

## Avaliação agendada {#scheduled-evaluation}

Por meio da avaliação programada, sua Organização IMS pode criar uma programação recorrente para executar automaticamente as tarefas de exportação.

>[!NOTE]
>
>A avaliação agendada pode ser ativada para caixas de proteção com um máximo de cinco (5) políticas de mesclagem para [!DNL XDM Individual Profile]. Se sua organização tiver mais de cinco políticas de mesclagem para [!DNL XDM Individual Profile] em um único ambiente de caixa de proteção, você não poderá usar a avaliação programada.

### Criar um agendamento

Ao fazer uma solicitação POST para o terminal `/config/schedules`, você pode criar um agendamento e incluir o horário específico em que o agendamento deve ser acionado.

Informações mais detalhadas sobre o uso desse terminal podem ser encontradas no [guia de endpoint de agendamentos](../api/schedules.md#create)

### Ativar um agendamento

Por padrão, uma programação fica inativa quando criada, a menos que a propriedade `state` esteja definida como `active` no corpo da solicitação create (POST). Você pode habilitar um agendamento (defina `state` como `active`), fazendo uma solicitação de PATCH para o terminal `/config/schedules` e incluindo a ID do agendamento no caminho.

Informações mais detalhadas sobre o uso desse terminal podem ser encontradas no [guia de endpoint de agendamentos](../api/schedules.md#update-state)

### Atualizar o horário agendado

O cronograma pode ser atualizado fazendo uma solicitação de PATCH ao terminal `/config/schedules` e incluindo a ID do agendamento no caminho.

Informações mais detalhadas sobre o uso desse terminal podem ser encontradas no [guia de endpoint de agendamentos](../api/schedules.md#update-schedule)

## Avaliação a pedido

A avaliação sob demanda permite criar um trabalho de segmento para gerar um segmento de audiência sempre que necessário. Ao contrário da avaliação agendada, isso ocorrerá somente quando solicitado e não é recorrente.

### Criar um trabalho de segmento

Um trabalho de segmento é um processo assíncrono que cria um novo segmento de audiência. Ele faz referência a uma definição de segmento, bem como a qualquer política de mesclagem que controle como [!DNL Real-time Customer Profile] mescla atributos sobrepostos em seus fragmentos de perfil. Quando uma tarefa de segmento é concluída com êxito, você pode coletar várias informações sobre o segmento, como quaisquer erros que possam ter ocorrido durante o processamento e o tamanho final da sua audiência.

Você pode criar um novo trabalho de segmento fazendo uma solicitação POST para o terminal `/segment/jobs` na API [!DNL Real-time Customer Profile].

Informações mais detalhadas sobre o uso desse ponto de extremidade podem ser encontradas no [guia de ponto de extremidade de jobs de segmento](../api/segment-jobs.md#create)


### Pesquisar o status do trabalho do segmento

Você pode usar `id` para um trabalho de segmento específico para executar uma solicitação de pesquisa (GET) para visualização do status atual do trabalho.

Informações mais detalhadas sobre o uso desse ponto de extremidade podem ser encontradas no [guia de ponto de extremidade de jobs de segmento](../api/segment-jobs.md#get)

## Interpretar os resultados do segmento

Quando os trabalhos de segmento são executados com êxito, o mapa `segmentMembership` é atualizado para cada perfil incluído no segmento. `segmentMembership` também armazena quaisquer segmentos de audiência pré-avaliados que sejam ingeridos  [!DNL Platform], permitindo a integração com outras soluções como  [!DNL Adobe Audience Manager].

O exemplo a seguir mostra a aparência do atributo `segmentMembership` para cada registro de perfil individual:

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

Se você souber o perfil específico que gostaria de acessar, poderá fazê-lo usando a API [!DNL Real-time Customer Profile]. As etapas completas para acessar perfis individuais estão disponíveis no tutorial [Acessar os dados do Perfil do cliente em tempo real usando a API do Perfil](../../profile/api/entities.md).

## Exportar um segmento {#export}

Depois que um trabalho de segmentação for concluído com êxito (o valor do atributo `status` for &quot;SUCEDIDO&quot;), você poderá exportar sua audiência para um conjunto de dados no qual ele possa ser acessado e executado.

As etapas a seguir são necessárias para exportar sua audiência:

- [Criar um conjunto de dados](#create-a-target-dataset)  de público alvo - Crie o conjunto de dados para manter membros de audiência.
- [Gerar perfis de audiência no conjunto de dados](#generate-profiles-for-audience-members)  - Preencha o conjunto de dados com Perfis individuais XDM com base nos resultados de um trabalho de segmento.
- [Monitorar o progresso](#monitor-export-progress)  da exportação - Verifique o andamento atual do processo de exportação.
- [Ler dados](#next-steps)  de audiência - recupere os Perfis individuais XDM resultantes que representam os membros da audiência.

### Criar um conjunto de dados de público alvo

Ao exportar uma audiência, um conjunto de dados de público alvo deve ser criado primeiro. É importante que o conjunto de dados seja configurado corretamente para garantir que a exportação seja bem-sucedida.

Uma das principais considerações é o schema no qual o conjunto de dados se baseia (`schemaRef.id` na solicitação de amostra de API abaixo). Para exportar um segmento, o conjunto de dados deve ter por base [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Um schema união é um schema gerado pelo sistema e somente leitura que agregação os campos de schemas que compartilham a mesma classe, neste caso, que é a classe de Perfil Individual XDM. Para obter mais informações sobre schemas de visualização de união, consulte a seção [Perfil do cliente em tempo real do guia do desenvolvedor do Registro do Schema](../../xdm/api/getting-started.md).

Há duas maneiras de criar o conjunto de dados necessário:

- **Usando APIs:** as etapas a seguir neste tutorial descrevem como criar um conjunto de dados que faz referência ao  [!DNL XDM Individual Profile Union Schema] uso da  [!DNL Catalog] API.
- **Uso da interface do usuário:** Para usar a interface do  [!DNL Adobe Experience Platform] usuário para criar um conjunto de dados que referencie o schema da união, siga as etapas no  [tutorial da ](../ui/overview.md) interface do usuário e retorne a este tutorial para prosseguir com as etapas de  [geração de perfis](#generate-xdm-profiles-for-audience-members) da audiência.

Se você já tiver um conjunto de dados compatível e souber sua ID, poderá prosseguir diretamente para a etapa para [gerar perfis audiências](#generate-xdm-profiles-for-audience-members).

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

Depois que você tiver um conjunto de dados que persiste na união, poderá criar um trabalho de exportação para persistir os membros da audiência no conjunto de dados, solicitando POST para o ponto final `/export/jobs` na API [!DNL Real-time Customer Profile] e fornecendo a ID do conjunto de dados e as informações do segmento para os segmentos que deseja exportar.

Informações mais detalhadas sobre o uso desse ponto de extremidade podem ser encontradas no [guia do ponto de extremidade de jobs de exportação](../api/export-jobs.md#create)

### Monitorar progresso de exportação

Como um trabalho de exportação processa, você pode monitorar seu status fazendo uma solicitação de GET para o ponto de extremidade `/export/jobs` e incluindo o `id` do trabalho de exportação no caminho. O trabalho de exportação é concluído assim que o campo `status` retorna o valor &quot;SUCEDIDO&quot;.

Informações mais detalhadas sobre o uso desse ponto de extremidade podem ser encontradas no [guia do ponto de extremidade de jobs de exportação](../api/export-jobs.md#get)

## Próximas etapas

Depois que a exportação for concluída com êxito, seus dados estarão disponíveis em [!DNL Data Lake] em [!DNL Experience Platform]. Você pode usar [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) para acessar os dados usando o `batchId` associado à exportação. Dependendo do tamanho do segmento, os dados podem estar em partes e o lote pode consistir em vários arquivos.

Para obter instruções passo a passo sobre como usar a API [!DNL Data Access] para acessar e baixar arquivos em lote, siga o [tutorial de Acesso a Dados](../../data-access/tutorials/dataset-data.md).

Você também pode acessar dados de segmento exportados com êxito usando [!DNL Adobe Experience Platform Query Service]. Usando a interface do usuário ou RESTful API, [!DNL Query Service] permite que você grave, valide e execute query em dados dentro de [!DNL Data Lake].

Para obter mais informações sobre como query dados de audiência, consulte a documentação em [[!DNL Query Service]](../../query-service/home.md).
