---
keywords: Experience Platform;página inicial;tópicos populares;privacidade data lake;namespaces de identidade;privacidade;data lake
solution: Experience Platform
title: Processamento de solicitação de privacidade no Data Lake
description: A Adobe Experience Platform Privacy Service processa solicitações de clientes para acessar, cancelar a venda ou excluir seus dados pessoais, conforme definido pelas regulamentações legais e organizacionais de privacidade. Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade para dados do cliente armazenados no data lake.
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1429'
ht-degree: 0%

---

# Processamento de solicitação de privacidade no data lake

O Adobe Experience Platform [!DNL Privacy Service] processa solicitações do cliente para acessar, cancelar a venda ou excluir seus dados pessoais, conforme definido pelas regulamentações legais e organizacionais de privacidade.

Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade para dados do cliente armazenados no data lake.

>[!NOTE]
>
>Este guia aborda apenas como fazer solicitações de privacidade para o data lake no Experience Platform. Se você também planeja fazer solicitações de privacidade para o armazenamento de dados do Perfil do cliente em tempo real, consulte o manual sobre [processamento de solicitação de privacidade para o Perfil](../profile/privacy.md), além deste tutorial.
>
>Para obter etapas sobre como fazer solicitações de privacidade para outros aplicativos da Adobe Experience Cloud, consulte a [documentação do Privacy Service](../privacy-service/experience-cloud-apps.md).

## Introdução

É recomendável que você tenha uma compreensão funcional dos seguintes serviços do [!DNL Experience Platform] antes de ler este guia:

* [[!DNL Privacy Service]](../privacy-service/home.md): gerencia solicitações de clientes para acesso, cancelamento de venda ou exclusão de dados pessoais nos aplicativos da Adobe Experience Cloud.
* [[!DNL Catalog Service]](home.md): O sistema de registro para localização e linhagem de dados em [!DNL Experience Platform]. Fornece uma API que pode ser usada para atualizar metadados do conjunto de dados.
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
* [[!DNL Identity Service]](../identity-service/home.md): resolve o desafio fundamental colocado pela fragmentação dos dados de experiência do cliente, unindo as identidades em dispositivos e sistemas.

## Compreensão dos namespaces de identidade {#namespaces}

O Adobe Experience Platform [!DNL Identity Service] une dados de identidade do cliente entre sistemas e dispositivos. [!DNL Identity Service] usa namespaces de identidade para fornecer contexto aos valores de identidade, relacionando-os ao seu sistema de origem. Um namespace pode representar um conceito genérico, como um endereço de email (&quot;Email&quot;) ou associar a identidade a um aplicativo específico, como uma Adobe Advertising Cloud ID (&quot;AdCloud&quot;) ou Adobe Target ID (&quot;TNTID&quot;).

[!DNL Identity Service] mantém um armazenamento de namespaces de identidade definidos globalmente (padrão) e definidos pelo usuário (personalizado). Os namespaces padrão estão disponíveis para todas as organizações (por exemplo, &quot;Email&quot; e &quot;ECID&quot;), enquanto sua organização também pode criar namespaces personalizados para atender às suas necessidades específicas.

Para obter mais informações sobre namespaces de identidade em [!DNL Experience Platform], consulte a [visão geral sobre namespaces de identidade](../identity-service/features/namespaces.md).

## Adição de dados de identidade a conjuntos de dados

Ao criar solicitações de privacidade para o data lake, valores de identidade válidos (e seus namespaces associados) devem ser fornecidos para cada cliente individual para localizar seus dados e processá-los adequadamente. Portanto, todos os conjuntos de dados sujeitos a solicitações de privacidade devem conter um descritor de identidade em seu esquema XDM associado.

>[!NOTE]
>
>Atualmente, todos os conjuntos de dados baseados em esquemas que não aceitam metadados de descritor de identidade (como conjuntos de dados ad-hoc) não podem ser processados em solicitações de privacidade.

Esta seção aborda as etapas de adição de um descritor de identidade a um esquema XDM do conjunto de dados existente. Se você já tiver um conjunto de dados com um descritor de identidade, poderá pular para a [próxima seção](#nested-maps).

>[!IMPORTANT]
>
>Ao decidir quais campos de esquema definir como identidades, lembre-se das [limitações do uso de campos aninhados do tipo mapa](#nested-maps).

Há dois métodos de adicionar um descritor de identidade a um esquema de conjunto de dados:

* [Uso da interface](#identity-ui)
* [Uso da API](#identity-api)

### Uso da interface {#identity-ui}

Na [!DNL Experience Platform]interface de usuário, o espaço de trabalho **[!UICONTROL Esquemas]** permite editar seus esquemas XDM existentes. Para adicionar um descritor de identidade a um esquema, selecione o esquema na lista e siga as etapas para [definir um campo de esquema como um campo de identidade](../xdm/tutorials/create-schema-ui.md#identity-field) no tutorial [!DNL Schema Editor].

Depois de definir os campos apropriados no esquema como campos de identidade, você pode prosseguir para a próxima seção em [enviando solicitações de privacidade](#submit).

### Uso da API {#identity-api}

>[!NOTE]
>
>Esta seção pressupõe que você saiba o valor da ID de URI exclusiva do esquema XDM do conjunto de dados. Se você não souber esse valor, poderá recuperá-lo usando a API [!DNL Catalog Service]. Depois de ler a seção [introdução](./api/getting-started.md) do guia do desenvolvedor, siga as etapas descritas em para [listagem](./api/list-objects.md) ou [pesquisa](./api/look-up-object.md) objetos [!DNL Catalog] para encontrar seu conjunto de dados. A ID do esquema pode ser encontrada em `schemaRef.id`
>
>Esta seção pressupõe que você saiba como fazer chamadas para a API do Registro de esquema. Para obter informações importantes relacionadas ao uso da API, incluindo o conhecimento do `{TENANT_ID}` e o conceito de contêineres, consulte a seção [introdução](../xdm/api/getting-started.md) do guia de API.

Você pode adicionar um descritor de identidade ao esquema XDM de um conjunto de dados fazendo uma solicitação POST para o ponto de extremidade `/descriptors` na API [!DNL Schema Registry].

**Formato da API**

```http
POST /descriptors
```

**Solicitação**

A solicitação a seguir define um descritor de identidade em um campo &quot;endereço de email&quot; em um esquema de amostra.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `@type` | O tipo de descritor sendo criado. Para descritores de identidade, o valor deve ser &quot;xdm:descriptorIdentity&quot;. |
| `xdm:sourceSchema` | A ID URI exclusiva do esquema XDM do seu conjunto de dados. |
| `xdm:sourceVersion` | A versão do esquema XDM especificada em `xdm:sourceSchema`. |
| `xdm:sourceProperty` | O caminho para o campo de esquema ao qual o descritor está sendo aplicado. |
| `xdm:namespace` | Um dos [namespaces de identidade padrão](../privacy-service/api/appendix.md#standard-namespaces) reconhecidos por [!DNL Privacy Service], ou um namespace personalizado definido por sua organização. |
| `xdm:property` | &quot;xdm:id&quot; ou &quot;xdm:code&quot;, dependendo do namespace em uso em `xdm:namespace`. |
| `xdm:isPrimary` | Um valor booleano opcional. Quando verdadeiro, indica que o campo é uma identidade primária. Os esquemas podem conter apenas uma identidade principal. O padrão é false, caso não esteja incluído. |

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 (Criado) e os detalhes do descritor recém-criado.

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Envio de solicitações {#submit}

>[!NOTE]
>
>Esta seção aborda como formatar solicitações de privacidade para o data lake. É altamente recomendável que você consulte a documentação da [[!DNL Privacy Service] Interface](../privacy-service/ui/overview.md) ou da [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) para ver as etapas completas sobre como enviar um trabalho de privacidade, incluindo como formatar corretamente os dados de identidade de usuário enviados nas cargas de solicitação.

A seção a seguir descreve como fazer solicitações de privacidade para o data lake usando a interface ou a API [!DNL Privacy Service].

>[!IMPORTANT]
>
>O tempo que uma solicitação de privacidade pode levar para ser concluída não pode ser garantido. Se ocorrerem alterações no data lake enquanto uma solicitação ainda estiver processando, não é possível garantir se esses registros são ou não processados.

### Uso da interface

Ao criar solicitações de trabalho na interface do usuário, selecione **[!UICONTROL Data Lake da AEP]** em **[!UICONTROL Produtos]** para processar trabalhos para dados armazenados no data lake.

![Imagem mostrando o produto data lake selecionado na caixa de diálogo de criação de solicitação de privacidade](./images/privacy/product-value.png)

### Uso da API

Ao criar solicitações de trabalho na API, qualquer `userIDs` fornecido deve usar um `namespace` e `type` específicos, dependendo do armazenamento de dados ao qual se aplicam. As IDs do data lake devem usar `unregistered` para seu valor `type` e um valor `namespace` que corresponda a um dos [rótulos de privacidade](#privacy-labels) que foram adicionados aos conjuntos de dados aplicáveis.

Além disso, a matriz `include` da carga da solicitação deve incluir os valores de produto para os diferentes armazenamentos de dados para os quais a solicitação está sendo feita. Ao fazer solicitações ao data lake, a matriz deve incluir o valor `aepDataLake`.

A solicitação a seguir cria um novo trabalho de privacidade para o data lake, usando o namespace `email_label` não registrado. Também inclui o valor do produto para o data lake na matriz `include`:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          },
          {
            "namespace": "email_label",
            "value": "jdoe@example.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

>[!IMPORTANT]
>
>A Platform processa solicitações de privacidade em todas as [sandboxes](../sandboxes/home.md) pertencentes à sua organização. Como resultado, qualquer cabeçalho `x-sandbox-name` incluído na solicitação é ignorado pelo sistema.

## Processamento de solicitação de exclusão

Quando [!DNL Experience Platform] recebe uma solicitação de exclusão de [!DNL Privacy Service], [!DNL Platform] envia uma confirmação para [!DNL Privacy Service] de que a solicitação foi recebida e de que os dados afetados foram marcados para exclusão. Os registros são removidos do data lake em sete dias. Durante esse período de sete dias, os dados são excluídos por software e, portanto, não estão acessíveis por nenhum serviço do [!DNL Platform].

Se você também incluiu `ProfileService` ou `identity` na solicitação de privacidade, os dados associados a eles serão tratados separadamente. Consulte a seção sobre [processamento de solicitação de exclusão do Perfil](../profile/privacy.md#delete) para obter mais informações.

## Próximas etapas

Ao ler este documento, você foi apresentado aos conceitos importantes envolvidos no processamento de solicitações de privacidade do data lake. É recomendável continuar lendo a documentação fornecida neste guia para aprofundar sua compreensão de como gerenciar dados de identidade e criar processos de privacidade.

Consulte o documento sobre [processamento de solicitação de privacidade para o Perfil de Cliente em Tempo Real](../profile/privacy.md) para obter as etapas sobre o processamento de solicitações de privacidade para a loja [!DNL Profile].

## Apêndice

A seção a seguir contém informações adicionais para o processamento de solicitações de privacidade no data lake.

### Rotulagem de campos aninhados do tipo mapa {#nested-maps}

É importante observar que há dois tipos de campos aninhados do tipo mapa que não oferecem suporte à rotulagem de privacidade:

* Um campo do tipo mapa dentro de um campo do tipo matriz
* Um campo do tipo mapa dentro de outro campo do tipo mapa

O processamento do trabalho de privacidade para qualquer um dos dois exemplos acima acabará falhando. Por esse motivo, é recomendável evitar o uso de campos aninhados do tipo mapa para armazenar dados privados do cliente. As IDs de consumidores relevantes devem ser armazenadas como um tipo de dados não mapeado no campo `identityMap` (ele próprio um campo do tipo mapa) para conjuntos de dados baseados em registro, ou no campo `endUserID` para conjuntos de dados baseados em série temporal.
