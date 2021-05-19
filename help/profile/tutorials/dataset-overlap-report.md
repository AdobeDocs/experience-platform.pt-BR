---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API, relatórios, relatório de sobreposição de conjunto de dados, dados do perfil
title: Gerar o relatório de sobreposição de conjunto de dados
type: Tutorial
description: Este tutorial descreve as etapas necessárias para gerar o relatório de sobreposição de conjunto de dados usando a API do perfil do cliente em tempo real.
source-git-commit: f30f87527f5e903c851a140e7cbaad1964a48803
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 1%

---


# Gerar o relatório de sobreposição de conjunto de dados

O relatório de sobreposição de conjunto de dados fornece visibilidade sobre a composição do armazenamento [!DNL Profile] de sua organização, expondo os conjuntos de dados que mais contribuem para seu público-alvo endereçável (perfis).

Além de fornecer insights sobre seus dados, este relatório pode ajudar você a tomar ações para otimizar o uso da licença, como definir um limite para a duração de determinados dados.

Este tutorial descreve as etapas necessárias para gerar o relatório de sobreposição de conjunto de dados usando a API [!DNL Real-time Customer Profile] e interpretar os resultados para sua organização.

## Introdução

Para usar APIs do Adobe Experience Platform, primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para coletar os valores necessários para os cabeçalhos necessários. Para saber mais sobre as APIs do Experience Platform, consulte a documentação de [introdução às APIs da plataforma](../../landing/api-guide.md).

Os cabeçalhos necessários para todas as chamadas de API neste tutorial são:

* `Authorization: Bearer {ACCESS_TOKEN}`: O  `Authorization` cabeçalho requer um token de acesso anexado à palavra  `Bearer`. Um novo valor de token de acesso deve ser gerado a cada 24 horas.
* `x-api-key: {API_KEY}`: O também  `API Key` é conhecido como um  `Client ID` e é um valor que só precisa ser gerado uma vez.
* `x-gw-ims-org-id: {IMS_ORG}`: O também  `IMS Org` é conhecido como um  `Organization ID` e só precisa ser gerado uma vez.

Depois de concluir o tutorial de autenticação e coletar os valores para os cabeçalhos necessários, você está pronto para começar a fazer chamadas para a API do cliente em tempo real.

## Gerar relatório de sobreposição de conjunto de dados usando a linha de comando

Se você estiver familiarizado com o uso da linha de comando, poderá usar a seguinte solicitação cURL para gerar o relatório de sobreposição de conjunto de dados executando uma solicitação GET para `/previewsamplestatus/report/dataset/overlap`.

**Solicitação**

A solicitação a seguir usa o parâmetro `date` para retornar o relatório mais recente da data especificada.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-04-19 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

| Parâmetro | Descrição |
|---|---|
| `date` | Especifique a data do relatório a ser retornado. Se vários relatórios foram executados na data, o relatório mais recente dessa data será retornado. Se um relatório não existir para a data especificada, um erro de status HTTP 404 (Not Found) será retornado. Se nenhuma data for especificada, o relatório mais recente será retornado. Formato: AAAA-MM-DD. Exemplo: `date=2024-12-31` |

**Resposta**

Uma solicitação bem-sucedida retorna o status HTTP 200 (OK) e o relatório de sobreposição de conjunto de dados. O relatório inclui um objeto `data` contendo listas de conjuntos de dados separadas por vírgulas e sua respectiva contagem de perfis. Para obter detalhes sobre como ler o relatório, consulte a seção sobre [interpretar os dados do relatório de sobreposição de conjunto de dados](#interpret-the-report) mais adiante neste tutorial.

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-04-19T19:55:31.147"
}
```

### Gerar relatório de sobreposição de conjunto de dados usando o Postman

O Postman é uma plataforma colaborativa para desenvolvimento de API e é útil para visualizar chamadas de API. Ele pode ser baixado gratuitamente no [site do Postman](https://www.postman.com) e fornece uma interface de usuário fácil de usar para executar chamadas de API. As capturas de tela a seguir usam a interface Postman .

**Solicitação**

Para solicitar o relatório de sobreposição de conjunto de dados usando o Postman, conclua as seguintes etapas:

* Usando a lista suspensa, selecione GET como o tipo de solicitação.
* Insira os cabeçalhos necessários na coluna `KEY`:
   * `Authorization`
   * `x-api-key`
   * `x-gw-ims-org-id`
* Insira os valores gerados durante a autenticação na coluna `VALUE`, substituindo as chaves (`{{ }}`) e qualquer conteúdo dentro das chaves.
* Insira o caminho da solicitação com ou sem o parâmetro `date` opcional:
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap`\
   ou
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=YYYY-MM-DD`

| Parâmetro | Descrição |
|---|---|
| `date` | Especifique a data do relatório a ser retornado. Se vários relatórios foram executados na data, o relatório mais recente dessa data será retornado. Se um relatório não existir para a data especificada, um erro de status HTTP 404 (Not Found) será retornado. Se nenhuma data for especificada, o relatório mais recente será retornado. <br/>Formato: AAAA-MM-DD. Exemplo: `date=2024-12-31` |

Depois que o tipo de solicitação, os cabeçalhos, valores e caminho são concluídos, selecione **Send** para enviar a solicitação da API e gerar o relatório.

![](../images/dataset-overlap-report/postman-request.png)

**Resposta**

Uma solicitação bem-sucedida retorna o status HTTP 200 (OK) e o relatório de sobreposição de conjunto de dados. O relatório inclui um objeto `data` contendo listas de conjuntos de dados separadas por vírgulas e sua respectiva contagem de perfis. Para obter detalhes sobre como ler o relatório, consulte a seção sobre [interpretar os dados do relatório de sobreposição do conjunto de dados](#interpret-the-report).

![](../images/dataset-overlap-report/postman-response.png)

## Interpretar os dados do relatório de sobreposição de conjunto de dados {#interpret-the-report}

O relatório de sobreposição de conjunto de dados gerado fornece um carimbo de data e hora que mostra a data e a hora do relatório e um objeto de dados que inclui combinações exclusivas de IDs de conjunto de dados como listas separadas por vírgulas. As seções a seguir fornecem informações adicionais sobre os componentes do relatório.

### Carimbo de data e hora do relatório

O `reportTimestamp` corresponde à data fornecida na solicitação da API, ou, se nenhuma data foi fornecida, o carimbo de data e hora do relatório mais recente.

### Lista de IDs de conjunto de dados

O objeto `data` inclui combinações exclusivas de IDs de conjunto de dados como listas separadas por vírgulas com a contagem de perfil correspondente para essa combinação de conjuntos de dados.

>[!NOTE]
>
>A soma de todas as contagens de perfil associadas a cada linha do relatório de sobreposição de conjunto de dados deve ser igual ao número total de perfis em sua organização.

Para interpretar os resultados do relatório, considere o seguinte exemplo:

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Este relatório fornece as seguintes informações:
* Há 123 perfis compostos de dados provenientes dos seguintes conjuntos de dados: `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Há 454.412 perfis compostos de dados provenientes desses dois conjuntos de dados: `5d92921872831c163452edc8` e `5eb2cdc6fa3f9a18a7592a98`.
* Há 107 perfis que são compostos apenas de dados do conjunto de dados `5eeda0032af7bb19162172a7`.
* Há um total de 454.642 perfis na organização.

## Próximas etapas

Após concluir este tutorial, você agora pode gerar o relatório de sobreposição de conjunto de dados usando a API do perfil do cliente em tempo real. Para saber mais sobre como trabalhar com dados de perfil na API e na interface do usuário do Experience Platform, comece lendo a [Documentação de visão geral do perfil](../home.md).