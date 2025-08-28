---
solution: Experience Platform
title: Criar uma definição de segmento usando a API do serviço de segmentação
type: Tutorial
description: Siga este tutorial para saber como desenvolver, testar, visualizar e salvar uma definição de segmento usando a API do serviço de segmentação do Adobe Experience Platform.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: d9fc1fa6a1bbc6b13b2600a5ec9400a0b488056a
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 6%

---

# Criar uma definição de segmento usando a API do serviço de segmentação

Este documento fornece um tutorial para desenvolver, testar, visualizar e salvar uma definição de segmento usando o [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Para obter informações sobre como criar definições de segmento usando a interface do usuário, consulte o [guia do Construtor de segmentos](../ui/segment-builder.md).

## Introdução

Este tutorial requer entendimento prático dos vários serviços do [!DNL Adobe Experience Platform] envolvidos na criação de definições de segmento. Antes de iniciar este tutorial, revise a documentação dos seguintes serviços:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): permite criar públicos-alvo usando definições de segmento ou outras fontes externas dos dados do Perfil do Cliente em Tempo Real.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente. Para melhor usar a Segmentação, verifique se seus dados são assimilados como perfis e eventos de acordo com as [práticas recomendadas para modelagem de dados](../../xdm/schema/best-practices.md).

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para as APIs do [!DNL Experience Platform].

### Leitura de chamadas de API de amostra

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para APIs do [!DNL Experience Platform], primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Experience Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Experience Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm um conteúdo (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Desenvolver uma definição de segmento

A primeira etapa na segmentação é definir uma definição de segmento. Uma definição de segmento é um objeto que encapsula uma consulta gravada em [!DNL Profile Query Language] (PQL). Esse objeto também é chamado de predicado PQL. Os predicados da PQL definem as regras para a definição de segmento com base nas condições relacionadas a qualquer registro ou série de tempo que você fornecer a [!DNL Real-Time Customer Profile]. Consulte o [guia do PQL](../pql/overview.md) para obter mais informações sobre como gravar consultas do PQL.

Você pode criar uma nova definição de segmento fazendo uma solicitação POST para o ponto de extremidade `/segment/definitions` na API [!DNL Segmentation]. O exemplo a seguir descreve como formatar uma solicitação de definição, incluindo quais informações são necessárias para que uma definição de segmento seja definida com sucesso.

Para obter uma explicação detalhada sobre como definir uma definição de segmento, leia o [guia do desenvolvedor de definição de segmento](../api/segment-definitions.md#create).

## Estimar e visualizar um público-alvo {#estimate-and-preview-an-audience}

À medida que você desenvolve a definição do segmento, pode usar as ferramentas de estimativa e visualização do [!DNL Real-Time Customer Profile] para exibir informações de nível de resumo e ajudar a garantir que está isolando o público-alvo esperado. As estimativas fornecem informações estatísticas sobre uma definição de segmento, como o tamanho do público projetado e o intervalo de confiança. As visualizações fornecem listas paginadas de perfis qualificados para uma definição de segmento, permitindo comparar os resultados com o que você espera.

Ao estimar e visualizar seu público-alvo, você pode testar e otimizar seus predicados do PQL até que eles produzam um resultado desejado, em que possam ser usados em uma definição de segmento atualizada.

Há duas etapas necessárias para visualizar ou obter uma estimativa da definição do segmento:

1. [Criar um trabalho de visualização](#create-a-preview-job)
2. [Exibir estimativa ou visualização](#view-an-estimate-or-preview) usando a ID do trabalho de visualização

### Como as estimativas são geradas

Como os dados ativados para o Perfil do cliente em tempo real são assimilados na Experience Platform, eles são armazenados no armazenamento de dados do Perfil. Quando a assimilação de registros no armazenamento de Perfil aumenta ou diminui a contagem total de perfis em mais de 5%, um trabalho de amostragem é acionado para atualizar a contagem. Se a contagem de perfis não for alterada em mais de 5%, o trabalho de amostragem será executado automaticamente uma vez por semana.

O modo como a amostra é acionada depende do tipo de ingestão sendo usado:

- Para workflows de dados de transmissão, uma verificação é feita por hora para determinar se o limite de aumento ou diminuição de 3% foi atingido. Se esse limite for atingido, um trabalho de amostra será acionado automaticamente para atualizar a contagem.
- Para assimilação em lote, dentro de 15 minutos após a assimilação bem-sucedida de um lote no Armazenamento de perfis, se o limite de aumento ou diminuição de 3% for atingido, um trabalho será executado para atualizar a contagem. Usando a API de perfil, é possível visualizar o trabalho de amostra bem-sucedido mais recente, bem como listar a distribuição do perfil por conjunto de dados e por namespace de identidade.

O tamanho da amostra depende do número geral de entidades no armazenamento de perfis. Esses tamanhos de amostra são representados na tabela a seguir:

| Entidades no armazenamento de perfis | Tamanho da amostra |
| ------------------------- | ----------- |
| Menos de 1 milhão | Conjunto de dados completo |
| 1 a 20 milhões | 1 milhão |
| Mais de 20 milhões | 5% do total |

As estimativas geralmente duram de 10 a 15 segundos, começando com uma estimativa aproximada e refinando à medida que mais registros são lidos.

### Criar um trabalho de visualização

Você pode criar um novo trabalho de visualização fazendo uma solicitação POST para o ponto de extremidade `/preview`.

Instruções detalhadas sobre como criar um trabalho de visualização podem ser encontradas no [guia de visualizações e pontos de extremidade de estimativas](../api/previews-and-estimates.md#create-preview).

### Exibir uma estimativa ou visualização

Os processos de estimativa e pré-visualização são executados de forma assíncrona, pois consultas diferentes podem levar períodos diferentes para serem concluídas. Depois que um query é iniciado, você pode usar chamadas de API para recuperar (GET) o estado atual da estimativa ou pré-visualização conforme avança.

Usando a API [!DNL Segmentation Service], você pode pesquisar o estado atual de um trabalho de visualização por sua ID. Se o estado for &quot;RESULT_READY&quot;, você poderá exibir os resultados. Para pesquisar o estado atual de um trabalho de visualização, leia a seção sobre [recuperação de uma seção de trabalho de visualização](../api/previews-and-estimates.md#get-preview) no guia de visualizações e estimativas de pontos de extremidade. Para pesquisar o estado atual de um trabalho estimado, leia a seção sobre [recuperação de um trabalho estimado](../api/previews-and-estimates.md#get-estimate) no guia de visualizações e pontos de extremidade de estimativas.


## Próximas etapas

Depois de desenvolver, testar e salvar a definição do segmento, você pode criar um trabalho de segmento para criar um público-alvo usando a API [!DNL Segmentation Service]. Consulte o tutorial sobre [avaliação e acesso a resultados de segmentos](./evaluate-a-segment.md) para obter etapas detalhadas sobre como fazer isso.
