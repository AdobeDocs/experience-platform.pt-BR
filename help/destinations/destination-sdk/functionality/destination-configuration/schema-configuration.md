---
description: Saiba como configurar o esquema de parceiro para destinos criados com o Destination SDK.
title: Configuração de esquema de parceiro
exl-id: 0548e486-206b-45c5-8d18-0d6427c177c5
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '1924'
ht-degree: 3%

---

# Configuração de esquema de parceiro

A Experience Platform usa esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Quando os dados são assimilados na Experience Platform, eles são estruturados de acordo com um esquema XDM. Para obter mais informações sobre o modelo de composição de esquema, incluindo princípios de design e práticas recomendadas, consulte as [noções básicas da composição de esquema](../../../../xdm/schema/composition.md).

Ao criar um destino com o Destination SDK, você pode definir seu próprio esquema de parceiro a ser usado pela plataforma de destino. Isso oferece aos usuários a capacidade de mapear atributos de perfil do Experience Platform para campos específicos reconhecidos pela plataforma de destino, tudo na interface do usuário do Experience Platform.

Ao configurar o esquema de parceiro para o seu destino, você pode ajustar o mapeamento de campos compatível com sua plataforma de destino, como:

* Permite que os usuários mapeiem um atributo XDM do `phoneNumber` para um atributo do `phone` compatível com sua plataforma de destino.
* Crie esquemas de parceiros dinâmicos que o Experience Platform possa chamar dinamicamente para recuperar uma lista de todos os atributos compatíveis no seu destino.
* Defina os mapeamentos de campo obrigatórios exigidos pela plataforma de destino.

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama na documentação de [opções de configuração](../configuration-options.md) ou consulte o guia sobre como [usar o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Você pode definir suas configurações de esquema por meio do ponto de extremidade `/authoring/destinations`. Consulte as seguintes páginas de referência de API para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Atualizar uma configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artigo descreve todas as opções de configuração de esquema compatíveis que você pode usar para o seu destino e mostra o que os clientes verão na interface do Experience Platform.

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros com suporte do Destination SDK diferenciam maiúsculas de minúsculas **1}.** Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações suportam a funcionalidade descrita nesta página.

| Tipo de integração | Suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (lote) | Sim |

## Configuração de esquema compatível {#supported-schema-types}

O Destination SDK é compatível com várias configurações de esquema:

* Os esquemas estáticos são definidos por meio da matriz `profileFields` na seção `schemaConfig`. Em um esquema estático, você define cada atributo de destino que deve ser mostrado na interface do usuário do Experience Platform na matriz `profileFields`. Se precisar atualizar seu esquema, você deve [atualizar a configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md).
* Os esquemas dinâmicos usam um tipo de servidor de destino adicional, chamado de [servidor de esquema dinâmico](../../authoring-api/destination-server/create-destination-server.md#dynamic-schema-servers), para recuperar dinamicamente os atributos de destino compatíveis e gerar esquemas com base em sua própria API. Esquemas dinâmicos não usam a matriz `profileFields`. Se você precisar atualizar seu esquema, não há necessidade de [atualizar a configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md). Em vez disso, o servidor de esquema dinâmico recupera o esquema atualizado da API.
* Na configuração do esquema, você tem a opção de adicionar mapeamentos necessários (ou predefinidos). Esses são mapeamentos que os usuários podem visualizar na interface do usuário do Experience Platform, mas não podem modificá-los ao configurar uma conexão com o seu destino. Por exemplo, é possível impor que o campo de endereço de email sempre seja enviado ao destino.

A seção `schemaConfig` usa vários parâmetros de configuração, dependendo do tipo de esquema necessário, conforme mostrado nas seções abaixo.

## Criar um esquema estático {#attributes-schema}

Para criar um esquema estático com atributos de perfil, defina os atributos de destino na matriz `profileFields` conforme mostrado abaixo.

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the mobilePhone.number value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"firstName",
              "title":"firstName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.firstName value in Experience Platform could be firstName on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"lastName",
              "title":"lastName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.lastName value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           }
        ],
      "useCustomerSchemaForAttributeMapping":false,
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true,
      "segmentNamespaceAllowList": ["someNamespace"],
      "segmentNamespaceDenyList": ["someOtherNamespace"]

}
```

| Parâmetro | Tipo | Obrigatório/Opcional | Descrição |
|---------|----------|------|---|
| `profileFields` | Matriz | Opcional | Define a matriz de atributos de destino aceitos pela plataforma de destino para a qual os clientes podem mapear seus atributos de perfil. Ao usar uma matriz `profileFields`, você pode omitir totalmente o parâmetro `useCustomerSchemaForAttributeMapping`. |
| `useCustomerSchemaForAttributeMapping` | Booleano | Opcional | Habilita ou desabilita o mapeamento de atributos do esquema do cliente para os atributos definidos na matriz `profileFields`. <ul><li>Se definido como `true`, os usuários verão somente a coluna de origem no campo de mapeamento. `profileFields` não são aplicáveis neste caso.</li><li>Se definido como `false`, os usuários podem mapear atributos de origem de seus esquemas para os atributos definidos na matriz `profileFields`.</li></ul> O valor padrão é `false`. |
| `profileRequired` | Booleano | Opcional | Use `true` se os usuários puderem mapear atributos de perfil do Experience Platform para atributos personalizados na sua plataforma de destino. |
| `segmentRequired` | Booleano | Obrigatório | Este parâmetro é requerido pela Destination SDK e deve sempre ser definido como `true`. |
| `identityRequired` | Booleano | Obrigatório | Defina como `true` se os usuários puderem mapear [tipos de identidade](identity-namespace-configuration.md) do Experience Platform para os atributos definidos na matriz `profileFields`. |
| `segmentNamespaceAllowList` | Matriz | Opcional | Permite mapear somente públicos-alvo dos namespaces de público-alvo definidos na matriz para o destino. <br><br> O uso deste parâmetro é desencorajado na maioria dos casos. Em vez disso, use o `"segmentNamespaceDenyList":[]` para permitir que todos os tipos de público sejam exportados para o seu destino. <br><br> Se `segmentNamespaceAllowList` e `segmentNamespaceDenyList` estiverem ausentes em sua configuração, os usuários só poderão exportar públicos-alvo originados do [Serviço de Segmentação](../../../../segmentation/home.md). <br><br>`segmentNamespaceAllowList` e `segmentNamespaceDenyList` são mutuamente exclusivos. |
| `segmentNamespaceDenyList` | Matriz | Opcional | Restringe os usuários de mapear públicos-alvo a partir de namespaces de público-alvo definidos na matriz para o destino. <br><br>A Adobe recomenda permitir a exportação de todos os públicos-alvo, independentemente da origem, definindo `"segmentNamespaceDenyList":[]`. <br><br>**Importante:** se você não especificar `segmentNamespaceDenyList` em seu `schemaConfig` e não usar o `segmentNamespaceAllowList`, o sistema definirá automaticamente o `segmentNamespaceDenyList` como `[]`. Isso evita a perda de públicos-alvo personalizados no futuro. Por questões de segurança, a Adobe recomenda que você defina explicitamente o `"segmentNamespaceDenyList":[]` na sua configuração. <br><br>`segmentNamespaceAllowList` e `segmentNamespaceDenyList` são mutuamente exclusivos. |

{style="table-layout:auto"}

A experiência de interface do usuário resultante é mostrada nas imagens abaixo.

Ao selecionar o target mapping, os usuários podem ver os campos definidos na matriz `profileFields`.

![Imagem da interface do usuário mostrando a tela de atributos de destino.](../../assets/functionality/destination-configuration/select-attributes.png)

Após selecionar os atributos, eles podem vê-los na coluna do campo de destino.

![Imagem de interface do usuário mostrando um esquema de destino estático com atributos](../../assets/functionality/destination-configuration/static-schema-attributes.png)

## Criar um esquema dinâmico {#dynamic-schema-configuration}

O Destination SDK oferece suporte à criação de esquemas de parceiros dinâmicos. Ao contrário de um esquema estático, um esquema dinâmico não usa uma matriz `profileFields`. Em vez disso, os esquemas dinâmicos usam um servidor de esquema dinâmico que se conecta à sua própria API de onde recupera a configuração do esquema.

>[!IMPORTANT]
>
>Antes de criar um esquema dinâmico, [crie um servidor de esquema dinâmico](../../authoring-api/destination-server/create-destination-server.md#dynamic-schema-servers).

Em uma configuração de esquema dinâmico, a matriz `profileFields` é substituída pela seção `dynamicSchemaConfig`, conforme mostrado abaixo.

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"DYNAMIC_SCHEMA_SERVER_ID",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| Parâmetro | Tipo | Obrigatório/Opcional | Descrição |
|---------|----------|------|---|
| `dynamicEnum.authenticationRule` | String | Obrigatório | Indica como [!DNL Experience Platform] clientes se conectam ao seu destino. Os valores aceitos são `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Use o `CUSTOMER_AUTHENTICATION` se os clientes da Experience Platform fizerem logon no sistema por meio de qualquer um dos métodos de autenticação descritos [aqui](customer-authentication.md). </li><li> Use o `PLATFORM_AUTHENTICATION` se houver um sistema de autenticação global entre o Adobe e o seu destino e o cliente do [!DNL Experience Platform] não precisar fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve [criar um objeto de credenciais](../../credentials-api/create-credential-configuration.md) usando a API de Credenciais e passar a ID do objeto de credencial no parâmetro `authenticationId` na configuração de [entrega de destino](/help/destinations/destination-sdk/functionality/destination-configuration/destination-delivery.md#platform-authentication). </li><li>Use `NONE` se nenhuma autenticação for necessária para enviar dados para a plataforma de destino. </li></ul> |
| `dynamicEnum.destinationServerId` | String | Obrigatório | O `instanceId` do seu servidor de esquema dinâmico. Esse servidor de destino inclui o endpoint da API chamado pelo Experience Platform para recuperar o esquema dinâmico. |
| `dynamicEnum.value` | String | Obrigatório | O nome do esquema dinâmico, conforme definido na configuração do servidor do esquema dinâmico. |
| `dynamicEnum.responseFormat` | String | Obrigatório | Sempre defina como `SCHEMA` ao definir um esquema dinâmico. |
| `profileRequired` | Booleano | Opcional | Use `true` se os usuários puderem mapear atributos de perfil do Experience Platform para atributos personalizados na sua plataforma de destino. |
| `segmentRequired` | Booleano | Obrigatório | Este parâmetro é requerido pela Destination SDK e deve sempre ser definido como `true`. |
| `identityRequired` | Booleano | Obrigatório | Defina como `true` se os usuários puderem mapear [tipos de identidade](identity-namespace-configuration.md) do Experience Platform para os atributos definidos na matriz `profileFields`. |

{style="table-layout:auto"}

## Mapeamentos necessários {#required-mappings}

Na configuração do esquema, além do esquema estático ou dinâmico, você tem a opção de adicionar mapeamentos necessários (ou predefinidos). Esses são mapeamentos que os usuários podem visualizar na interface do usuário do Experience Platform, mas não podem modificá-los ao configurar uma conexão com o seu destino.

Por exemplo, é possível impor que o campo de endereço de email sempre seja enviado ao destino.

>[!NOTE]
>
>As seguintes combinações de mapeamentos necessários são compatíveis no momento:
>* Você pode configurar um campo de origem e um campo de destino obrigatórios. Nesse caso, os usuários não podem editar ou selecionar nenhum dos dois campos e só podem visualizar a seleção.
>* Você pode configurar apenas um campo de destino obrigatório. Nesse caso, os usuários poderão selecionar um campo de origem para mapear para o destino.
>
> No momento, *não* é possível configurar somente um campo de origem obrigatório.

Veja abaixo dois exemplos de uma configuração de esquema com os mapeamentos necessários e como eles se parecem na etapa de mapeamento do [fluxo de trabalho ativar dados para destinos em lote](../../../ui/activate-batch-profile-destinations.md).


>[!BEGINTABS]

>[!TAB Mapeamentos de origem e destino necessários]

O exemplo abaixo mostra os mapeamentos de origem e de destino necessários. Quando os campos de origem e de destino são especificados como mapeamentos obrigatórios, os usuários não podem selecionar ou editar nenhum dos dois campos e só podem exibir a seleção predefinida.

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "sourceType": "text/x.schema-path",
        "source": "personalEmail.address",
        "destination": "personalEmail.address"
      }
    ] 
}
```

| Parâmetro | Tipo | Obrigatório/Opcional | Descrição |
|---|---|---|---|
| `requiredMappingsOnly` | Booleano | Opcional | Quando definido como true, os usuários não poderão mapear outros atributos e identidades no fluxo de ativação, exceto os mapeamentos necessários definidos na matriz `requiredMappings`. |
| `requiredMappings.sourceType` | String | Obrigatório | Indica o tipo do campo `source`. Valores compatíveis: <ul><li>`text/x.schema-path`: Use esse valor quando o campo `source` for um atributo de perfil de um esquema XDM.</li><li>`text/x.aep-xl`: Use esse valor quando o campo `source` for definido por uma expressão regular. Exemplo: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`</li><li>`text/plain`: Use esse valor quando o campo `source` for definido por um modelo de macro. Atualmente, o único modelo de macro compatível é `metadata.segment.alias`.</li></ul> |
| `requiredMappings.source` | String | Obrigatório | Indica o valor do campo de origem. Tipos de valores suportados: <ul><li>Atributos do perfil XDM. Exemplo: `personalEmail.address`. Quando o atributo de origem for um atributo de perfil XDM, defina o parâmetro `sourceType` como `text/x.schema-path`.</li><li>Expressões regulares. Exemplo: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`. Quando o atributo de origem for uma expressão regular, defina o parâmetro `sourceType` como `text/x.aep-xl`.</li><li>Modelos de macro. Exemplo:`metadata.segment.alias`. Quando o atributo de origem for um modelo de macro, defina o parâmetro `sourceType` como `text/plain`. Atualmente, o único modelo de macro compatível é `metadata.segment.alias`.</li></ul> |
| `requiredMappings.destination` | String | Obrigatório | Indica o valor do campo de destino. Quando os campos de origem e de destino são especificados como mapeamentos obrigatórios, os usuários não podem selecionar ou editar nenhum dos dois campos e só podem exibir a seleção. |

{style="table-layout:auto"}

Como resultado, as seções do **[!UICONTROL campo do Source]** e do **[!UICONTROL campo do Target]** na interface do usuário do Experience Platform estão esmaecidas.

![Imagem dos mapeamentos necessários no fluxo de ativação da interface do usuário.](../../assets/functionality/destination-configuration/required-mappings-2.png)

>[!TAB Mapeamento de destino necessário]

O exemplo abaixo mostra um mapeamento de destino necessário. Se apenas o campo de destino for especificado conforme necessário, os usuários poderão selecionar qual campo de origem mapear para ele.

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "destination": "identityMap.ExamplePartner_ID",
        "mandatoryRequired": true,
        "primaryKeyRequired": true
      }
    ] 
}
```

| Parâmetro | Tipo | Obrigatório/Opcional | Descrição |
|---|---|---|---|
| `requiredMappingsOnly` | Booleano | Opcional | Quando definido como true, os usuários não poderão mapear outros atributos e identidades no fluxo de ativação, exceto os mapeamentos necessários definidos na matriz `requiredMappings`. |
| `requiredMappings.destination` | String | Obrigatório | Indica o valor do campo de destino. Quando apenas o campo de destino é especificado, os usuários podem selecionar um campo de origem para mapear para o destino. |
| `mandatoryRequired` | Booleano | Opcional | Indica se o mapeamento deve ser marcado como um [atributo obrigatório](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `primaryKeyRequired` | Booleano | Opcional | Indica se o mapeamento deve ser marcado como uma [chave de desduplicação](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |

{style="table-layout:auto"}

Como resultado, a seção **[!UICONTROL Campo de destino]** da interface do usuário do Experience Platform fica esmaecida, enquanto a seção **[!UICONTROL Campo do Source]** está ativa e os usuários podem interagir com ela. As opções **[!UICONTROL Chave obrigatória]** e **[!UICONTROL Chave de desduplicação]** estão ativas e os usuários não podem alterá-las.

![Imagem dos mapeamentos necessários no fluxo de ativação da interface do usuário.](../../assets/functionality/destination-configuration/required-mappings-1.png)

>[!ENDTABS]

## Configuração do suporte para públicos externos {#external-audiences}

Para configurar o destino para oferecer suporte à ativação de [públicos gerados externamente](../../../../segmentation/ui/audience-portal.md#import-audience), inclua o trecho abaixo na seção `schemaConfig`.

```json
"schemaConfig": {
  "segmentNamespaceDenyList": [],
  ...
}
```

Consulte as descrições de propriedade na [tabela](#attributes-schema) mais acima nesta página para saber mais sobre a funcionalidade `segmentNamespaceDenyList`.

## Próximas etapas {#next-steps}

Depois de ler este artigo, você deve entender melhor quais tipos de esquema são compatíveis com o Destination SDK e como configurar seu esquema.

Para saber mais sobre os outros componentes de destino, consulte os seguintes artigos:

* [Autenticação do cliente](customer-authentication.md)
* [Autorização OAuth2](oauth2-authorization.md)
* [Atributos da interface](ui-attributes.md)
* [Campos de dados do cliente](customer-data-fields.md)
* [Configuração do namespace de identidade](identity-namespace-configuration.md)
* [Configurações de mapeamento compatíveis](supported-mapping-configurations.md)
* [Entrega de destino](destination-delivery.md)
* [Configuração de metadados de público](audience-metadata-configuration.md)
* [Política de agregação](aggregation-policy.md)
* [Configuração em lote](batch-configuration.md)
* [Qualificações do perfil histórico](historical-profile-qualifications.md)
