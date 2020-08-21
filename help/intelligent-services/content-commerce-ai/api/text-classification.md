---
keywords: text classification;Text classification
solution: Experience Platform
title: Ponto final da API de classificação de texto
topic: Developer guide
description: O serviço de classificação de texto, quando recebe um fragmento de texto, pode classificá-lo em um ou mais rótulos. A classificação pode ser de rótulo único, de vários rótulos ou hierárquica.
translation-type: tm+mt
source-git-commit: 4f7b5ca50171f4948726c44dbf31025011adf35f
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 4%

---


# Classificação de texto

>[!NOTE]
>
>A API de conteúdo e comércio está em beta. A documentação está sujeita a alterações.

O serviço de classificação de texto, quando recebe um fragmento de texto, pode classificá-lo em um ou mais rótulos. A classificação pode ser de rótulo único, de vários rótulos ou hierárquica.

A classificação de texto usa um modelo baseado em [FastText](https://fasttext.cc/) que foi treinado com o uso de dados personalizados.

**Formato da API**

```http
POST /services/v1/predict
```

**Solicitação**

A solicitação a seguir classifica o texto de um fragmento com base nos parâmetros de entrada fornecidos na carga. Consulte a tabela abaixo do exemplo de carga para obter mais informações sobre os parâmetros de entrada mostrados.

>[!CAUTION]
>
>`analyzer_id` determina qual [!DNL Sensei Content Framework] é usado. Verifique se você tem o direito `analyzer_id` antes de fazer sua solicitação. Entre em contato com a equipe beta do AI do Content and Commerce para receber seu serviço `analyzer_id` para este serviço.

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
| `analyzer_id` | A ID de [!DNL Sensei] serviço em que sua solicitação é implantada. Essa ID determina qual dos [!DNL Sensei Content Frameworks] é usada. Para serviços personalizados, entre em contato com a equipe do AI de Conteúdo e Comércio para configurar uma ID personalizada. | Sim |
| `application-id` | A ID do aplicativo criado. | Sim |
| `data` | Uma matriz que contém um objeto JSON com cada objeto na matriz que representa um documento. Todos os parâmetros transmitidos como parte dessa matriz substituem os parâmetros globais especificados fora da `data` matriz. Qualquer uma das propriedades restantes descritas abaixo nesta tabela pode ser substituída de dentro `data`. | Sim |
| `language` | Idioma do texto de entrada. O valor padrão é `en`. | Não |
| `content-type` | Usado para indicar se a entrada é parte do corpo da solicitação ou um url assinado para um bucket S3. O padrão para essa propriedade é `inline`. | Não |
| `encoding` | O formato de codificação do texto de entrada. Isso pode ser `utf-8` ou `utf-16`. O padrão para essa propriedade é `utf-8`. | Não |
| `threshold` | O limite de pontuação (0 a 1) acima do qual os resultados precisam ser retornados. Use o valor `0` para retornar todos os resultados. O padrão para essa propriedade é `0`. | Não |
| `top-N` | O número de resultados a serem retornados (não pode ser um número inteiro negativo). Use o valor `0` para retornar todos os resultados. Quando usado em conjunto com `threshold`, o número de resultados retornados é o menor dos dois limites definidos. O padrão para essa propriedade é `0`. | Não |
| `custom` | Quaisquer parâmetros personalizados a serem transmitidos. Essa propriedade requer um objeto JSON válido para funcionar. | Não |
| `content-id` | A ID exclusiva do elemento de dados retornado na resposta. Se isso não for passado, uma ID gerada automaticamente será atribuída. | Não |
| `content` | O conteúdo usado pelo serviço de classificação de texto. O conteúdo pode ser texto bruto (tipo de conteúdo &quot;em linha&quot;). <br> Se o conteúdo for um arquivo em S3 (tipo de conteúdo &quot;s3-bucket&quot;), passe o url assinado. | Sim |

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
