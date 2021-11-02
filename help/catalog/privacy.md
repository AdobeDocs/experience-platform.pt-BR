---
keywords: Experience Platform, home, tópicos populares, privacidade do data lake, namespaces de identidade, privacidade, data lake
solution: Experience Platform
title: Processamento de solicitação de privacidade no Data Lake
topic-legacy: overview
description: A Adobe Experience Platform Privacy Service processa solicitações do cliente para acessar, recusar a venda ou excluir seus dados pessoais, conforme definido pelas regulamentações legais e organizacionais de privacidade. Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade de dados do cliente armazenados no Data Lake.
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
source-git-commit: d8665a349c6f453d83b64317982f3544bbcde0f7
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 0%

---

# Processamento de solicitação de privacidade na [!DNL Data Lake]

Adobe Experience Platform [!DNL Privacy Service] O processa solicitações do cliente para acessar, recusar a venda ou excluir seus dados pessoais, conforme definido pelas regulamentações legais e organizacionais de privacidade.

Este documento aborda conceitos essenciais relacionados ao processamento de solicitações de privacidade de dados do cliente armazenados no [!DNL Data Lake].

>[!NOTE]
>
>Este guia só aborda como fazer solicitações de privacidade para o Data Lake no Experience Platform. Se você também planeja fazer solicitações de privacidade para o armazenamento de dados do Perfil do cliente em tempo real, consulte o guia em [processamento de solicitação de privacidade para Perfil](../profile/privacy.md) além deste tutorial.
>
>Para obter etapas sobre como fazer solicitações de privacidade para outros aplicativos Adobe Experience Cloud, consulte o [Documentação do Privacy Service](../privacy-service/experience-cloud-apps.md).

## Introdução

É recomendável que você tenha uma compreensão funcional do seguinte [!DNL Experience Platform] antes de ler este guia:

* [[!DNL Privacy Service]](../privacy-service/home.md): Gerencia solicitações de clientes para acessar, recusar a venda ou excluir seus dados pessoais nos aplicativos Adobe Experience Cloud.
* [[!DNL Catalog Service]](home.md): O sistema de registro para localização e linhagem de dados no [!DNL Experience Platform]. Fornece uma API que pode ser usada para atualizar metadados do conjunto de dados.
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
* [[!DNL Identity Service]](../identity-service/home.md): Resolve o desafio fundamental colocado pela fragmentação dos dados de experiência do cliente ao unir identidades entre dispositivos e sistemas.

## Noções básicas sobre namespaces de identidade {#namespaces}

Adobe Experience Platform [!DNL Identity Service] faz a ponte entre os dados de identidade do cliente em todos os sistemas e dispositivos. [!DNL Identity Service] O usa namespaces de identidade para fornecer contexto para valores de identidade, relacionando-os com seu sistema de origem. Um namespace pode representar um conceito genérico, como um endereço de email (&quot;Email&quot;) ou associar a identidade a um aplicativo específico, como uma Adobe Advertising Cloud ID (&quot;AdCloud&quot;) ou Adobe Target ID (&quot;TNTID&quot;).

[!DNL Identity Service] O mantém um armazenamento de namespaces de identidade definidos globalmente (padrão) e definidos pelo usuário (personalizados). Os namespaces padrão estão disponíveis para todas as organizações (por exemplo, &quot;Email&quot; e &quot;ECID&quot;), enquanto sua organização também pode criar namespaces personalizados para atender às suas necessidades específicas.

Para obter mais informações sobre namespaces de identidade em [!DNL Experience Platform], consulte o [visão geral do namespace de identidade](../identity-service/namespaces.md).

## Adicionar dados de identidade aos conjuntos de dados

Ao criar solicitações de privacidade para a [!DNL Data Lake], os valores de identidade válidos (e seus namespaces associados) devem ser fornecidos para cada cliente individual, a fim de localizar seus dados e processá-los adequadamente. Portanto, todos os conjuntos de dados que estão sujeitos a solicitações de privacidade devem conter um descritor de identidade em seu esquema XDM associado.

>[!NOTE]
>
>Qualquer conjunto de dados baseado em esquemas que não suportam metadados de descritor de identidade (como conjuntos de dados ad-hoc) atualmente não pode ser processado em solicitações de privacidade.

Esta seção aborda as etapas de adição de um descritor de identidade ao esquema XDM de um conjunto de dados existente. Se você já tiver um conjunto de dados com um descritor de identidade, poderá ignorar [próxima seção](#nested-maps).

>[!IMPORTANT]
>
>Ao decidir quais campos de esquema devem ser definidos como identidades, lembre-se do [limitações do uso de campos do tipo mapa aninhados](#nested-maps).

Há dois métodos de adicionar um descritor de identidade a um esquema de conjunto de dados:

* [Uso da interface do usuário](#identity-ui)
* [Uso da API](#identity-api)

### Uso da interface do usuário {#identity-ui}

No [!DNL Experience Platform ]interface do usuário, a **[!UICONTROL Esquemas]** o workspace permite editar seus esquemas XDM existentes. Para adicionar um descritor de identidade a um esquema, selecione o esquema na lista e siga as etapas para [definição de um campo de esquema como um campo de identidade](../xdm/tutorials/create-schema-ui.md#identity-field) no [!DNL Schema Editor] tutorial.

Depois de definir os campos apropriados no schema como campos de identidade, você pode prosseguir para a próxima seção em [envio de solicitações de privacidade](#submit).

### Uso da API {#identity-api}

>[!NOTE]
>
>Esta seção supõe que você saiba o valor de ID de URI exclusivo do esquema XDM do conjunto de dados. Se você não souber esse valor, poderá recuperá-lo usando a variável [!DNL Catalog Service] API. Depois de ler o [introdução](./api/getting-started.md) do guia do desenvolvedor, siga as etapas descritas em para [listagem](./api/list-objects.md) ou [pesquisa](./api/look-up-object.md) [!DNL Catalog] objetos para localizar o conjunto de dados. A ID do esquema pode ser encontrada em `schemaRef.id`
>
>Essa seção também pressupõe que você saiba como fazer chamadas para a API do Registro de Schema. Para obter informações importantes relacionadas ao uso da API, incluindo conhecer o `{TENANT_ID}` e o conceito de contêineres, consulte o [introdução](../xdm/api/getting-started.md) seção do guia da API.

Você pode adicionar um descritor de identidade ao esquema XDM de um conjunto de dados, fazendo uma solicitação de POST para a variável `/descriptors` endpoint no [!DNL Schema Registry] API.

**Formato da API**

```http
POST /descriptors
```

**Solicitação**

A solicitação a seguir define um descritor de identidade em um campo &quot;endereço de email&quot; em um schema de exemplo.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `@type` | O tipo de descritor que está sendo criado. Para descritores de identidade, o valor deve ser &quot;xdm:descriptorIdentity&quot;. |
| `xdm:sourceSchema` | A ID de URI exclusiva do esquema XDM do conjunto de dados. |
| `xdm:sourceVersion` | A versão do esquema XDM especificada em `xdm:sourceSchema`. |
| `xdm:sourceProperty` | O caminho para o campo de esquema ao qual o descritor está sendo aplicado. |
| `xdm:namespace` | Um dos [namespaces de identidade padrão](../privacy-service/api/appendix.md#standard-namespaces) reconhecido por [!DNL Privacy Service]ou um namespace personalizado definido pela organização. |
| `xdm:property` | &quot;xdm:id&quot; ou &quot;xdm:code&quot;, dependendo do namespace que está sendo usado em `xdm:namespace`. |
| `xdm:isPrimary` | Um valor booleano opcional. Quando true, isso indica que o campo é uma identidade primária. Os esquemas podem conter apenas uma identidade primária. O padrão é false , caso não esteja incluído. |

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
>Esta seção aborda como formatar solicitações de privacidade para o [!DNL Data Lake]. É altamente recomendável revisar a variável [[!DNL Privacy Service] interface](../privacy-service/ui/overview.md) ou [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) documentação para obter as etapas completas sobre como enviar um trabalho de privacidade, incluindo como formatar corretamente os dados de identidade do usuário enviados nas cargas de solicitação.

A seção a seguir descreve como fazer solicitações de privacidade para o [!DNL Data Lake] usando o [!DNL Privacy Service] Interface do usuário ou API.

>[!IMPORTANT]
>
>Não é possível garantir o tempo que uma solicitação de privacidade pode levar para ser concluída. Se ocorrerem alterações no Data Lake enquanto uma solicitação ainda estiver sendo processada, o processamento desses registros também não poderá ser garantido.

### Uso da interface do usuário

Ao criar solicitações de trabalho na interface do usuário, selecione **[!UICONTROL AEP Data Lake]** e/ou **[!UICONTROL Perfil]** under **[!UICONTROL Produtos]** para processar tarefas para dados armazenados no [!DNL Data Lake] ou [!DNL Real-time Customer Profile], respectivamente.

<img src="images/privacy/product-value.png" width="450"><br>

### Uso da API

Ao criar solicitações de trabalho na API, qualquer `userIDs` que são fornecidas devem usar um `namespace` e `type` dependendo do armazenamento de dados ao qual se aplicam. IDs para o [!DNL Data Lake] deve usar `unregistered` para `type` e um `namespace` que corresponde a um dos valores de [rótulos de privacidade](#privacy-labels) que foram adicionados aos conjuntos de dados aplicáveis.

Além disso, a variável `include` a matriz da carga da solicitação deve incluir os valores do produto para os diferentes armazenamentos de dados em que a solicitação está sendo feita. Ao fazer solicitações à [!DNL Data Lake], a matriz deve incluir o valor `aepDataLake`.

A solicitação a seguir cria um novo trabalho de privacidade para a variável [!DNL Data Lake], usando o `email_label` namespace. Também inclui o valor do produto para a variável [!DNL Data Lake] no `include` array:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
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

>[!IMPORTANT]
>
>A plataforma processa solicitações de privacidade em todas as [sandboxes](../sandboxes/home.md) pertencente à sua organização. Como resultado, qualquer `x-sandbox-name` o cabeçalho incluído na solicitação é ignorado pelo sistema.

## Excluir processamento de solicitação

When [!DNL Experience Platform] recebe uma solicitação de exclusão de [!DNL Privacy Service], [!DNL Platform] envia confirmação para [!DNL Privacy Service] que a solicitação foi recebida e os dados afetados foram marcados para exclusão. Os registros são então removidos do [!DNL Data Lake] no prazo de sete dias. Durante esse período de sete dias, os dados são excluídos automaticamente e, portanto, não podem ser acessados por qualquer [!DNL Platform] serviço.

Em versões futuras, [!DNL Platform] enviará confirmação para [!DNL Privacy Service] após os dados terem sido fisicamente excluídos.

## Próximas etapas

Ao ler este documento, você foi introduzido nos conceitos importantes envolvidos no processamento de solicitações de privacidade para o [!DNL Data Lake]. É recomendável continuar lendo a documentação fornecida neste guia para aprofundar sua compreensão de como gerenciar dados de identidade e criar tarefas de privacidade.

Consulte o documento em [processamento de solicitação de privacidade para o Perfil do cliente em tempo real](../profile/privacy.md) para obter as etapas sobre o processamento de solicitações de privacidade do [!DNL Profile] armazenar.

## Apêndice

A seção a seguir contém informações adicionais para o processamento de solicitações de privacidade no [!DNL Data Lake].

### Rotular campos de tipo de mapa aninhados {#nested-maps}

É importante observar que há dois tipos de campos de tipo de mapa aninhados que não oferecem suporte à rotulagem de privacidade:

* Um campo do tipo mapa dentro de um campo do tipo matriz
* Um campo do tipo mapa dentro de outro campo do tipo mapa

O processamento do trabalho de privacidade de qualquer um dos dois exemplos acima eventualmente falhará. Por esse motivo, é recomendável evitar o uso de campos do tipo mapa aninhados para armazenar dados privados do cliente. As IDs de consumidor relevantes devem ser armazenadas como um tipo de dados não mapeado no `identityMap` campo (ele mesmo um campo do tipo mapa) para conjuntos de dados baseados em registros ou o campo `endUserID` para conjuntos de dados baseados em séries de tempo.
