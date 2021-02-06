---
keywords: Experience Platform;home;popular topics;streaming;streaming ingestão;solução de problemas;streaming ingestão troubleshooting;streaming ingestão troubleshooting;streaming ingestão faq;faq;
solution: Experience Platform
title: Guia de solução de problemas de ingestão de fluxo
topic: troubleshooting
description: Este documento fornece respostas para perguntas frequentes sobre a assimilação de streaming no Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 0%

---


# Guia de solução de problemas de ingestão de streaming

Este documento fornece respostas para perguntas frequentes sobre a assimilação de streaming no Adobe Experience Platform. Para perguntas e solução de problemas relacionados a outros serviços [!DNL Platform], incluindo aqueles encontrados em todas as [!DNL Platform] APIs, consulte o [guia de solução de problemas do Experience Platform](../../landing/troubleshooting.md).

O Adobe Experience Platform [!DNL Data Ingestion] fornece APIs RESTful que você pode usar para assimilar dados em [!DNL Experience Platform]. Os dados ingeridos são usados para atualizar perfis individuais do cliente em tempo quase real, permitindo que você forneça experiências personalizadas e relevantes em vários canais. Leia a [visão geral da ingestão de dados](../home.md) para obter mais informações sobre o serviço e os diferentes métodos de ingestão. Para obter etapas sobre como usar APIs de ingestão de streaming, leia a [visão geral de ingestão de streaming](../streaming-ingestion/overview.md).

## Perguntas frequentes

Veja a seguir uma lista de respostas para perguntas frequentes sobre a ingestão de streaming.

### Como saber se a carga que estou enviando está formatada corretamente?

[!DNL Data Ingestion] aproveita os schemas  [!DNL Experience Data Model] (XDM) para validar o formato dos dados recebidos. Enviar dados que não estejam em conformidade com a estrutura de um schema XDM predefinido causará a falha da ingestão. Para obter mais informações sobre o XDM e seu uso em [!DNL Experience Platform], consulte [Visão geral do Sistema XDM](../../xdm/home.md).

A assimilação de fluxo suporta dois modos de validação: síncrono e assíncrono. Cada método de validação lida com dados com falha de forma diferente.

**A** validação síncrona deve ser usada durante o processo de desenvolvimento. Os registros que falharem na validação são descartados e retornam uma mensagem de erro sobre o motivo da falha (por exemplo: &quot;Formato de mensagem XDM inválido&quot;).

**A** validação assíncrona deve ser usada na produção. Todos os dados malformados que não passam na validação são enviados para [!DNL Data Lake] como um arquivo de lote com falha, onde podem ser recuperados posteriormente para obter mais análises.

Para obter mais informações sobre a validação síncrona e assíncrona, consulte a [visão geral da validação de streaming](../quality/streaming-validation.md). Para obter etapas sobre como visualização lotes com falha na validação, consulte o guia em [recuperação de lotes com falha](../quality/retrieve-failed-batches.md).

### É possível validar uma carga de solicitação antes de enviá-la para [!DNL Platform]?

As cargas de solicitação só podem ser avaliadas depois de terem sido enviadas para [!DNL Platform]. Ao executar a validação síncrona, as cargas válidas retornam objetos JSON preenchidos enquanto cargas inválidas retornam mensagens de erro. Durante a validação assíncrona, o serviço detecta e envia todos os dados malformados para [!DNL Data Lake], onde podem ser recuperados posteriormente para análise. Consulte a [visão geral de validação de fluxo](../quality/streaming-validation.md) para obter mais informações.

### O que acontece quando a validação síncrona é solicitada em uma borda que não oferece suporte a ela?

Quando a validação síncrona não é compatível com o local solicitado, uma resposta de erro 501 é retornada. Consulte a [visão geral da validação de fluxo](../quality/streaming-validation.md) para obter mais informações sobre a validação síncrona.

### Como faço para garantir que os dados sejam coletados somente de fontes confiáveis?

[!DNL Experience Platform] oferece suporte à coleta de dados protegida. Quando a coleta de dados autenticada está ativada, os clientes devem enviar um JSON Web Token (JWT) e sua ID de organização IMS como cabeçalhos de solicitação. Para obter mais informações sobre como enviar dados autenticados para [!DNL Platform], consulte o guia em [coleta de dados autenticada](../tutorials/create-authenticated-streaming-connection.md).

### Qual é a latência para transmissão de dados para [!DNL Real-time Customer Profile]?

Eventos com transmissão contínua geralmente são refletidos em [!DNL Real-time Customer Profile] em menos de 60 segundos. As latências reais podem variar devido a limitações de volume de dados, tamanho da mensagem e largura de banda.

### É possível incluir várias mensagens na mesma solicitação de API?

Você pode agrupar várias mensagens em uma única carga de solicitação e fazer o stream delas para [!DNL Platform]. Quando usado corretamente, agrupar várias mensagens em uma única solicitação é uma excelente maneira de otimizar suas operações de dados. Leia o tutorial em [enviando várias mensagens em uma solicitação](../tutorials/streaming-multiple-messages.md) para obter mais informações.

### Como saber se os dados que estou enviando estão sendo recebidos?

Todos os dados enviados para [!DNL Platform] (com êxito ou não) são armazenados como arquivos em lote antes de serem persistentes em conjuntos de dados. O status de processamento dos lotes é exibido no conjunto de dados para o qual foram enviados.

Você pode verificar se os dados foram ingeridos com êxito verificando a atividade do conjunto de dados usando a [interface do usuário do Experience Platform](https://platform.adobe.com). Clique em **[!UICONTROL Conjuntos de dados]** na navegação à esquerda para exibir uma lista de conjuntos de dados. Selecione o conjunto de dados para o qual você está fazendo streaming na lista exibida para abrir sua página **[!UICONTROL atividade do conjunto de dados]**, mostrando todos os lotes enviados durante um período de tempo selecionado. Para obter mais informações sobre como usar [!DNL Experience Platform] para monitorar fluxos de dados, consulte o guia em [monitorar fluxos de dados de transmissão](../quality/monitor-data-ingestion.md).

Se os seus dados não foram assimilados e você deseja recuperá-los de [!DNL Platform], é possível recuperar os lotes com falha enviando suas IDs para [!DNL Data Access API]. Consulte o guia em [recuperação de lotes com falha](../quality/retrieve-failed-batches.md) para obter mais informações.

### Por que meus dados de transmissão não estão disponíveis no Data Lake?

Há vários motivos pelos quais a ingestão em lote pode falhar ao alcançar [!DNL Data Lake], como formatação inválida, dados ausentes ou erros do sistema. Para determinar por que o lote falhou, você deve recuperar o lote usando [!DNL Data Ingestion Service API] e visualização seus detalhes. Para obter etapas detalhadas sobre como recuperar um lote com falha, consulte o guia em [recuperação de lotes com falha](../quality/retrieve-failed-batches.md).

### Como analiso a resposta retornada para a solicitação de API?

Você pode analisar uma resposta primeiro verificando o código de resposta do servidor para determinar se sua solicitação foi aceita. Se um código de resposta bem-sucedido for retornado, você poderá revisar o objeto de matriz `responses` para determinar o status da tarefa de ingestão.

Uma solicitação de API de mensagem única bem-sucedida retorna o código de status 200. Uma solicitação de API de mensagem em lote bem-sucedida (ou parcialmente bem-sucedida) retorna o código de status 207.

O JSON a seguir é um exemplo de objeto de resposta para uma solicitação de API com duas mensagens: uma foi bem sucedida e outra falhou. As mensagens que fazem o stream com êxito retornam uma propriedade `xactionId`. As mensagens que falham ao transmitir retornam uma propriedade `statusCode` e uma resposta `message` com mais informações.

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

Existem dois tipos de namespaces de identidade: padrão e personalizado. Ao usar namespaces personalizadas, verifique se a namespace foi registrada em [!DNL Identity Service]. Consulte [visão geral da namespace de identidade](../../identity-service/namespaces.md) para obter mais informações sobre o uso de namespaces padrão e personalizadas.

Você pode usar [[!DNL Experience Platform UI]](https://platform.adobe.com) para ver mais informações sobre por que uma mensagem falhou na ingestão. Clique em **[!UICONTROL Monitoramento]** no menu de navegação esquerdo, em seguida, visualização a guia **[!UICONTROL Transmissão completa]** para ver os lotes de mensagens transmitidos durante um período selecionado.
