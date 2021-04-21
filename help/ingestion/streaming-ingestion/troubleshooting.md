---
keywords: Experience Platform, home, tópicos populares, transmissão, assimilação de streaming, solução de problemas, solução de problemas de assimilação de streaming, perguntas frequentes sobre assimilação de streaming, perguntas frequentes;
solution: Experience Platform
title: Guia de solução de problemas de assimilação de fluxo
topic-legacy: troubleshooting
description: Este documento fornece respostas a perguntas frequentes sobre a assimilação de streaming no Adobe Experience Platform.
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# Guia de solução de problemas de assimilação de streaming

Este documento fornece respostas a perguntas frequentes sobre a assimilação de streaming no Adobe Experience Platform. Para perguntas e solução de problemas relacionados a outros [!DNL Platform] serviços, incluindo aqueles encontrados em todas as [!DNL Platform] APIs, consulte o [Guia de solução de problemas do Experience Platform](../../landing/troubleshooting.md).

O Adobe Experience Platform [!DNL Data Ingestion] fornece APIs RESTful que podem ser usadas para assimilar dados em [!DNL Experience Platform]. Os dados assimilados são usados para atualizar perfis de clientes individuais em tempo quase real, permitindo que você forneça experiências personalizadas e relevantes em vários canais. Leia a [Visão geral da assimilação de dados](../home.md) para obter mais informações sobre o serviço e os diferentes métodos de assimilação. Para obter as etapas sobre como usar APIs de assimilação de streaming, leia a [visão geral de assimilação de streaming](../streaming-ingestion/overview.md).

## Perguntas frequentes

Veja a seguir uma lista de respostas para perguntas frequentes sobre a assimilação de streaming.

### Como sei se a carga que estou enviando está formatada corretamente?

[!DNL Data Ingestion] usam esquemas  [!DNL Experience Data Model] (XDM) para validar o formato de dados de entrada. Enviar dados que não estão em conformidade com a estrutura de um esquema XDM predefinido causará falha na assimilação. Para obter mais informações sobre o XDM e seu uso em [!DNL Experience Platform], consulte a [Visão geral do sistema XDM](../../xdm/home.md).

A assimilação de streaming suporta dois modos de validação: síncrono e assíncrono. Cada método de validação trata os dados com falha de forma diferente.

**A** validação síncrona deve ser usada durante o processo de desenvolvimento. Os registros que falharam na validação são descartados e retornam uma mensagem de erro sobre por que falharam (por exemplo: &quot;Formato de Mensagem XDM Inválido&quot;).

**A** validação assíncrona deve ser usada na produção. Todos os dados malformados que não passam pela validação são enviados para [!DNL Data Lake] como um arquivo de lote com falha, onde podem ser recuperados posteriormente para análise adicional.

Para obter mais informações sobre validação síncrona e assíncrona, consulte a [visão geral da validação de transmissão](../quality/streaming-validation.md). Para obter etapas sobre como visualizar lotes que falharam na validação, consulte o guia em [recuperar lotes com falha](../quality/retrieve-failed-batches.md).

### Posso validar uma carga de solicitação antes de enviá-la para [!DNL Platform]?

As cargas de solicitação só podem ser avaliadas depois de terem sido enviadas para [!DNL Platform]. Ao executar a validação síncrona, as cargas válidas retornam objetos JSON preenchidos, enquanto cargas inválidas retornam mensagens de erro. Durante a validação assíncrona, o serviço detecta e envia dados malformados para o [!DNL Data Lake], onde podem ser recuperados posteriormente para análise. Consulte a [visão geral da validação de transmissão](../quality/streaming-validation.md) para obter mais informações.

### O que acontece quando a validação síncrona é solicitada em uma borda que não oferece suporte a ela?

Quando a validação síncrona não é compatível com o local solicitado, uma resposta de erro 501 é retornada. Consulte a [visão geral da validação de fluxo](../quality/streaming-validation.md) para obter mais informações sobre a validação síncrona.

### Como posso garantir que os dados sejam coletados somente de fontes confiáveis?

[!DNL Experience Platform] O suporta coleta de dados segura. Quando a coleta de dados autenticada está ativada, os clientes devem enviar um JSON Web Token (JWT) e sua IMS Organization ID como cabeçalhos de solicitação. Para obter mais informações sobre como enviar dados autenticados para [!DNL Platform], consulte o guia em [coleta de dados autenticada](../tutorials/create-authenticated-streaming-connection.md).

### Qual é a latência de dados de transmissão para [!DNL Real-time Customer Profile]?

Os eventos streaming geralmente são refletidos em [!DNL Real-time Customer Profile] em menos de 60 segundos. As latências reais podem variar devido ao volume de dados, tamanho da mensagem e limitações de largura de banda.

### É possível incluir várias mensagens na mesma solicitação de API?

Você pode agrupar várias mensagens em uma única carga de solicitação e fazer o stream delas para [!DNL Platform]. Quando usado corretamente, agrupar várias mensagens em uma única solicitação é uma excelente maneira de otimizar suas operações de dados. Leia o tutorial em [enviando várias mensagens em uma solicitação](../tutorials/streaming-multiple-messages.md) para obter mais informações.

### Como faço para saber se os dados que estou enviando estão sendo recebidos?

Todos os dados enviados para [!DNL Platform] (com êxito ou não) são armazenados como arquivos em lote antes de serem mantidos em conjuntos de dados. O status de processamento dos lotes é exibido dentro do conjunto de dados para o qual foram enviados.

Você pode verificar se os dados foram assimilados com êxito verificando a atividade do conjunto de dados usando a [interface do usuário do Experience Platform](https://platform.adobe.com). Clique em **[!UICONTROL Datasets]** na navegação à esquerda para exibir uma lista de conjuntos de dados. Selecione o conjunto de dados para o qual você está fazendo streaming na lista exibida para abrir sua página **[!UICONTROL Dataset activity]**, mostrando todos os lotes enviados durante um período de tempo selecionado. Para obter mais informações sobre como usar [!DNL Experience Platform] para monitorar fluxos de dados, consulte o guia em [monitorar fluxos de dados de transmissão](../quality/monitor-data-ingestion.md).

Se os dados falharam ao assimilar e você deseja recuperá-los de [!DNL Platform], é possível recuperar os lotes com falha enviando as IDs para [!DNL Data Access API]. Consulte o guia em [recuperação de lotes com falha](../quality/retrieve-failed-batches.md) para obter mais informações.

### Por que meus dados de transmissão não estão disponíveis no Data Lake?

Há uma variedade de motivos pelos quais a assimilação em lote pode falhar ao alcançar o [!DNL Data Lake], como formatação inválida, dados ausentes ou erros de sistema. Para determinar por que o lote falhou, você deve recuperar o lote usando o [!DNL Data Ingestion Service API] e exibir seus detalhes. Para obter etapas detalhadas sobre como recuperar um lote com falha, consulte o guia em [recuperar lotes com falha](../quality/retrieve-failed-batches.md).

### Como analisar a resposta retornada para a solicitação da API?

Você pode analisar uma resposta verificando primeiro o código de resposta do servidor para determinar se sua solicitação foi aceita. Se um código de resposta bem-sucedido for retornado, você poderá revisar o objeto da matriz `responses` para determinar o status da tarefa de assimilação.

Uma solicitação de API de mensagem única bem-sucedida retorna o código de status 200. Uma solicitação de API de mensagem em lote bem-sucedida (ou parcialmente bem-sucedida) retorna o código de status 207.

O JSON a seguir é um exemplo de objeto de resposta para uma solicitação de API com duas mensagens: um foi bem-sucedido e outro falhou. As mensagens que fazem o stream com êxito retornam uma propriedade `xactionId`. Mensagens que não conseguem fazer o stream retornam uma propriedade `statusCode` e uma resposta `message` com mais informações.

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
                imsOrgId: [{IMS_ORG}] 
                Message has unknown xdm format"
        }
    ]
}
```

### Por que minhas mensagens enviadas não estão sendo recebidas por [!DNL Real-time Customer Profile]?

Se [!DNL Real-time Customer Profile] rejeitar uma mensagem, provavelmente ela se deve a informações de identidade incorretas. Isso pode ser o resultado de fornecer um valor ou namespace inválido para uma identidade.

Há dois tipos de namespaces de identidade: padrão e personalizado. Ao usar namespaces personalizados, verifique se o namespace foi registrado em [!DNL Identity Service]. Consulte a [visão geral do namespace de identidade](../../identity-service/namespaces.md) para obter mais informações sobre o uso de namespaces padrão e personalizados.

Você pode usar o [[!DNL Experience Platform UI]](https://platform.adobe.com) para ver mais informações sobre por que uma mensagem falhou na assimilação. Clique em **[!UICONTROL Monitoring]** na navegação à esquerda e exiba a guia **[!UICONTROL Streaming end-to-end]** para ver os lotes de mensagens transmitidos durante um período de tempo selecionado.
