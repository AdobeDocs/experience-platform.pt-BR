---
keywords: Experience Platform;home;popular topics;data lake privacy;identity namespaces;privacy;data lake
solution: Experience Platform
title: Processamento de solicitação de privacidade no Data Lake
topic: overview
description: A Adobe Experience Platform Privacy Service processa solicitações do cliente para acessar, opt out da venda ou excluir seus dados pessoais, conforme delineado pelas regulamentações legais e organizacionais de privacidade. Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade para dados de clientes armazenados no Data Lake.
translation-type: tm+mt
source-git-commit: 397f08efa276f7885e099a0a8d9dc6d23fe0e8cc
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 0%

---


# Processamento de solicitação de privacidade na [!DNL Data Lake]

A Adobe Experience Platform [!DNL Privacy Service] processa solicitações do cliente para acessar, opt out da venda ou excluir seus dados pessoais, conforme delineado pelas regulamentações legais e organizacionais de privacidade.

Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade para dados de clientes armazenados no [!DNL Data Lake].

## Introdução

É recomendável que você tenha uma compreensão funcional dos seguintes [!DNL Experience Platform] serviços antes de ler este guia:

* [[!DNL Privacy Service]](../privacy-service/home.md): Gerencia solicitações de clientes para acessar, opt out da venda ou excluir seus dados pessoais em aplicativos Adobe Experience Cloud.
* [[!DNL Catalog Service]](home.md): O sistema de registro para localização e linhagem de dados no [!DNL Experience Platform]. Fornece uma API que pode ser usada para atualizar metadados do conjunto de dados.
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
* [[!DNL Identity Service]](../identity-service/home.md): Resolve o desafio fundamental colocado pela fragmentação dos dados de experiência do cliente ao unir identidades entre dispositivos e sistemas.

## Noções básicas sobre namespaces de identidade {#namespaces}

A Adobe Experience Platform [!DNL Identity Service] faz a ponte entre os dados de identidade do cliente nos sistemas e dispositivos. [!DNL Identity Service] usa namespaces **[!UICONTROL de]** identidade para fornecer contexto aos valores de identidade relacionando-os ao seu sistema de origem. Uma namespace pode representar um conceito genérico, como um endereço de email (&quot;Email&quot;) ou associar a identidade a um aplicativo específico, como uma Adobe Advertising Cloud ID (&quot;AdCloud&quot;) ou Adobe Target ID (&quot;TNTID&quot;).

[!DNL Identity Service] mantém um armazenamento de namespaces de identidade definidas globalmente (padrão) e definidas pelo usuário (personalizadas). Namespaces padrão estão disponíveis para todas as organizações (por exemplo, &quot;Email&quot; e &quot;ECID&quot;), enquanto sua organização também pode criar namespaces personalizadas para atender às suas necessidades específicas.

Para obter mais informações sobre namespaces de identidade em [!DNL Experience Platform], consulte a visão geral [da namespace de](../identity-service/namespaces.md)identidade.

## Adicionar dados de identidade a conjuntos de dados

Ao criar solicitações de privacidade para o [!DNL Data Lake], devem ser fornecidos valores de identidade válidos (e suas namespaces associadas) para cada cliente individual, a fim de localizar seus dados e processá-los de acordo. Portanto, todos os conjuntos de dados sujeitos a solicitações de privacidade devem conter um descritor **[!UICONTROL de]** identidade em seu schema XDM associado.

>[!NOTE]
>
>Todos os conjuntos de dados baseados em schemas que não suportam metadados de descritor de identidade (como conjuntos de dados ad-hoc) não podem ser processados em solicitações de privacidade.

Esta seção aborda as etapas de adição de um descritor de identidade a um schema XDM do conjunto de dados existente. Se você já tiver um conjunto de dados com um descritor de identidade, poderá pular para a [próxima seção](#nested-maps).

>[!IMPORTANT]
>
>Ao decidir quais campos de schema definir como identidades, lembre-se das [limitações do uso de campos](#nested-maps)do tipo de mapa aninhados.

Há dois métodos de adicionar um descritor de identidade a um schema de conjunto de dados:

* [Uso da interface](#identity-ui)
* [Uso da API](#identity-api)

### Uso da interface {#identity-ui}

Na interface do [!DNL Experience Platform ]usuário, a área de trabalho de **[!UICONTROL Schemas]** permite que você edite seus schemas XDM existentes. Para adicionar um descritor de identidade a um schema, selecione-o na lista e siga as etapas para [definir um campo de schema como um campo](../xdm/tutorials/create-schema-ui.md#identity-field) de identidade no [!DNL Schema Editor] tutorial.

Depois de definir os campos apropriados dentro do schema como campos de identidade, você pode ir para a próxima seção sobre [envio de solicitações](#submit)de privacidade.

### Uso da API {#identity-api}

>[!NOTE]
>
>Esta seção supõe que você saiba o valor de ID de URI exclusivo do schema XDM do seu conjunto de dados. Se você não souber esse valor, poderá recuperá-lo usando a [!DNL Catalog Service] API. Após ler a seção [Introdução](./api/getting-started.md) do guia do desenvolvedor, siga as etapas descritas para [listar](./api/list-objects.md) ou [pesquisar](./api/look-up-object.md) [!DNL Catalog] objetos para encontrar seu conjunto de dados. A ID do schema pode ser encontrada em `schemaRef.id`
>
> Esta seção inclui chamadas para a API do Registro do Schema. Para obter informações importantes relacionadas ao uso da API, incluindo o conhecimento de sua identidade `{TENANT_ID}` e do conceito de container, consulte a seção [Introdução](../xdm/api/getting-started.md) do guia do desenvolvedor.

Você pode adicionar um descritor de identidade ao schema XDM de um conjunto de dados, fazendo uma solicitação de POST para o `/descriptors` endpoint na [!DNL Schema Registry] API.

**Formato da API**

```http
POST /descriptors
```

**Solicitação**

A solicitação a seguir define um descritor de identidade em um campo &quot;endereço de email&quot; em um schema de amostra.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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
| `@type` | O tipo de descritor que está sendo criado. Para descritores de identidade, o valor deve ser &quot;xdm:descriptorIdentity&quot;. |
| `xdm:sourceSchema` | A ID de URI exclusiva do schema XDM do seu conjunto de dados. |
| `xdm:sourceVersion` | A versão do schema XDM especificada em `xdm:sourceSchema`. |
| `xdm:sourceProperty` | O caminho para o campo de schema ao qual o descritor está sendo aplicado. |
| `xdm:namespace` | Uma das namespaces [de identidade](../privacy-service/api/appendix.md#standard-namespaces) padrão reconhecidas pela [!DNL Privacy Service]ou uma namespace personalizada definida pela sua organização. |
| `xdm:property` | &quot;xdm:id&quot; ou &quot;xdm:code&quot;, dependendo da namespace em `xdm:namespace`. |
| `xdm:isPrimary` | Um valor booliano opcional. Quando verdadeiro, isso indica que o campo é uma identidade primária. Os schemas podem conter apenas uma identidade primária. O padrão é false se não estiver incluído. |

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

## Enviando solicitações {#submit}

>[!NOTE]
>
>Esta seção aborda como formatar solicitações de privacidade para o [!DNL Data Lake]. É altamente recomendável que você reveja a documentação da [[!DNL Privacy Service] IU](../privacy-service/ui/overview.md) ou da [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) para obter etapas completas sobre como enviar um trabalho de privacidade, incluindo como formatar corretamente os dados de identidade do usuário enviados nas cargas de solicitação.

A seção a seguir descreve como fazer solicitações de privacidade para o [!DNL Data Lake] usando a [!DNL Privacy Service] interface do usuário ou a API.

### Uso da interface

Ao criar solicitações de trabalho na interface do usuário, selecione **[!UICONTROL AEP Data Lake]** e/ou **[!UICONTROL Perfil]** em **[!UICONTROL Products]** para processar jobs para dados armazenados no [!DNL Data Lake] ou [!DNL Real-time Customer Profile], respectivamente.

<img src="images/privacy/product-value.png" width="450"><br>

### Uso da API

Ao criar solicitações de trabalho na API, qualquer `userIDs` um fornecido deve usar um arquivo específico `namespace` e `type` dependendo do armazenamento de dados ao qual se aplicam. As IDs do [!DNL Data Lake] devem usar &quot;não registrado&quot; para o `type` valor e um `namespace` valor que corresponda a uma das etiquetas [de](#privacy-labels) privacidade que foram adicionadas aos conjuntos de dados aplicáveis.

Além disso, a `include` matriz da carga da solicitação deve incluir os valores do produto para os diferentes armazenamentos de dados aos quais a solicitação está sendo feita. Ao fazer solicitações ao [!DNL Data Lake], a matriz deve incluir o valor `aepDataLake`.

A solicitação a seguir cria um novo trabalho de privacidade para o [!DNL Data Lake], usando a namespace &quot;email_label&quot; não registrada. Também inclui o valor do produto para o [!DNL Data Lake] no `include` array:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
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

## Excluir processamento de solicitação

Quando [!DNL Experience Platform] recebe uma solicitação de exclusão de [!DNL Privacy Service], [!DNL Platform] envia uma confirmação para [!DNL Privacy Service] que a solicitação foi recebida e os dados afetados foram marcados para exclusão. Os registros são depois removidos do registro no [!DNL Data Lake] prazo de sete dias. Durante esse período de sete dias, os dados são apagados em modo suave e, portanto, não podem ser acessados por nenhum [!DNL Platform] serviço.

Em versões futuras, [!DNL Platform] enviará uma confirmação para [!DNL Privacy Service] depois que os dados tiverem sido fisicamente excluídos.

## Próximas etapas

Ao ler este documento, você foi apresentado aos conceitos importantes envolvidos no processamento de solicitações de privacidade para o [!DNL Data Lake]. É recomendável que você continue lendo a documentação fornecida em todo este guia para aprofundar sua compreensão sobre como gerenciar dados de identidade e criar trabalhos de privacidade.

Consulte o documento sobre o processamento de solicitações de [privacidade para o Perfil](../profile/privacy.md) Cliente em tempo real para obter as etapas sobre o processamento de solicitações de privacidade da [!DNL Profile] loja.

## Apêndice

A seção a seguir contém informações adicionais para o processamento de solicitações de privacidade no [!DNL Data Lake].

### Como rotular campos de tipo de mapa aninhados {#nested-maps}

É importante observar que existem dois tipos de campos do tipo mapa aninhados que não suportam a rotulagem de privacidade:

* Um campo tipo mapa dentro de um campo tipo matriz
* Um campo tipo mapa dentro de outro campo tipo mapa

O processamento do trabalho de privacidade para qualquer um dos dois exemplos acima pode falhar. Por esse motivo, é recomendável evitar o uso de campos do tipo mapa aninhados para armazenar dados de clientes privados. As IDs de consumidor relevantes devem ser armazenadas como um tipo de dados não mapeado dentro do `identityMap` campo (por si só, um campo tipo mapa) para conjuntos de dados baseados em registros, ou o `endUserID` campo para conjuntos de dados baseados em séries de tempo.
