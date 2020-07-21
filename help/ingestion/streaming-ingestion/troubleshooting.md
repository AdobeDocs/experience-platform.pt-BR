---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Solução de problemas de ingestão de streaming
topic: troubleshooting
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 0%

---


# Guia de solução de problemas de ingestão de streaming

Este documento fornece respostas para perguntas frequentes sobre a assimilação de streaming no Adobe Experience Platform. Para questões e solução de problemas relacionados a outros [!DNL Platform] serviços, incluindo aqueles encontrados em todas as [!DNL Platform] APIs, consulte o guia [de solução de problemas do](../../landing/troubleshooting.md)Experience Platform.

O Adobe Experience Platform [!DNL Data Ingestion] fornece APIs RESTful que podem ser usadas para assimilar dados [!DNL Experience Platform]. Os dados ingeridos são usados para atualizar perfis individuais do cliente em tempo quase real, permitindo que você forneça experiências personalizadas e relevantes em vários canais. Leia a visão geral [da Ingestão de](../home.md) dados para obter mais informações sobre o serviço e os diferentes métodos de ingestão. Para obter etapas sobre como usar APIs de ingestão de streaming, leia a visão geral [de ingestão de](../streaming-ingestion/overview.md)streaming.

## Perguntas frequentes

Veja a seguir uma lista de respostas para perguntas frequentes sobre a ingestão de streaming.

### Como saber se a carga que estou enviando está formatada corretamente?

[!DNL Data Ingestion] aproveita os schemas [!DNL Experience Data Model] (XDM) para validar o formato dos dados recebidos. Enviar dados que não estejam em conformidade com a estrutura de um schema XDM predefinido causará a falha da ingestão. Para obter mais informações sobre o XDM e seu uso no [!DNL Experience Platform], consulte a visão geral [do Sistema](../../xdm/home.md)XDM.

A assimilação de fluxo suporta dois modos de validação: síncrono e assíncrono. Cada método de validação lida com dados com falha de forma diferente.

**A validação** síncrona deve ser usada durante o processo de desenvolvimento. Os registros que falharem na validação são descartados e retornam uma mensagem de erro sobre o motivo da falha (por exemplo: &quot;Formato de mensagem XDM inválido&quot;).

**A validação** assíncrona deve ser usada na produção. Quaisquer dados malformados que não passem na validação são enviados para o arquivo de lote [!DNL Data Lake] com falha, onde podem ser recuperados posteriormente para obter mais análises.

Para obter mais informações sobre a validação síncrona e assíncrona, consulte a visão geral [da validação do](../quality/streaming-validation.md)streaming. Para obter etapas sobre como visualização lotes com falha na validação, consulte o guia sobre como [recuperar lotes](../quality/retrieve-failed-batches.md)com falha.

### É possível validar uma carga de solicitação antes de enviá-la para [!DNL Platform]?

As cargas de solicitação só podem ser avaliadas depois de enviadas para [!DNL Platform]. Ao executar a validação síncrona, as cargas válidas retornam objetos JSON preenchidos enquanto cargas inválidas retornam mensagens de erro. Durante a validação assíncrona, o serviço detecta e envia todos os dados malformados para o local em [!DNL Data Lake] que podem ser recuperados posteriormente para análise. Consulte a visão geral [da validação de](../quality/streaming-validation.md) streaming para obter mais informações.

### O que acontece quando a validação síncrona é solicitada em uma borda que não oferece suporte a ela?

Quando a validação síncrona não é compatível com o local solicitado, uma resposta de erro 501 é retornada. Consulte a visão geral [da validação de](../quality/streaming-validation.md) streaming para obter mais informações sobre a validação síncrona.

### Como faço para garantir que os dados sejam coletados somente de fontes confiáveis?

[!DNL Experience Platform] oferece suporte à coleta de dados protegida. Quando a coleta de dados autenticada está ativada, os clientes devem enviar um JSON Web Token (JWT) e sua ID de organização IMS como cabeçalhos de solicitação. Para obter mais informações sobre como enviar dados autenticados para [!DNL Platform], consulte o guia sobre a coleta [de dados](../tutorials/create-authenticated-streaming-connection.md)autenticada.

### Para qual é a latência do streaming de dados [!DNL Real-time Customer Profile]?

eventos com transmissão contínua geralmente são refletidos em menos [!DNL Real-time Customer Profile] de 60 segundos. As latências reais podem variar devido a limitações de volume de dados, tamanho da mensagem e largura de banda.

### É possível incluir várias mensagens na mesma solicitação de API?

É possível agrupar várias mensagens em uma única carga de solicitação e fazer o stream delas para [!DNL Platform]. Quando usado corretamente, agrupar várias mensagens em uma única solicitação é uma excelente maneira de otimizar suas operações de dados. Leia o tutorial sobre como [enviar várias mensagens em uma solicitação](../tutorials/streaming-multiple-messages.md) para obter mais informações.

### Como saber se os dados que estou enviando estão sendo recebidos?

Todos os dados enviados para [!DNL Platform] (com êxito ou de outra forma) são armazenados como arquivos em lote antes de serem persistentes em conjuntos de dados. O status de processamento dos lotes é exibido no conjunto de dados para o qual foram enviados.

Você pode verificar se os dados foram ingeridos com êxito verificando a atividade do conjunto de dados usando a interface [do usuário do](https://platform.adobe.com)Experience Platform. Clique em **[!UICONTROL Conjuntos]** de dados na navegação à esquerda para exibir uma lista de conjuntos de dados. Selecione o conjunto de dados para o qual você está fazendo streaming na lista exibida para abrir a página de atividade *[!UICONTROL do Conjunto de]* Dados, mostrando todos os lotes enviados durante um período selecionado. Para obter mais informações sobre como usar [!DNL Experience Platform] para monitorar fluxos de dados, consulte o guia sobre como [monitorar fluxos](../quality/monitor-data-flows.md)de dados de transmissão.

Se os seus dados não foram assimilados e você deseja recuperá-los, [!DNL Platform]é possível recuperar os lotes com falha enviando suas IDs para o [!DNL Data Access API]. Consulte o guia sobre como [recuperar lotes](../quality/retrieve-failed-batches.md) com falha para obter mais informações.

### Por que meus dados de transmissão não estão disponíveis no Data Lake?

Há várias razões pelas quais a ingestão em lote pode falhar ao atingir o [!DNL Data Lake], como formatação inválida, dados ausentes ou erros do sistema. Para determinar por que o lote falhou, você deve recuperar o lote usando o [!DNL Data Ingestion Service API] e visualização seus detalhes. Para obter etapas detalhadas sobre como recuperar um lote com falha, consulte o guia sobre como [recuperar lotes](../quality/retrieve-failed-batches.md)com falha.

### Como analiso a resposta retornada para a solicitação de API?

Você pode analisar uma resposta primeiro verificando o código de resposta do servidor para determinar se sua solicitação foi aceita. Se um código de resposta bem-sucedido for retornado, você poderá revisar o objeto da `responses` matriz para determinar o status da tarefa de ingestão.

Uma solicitação de API de mensagem única bem-sucedida retorna o código de status 200. Uma solicitação de API de mensagem em lote bem-sucedida (ou parcialmente bem-sucedida) retorna o código de status 207.

O JSON a seguir é um exemplo de objeto de resposta para uma solicitação de API com duas mensagens: uma foi bem sucedida e outra falhou. As mensagens que fazem o stream com êxito retornam uma `xactionId` propriedade. As mensagens que falham no fluxo retornam uma `statusCode` propriedade e uma resposta `message` com mais informações.

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

Existem dois tipos de namespaces de identidade: padrão e personalizado. Ao usar namespaces personalizadas, verifique se a namespace foi registrada dentro [!DNL Identity Service]. Consulte a visão geral [da namespace de](../../identity-service/namespaces.md) identidade para obter mais informações sobre o uso de namespaces padrão e personalizadas.

Você pode usar o para obter mais informações sobre [!DNL Experience Platform UI](https://platform.adobe.com) o motivo pelo qual uma mensagem falhou na ingestão. Clique em **[!UICONTROL Monitoramento]** na navegação à esquerda e, em seguida, visualização a guia _[!UICONTROL Streaming end-to-end]_para ver os lotes de mensagens transmitidos durante um período selecionado.