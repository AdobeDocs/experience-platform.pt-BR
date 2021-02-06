---
keywords: Experience Platform;home;popular topics;segment;Segment;create segment;segmentation;create a segment;Segmentation Service;
solution: Experience Platform
title: Criar um segmento usando a API do serviço de segmentação
topic: tutorial
type: Tutorial
description: Siga este tutorial para saber como desenvolver, testar, pré-visualização e salvar uma definição de segmento usando a Adobe Experience Platform Segmentation Service API.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---


# Criar um segmento usando a API do Serviço de segmentação

Este documento fornece um tutorial para desenvolver, testar, visualizar e salvar uma definição de segmento usando [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Para obter informações sobre como criar segmentos usando a interface do usuário, consulte o [guia do Construtor de segmentos](../ui/overview.md).

## Introdução

Este tutorial requer uma compreensão funcional dos vários [!DNL Adobe Experience Platform] serviços envolvidos na criação de segmentos de audiência. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Permite criar segmentos de audiência a partir de dados de Perfil do cliente em tempo real.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Platform] organiza os dados de experiência do cliente.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas bem-sucedidas para as APIs [!DNL Platform].

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API [!DNL Experience Platform], como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a [documentação de visão geral da caixa de proteção](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Desenvolver uma definição de segmento

A primeira etapa da segmentação é definir um segmento, representado em uma construção chamada definição de segmento. Uma definição de segmento é um objeto que encapsula um query gravado em [!DNL Profile Query Language] (PQL). Esse objeto também é chamado de predicado PQL. Os predicados de PQL definem as regras para o segmento com base nas condições relacionadas a qualquer registro ou série de tempo que você fornecer a [!DNL Real-time Customer Profile]. Consulte o [guia PQL](../pql/overview.md) para obter mais informações sobre como gravar query PQL.

Você pode criar uma nova definição de segmento, solicitando um POST para o terminal `/segment/definitions` na API [!DNL Segmentation]. O exemplo a seguir descreve como formatar uma solicitação de definição, incluindo quais informações são necessárias para que um segmento seja definido com sucesso.

Para obter uma explicação detalhada sobre como definir um segmento, leia o [guia do desenvolvedor de definição de segmento](../api/segment-definitions.md#create).

## Estime e pré-visualização uma audiência {#estimate-and-preview-an-audience}

À medida que você desenvolve a definição do segmento, você pode usar as ferramentas de estimativa e pré-visualização em [!DNL Real-time Customer Profile] para visualização de informações de nível de resumo para ajudar a garantir que você esteja isolando a audiência esperada. As estimativas fornecem informações estatísticas sobre uma definição de segmento, como o tamanho da audiência projetada e o intervalo de confiança. As pré-visualizações fornecem listas paginadas de perfis qualificados para uma definição de segmento, permitindo que você compare os resultados com o esperado.

Ao estimar e visualizar sua audiência, você pode testar e otimizar seus predicados de PQL até que produzam um resultado desejável, onde eles poderão ser usados em uma definição de segmento atualizada.

Há duas etapas necessárias para pré-visualização ou obter uma estimativa do seu segmento:

1. [Criar um trabalho de pré-visualização](#create-a-preview-job)
2. [Estimativa de visualização ou ](#view-an-estimate-or-preview) visualização usando a ID do trabalho de pré-visualização

### Como as estimativas são geradas

As amostras de dados são usadas para avaliar segmentos e estimar o número de perfis qualificados. Novos dados são carregados na memória todas as manhãs (entre 12AM-2AM PT, que é 7-9AM UTC), e todos os query de segmentação são estimados usando os dados de amostra desse dia. Consequentemente, quaisquer novos campos adicionados ou dados adicionais recolhidos serão refletidos nas estimativas do dia seguinte.

O tamanho da amostra depende do número total de entidades na loja de perfis. Esses tamanhos de amostra são representados na tabela a seguir:

| Entidades na loja de perfis | Tamanho da amostra |
| ------------------------- | ----------- |
| Menos de 1 milhão | Conjunto completo de dados |
| 1 a 20 milhões | 1 milhão |
| Mais de 20 milhões | 5% do total |

As estimativas geralmente são executadas de 10 a 15 segundos, começando com uma estimativa aproximada e refinando à medida que mais registros são lidos.

### Criar um trabalho de pré-visualização

Você pode criar um novo trabalho de pré-visualização, fazendo uma solicitação de POST para o terminal `/preview`.

Instruções detalhadas sobre a criação de um trabalho de pré-visualização podem ser encontradas no guia [pré-visualizações e estimativas de pontos finais](../api/previews-and-estimates.md#create-preview).

### Visualização de uma estimativa ou pré-visualização

Os processos de estimativa e pré-visualização são executados de forma assíncrona, pois query diferentes podem demorar tempos diferentes para serem concluídos. Depois que um query é iniciado, você pode usar chamadas de API para recuperar (GET) o estado atual da estimativa ou pré-visualização à medida que ela avança.

Usando a API [!DNL Segmentation Service], você pode procurar o estado atual de um trabalho de pré-visualização por sua ID. Se o estado for &quot;RESULT_READY&quot;, você poderá visualização os resultados. Para pesquisar o estado atual de um trabalho de pré-visualização, leia a seção em [recuperando uma seção de trabalho de pré-visualização](../api/previews-and-estimates.md#get-preview) no guia de pontos de extremidade de pré-visualizações e estimativas. Para procurar o estado atual de uma tarefa de estimativa, leia a seção sobre [como recuperar uma tarefa de estimativa](../api/previews-and-estimates.md#get-estimate) no guia de pontos de extremidade de pré-visualizações e estimativas.


## Próximas etapas

Depois de desenvolver, testar e salvar sua definição de segmento, você pode criar um trabalho de segmento para criar uma audiência usando a API [!DNL Segmentation Service]. Consulte o tutorial em [avaliar e acessar os resultados do segmento](./evaluate-a-segment.md) para obter etapas detalhadas sobre como fazer isso.