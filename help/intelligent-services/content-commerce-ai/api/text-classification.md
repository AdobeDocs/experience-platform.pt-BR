---
keywords: classificação de texto;Classificação de texto
solution: Experience Platform
title: Classificação de texto na API da API do Content and Commerce AI
topic-legacy: Developer guide
description: O serviço de classificação de texto, ao receber um fragmento de texto, pode classificá-lo em um ou mais rótulos. A classificação pode ser de rótulo único, multirótulo ou hierárquico.
exl-id: f240519a-0d83-4309-91e4-4e48be7955a1
source-git-commit: eae43834d1cd5931dd752b95023da7ac77668e56
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 4%

---

# Classificação de texto

>[!NOTE]
>
>A API do conteúdo e do comércio está em beta. A documentação está sujeita a alterações.

O serviço de classificação de texto, ao receber um fragmento de texto, pode classificá-lo em um ou mais rótulos. A classificação pode ser de rótulo único, multirótulo ou hierárquico.

**Formato da API**

```http
POST /services/v1/predict
```

**Solicitação**

A solicitação a seguir classifica o texto de um fragmento com base nos parâmetros de entrada fornecidos no payload. Consulte a tabela abaixo do exemplo de carga para obter mais informações sobre os parâmetros de entrada mostrados.

>[!CAUTION]
>
>`analyzer_id` determina qual [!DNL Sensei Content Framework] é usada. Verifique se você tem a `analyzer_id` antes de fazer sua solicitação. Entre em contato com a equipe beta do Content and Commerce AI para receber seu `analyzer_id` para este serviço.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file="{
    \"application-id\": \"1234\", 
    \"language\": \"en\", 
    \"content-type\": \"inline\", 
    \"encoding\": \"utf-8\", 
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"Server and Workstation Processors, Microcode Update is a self-extracting executable file containing the latest beta microcode updates (System Configuration Data) and software license agreement.\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-text-classifier:Service-38a4cc7b286449e6bc1977f59df01b47",
         "parameters": {}
    }]
}'
```

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| `analyzer_id` | O [!DNL Sensei] ID de serviço em que sua solicitação é implantada. Essa ID determina qual das [!DNL Sensei Content Frameworks] são usadas. Para serviços personalizados, entre em contato com a equipe de API de Conteúdo e Comércio para configurar uma ID personalizada. | Sim |
| `application-id` | A ID do aplicativo criado. | Sim |
| `data` | Uma matriz que contém um objeto JSON com cada objeto na matriz que representa um documento. Quaisquer parâmetros transmitidos como parte dessa matriz substituem os parâmetros globais especificados fora da `data` matriz. Qualquer uma das propriedades restantes descritas abaixo nesta tabela pode ser substituída por dentro de `data`. | Sim |
| `language` | Idioma do texto de entrada. O valor padrão é `en`. | Não |
| `content-type` | Usado para indicar se a entrada é parte do corpo da solicitação ou um url assinado para um bucket S3. O padrão para essa propriedade é `inline`. | Não |
| `encoding` | O formato de codificação do texto de entrada. Pode ser `utf-8` ou `utf-16`. O padrão para essa propriedade é `utf-8`. | Não |
| `threshold` | O limite de pontuação (0 a 1) acima do qual os resultados precisam ser retornados. Use o valor `0` para retornar todos os resultados. O padrão para essa propriedade é `0`. | Não |
| `top-N` | O número de resultados a serem retornados (não pode ser um número inteiro negativo). Use o valor `0` para retornar todos os resultados. Quando usado em conjunto com `threshold`, o número de resultados devolvidos é o menor de qualquer um dos limites definidos. O padrão para essa propriedade é `0`. | Não |
| `custom` | Quaisquer parâmetros personalizados a serem transmitidos. Essa propriedade requer um objeto JSON válido para funcionar. | Não |
| `content-id` | A ID exclusiva para o elemento de dados retornado na resposta. Se isso não for passado, uma ID gerada automaticamente será atribuída. | Não |
| `content` | O conteúdo usado pelo serviço de classificação de texto. O conteúdo pode ser texto bruto (tipo de conteúdo &quot;em linha&quot;). <br> Se o conteúdo for um arquivo no tipo de conteúdo S3 (s3-bucket&#39;), passe o url assinado. | Sim |

**Resposta**

Uma resposta bem-sucedida retorna o texto classificado em uma matriz de resposta.

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-text-classifier:Service-38a4cc7b286449e6bc1977f59df01b47",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_name": "abc123",
            "feature_value": [
              {
                "feature_value": [
                  {
                    "feature_value": 0.6899315714836121,
                    "feature_name": "Embedded & IoT"
                  }
                ],
                "feature_name": "labels"
              },
              {
                "feature_name": "status",
                "feature_value": "success"
              }
            ]
          }
        ]
      }
    }
  ],
  "error": []
}
```
