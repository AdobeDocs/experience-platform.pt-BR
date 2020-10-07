---
keywords: OCR;text presence;optical character recognition
solution: Experience Platform
title: Reconhecimento ótico de caracteres
topic: Developer guide
description: O serviço de Presença de texto / Reconhecimento ótico de caracteres (OCR), quando recebe uma imagem, pode indicar se o texto está presente na imagem. Se houver texto, o OCR poderá retornar o texto
translation-type: tm+mt
source-git-commit: 4d12caf949aeb6619cd27b55855014a61d4e54bb
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 3%

---


# Presença de texto e reconhecimento óptico de caracteres

>[!NOTE]
>
>A API de conteúdo e comércio está em beta. A documentação está sujeita a alterações.

O serviço de Presença de texto / Reconhecimento ótico de caracteres (OCR), quando recebe uma imagem, pode indicar se o texto está presente na imagem. Se houver texto, o OCR poderá retornar o texto.

A imagem a seguir foi usada na solicitação de exemplo mostrada neste documento:

![imagem de teste](../images/shef.jpeg)

**Formato da API**

```http
POST /services/v1/predict
```

**Solicitação**

A solicitação a seguir verifica se o texto está presente com base na imagem de entrada fornecida na carga. Consulte a tabela abaixo do exemplo de carga para obter mais informações sobre os parâmetros de entrada mostrados.

>[!CAUTION]
>
>`analyzer_id` determina qual [!DNL Sensei Content Framework] é usado. Verifique se você tem o direito `analyzer_id` antes de fazer sua solicitação. Entre em contato com a equipe beta do AI do Content and Commerce para receber seu serviço `analyzer_id` para este serviço.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestImage.jpg \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:image-text-extractor-ocr:Service-b0675160421e404ca3c7ca60f46a5b29",
    "parameters": {
      "application-id": "1234",
      "content-type": "inline",
      "encoding": "jpeg",
      "threshold": "0",
      "top-N": "0",
      "custom": {},
      "data": [{
        "content-id": "0987",
        "content": "inline-image",
        "content-type": "inline",
        "encoding": "jpeg",
        "threshold": "0",
        "top-N": "0",
        "historic-metadata": [],
        "custom": {}
        }]
      }
    }]
  }'
```

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| `analyzer_id` | A ID de [!DNL Sensei] serviço em que sua solicitação é implantada. Essa ID determina qual dos [!DNL Sensei Content Frameworks] é usada. Para serviços personalizados, entre em contato com a equipe do AI de Conteúdo e Comércio para configurar uma ID personalizada. | Sim |
| `application-id` | A ID do aplicativo criado. | Sim |
| `data` | Uma matriz que contém um objeto JSON com cada objeto na matriz que representa uma imagem transmitida. Todos os parâmetros transmitidos como parte dessa matriz substituem os parâmetros globais especificados fora da `data` matriz. Qualquer uma das propriedades restantes descritas abaixo nesta tabela pode ser substituída de dentro `data`. | Sim |
| `language` | Idioma do texto de entrada. O valor padrão é `en`. | Não |
| `content-type` | Usado para indicar se a entrada é parte do corpo da solicitação ou um url assinado para um bucket S3. O padrão para essa propriedade é `inline`. | Não |
| `encoding` | O formato de arquivo da imagem de entrada. Atualmente, somente imagens JPEG e PNG podem ser processadas. O padrão para essa propriedade é `jpeg`. | Não |
| `threshold` | O limite de pontuação (0 a 1) acima do qual os resultados precisam ser retornados. Use o valor `0` para retornar todos os resultados. O padrão para essa propriedade é `0`. | Não |
| `top-N` | O número de resultados a serem retornados (não pode ser um número inteiro negativo). Use o valor `0` para retornar todos os resultados. Quando usado em conjunto com `threshold`, o número de resultados retornados é o menor dos dois limites definidos. O padrão para essa propriedade é `0`. | Não |
| `custom` | Quaisquer parâmetros personalizados a serem transmitidos. Essa propriedade requer um objeto JSON válido para funcionar. | Não |
| `content-id` | A ID exclusiva do elemento de dados retornado na resposta. Se isso não for passado, uma ID gerada automaticamente será atribuída. | Não |
| `content` | O conteúdo pode ser uma imagem bruta (tipo de conteúdo &quot;inline&quot;). <br> Se o conteúdo for um arquivo no S3 (&#39;s3-bucket&#39; content-type), passe o URL assinado. | Sim |

**Resposta**

Uma resposta bem-sucedida retorna o texto que foi detectado na `feature_value` matriz. O texto é lido e retornado de cima para baixo da esquerda para a direita. Isso significa que se &quot;Eu amo Adobe&quot; foi detectado, sua carga retorna &quot;Eu&quot;, &quot;Amor&quot; e &quot;Adobe&quot; em objetos separados. No objeto, você recebe uma `feature_name` que contém a palavra e uma `feature_value` que contém uma métrica de confiança para esse texto.

```json
{
  "status": 200,
  "content_id": "TestImage.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:image-text-extractor-ocr:Service-b0675160421e404ca3c7ca60f46a5b29",
      "content_id": "TestImage.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "yes",
                "feature_name": "has_text"
              },
              {
                "feature_value": "0.977",
                "feature_name": "CHEF"
              },
              {
                "feature_value": "success",
                "feature_name": "text_processing_status"
              }
            ],
            "feature_name": "ocr"
          }
        ]
      }
    }
  ],
  "error": []
}
```
