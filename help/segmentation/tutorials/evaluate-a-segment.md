---
solution: Experience Platform
title: Avaliar e acessar resultados do segmento
type: Tutorial
description: Siga este tutorial para saber como avaliar definições de segmento e acessar resultados da segmentação usando a API do serviço de segmentação do Adobe Experience Platform.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 2%

---

# Avaliar e acessar resultados de definição de segmento

Este documento fornece um tutorial para avaliar as definições de segmento e acessar esses resultados usando o [[!DNL Segmentation API]](../api/getting-started.md).

## Introdução

Este tutorial requer um entendimento prático dos vários [!DNL Adobe Experience Platform] serviços envolvidos na criação de públicos. Antes de iniciar este tutorial, revise a documentação dos seguintes serviços:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): permite criar públicos-alvo a partir do [!DNL Real-Time Customer Profile] dados.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): a estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente. Para melhor usar a segmentação, verifique se seus dados são assimilados como perfis e eventos de acordo com a [práticas recomendadas para modelagem de dados](../../xdm/schema/best-practices.md).
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] O fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Cabeçalhos obrigatórios

Este tutorial também requer que você tenha concluído a [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para o [!DNL Platform] APIs. Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isolados em sandboxes virtuais específicas. Solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes no [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações de POST, PUT e PATCH exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Avaliar uma definição de segmento {#evaluate-a-segment}

Depois de desenvolver, testar e salvar a definição do segmento, é possível avaliá-la por meio da avaliação programada ou por meio da avaliação sob demanda.

[Avaliação programada](#scheduled-evaluation) (também conhecida como &quot;segmentação programada&quot;) permite criar uma programação recorrente para executar um trabalho de exportação em um horário específico, enquanto [avaliação sob demanda](#on-demand-evaluation) envolve a criação de um trabalho de segmento para criar o público-alvo imediatamente. As etapas para cada um são descritas abaixo.

Se você ainda não tiver concluído a [criar uma definição de segmento usando a API de segmentação](./create-a-segment.md) tutorial ou criou uma definição de segmento usando [Construtor de segmentos](../ui/overview.md), faça isso antes de prosseguir com este tutorial.

## Avaliação programada {#scheduled-evaluation}

Por meio da avaliação programada, sua organização pode criar uma programação recorrente para executar trabalhos de exportação automaticamente.

>[!NOTE]
>
>A avaliação agendada pode ser ativada para sandboxes com um máximo de cinco (5) políticas de mesclagem para [!DNL XDM Individual Profile]. Se sua organização tiver mais de cinco políticas de mesclagem para [!DNL XDM Individual Profile] em um único ambiente de sandbox, não será possível usar a avaliação programada.

### Criar um agendamento

Ao fazer uma solicitação POST para o `/config/schedules` você pode criar um agendamento e incluir a hora específica em que o agendamento deve ser acionado.

Informações mais detalhadas sobre como usar este endpoint podem ser encontradas na [guia de endpoint de agendamentos](../api/schedules.md#create)

### Ativar um agendamento

Por padrão, um agendamento fica inativo quando criado, a menos que `state` propriedade está definida como `active` no corpo da solicitação create (POST). Você pode habilitar um agendamento (defina o `state` para `active`) fazendo um pedido PATCH ao `/config/schedules` e incluindo a ID do agendamento no caminho.

Informações mais detalhadas sobre como usar este endpoint podem ser encontradas na [guia de endpoint de agendamentos](../api/schedules.md#update-state)

### Atualizar o horário agendado

O cronograma pode ser atualizado fazendo uma solicitação PATCH para o `/config/schedules` e incluindo a ID do agendamento no caminho.

Informações mais detalhadas sobre como usar este endpoint podem ser encontradas na [guia de endpoint de agendamentos](../api/schedules.md#update-schedule)

## Avaliação sob demanda

A avaliação sob demanda permite criar um trabalho de segmento para gerar um público-alvo sempre que você precisar. Ao contrário da avaliação agendada, isso ocorrerá somente quando solicitado e não é recorrente.

### Criar um trabalho de segmento

Um trabalho de segmento é um processo assíncrono que cria um segmento de público-alvo sob demanda. Ele faz referência a uma definição de segmento, bem como a quaisquer políticas de mesclagem que controlam como [!DNL Real-Time Customer Profile] O mescla atributos sobrepostos nos fragmentos de perfil. Quando um trabalho de segmento é concluído com sucesso, você pode coletar várias informações sobre a definição do segmento, como erros que possam ter ocorrido durante o processamento e o tamanho máximo do seu público-alvo. Um trabalho de segmento precisa ser executado sempre que você quiser atualizar o público-alvo que a definição de segmento qualifica atualmente.

Você pode criar um novo trabalho de segmento fazendo uma solicitação POST para o `/segment/jobs` endpoint na variável [!DNL Real-Time Customer Profile] API.

Informações mais detalhadas sobre como usar este endpoint podem ser encontradas na [manual de endpoint de trabalhos de segmento](../api/segment-jobs.md#create)

### Pesquisar status do trabalho do segmento

Você pode usar o `id` para um job de segmento específico, execute uma solicitação de pesquisa (GET) para exibir o status atual do job.

Informações mais detalhadas sobre como usar este endpoint podem ser encontradas na [manual de endpoint de trabalhos de segmento](../api/segment-jobs.md#get)

## Interpretar resultados do trabalho do segmento

Quando os trabalhos de segmento são executados com sucesso, a variável `segmentMembership` O mapa é atualizado para cada perfil incluído na definição do segmento. `segmentMembership` O também armazena quaisquer públicos-alvo pré-avaliados que são assimilados na [!DNL Platform], permitindo a integração com outras soluções, como [!DNL Adobe Audience Manager].

O exemplo a seguir mostra o que `segmentMembership` O atributo é semelhante a para cada registro de perfil individual:

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "realized"
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
| `lastQualificationTime` | O carimbo de data e hora quando a declaração de associação do segmento foi feita e o perfil entrou ou saiu da definição do segmento. |
| `status` | O status de participação da definição de segmento como parte da solicitação atual. Deve ser igual a um dos seguintes valores conhecidos: <ul><li>`realized`: a entidade se qualifica para a definição do segmento.</li><li>`exited`: a entidade está saindo da definição do segmento.</li></ul> |

>[!NOTE]
>
>Qualquer associação de segmento que esteja no `exited` por mais de 30 dias, com base na `lastQualificationTime`, estará sujeita a exclusão.

## Acessar resultados de trabalho do segmento

Os resultados de um trabalho de segmento podem ser acessados de uma das duas formas a seguir: você pode acessar perfis individuais ou exportar um público-alvo inteiro para um conjunto de dados.

As seções a seguir descrevem essas opções com mais detalhes.

## Pesquisar um perfil

Se você souber o perfil específico que gostaria de acessar, é possível fazer isso usando o [!DNL Real-Time Customer Profile] API. As etapas completas para acessar perfis individuais estão disponíveis na [Acessar dados do Perfil do cliente em tempo real usando a API do perfil](../../profile/api/entities.md) tutorial.

## Exportar um segmento {#export}

Depois que um trabalho de segmentação é concluído com sucesso (o valor da variável `status` atributo é &quot;SUCCEEDED&quot;), você pode exportar seu público-alvo para um conjunto de dados em que ele possa ser acessado e aplicado.

As seguintes etapas são necessárias para exportar seu público-alvo:

- [Criar um conjunto de dados de destino](#create-a-target-dataset) : crie o conjunto de dados para conter membros do público-alvo.
- [Gerar perfis de público-alvo no conjunto de dados](#generate-profiles) - Preencha o conjunto de dados com Perfis individuais XDM com base nos resultados de um trabalho de segmento.
- [Monitorar o progresso da exportação](#monitor-export-progress) - Verifique o progresso atual do processo de exportação.
- [Ler dados do público](#next-steps) - Recupere os Perfis individuais XDM resultantes que representam os membros do público-alvo.

### Criar um conjunto de dados de destino {#create-dataset}

Ao exportar um público-alvo, um conjunto de dados de destino deve ser criado primeiro. É importante que o conjunto de dados seja configurado corretamente para garantir que a exportação seja bem-sucedida.

Uma das principais considerações é o esquema no qual o conjunto de dados se baseia (`schemaRef.id` na solicitação de amostra de API abaixo). Para exportar uma definição de segmento, o conjunto de dados deve ser baseado na variável [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Um esquema de união é um esquema somente leitura gerado pelo sistema que agrega os campos de esquemas que compartilham a mesma classe, neste caso, a classe Perfil individual XDM. Para obter mais informações sobre esquemas de visualização de união, consulte a [Seção Perfil do cliente em tempo real do guia do desenvolvedor do Registro de esquema](../../xdm/api/getting-started.md).

Há duas maneiras de criar o conjunto de dados necessário:

- **Uso de APIs:** As etapas a seguir neste tutorial descrevem como criar um conjunto de dados que faça referência ao [!DNL XDM Individual Profile Union Schema] usando o [!DNL Catalog] API.
- **Uso da interface do usuário:** Para usar o [!DNL Adobe Experience Platform] para criar um conjunto de dados que faça referência ao esquema de união, siga as etapas da seção [Tutorial de interface do usuário](../ui/overview.md) e retorne a este tutorial para prosseguir com as etapas para [geração de perfis de público](#generate-profiles).

Se você já tiver um conjunto de dados compatível e souber sua ID, poderá prosseguir diretamente para a etapa para [geração de perfis de público](#generate-profiles).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | Um nome descritivo para o conjunto de dados. |
| `schemaRef.id` | A ID da visualização de união (esquema) à qual o conjunto de dados será associado. |

**Resposta**

Uma resposta bem-sucedida retorna uma matriz que contém a ID exclusiva gerada pelo sistema somente leitura do conjunto de dados recém-criado. Uma ID de conjunto de dados configurada corretamente é necessária para exportar membros do público-alvo com êxito.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Gerar perfis para membros do público {#generate-profiles}

Depois de ter um conjunto de dados persistente em união, você pode criar um trabalho de exportação para persistir os membros do público-alvo para o conjunto de dados fazendo uma solicitação POST para o `/export/jobs` endpoint na variável [!DNL Real-Time Customer Profile] e fornecendo a ID do conjunto de dados e as informações de definição de segmento para as definições de segmento que você deseja exportar.

Informações mais detalhadas sobre como usar este endpoint podem ser encontradas na [guia de endpoint de trabalhos de exportação](../api/export-jobs.md#create)

### Monitorar o progresso da exportação

Como um processo de trabalho de exportação, é possível monitorar seu status fazendo uma solicitação GET ao `/export/jobs` e incluindo o `id` do trabalho de exportação no caminho. O trabalho de exportação é concluído depois que a variável `status` O campo retorna o valor &quot;SUCCEEDED&quot;.

Informações mais detalhadas sobre como usar este endpoint podem ser encontradas na [guia de endpoint de trabalhos de exportação](../api/export-jobs.md#get)

## Próximas etapas

Após a exportação ser concluída com êxito, os dados estarão disponíveis na [!DNL Data Lake] in [!DNL Experience Platform]. Em seguida, você pode usar o [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) para acessar os dados usando o `batchId` associada à exportação. Dependendo do tamanho da definição do segmento, os dados podem estar em partes e o lote pode consistir em vários arquivos.

Para obter instruções passo a passo sobre como usar o [!DNL Data Access] para acessar e baixar arquivos em lote, siga as [Tutorial de acesso a dados](../../data-access/tutorials/dataset-data.md).

Você também pode acessar dados de definição de segmento exportados com sucesso usando [!DNL Adobe Experience Platform Query Service]. Usando a IU ou a API RESTful, [!DNL Query Service] permite gravar, validar e executar consultas em dados no [!DNL Data Lake].

Para obter mais informações sobre como consultar dados de público, consulte a documentação em [[!DNL Query Service]](../../query-service/home.md).
