---
solution: Experience Platform
title: Criar uma definição de segmento usando a API do serviço de segmentação
type: Tutorial
description: Siga este tutorial para saber como desenvolver, testar, visualizar e salvar uma definição de segmento usando a API do serviço de segmentação do Adobe Experience Platform.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 1%

---

# Criar uma definição de segmento usando a API do serviço de segmentação

Este documento fornece um tutorial para desenvolver, testar, visualizar e salvar uma definição de segmento usando o [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Para obter informações sobre como criar definições de segmento usando a interface do usuário, consulte o [Guia do Construtor de segmentos](../ui/overview.md).

## Introdução

Este tutorial requer um entendimento prático dos vários [!DNL Adobe Experience Platform] serviços envolvidos na criação de definições de segmento. Antes de iniciar este tutorial, revise a documentação dos seguintes serviços:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): permite criar públicos-alvo usando definições de segmento ou outras fontes externas dos dados do Perfil do cliente em tempo real.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): o quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente. Para melhor usar a segmentação, verifique se seus dados são assimilados como perfis e eventos de acordo com a [práticas recomendadas para modelagem de dados](../../xdm/schema/best-practices.md).

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para o [!DNL Platform] APIs.

### Leitura de chamadas de API de amostra

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O exemplo de JSON retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos obrigatórios

Para fazer chamadas para [!DNL Platform] APIs, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos os [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes no [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Desenvolver uma definição de segmento

A primeira etapa na segmentação é definir uma definição de segmento. Uma definição de segmento é um objeto que encapsula uma consulta gravada em [!DNL Profile Query Language] (PQL). Esse objeto também é chamado de predicado PQL. Os predicados de PQL definem as regras para a definição de segmento com base nas condições relacionadas a qualquer registro ou dados de série de tempo fornecidos a [!DNL Real-Time Customer Profile]. Consulte a [Guia de PQL](../pql/overview.md) para obter mais informações sobre como gravar consultas PQL.

Você pode criar uma nova definição de segmento fazendo uma solicitação POST para o `/segment/definitions` endpoint na variável [!DNL Segmentation] API. O exemplo a seguir descreve como formatar uma solicitação de definição, incluindo quais informações são necessárias para que uma definição de segmento seja definida com sucesso.

Para obter uma explicação detalhada sobre como definir uma definição de segmento, leia o [guia do desenvolvedor de definição de segmento](../api/segment-definitions.md#create).

## Estimar e visualizar um público {#estimate-and-preview-an-audience}

À medida que desenvolve a definição do segmento, é possível usar as ferramentas de estimativa e visualização no [!DNL Real-Time Customer Profile] para exibir informações de resumo para ajudar a garantir que você esteja isolando o público-alvo esperado. As estimativas fornecem informações estatísticas sobre uma definição de segmento, como o tamanho do público projetado e o intervalo de confiança. As visualizações fornecem listas paginadas de perfis qualificados para uma definição de segmento, permitindo comparar os resultados com o que você espera.

Ao estimar e visualizar seu público-alvo, você pode testar e otimizar seus predicados de PQL até que eles produzam um resultado desejado, em que possam ser usados em uma definição de segmento atualizada.

Há duas etapas necessárias para visualizar ou obter uma estimativa da definição do segmento:

1. [Criar um trabalho de visualização](#create-a-preview-job)
2. [Exibir estimativa ou visualização](#view-an-estimate-or-preview) usar a ID do trabalho de visualização

### Como as estimativas são geradas

As amostras de dados são usadas para avaliar as definições de segmentos e estimar o número de perfis qualificados. Novos dados são carregados na memória a cada manhã (entre 12AM-2AM PT, que é 7-9AM UTC) e todas as consultas de segmentação são estimadas usando os dados de amostra desse dia. Consequentemente, quaisquer novos campos adicionados ou dados adicionais coletados serão refletidos em estimativas no dia seguinte.

O tamanho da amostra depende do número geral de entidades no armazenamento de perfis. Esses tamanhos de amostra são representados na tabela a seguir:

| Entidades na loja de perfis | Tamanho da amostra |
| ------------------------- | ----------- |
| Menos de 1 milhão | Conjunto de dados completo |
| 1 a 20 milhões | 1 milhão |
| Mais de 20 milhões | 5% do total |

As estimativas geralmente duram de 10 a 15 segundos, começando com uma estimativa aproximada e refinando à medida que mais registros são lidos.

### Criar um trabalho de visualização

Você pode criar um novo trabalho de visualização fazendo uma solicitação POST para a `/preview` terminal.

Instruções detalhadas sobre como criar um trabalho de visualização podem ser encontradas na [guia de visualizações e estimativas de endpoints](../api/previews-and-estimates.md#create-preview).

### Exibir uma estimativa ou visualização

Os processos de estimativa e pré-visualização são executados de forma assíncrona, pois consultas diferentes podem levar períodos diferentes para serem concluídas. Depois que um query for iniciado, você poderá usar chamadas de API para recuperar (GET) o estado atual da estimativa ou pré-visualização conforme avança.

Usar o [!DNL Segmentation Service] , você pode pesquisar o estado atual de um trabalho de visualização pela respectiva ID. Se o estado for &quot;RESULT_READY&quot;, você poderá exibir os resultados. Para pesquisar o estado atual de um trabalho de visualização, leia a seção sobre [recuperação de uma seção do trabalho de visualização](../api/previews-and-estimates.md#get-preview) no guia de endpoints de visualizações e estimativas. Para pesquisar o estado atual de um trabalho estimado, leia a seção sobre [recuperação de um trabalho estimado](../api/previews-and-estimates.md#get-estimate) no guia de endpoints de visualizações e estimativas.


## Próximas etapas

Depois de desenvolver, testar e salvar a definição do segmento, é possível criar um trabalho de segmento para criar um público-alvo usando o [!DNL Segmentation Service] API. Veja o tutorial sobre [avaliação e acesso aos resultados do segmento](./evaluate-a-segment.md) para obter etapas detalhadas sobre como fazer isso.
