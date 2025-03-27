---
title: Aplicar rótulos de acesso para gerenciar o acesso do usuário aos fluxos de dados de origens usando a API
description: Saiba como usar a API de serviço de fluxo para aplicar rótulos de acesso e gerenciar o acesso do usuário aos fluxos de dados de suas fontes.
exl-id: 572d6838-3e4c-4fd5-89fa-32cad6280325
source-git-commit: f57fa04e668fa9c61b9b15778e74969edffae0fa
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 4%

---

# Aplicar rótulos de acesso para gerenciar o acesso do usuário aos fluxos de dados de origens usando a API

Você pode usar as funcionalidades fornecidas pelo [controle de acesso baseado em atributos](../../../access-control/abac/overview.md) no Real-Time CDP para aplicar rótulos aos seus fluxos de dados de fontes. Com esse recurso, você pode garantir que apenas um subconjunto de usuários em sua organização tenha acesso a fluxos de dados de fontes específicas.

Ao adicionar um rótulo de acesso a um fluxo de dados específico, somente os usuários que têm acesso a uma função atribuída a esse rótulo podem exibir e editar esse fluxo de dados. Se um fluxo de dados de fontes não estiver marcado com rótulos, ele ficará visível para todos os usuários que pertencem à sua organização. Por exemplo, se você aplicar o rótulo C12 a um fluxo de dados, os usuários atribuídos a uma função que não tem o rótulo C12 não poderão exibir e editar o fluxo de dados com o rótulo C12.

Leia este guia para obter informações sobre como aplicar rótulos de acesso aos fluxos de dados de suas fontes usando a [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introdução

Antes de trabalhar com rótulos de controle de acesso, primeiro familiarize-se com os recursos do controle de acesso baseado em atributos. Para obter mais informações, leia a seguinte documentação:

* [Visão geral do controle de acesso baseado em atributos](../../../access-control/abac/overview.md)
* [Guia completo do controle de acesso baseado em atributos](../../../access-control/abac/end-to-end-guide.md)
* [Guia da API de controle de acesso baseado em atributos](../../../access-control/abac/api/overview.md)
* [Glossário de rótulos de uso de dados](../../../data-governance/labels/reference.md)

## Aplicar rótulos de acesso a fluxos de dados de origens

>[!NOTE]
>
>* Não é possível aplicar rótulos a uma execução de fluxo. No entanto, as execuções de fluxo herdam todos os rótulos que você aplica ao fluxo de dados principal.
>
>* Se você não tiver acesso de visualização a um fluxo de dados, também não poderá visualizar as execuções de fluxo correspondentes.

Para adicionar um rótulo a um fluxo de dados, faça uma solicitação PATCH para o ponto de extremidade `/flows` e forneça a ID do fluxo de dados que você deseja atualizar.

**Formato da API**

```http
PATCH /flows/{FLOW_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{FLOW_ID}` | A ID do fluxo de dados que você deseja atualizar. |

**Solicitação**

>[!TIP]
>
>Para fazer uma solicitação PATCH, forneça a versão/tag do fluxo de dados que você deseja atualizar como um parâmetro de cabeçalho `if-match`.

A solicitação a seguir adiciona o rótulo C12 ao fluxo de dados com ID: `84224def-1e2a-4d95-9ea2-132d697ed2aa`.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/84224def-1e2a-4d95-9ea2-132d697ed2aa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'if-match: "c5002e0e-0000-0200-0000-67a3c3b70000"'
  -d '[
    {
        "op": "add",
        "path": "/labels",
        "value": ["core/C12"]
    }
]'
```

| Propriedade | Descrição |
| --- | --- |
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace` e `remove`. |
| `path` | A parte do fluxo de dados que será atualizada. |
| `value` | O novo valor com o qual você deseja atualizar sua propriedade. |



**Resposta**

Uma resposta bem-sucedida retorna a ID de fluxo e uma tag atualizada. Você pode verificar a atualização fazendo uma solicitação GET para a API [!DNL Flow Service] e, ao mesmo tempo, fornecendo a ID do fluxo.

```json
{
    "id": "84224def-1e2a-4d95-9ea2-132d697ed2aa",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

Depois de configurar com sucesso os rótulos de acesso ao seu fluxo de dados, qualquer usuário que não tenha acesso a esse rótulo não poderá mais recuperar o fluxo de dados. Por exemplo, se um usuário que não está provisionado com o rótulo C12 fizer uma solicitação do GET para recuperar o fluxo de dados com ID: `84224def-1e2a-4d95-9ea2-132d697ed2aa`, ele receberá a seguinte resposta:

```json
{
    "type": "https://ns.adobe.com/aep/errors/FLOW-1439-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "detailed-message": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again.",
        "id": "84224def-1e2a-4d95-9ea2-132d697ed2aa",
        "request-id": "{REQUEST_ID}",
        "type": "flows"
    },
    "errorMessage": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again.",
    "errorDetails": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again."
}
```

Da mesma forma, os usuários sem acesso ao rótulo C12 não poderão fazer solicitações do PATCH ou do DELETE no fluxo de dados atualizado e receberão a seguinte resposta:

```json
{
    "type": "https://ns.adobe.com/aep/errors/FLOW-2120-403",
    "title": "Forbidden",
    "status": 403,
    "report": {
        "detailed-message": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again.",
        "request-id": "{REQUEST_ID}"
    },
    "errorMessage": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again.",
    "errorDetails": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again."
}
```

## Próximas etapas

Agora você sabe como aplicar rótulos de acesso aos fluxos de dados de suas fontes. Agora é possível garantir que somente um grupo específico de usuários em sua organização possa acessar determinados fluxos de dados de fontes. Leia a documentação a seguir para obter mais informações:

* [Aplicar rótulos de acesso a fluxos de dados de origens na interface do usuário](../ui/labels.md)
* [Visão geral do controle de acesso](../../../access-control/home.md)
