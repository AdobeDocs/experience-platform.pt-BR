---
keywords: Experience Platform, página inicial, tópicos populares, segmento, segmento, criar segmento, segmentação, criar um segmento, Serviço de segmentação;
solution: Experience Platform
title: Criar um segmento usando a API do serviço de segmentação
topic-legacy: tutorial
type: Tutorial
description: Siga este tutorial para saber como desenvolver, testar, visualizar e salvar uma definição de segmento usando a API do serviço de segmentação do Adobe Experience Platform.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# Criar um segmento usando a API do serviço de segmentação

Este documento fornece um tutorial para desenvolver, testar, visualizar e salvar uma definição de segmento usando o [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Para obter informações sobre como criar segmentos usando a interface do usuário, consulte o [Guia do Construtor de segmentos](../ui/overview.md).

## Introdução

Este tutorial requer uma compreensão funcional das várias [!DNL Adobe Experience Platform] serviços envolvidos na criação de segmentos de público-alvo. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Allows you to build audience segments from Real-time Customer Profile data.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): O quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente. Para utilizar melhor a Segmentação, verifique se os dados são assimilados como perfis e eventos de acordo com a variável [práticas recomendadas para modelagem de dados](../../xdm/schema/best-practices.md).

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas para o [!DNL Platform] APIs.

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] As APIs devem ser concluídas primeiro [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isoladas em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Desenvolver uma definição de segmento

A primeira etapa da segmentação é definir um segmento, representado em uma construção chamada de definição de segmento. Uma definição de segmento é um objeto que encapsula uma consulta escrita em [!DNL Profile Query Language] (PQL). Esse objeto também é chamado de predicado PQL. Os predicados PQL definem as regras para o segmento com base nas condições relacionadas a qualquer registro ou série de tempo que você fornecer para [!DNL Real-time Customer Profile]. Consulte a [Guia PQL](../pql/overview.md) para obter mais informações sobre como gravar consultas PQL.

Você pode criar uma nova definição de segmento fazendo uma solicitação de POST para a variável `/segment/definitions` endpoint no [!DNL Segmentation] API. O exemplo a seguir descreve como formatar uma solicitação de definição, incluindo quais informações são necessárias para que um segmento seja definido com êxito.

Para obter uma explicação detalhada sobre como definir um segmento, leia o [guia do desenvolvedor de definição de segmento](../api/segment-definitions.md#create).

## Estimar e visualizar um público-alvo {#estimate-and-preview-an-audience}

As you develop your segment definition, you can use the estimate and preview tools within [!DNL Real-time Customer Profile] to view summary-level information to help ensure you are isolating the expected audience. As estimativas fornecem informações estatísticas sobre uma definição de segmento, como o tamanho projetado do público-alvo e o intervalo de confiança. Previews provide paginated lists of qualifying profiles for a segment definition, allowing you to compare the results against what you expect.

Ao estimar e visualizar seu público-alvo, você pode testar e otimizar seus predicados de PQL até que eles produzam um resultado desejável, onde poderão ser usados em uma definição de segmento atualizada.

Há duas etapas necessárias para visualizar ou obter uma estimativa do seu segmento:

1. [Criar um trabalho de pré-visualização](#create-a-preview-job)
2. [Exibir estimativa ou pré-visualização](#view-an-estimate-or-preview) usar a ID do trabalho de visualização

### How estimates are generated

As amostras de dados são usadas para avaliar segmentos e estimar o número de perfis qualificados. Novos dados são carregados na memória toda manhã (entre 12AM e 2AM PT, que é de 7 a 9AM UTC), e todas as consultas de segmentação são estimadas usando os dados de amostra desse dia. Consequentemente, quaisquer novos campos ou dados adicionais recolhidos serão refletidos nas estimativas do dia seguinte.

O tamanho da amostra depende do número geral de entidades no armazenamento de perfil. Esses tamanhos de amostra são representados na tabela a seguir:

| Entidades no armazenamento de perfis | Tamanho da amostra |
| ------------------------- | ----------- |
| Menos de 1 milhão | Conjunto de dados completo |
| 1 to 20 million | 1 milhão |
| Mais de 20 milhões | 5% do total |

Estimates generally run over 10-15 seconds, beginning with a rough estimate and refining as more records are read.

### Criar um trabalho de pré-visualização

Você pode criar um novo trabalho de pré-visualização, fazendo uma solicitação de POST para o `/preview` endpoint .

Detailed instructions on creating a preview job can be found in the [previews and estimates endpoints guide](../api/previews-and-estimates.md#create-preview).

### Exibir uma estimativa ou pré-visualização

Os processos de estimativa e pré-visualização são executados de forma assíncrona, pois consultas diferentes podem levar períodos diferentes para serem concluídas. Depois que uma consulta é iniciada, você pode usar chamadas de API para recuperar (GET) o estado atual da estimativa ou pré-visualização à medida que progride.

Usar o [!DNL Segmentation Service] Você pode pesquisar o estado atual de um trabalho de visualização pela ID. Se o estado for &quot;RESULT_READY&quot;, você poderá visualizar os resultados. Para procurar o estado atual de um trabalho de visualização, leia a seção sobre [recuperação de uma seção de trabalho de pré-visualização](../api/previews-and-estimates.md#get-preview) no guia de endpoints de visualizações e estimativas. Para procurar o estado atual de uma tarefa de estimativa, leia a seção sobre [recuperando um trabalho de estimativa](../api/previews-and-estimates.md#get-estimate) no guia de endpoints de visualizações e estimativas.


## Próximas etapas

Depois de desenvolver, testar e salvar a definição de segmento, você pode criar um trabalho de segmento para criar um público-alvo usando a [!DNL Segmentation Service] API. Veja o tutorial em [avaliação e acesso aos resultados do segmento](./evaluate-a-segment.md) para obter etapas detalhadas sobre como fazer isso.
