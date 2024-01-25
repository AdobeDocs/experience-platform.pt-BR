---
keywords: Experience Platform;página inicial;tópicos populares;streaming;assimilação de streaming;solução de problemas;solução de problemas de assimilação de streaming;perguntas frequentes de assimilação de streaming;faq;
solution: Experience Platform
title: Guia de solução de problemas de assimilação de streaming
description: Este documento fornece respostas a perguntas frequentes sobre a assimilação de streaming no Adobe Experience Platform.
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 0%

---

# Guia de solução de problemas de assimilação de streaming

Este documento fornece respostas a perguntas frequentes sobre a assimilação de streaming no Adobe Experience Platform. Para perguntas e solução de problemas relacionados a outros [!DNL Platform] serviços, incluindo os encontrados em todas as [!DNL Platform] APIs, consulte o [guia de solução de problemas do Experience Platform](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] O fornece APIs RESTful que você pode usar para assimilar dados no [!DNL Experience Platform]. Os dados assimilados são usados para atualizar perfis de clientes individuais em tempo quase real, permitindo que você forneça experiências personalizadas e relevantes em vários canais. Leia as [Visão geral da assimilação de dados](../home.md) para obter mais informações sobre o serviço e os diferentes métodos de assimilação. Para obter etapas sobre como usar APIs de assimilação de streaming, leia o [visão geral da assimilação por transmissão](../streaming-ingestion/overview.md).

## Perguntas frequentes

Veja a seguir uma lista de respostas para perguntas frequentes sobre a assimilação por transmissão.

### Como saber se a carga que estou enviando está formatada corretamente?

[!DNL Data Ingestion] aproveita [!DNL Experience Data Model] Esquemas de (XDM) para validar o formato dos dados recebidos. O envio de dados que não estão em conformidade com a estrutura de um esquema XDM predefinido causará falha na assimilação. Para obter mais informações sobre o XDM e seu uso no [!DNL Experience Platform], consulte o [Visão geral do sistema XDM](../../xdm/home.md).

A assimilação de streaming suporta dois modos de validação: síncrono e assíncrono. Cada método de validação trata os dados com falha de forma diferente.

**Validação síncrona** O deve ser usado durante o processo de desenvolvimento. Os registros que falham na validação são descartados e retornam uma mensagem de erro sobre o motivo da falha (por exemplo: &quot;Formato de mensagem XDM inválido&quot;).

**Validação assíncrona** deve ser usado na produção. Quaisquer dados malformados que não passarem na validação serão enviados para o [!DNL Data Lake] como um arquivo de lote com falha, onde pode ser recuperado posteriormente para análise adicional.

Para obter mais informações sobre validação síncrona e assíncrona, consulte a [visão geral da validação de transmissão](../quality/streaming-validation.md). Para obter etapas sobre como visualizar lotes que falharam na validação, consulte o manual em [recuperação de lotes com falha](../quality/retrieve-failed-batches.md).

### Posso validar uma carga de solicitação antes de enviá-la para o [!DNL Platform]?

As cargas de solicitação só podem ser avaliadas depois de terem sido enviadas para [!DNL Platform]. Ao executar a validação síncrona, cargas válidas retornam objetos JSON preenchidos, enquanto cargas inválidas retornam mensagens de erro. Durante a validação assíncrona, o serviço detecta e envia dados malformados para o [!DNL Data Lake] onde pode ser recuperado posteriormente para análise. Consulte a [visão geral da validação de transmissão](../quality/streaming-validation.md) para obter mais informações.

### O que acontece quando a validação síncrona é solicitada em uma borda que não oferece suporte a ela?

Quando a validação síncrona não é suportada para o local solicitado, uma resposta de erro 501 é retornada. Consulte a [visão geral da validação de transmissão](../quality/streaming-validation.md) para obter mais informações sobre validação síncrona.

### Como posso garantir que os dados sejam coletados somente de fontes confiáveis?

[!DNL Experience Platform] O oferece suporte à coleta de dados segura. Quando a coleta de dados autenticada estiver ativada, os clientes deverão enviar um JSON Web Token (JWT) e sua ID da organização como cabeçalhos de solicitação. Para obter mais informações sobre como enviar dados autenticados para o [!DNL Platform], consulte o guia em [coleção de dados autenticada](../tutorials/create-authenticated-streaming-connection.md).

### Qual é a latência para transmissão de dados para [!DNL Real-Time Customer Profile]?

Os eventos transmitidos geralmente são refletidos na [!DNL Real-Time Customer Profile] em menos de 60 segundos. As latências reais podem variar devido a limitações de volume de dados, tamanho da mensagem e largura de banda.

### É possível incluir várias mensagens na mesma solicitação de API?

Você pode agrupar várias mensagens em uma única carga de solicitação e transmiti-las para [!DNL Platform]. Quando usado corretamente, agrupar várias mensagens em uma única solicitação é uma excelente maneira de otimizar as operações de dados. Leia o tutorial sobre [envio de várias mensagens em uma solicitação](../tutorials/streaming-multiple-messages.md) para obter mais informações.

### Como faço para saber se os dados que estou enviando estão sendo recebidos?

Todos os dados enviados para [!DNL Platform] (com sucesso ou não) é armazenado como arquivos em lote antes de ser mantido em conjuntos de dados do. O status de processamento dos lotes é exibido dentro do conjunto de dados para o qual foram enviados.

Você pode verificar se os dados foram assimilados com êxito verificando a atividade do conjunto de dados usando o [Interface do usuário do Experience Platform](https://platform.adobe.com). Clique em **[!UICONTROL Conjuntos de dados]** no painel de navegação esquerdo para exibir uma lista de conjuntos de dados. Selecione o conjunto de dados para o qual você está transmitindo na lista exibida para abrir seu **[!UICONTROL Atividade do conjunto de dados]** mostrando todos os lotes enviados durante um período selecionado. Para obter mais informações sobre o uso de [!DNL Experience Platform] para monitorar fluxos de dados, consulte o guia sobre [monitoramento de fluxos de dados de transmissão](../quality/monitor-data-ingestion.md).

Se os dados não forem assimilados e você quiser recuperá-los do [!DNL Platform], você poderá recuperar os lotes com falha enviando suas IDs para a [!DNL Data Access API]. Consulte o guia sobre [recuperação de lotes com falha](../quality/retrieve-failed-batches.md) para obter mais informações.

### Por que meus dados de transmissão não estão disponíveis no Data Lake?

Há várias razões pelas quais a assimilação em lote pode não atingir o [!DNL Data Lake], como formatação inválida, dados ausentes ou erros de sistema. Para determinar por que o lote falhou, você deve recuperar o lote usando a [!DNL Data Ingestion Service API] e visualize seus detalhes. Para obter etapas detalhadas sobre como recuperar um lote com falha, consulte o manual no [recuperação de lotes com falha](../quality/retrieve-failed-batches.md).

### Como faço para analisar a resposta retornada para a solicitação da API?

Você pode analisar uma resposta verificando primeiro o código de resposta do servidor para determinar se sua solicitação foi aceita. Se um código de resposta bem-sucedido for retornado, você poderá revisar a variável `responses` array para determinar o status da tarefa de assimilação.

Uma solicitação de API de mensagem única bem-sucedida retorna o código de status 200. Uma solicitação de API de mensagem em lote bem-sucedida (ou parcialmente bem-sucedida) retorna o código de status 207.

O JSON a seguir é um objeto de resposta de exemplo para uma solicitação de API com duas mensagens: uma bem-sucedida e outra com falha. As mensagens cujo fluxo foi bem-sucedido retornam um `xactionId` propriedade. As mensagens que não são transmitidas retornam um `statusCode` propriedade e uma resposta `message` com mais informações.

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a
                79b25e9421ea127f5] 
                imsOrgId: [{ORG_ID}] 
                Message has unknown xdm format"
        }
    ]
}
```

### Por que minhas mensagens enviadas não estão sendo recebidas por [!DNL Real-Time Customer Profile]?

Se [!DNL Real-Time Customer Profile] rejeitar uma mensagem, provavelmente devido a informações de identidade incorretas. Isso pode ser o resultado de fornecer um valor ou namespace inválido para uma identidade.

Há dois tipos de namespaces de identidade: padrão e personalizado. Ao usar namespaces personalizados, verifique se o namespace foi registrado em [!DNL Identity Service]. Consulte a [visão geral do namespace de identidade](../../identity-service/features/namespaces.md) para obter mais informações sobre o uso de namespaces padrão e personalizados.

Você pode usar o [[!DNL Experience Platform UI]](https://platform.adobe.com) para ver mais informações sobre por que uma mensagem falhou na assimilação. Clique em **[!UICONTROL Monitoramento]** no painel de navegação esquerdo, exiba a **[!UICONTROL Transmissão de ponta a ponta]** para ver os lotes de mensagens transmitidos durante um período selecionado.
