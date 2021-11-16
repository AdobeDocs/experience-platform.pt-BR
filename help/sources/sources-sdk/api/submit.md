---
keywords: Experience Platform, home, tópicos populares, fontes, conectores, conectores de origem, sdk de fontes, sdk, SDK
title: Envie sua fonte (Beta)
topic-legacy: overview
description: O documento a seguir fornece etapas sobre como testar e verificar uma nova fonte usando a API do Serviço de Fluxo e integrar uma nova fonte por meio do SDK de Fontes.
hide: true
hidefromtoc: true
source-git-commit: 274784a5b82d12497f7437fdeaf665dd64224c2d
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 0%

---

# Envie sua fonte (Beta)

>[!IMPORTANT]
>
>O SDK das Fontes está atualmente na versão beta e sua organização pode ainda não ter acesso a ele. A funcionalidade descrita nesta documentação está sujeita a alterações.

A etapa final para integrar sua nova fonte ao Adobe Experience Platform usando [!DNL Sources SDK] O é o para testar sua fonte para verificação. Após obter o sucesso, envie sua nova fonte entrando em contato com o representante do Adobe.

O documento a seguir fornece etapas sobre como testar e depurar sua fonte usando o [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

* Para obter informações sobre como fazer chamadas para APIs da plataforma com êxito, consulte o guia em [introdução às APIs do Platform](../../../landing/api-guide.md).
* Para obter informações sobre como gerar suas credenciais para APIs da plataforma, consulte o tutorial em [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md).
* Para obter informações sobre como configurar [!DNL Postman] para APIs da plataforma, consulte o tutorial em [configurar o console do desenvolvedor e [!DNL Postman]](../../../landing/postman.md).
* Para ajudar no processo de teste e depuração, baixe a variável [[!DNL Sources SDK] coleta de verificação e ambiente aqui](../assets/sdk-verification.zip) e siga as etapas descritas abaixo.

## Testar sua fonte

Para testar sua fonte, você deve executar o [[!DNL Sources SDK] coleta e ambiente de verificação](../assets/sdk-verification.zip) on [!DNL Postman] ao mesmo tempo em que fornece as variáveis de ambiente apropriadas que pertencem à sua fonte.

Para iniciar os testes, primeiro configure a coleção e o ambiente em [!DNL Postman]. Em seguida, especifique a ID da especificação de conexão que deseja testar. Essa ID deve ser a mesma que você gerou usando [!DNL Sources SDK].

### Especificar `authSpecName`

Depois de inserir a ID da especificação de conexão, você deve especificar a variável `authSpecName` que você está usando para sua conexão básica. Dependendo da sua escolha, isso pode ser `OAuth 2 Refresh Code` ou  `Basic Authentication`. Depois de especificar o `authSpecName`, você deve incluir as credenciais necessárias no ambiente . Por exemplo, se você especificar `authSpecName` as `OAuth 2 Refresh Code`, você deve fornecer as credenciais necessárias para o OAuth 2, que são `host` e `accessToken`.

### Especificar `sourceSpec`

Com a adição dos parâmetros de especificação de autenticação, é necessário adicionar as propriedades necessárias da especificação de origem. Você pode encontrar as propriedades necessárias em `sourceSpec.spec.properties`. No caso de [!DNL MailChimp Members] exemplo abaixo, a única propriedade obrigatória é `listId`, o que significa `listId` e é o valor da ID correspondente ao seu [!DNL Postman] ambiente.

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

Depois que os parâmetros de autenticação e especificação de origem forem fornecidos, você poderá começar a preencher o restante das variáveis de ambiente, consulte a tabela abaixo para obter a referência:

>[!NOTE]
>
>Todas as variáveis de exemplo abaixo são valores de espaço reservado que devem ser atualizados, exceto para `flowSpecificationId` e `targetConnectionSpecId`, que são valores fixos.

| Parâmetro | Descrição | Exemplo |
| --- | --- | --- |
| `x-api-key` | Um identificador exclusivo usado para autenticar chamadas para APIs do Experience Platform. Veja o tutorial em [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como recuperar seu `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | Uma entidade corporativa que pode ser proprietária ou licenciar produtos e serviços e permitir o acesso a seus membros. Veja o tutorial em [configurar o console do desenvolvedor e [!DNL Postman]](../../../landing/postman.md) para obter instruções sobre como recuperar seu `x-gw-ims-org-id` informações. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | O token de autorização necessário para concluir chamadas para APIs do Experience Platform. Veja o tutorial em [autenticação e acesso às APIs do Experience Platform](../../../landing/api-authentication.md) para obter informações sobre como recuperar seu `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | Para que os dados de origem sejam usados na Platform, um schema de target deve ser criado para estruturar os dados de origem de acordo com suas necessidades. Para obter etapas detalhadas sobre como criar um esquema XDM de destino, consulte o tutorial em [criação de um schema usando a API](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | A versão exclusiva que corresponde ao esquema. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | O `meta:altId` que é retornado junto com o  `schemaId` ao criar um novo schema. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Para obter etapas detalhadas sobre como criar um conjunto de dados de destino, consulte o tutorial em [criação de um conjunto de dados usando a API](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | Conjuntos de mapeamento podem ser usados para definir como os dados em um schema de origem mapeiam para o de um schema de destino. Para obter etapas detalhadas sobre como criar um mapeamento, consulte o tutorial em [criação de um conjunto de mapeamento usando a API](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | A ID exclusiva que corresponde ao conjunto de mapeamentos. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | A ID da especificação de conexão que corresponde à sua origem. Essa é a ID que você gerou depois [criação de uma nova especificação de conexão](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | A ID de especificação de fluxo de `RestStorageToAEP`. **Este é um valor fixo**. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | A ID de conexão de destino do lago de dados onde os dados ingeridos chegam. **Este é um valor fixo**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | O intervalo de tempo designado a ser seguido ao verificar a conclusão de uma execução de fluxo. | `40` |
| `startTime` | A hora de início designada para o fluxo de dados. A hora de início deve ser formatada em horário unix. | `1597784298` |

Depois de fornecer todas as variáveis de ambiente, você pode começar a executar a coleção usando o [!DNL Postman] interface. No [!DNL Postman] selecione as reticências (**...**) ao lado [!DNL Sources SSSs Verification Collection] e depois selecione **Executar coleção**.

![corredor](../assets/runner.png)

O [!DNL Runner] for exibida, permitindo configurar a ordem de execução do fluxo de dados. Selecionar **Executar Coleta de Verificação SSS** para executar a coleção.

>[!NOTE]
>
>Você pode desativar **Excluir fluxo** na lista de verificação da ordem de execução, se preferir usar o painel de monitoramento de fontes na interface do usuário da plataforma. No entanto, uma vez terminado o teste, você deve garantir que os fluxos de teste sejam excluídos.

![run-collection](../assets/run-collection.png)

## Enviar sua fonte

Assim que sua fonte puder concluir o fluxo de trabalho inteiro, você poderá continuar a entrar em contato com o representante do Adobe e enviar sua fonte para integração.