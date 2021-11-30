---
keywords: Experience Platform, home, tópicos populares, avaliação de segmento, Serviço de segmentação, segmentação, Segmentação, avaliar um segmento, acessar resultados do segmento, avaliar e acessar segmento;
solution: Experience Platform
title: Avaliar e acessar os resultados do segmento
topic-legacy: tutorial
type: Tutorial
description: Siga este tutorial para saber como avaliar segmentos e acessar resultados de segmentos usando a API do Serviço de segmentação da Adobe Experience Platform.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: 9e73925b0842c3b67db8bfda4b984bfa3e98a2fe
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 0%

---

# Avaliar e acessar os resultados do segmento

Este documento fornece um tutorial para avaliar segmentos e acessar resultados de segmentos usando o [[!DNL Segmentation API]](../api/getting-started.md).

## Introdução

Este tutorial requer uma compreensão funcional das várias [!DNL Adobe Experience Platform] serviços envolvidos na criação de segmentos de público-alvo. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Permite criar segmentos de público-alvo a partir de [!DNL Real-time Customer Profile] dados.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente. Para utilizar melhor a Segmentação, verifique se os dados são assimilados como perfis e eventos de acordo com a variável [práticas recomendadas para modelagem de dados](../../xdm/schema/best-practices.md).
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Cabeçalhos obrigatórios

Este tutorial também requer que você tenha completado o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas para [!DNL Platform] APIs. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isoladas em sandboxes virtuais específicas. Solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações de POST, PUT e PATCH exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Avaliar um segmento

Depois de desenvolver, testar e salvar a definição de segmento, você pode avaliar o segmento por meio de avaliação programada ou sob demanda.

[Avaliação programada](#scheduled-evaluation) (também conhecida como &quot;segmentação agendada&quot;) permite criar uma programação recorrente para executar um trabalho de exportação em um horário específico, enquanto [avaliação por demanda](#on-demand-evaluation) envolve criar um trabalho de segmento para criar o público-alvo imediatamente. As etapas para cada um são descritas abaixo.

Se você ainda não tiver concluído o [criar um segmento usando a API de segmentação](./create-a-segment.md) tutorial ou criado uma definição de segmento usando [Construtor de segmentos](../ui/overview.md), faça isso antes de prosseguir com este tutorial.

## Avaliação programada {#scheduled-evaluation}

Por meio da avaliação agendada, a Organização IMS pode criar um agendamento recorrente para executar automaticamente tarefas de exportação.

>[!NOTE]
>
>A avaliação programada pode ser ativada para sandboxes com no máximo cinco (5) políticas de mesclagem para [!DNL XDM Individual Profile]. Se sua organização tiver mais de cinco políticas de mesclagem para [!DNL XDM Individual Profile] em um único ambiente de sandbox, você não poderá usar a avaliação agendada.

### Criar um agendamento

Ao fazer uma solicitação de POST para a `/config/schedules` endpoint , é possível criar um agendamento e incluir o horário específico em que o agendamento deve ser acionado.

Informações mais detalhadas sobre o uso desse endpoint podem ser encontradas na seção [guia de endpoint de agendamentos](../api/schedules.md#create)

### Habilitar um agendamento

Por padrão, um agendamento fica inativo ao ser criado, a menos que a variável `state` está definida como `active` no corpo da solicitação de criação (POST). Você pode ativar uma programação (defina a variável `state` para `active`), fazendo uma solicitação de PATCH à `/config/schedules` endpoint e incluindo a ID do agendamento no caminho.

Informações mais detalhadas sobre o uso desse endpoint podem ser encontradas na seção [guia de endpoint de agendamentos](../api/schedules.md#update-state)

### Atualizar a hora da programação

O cronograma pode ser atualizado fazendo uma solicitação de PATCH para `/config/schedules` endpoint e incluindo a ID do agendamento no caminho.

Informações mais detalhadas sobre o uso desse endpoint podem ser encontradas na seção [guia de endpoint de agendamentos](../api/schedules.md#update-schedule)

## Avaliação por demanda

A avaliação sob demanda permite criar um trabalho de segmento para gerar um segmento de público-alvo sempre que necessário. Ao contrário da avaliação agendada, isso só acontecerá quando solicitado e não é recorrente.

### Criar um trabalho de segmento

Um trabalho de segmento é um processo assíncrono que cria um segmento de público-alvo sob demanda. Ele faz referência a uma definição de segmento, bem como a quaisquer políticas de mesclagem que controlam como [!DNL Real-time Customer Profile] mescla atributos sobrepostos nos fragmentos de perfil. Quando um trabalho de segmento é concluído com êxito, você pode coletar várias informações sobre o segmento, como erros que possam ter ocorrido durante o processamento e o tamanho final do público-alvo. Um trabalho de segmento precisa ser executado sempre que você quiser atualizar o público-alvo que está qualificado para a definição do segmento no momento.

Você pode criar um novo trabalho de segmento fazendo uma solicitação de POST para a variável `/segment/jobs` endpoint no [!DNL Real-time Customer Profile] API.

Informações mais detalhadas sobre o uso desse endpoint podem ser encontradas na seção [guia do endpoint de tarefas do segmento](../api/segment-jobs.md#create)

### Pesquisar o status do trabalho do segmento

Você pode usar o `id` para um trabalho de segmento específico executar uma solicitação de pesquisa (GET) para visualizar o status atual do trabalho.

Informações mais detalhadas sobre o uso desse endpoint podem ser encontradas na seção [guia do endpoint de tarefas do segmento](../api/segment-jobs.md#get)

## Interpretar os resultados do segmento

Quando as tarefas de segmento são executadas com êxito, a variável `segmentMembership` O mapa é atualizado para cada perfil incluído no segmento. `segmentMembership` também armazena quaisquer segmentos de público-alvo pré-avaliados que estejam assimilados em [!DNL Platform], permitindo a integração com outras soluções como [!DNL Adobe Audience Manager].

O exemplo a seguir mostra o que a função `segmentMembership` é semelhante para cada registro de perfil individual:

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

Os resultados de um trabalho de segmento podem ser acessados de uma das duas formas a seguir: você pode acessar perfis individuais ou exportar um público-alvo inteiro para um conjunto de dados.

As seções a seguir descrevem essas opções com mais detalhes.

## Pesquisar um perfil

Se você souber o perfil específico que gostaria de acessar, poderá fazer isso usando o [!DNL Real-time Customer Profile] API. As etapas completas para acessar perfis individuais estão disponíveis na variável [Acesse os dados do Perfil do cliente em tempo real usando a API do perfil](../../profile/api/entities.md) tutorial.

## Exportar um segmento {#export}

Após a conclusão bem-sucedida de um trabalho de segmentação (o valor da variável `status` é &quot;SUCCEEDED&quot;), você pode exportar seu público para um conjunto de dados, onde ele pode ser acessado e tratado.

As etapas a seguir são necessárias para exportar seu público-alvo:

- [Criar um conjunto de dados de destino](#create-a-target-dataset) - Crie o conjunto de dados para manter os membros do público-alvo.
- [Gerar perfis de público-alvo no conjunto de dados](#generate-profiles) - Preencha o conjunto de dados com Perfis individuais XDM com base nos resultados de um trabalho de segmento.
- [Monitorar progresso da exportação](#monitor-export-progress) - Verifique o progresso atual do processo de exportação.
- [Ler dados do público-alvo](#next-steps) - Recupere os perfis individuais XDM resultantes que representam os membros do seu público-alvo.

### Criar um conjunto de dados de destino

Ao exportar um público-alvo, um conjunto de dados de destino deve ser criado primeiro. É importante que o conjunto de dados seja configurado corretamente para garantir que a exportação seja bem-sucedida.

Uma das principais considerações é o schema no qual o conjunto de dados se baseia (`schemaRef.id` na solicitação de exemplo de API abaixo). Para exportar um segmento, o conjunto de dados deve ser baseado na variável [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Um schema de união é um schema gerado pelo sistema e somente leitura que agrega os campos de esquemas que compartilham a mesma classe, neste caso, que é a classe de Perfil individual XDM. Para obter mais informações sobre schemas de exibição de união, consulte o [Seção Perfil do cliente em tempo real do guia do desenvolvedor do Registro de esquemas](../../xdm/api/getting-started.md).

Há duas maneiras de criar o conjunto de dados necessário:

- **Uso de APIs:** As etapas a seguir neste tutorial descrevem como criar um conjunto de dados que faça referência à variável [!DNL XDM Individual Profile Union Schema] usando o [!DNL Catalog] API.
- **Utilização da interface de usuário:** Para usar o [!DNL Adobe Experience Platform] interface do usuário para criar um conjunto de dados que faça referência ao esquema de união, siga as etapas em [Tutorial da interface do usuário](../ui/overview.md) e retorne a este tutorial para prosseguir com as etapas para [geração de perfis de público-alvo](#generate-profiles).

Se você já tiver um conjunto de dados compatível e souber sua ID, poderá prosseguir diretamente para a etapa para [geração de perfis de público-alvo](#generate-profiles).

**Formato da API**

```http
POST /dataSets
```

**Solicitação**

A solicitação a seguir cria um novo conjunto de dados, fornecendo parâmetros de configuração no payload.

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
    }
}'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | Um nome descritivo para o conjunto de dados. |
| `schemaRef.id` | A ID da exibição de união (schema) à qual o conjunto de dados será associado. |

**Resposta**

Uma resposta bem-sucedida retorna uma matriz contendo a ID exclusiva gerada pelo sistema e somente leitura do conjunto de dados recém-criado. É necessária uma ID de conjunto de dados devidamente configurada para exportar os membros do público-alvo com êxito.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Gerar perfis para membros do público-alvo {#generate-profiles}

Depois de ter um conjunto de dados que persiste em união, você pode criar um trabalho de exportação para manter os membros do público-alvo no conjunto de dados, fazendo uma solicitação de POST para a variável `/export/jobs` endpoint no [!DNL Real-time Customer Profile] API e o fornecimento da ID do conjunto de dados e das informações do segmento para os segmentos que você deseja exportar.

Informações mais detalhadas sobre o uso desse endpoint podem ser encontradas na seção [guia do endpoint de tarefas de exportação](../api/export-jobs.md#create)

### Monitorar progresso da exportação

Como um trabalho de exportação processa, você pode monitorar seu status fazendo uma solicitação de GET para a `/export/jobs` endpoint e incluindo o `id` do trabalho de exportação no caminho. O trabalho de exportação é concluído assim que o `status` retorna o valor &quot;SUCCEEDED&quot;.

Informações mais detalhadas sobre o uso desse endpoint podem ser encontradas na seção [guia do endpoint de tarefas de exportação](../api/export-jobs.md#get)

## Próximas etapas

Depois que a exportação for concluída com êxito, seus dados estarão disponíveis no [!DNL Data Lake] em [!DNL Experience Platform]. Em seguida, você pode usar o [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) para acessar os dados usando o `batchId` associado à exportação. Dependendo do tamanho do segmento, os dados podem estar em partes e o lote pode consistir em vários arquivos.

Para obter instruções passo a passo sobre como usar o [!DNL Data Access] API para acessar e baixar arquivos em lote, siga as [Tutorial de acesso a dados](../../data-access/tutorials/dataset-data.md).

Você também pode acessar dados de segmentos exportados com êxito usando [!DNL Adobe Experience Platform Query Service]. Usar a interface do usuário ou a RESTful API, [!DNL Query Service] O permite gravar, validar e executar consultas em dados no [!DNL Data Lake].

Para obter mais informações sobre como consultar dados do público-alvo, consulte a documentação em [[!DNL Query Service]](../../query-service/home.md).
