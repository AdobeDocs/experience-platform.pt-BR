---
keywords: Experience Platform;página inicial;tópicos populares;fontes;conectores;conectores de origem;fontes sdk;sdk;SDK
title: Enviar sua fonte
description: O documento a seguir fornece etapas sobre como testar e verificar uma nova fonte usando a API do Serviço de fluxo e integrar uma nova fonte por meio de Fontes de autoatendimento (SDK em lote).
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---

# Enviar sua fonte

A etapa final para integrar sua nova origem ao Adobe Experience Platform usando Fontes de autoatendimento (SDK em lote) é testar sua origem para verificação. Depois de bem-sucedido, você pode enviar sua nova fonte entrando em contato com o representante da Adobe.

O documento a seguir fornece etapas sobre como testar e depurar sua origem usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

* Para obter informações sobre como fazer chamadas para APIs da Platform com êxito, consulte o manual em [introdução às APIs da Platform](../../../landing/api-guide.md).
* Para obter informações sobre como gerar suas credenciais para APIs da Platform, consulte o tutorial em [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md).
* Para obter informações sobre como configurar [!DNL Postman] para APIs da Platform, consulte o tutorial em [configuração do console do desenvolvedor e [!DNL Postman]](../../../landing/postman.md).
* Para ajudar no processo de teste e depuração, baixe o [Coleção e ambiente de verificação de fontes de autoatendimento aqui](../assets/sdk-verification.zip) e siga as etapas descritas abaixo.

## Testar sua origem

Para testar sua fonte, você deve executar o [Coleção e ambiente de verificação de fontes de autoatendimento](../assets/sdk-verification.zip) em [!DNL Postman] ao fornecer as variáveis de ambiente apropriadas que pertencem à sua origem.

Para iniciar o teste, primeiro você deve configurar a coleção e o ambiente em [!DNL Postman]. Em seguida, especifique a ID de especificação de conexão que deseja testar.

### Especificar `authSpecName`

Depois de inserir a ID de especificação de conexão, você deverá especificar a `authSpecName` que você está usando para a conexão básica. Dependendo da sua escolha, pode ser `OAuth 2 Refresh Code` ou  `Basic Authentication`. Depois de especificar o `authSpecName`, você deve incluir as credenciais necessárias no ambiente. Por exemplo, se você especificar `authSpecName` as `OAuth 2 Refresh Code`, você deverá fornecer as credenciais necessárias para o OAuth 2, que são `host` e `accessToken`.

### Especificar `sourceSpec`

Com os parâmetros de especificação de autenticação adicionados, você deverá adicionar as propriedades necessárias da especificação de origem. Você pode encontrar as propriedades necessárias em `sourceSpec.spec.properties`. No caso do [!DNL MailChimp Members] exemplo abaixo, a única propriedade obrigatória é `listId`, o que significa `listId` e seu valor de ID correspondente à [!DNL Postman] ambiente.

```json
"spec": {
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "description": "Define user input parameters to fetch resource values.",
  "properties": {
    "listId": {
      "type": "string",
      "description": "listId for which members need to fetch."
    }
  }
}
```

Depois que os parâmetros de autenticação e especificação de origem forem fornecidos, você poderá começar a preencher o restante das variáveis de ambiente. Consulte a tabela abaixo para obter referência:

>[!NOTE]
>
>Todas as variáveis de exemplo abaixo são valores de espaço reservado que devem ser atualizados, exceto para `flowSpecificationId` e `targetConnectionSpecId`, que são valores fixos.

| Parâmetro | Descrição | Exemplo |
| --- | --- | --- |
| `x-api-key` | Um identificador exclusivo usado para autenticar chamadas para APIs Experience Platform. Veja o tutorial sobre [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como recuperar o `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | Uma entidade corporativa que pode ser proprietária ou licenciar produtos e serviços e permitir acesso a seus membros. Veja o tutorial sobre [configuração do console do desenvolvedor e [!DNL Postman]](../../../landing/postman.md) para obter instruções sobre como recuperar o `x-gw-ims-org-id` informações. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | O token de autorização necessário para completar chamadas para APIs de Experience Platform. Veja o tutorial sobre [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como recuperar o `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | Para que os dados de origem sejam usados na Platform, um esquema de destino deve ser criado para estruturar os dados de origem de acordo com suas necessidades. Para obter etapas detalhadas sobre como criar um esquema XDM de destino, consulte o tutorial sobre [criação de um schema usando a API](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | A versão exclusiva que corresponde ao esquema. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | A variável `meta:altId` que é devolvido juntamente com o  `schemaId` ao criar um novo schema. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Para obter etapas detalhadas sobre como criar um conjunto de dados de destino, consulte o tutorial sobre [criação de um conjunto de dados usando a API](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | Os conjuntos de mapeamento podem ser usados para definir como os dados em um esquema de origem são mapeados para o de um esquema de destino. Para obter etapas detalhadas sobre como criar um mapeamento, consulte o tutorial sobre [criação de um conjunto de mapeamento usando a API](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | O identificador exclusivo que corresponde ao seu conjunto de mapeamento. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | A ID de especificação de conexão que corresponde à sua origem. Esta é a ID gerada após [criação de uma nova especificação de conexão](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | A ID da especificação de fluxo de `RestStorageToAEP`. **Este é um valor fixo**. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | A ID de conexão de destino do data lake onde os dados assimilados chegam. **Este é um valor fixo**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | O intervalo de tempo designado a ser seguido ao verificar a conclusão de uma execução de fluxo. | `40` |
| `startTime` | A hora de início designada para seu fluxo de dados. A hora inicial deve ser formatada em hora unix. | `1597784298` |

Depois de fornecer todas as variáveis de ambiente, você pode começar a executar a coleção usando o [!DNL Postman] interface. No [!DNL Postman] , selecione as reticências (**..**) ao lado [!DNL Sources SSSs Verification Collection] e selecione **Executar coleção**.

![executor](../assets/runner.png)

A variável [!DNL Runner] é exibida, permitindo configurar a ordem de execução do fluxo de dados. Selecionar **Executar Coleta de Verificação do SSS** para executar a coleção.

>[!NOTE]
>
>Você pode desativar o **Excluir Fluxo** na lista de verificação de ordem de execução se preferir usar o painel monitoramento de fontes na interface do usuário da Platform. No entanto, após concluir o teste, é necessário garantir que os fluxos de teste sejam excluídos.

![run-collection](../assets/run-collection.png)

## Enviar sua fonte

Assim que a origem puder concluir todo o fluxo de trabalho, você poderá continuar a entrar em contato com o representante da Adobe e enviar a origem para integração.
