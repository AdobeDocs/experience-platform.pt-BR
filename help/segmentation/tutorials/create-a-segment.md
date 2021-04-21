---
keywords: Experience Platform, página inicial, tópicos populares, segmento, segmento, criar segmento, segmentação, criar um segmento, Serviço de segmentação;
solution: Experience Platform
title: Criar um segmento usando a API do serviço de segmentação
topic-legacy: tutorial
type: Tutorial
description: Siga este tutorial para saber como desenvolver, testar, visualizar e salvar uma definição de segmento usando a API do serviço de segmentação do Adobe Experience Platform.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# Criar um segmento usando a API do serviço de segmentação

Este documento fornece um tutorial para desenvolver, testar, visualizar e salvar uma definição de segmento usando o [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Para obter informações sobre como criar segmentos usando a interface do usuário, consulte o [Guia do Construtor de Segmentos](../ui/overview.md).

## Introdução

Este tutorial requer uma compreensão funcional dos vários [!DNL Adobe Experience Platform] serviços envolvidos na criação de segmentos de público-alvo. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Permite criar segmentos de público-alvo a partir de dados do Perfil do cliente em tempo real.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs [!DNL Platform].

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Desenvolver uma definição de segmento

A primeira etapa da segmentação é definir um segmento, representado em uma construção chamada de definição de segmento. Uma definição de segmento é um objeto que encapsula uma consulta escrita em [!DNL Profile Query Language] (PQL). Esse objeto também é chamado de predicado PQL. Os predicados PQL definem as regras para o segmento com base nas condições relacionadas a qualquer registro ou série de tempo que você fornecer para [!DNL Real-time Customer Profile]. Consulte o [Guia PQL](../pql/overview.md) para obter mais informações sobre como gravar consultas PQL.

Você pode criar uma nova definição de segmento fazendo uma solicitação POST para o endpoint `/segment/definitions` na API [!DNL Segmentation]. O exemplo a seguir descreve como formatar uma solicitação de definição, incluindo quais informações são necessárias para que um segmento seja definido com êxito.

Para obter uma explicação detalhada sobre como definir um segmento, leia o [guia do desenvolvedor de definição de segmento](../api/segment-definitions.md#create).

## Estimar e visualizar um público {#estimate-and-preview-an-audience}

À medida que desenvolve a definição do segmento, você pode usar as ferramentas de estimativa e visualização em [!DNL Real-time Customer Profile] para exibir as informações de nível de resumo, de modo a ajudar a garantir que você esteja isolando o público-alvo esperado. As estimativas fornecem informações estatísticas sobre uma definição de segmento, como o tamanho projetado do público-alvo e o intervalo de confiança. As visualizações fornecem listas paginadas de perfis de qualificação para uma definição de segmento, permitindo que você compare os resultados com o que espera.

Ao estimar e visualizar seu público-alvo, você pode testar e otimizar seus predicados de PQL até que eles produzam um resultado desejável, onde poderão ser usados em uma definição de segmento atualizada.

Há duas etapas necessárias para visualizar ou obter uma estimativa do seu segmento:

1. [Criar um trabalho de pré-visualização](#create-a-preview-job)
2. [Exibir estimativa ou ](#view-an-estimate-or-preview) pré-visualização usando a ID do trabalho de pré-visualização

### Como as estimativas são geradas

As amostras de dados são usadas para avaliar segmentos e estimar o número de perfis qualificados. Novos dados são carregados na memória toda manhã (entre 12AM e 2AM PT, que é de 7 a 9AM UTC), e todas as consultas de segmentação são estimadas usando os dados de amostra desse dia. Consequentemente, quaisquer novos campos ou dados adicionais recolhidos serão refletidos nas estimativas do dia seguinte.

O tamanho da amostra depende do número geral de entidades no armazenamento de perfil. Esses tamanhos de amostra são representados na tabela a seguir:

| Entidades no armazenamento de perfis | Tamanho da amostra |
| ------------------------- | ----------- |
| Menos de 1 milhão | Conjunto de dados completo |
| 1 a 20 milhões | 1 milhão |
| Mais de 20 milhões | 5% do total |

As estimativas geralmente são executadas de 10 a 15 segundos, começando com uma estimativa aproximada e refinando à medida que mais registros são lidos.

### Criar um trabalho de pré-visualização

Você pode criar um novo trabalho de visualização, fazendo uma solicitação de POST ao endpoint `/preview`.

Instruções detalhadas sobre como criar um trabalho de visualização podem ser encontradas no [guia de visualizações e estimativas de endpoints](../api/previews-and-estimates.md#create-preview).

### Exibir uma estimativa ou pré-visualização

Os processos de estimativa e pré-visualização são executados de forma assíncrona, pois consultas diferentes podem levar períodos diferentes para serem concluídas. Depois que uma consulta é iniciada, você pode usar chamadas de API para recuperar (GET) o estado atual da estimativa ou pré-visualização à medida que progride.

Usando a API [!DNL Segmentation Service], você pode pesquisar o estado atual de um trabalho de visualização por sua ID. Se o estado for &quot;RESULT_READY&quot;, você poderá visualizar os resultados. Para procurar o estado atual de um trabalho de visualização, leia a seção sobre [recuperar uma seção de trabalho de visualização](../api/previews-and-estimates.md#get-preview) no guia de visualizações e estimativas de pontos finais. Para pesquisar o estado atual de uma tarefa de estimativa, leia a seção sobre [recuperação de uma tarefa de estimativa](../api/previews-and-estimates.md#get-estimate) no guia de endpoints de visualizações e estimativas.


## Próximas etapas

Depois de desenvolver, testar e salvar a definição de segmento, você pode criar um trabalho de segmento para criar um público-alvo usando a API [!DNL Segmentation Service]. Consulte o tutorial em [avaliar e acessar os resultados do segmento](./evaluate-a-segment.md) para obter etapas detalhadas sobre como fazer isso.
