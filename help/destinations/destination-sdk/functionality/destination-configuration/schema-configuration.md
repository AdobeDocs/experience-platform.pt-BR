---
description: Saiba como configurar o esquema de parceiro para destinos criados com o Destination SDK.
title: Configuração de esquema de parceiro
exl-id: 0548e486-206b-45c5-8d18-0d6427c177c5
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '1897'
ht-degree: 4%

---

# Configuração de esquema de parceiro

A Experience Platform utiliza esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Quando os dados são assimilados na Platform, eles são estruturados de acordo com um esquema XDM. Para obter mais informações sobre o modelo de composição do schema, incluindo princípios de design e práticas recomendadas, consulte o [noções básicas da composição do esquema](../../../../xdm/schema/composition.md).

Ao criar um destino com o Destination SDK, você pode definir seu próprio esquema de parceiro a ser usado pela plataforma de destino. Isso oferece aos usuários a capacidade de mapear atributos de perfil da Platform para campos específicos reconhecidos pela plataforma de destino, tudo na interface do usuário da Platform.

Ao configurar o esquema de parceiro para o seu destino, você pode ajustar o mapeamento de campos compatível com sua plataforma de destino, como:

* Permitir que os usuários mapeiem um `phoneNumber` Atributo XDM para um `phone` atributo compatível com sua plataforma de destino.
* Crie esquemas de parceiros dinâmicos que o Experience Platform possa chamar dinamicamente para recuperar uma lista de todos os atributos compatíveis no seu destino.
* Defina os mapeamentos de campo obrigatórios exigidos pela plataforma de destino.

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama no [opções de configuração](../configuration-options.md) ou consulte o guia sobre como [usar o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Você pode definir as configurações do esquema por meio da `/authoring/destinations` terminal. Consulte as seguintes páginas de referência de API para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Atualizar uma configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artigo descreve todas as opções de configuração de esquema compatíveis que você pode usar para o seu destino e mostra o que os clientes verão na interface do usuário da Platform.

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros compatíveis com o Destination SDK são **diferencia maiúsculas de minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações suportam a funcionalidade descrita nesta página.

| Tipo de integração | Suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (lote) | Sim |

## Configuração de esquema compatível {#supported-schema-types}

O Destination SDK suporta várias configurações de esquema:

* Os esquemas estáticos são definidos por meio da variável `profileFields` matriz no `schemaConfig` seção. Em um esquema estático, você define cada atributo de destino que deve ser mostrado na interface do usuário do Experience Platform na `profileFields` matriz. Se precisar atualizar seu esquema, você deve [atualizar a configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md).
* Os esquemas dinâmicos usam um tipo de servidor de destino adicional, chamado de [servidor de esquema dinâmico](../../authoring-api/destination-server/create-destination-server.md#dynamic-schema-servers), para recuperar dinamicamente os atributos de destino compatíveis e gerar esquemas com base em sua própria API. Os esquemas dinâmicos não usam o `profileFields` matriz. Se precisar atualizar o esquema, não há necessidade de [atualizar a configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md). Em vez disso, o servidor de esquema dinâmico recupera o esquema atualizado da API.
* Na configuração do esquema, você tem a opção de adicionar mapeamentos necessários (ou predefinidos). Esses são mapeamentos que os usuários podem visualizar na interface do usuário da Platform, mas não podem modificá-los ao configurar uma conexão com o seu destino. Por exemplo, é possível impor que o campo de endereço de email sempre seja enviado ao destino.

A variável `schemaConfig` A seção usa vários parâmetros de configuração, dependendo do tipo de esquema necessário, conforme mostrado nas seções abaixo.

## Criar um esquema estático {#attributes-schema}

Para criar um esquema estático com atributos de perfil, defina os atributos de público alvo no `profileFields` conforme mostrado abaixo.

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

| Parâmetro | Tipo | Obrigatório / Opcional | Descrição |
|---------|----------|------|---|
| `profileFields` | Matriz | Opcional | Define a matriz de atributos de destino aceitos pela plataforma de destino para a qual os clientes podem mapear seus atributos de perfil. Ao usar uma `profileFields` , você pode omitir o `useCustomerSchemaForAttributeMapping` totalmente. |
| `useCustomerSchemaForAttributeMapping` | Booleano | Opcional | Ativa ou desativa o mapeamento de atributos do esquema do cliente para os atributos definidos na `profileFields` matriz. <ul><li>Se definida como `true`, os usuários só verão a coluna de origem no campo de mapeamento. `profileFields` não são aplicáveis no caso em apreço.</li><li>Se definida como `false`, os usuários podem mapear atributos de origem de seu esquema para os atributos definidos na variável `profileFields` matriz.</li></ul> O valor padrão é `false`. |
| `profileRequired` | Booleano | Opcional | Uso `true` se os usuários precisarem mapear atributos de perfil do Experience Platform para atributos personalizados na plataforma de destino. |
| `segmentRequired` | Booleano | Obrigatório | Este parâmetro é requerido pelo Destination SDK e sempre deve ser definido como `true`. |
| `identityRequired` | Booleano | Obrigatório | Defina como `true` se os usuários devem ser capazes de mapear [tipos de identidade](identity-namespace-configuration.md) de Experience Platform para os atributos definidos na variável `profileFields` matriz . |
| `segmentNamespaceAllowList` | Matriz | Opcional | Define namespaces de público-alvo específicos a partir dos quais os usuários podem mapear públicos-alvo para o destino. Use esse parâmetro para restringir os usuários do Platform a exportar públicos-alvo somente dos namespaces de público-alvo definidos na matriz. Este parâmetro não pode ser usado junto com `segmentNamespaceDenyList`.<br> <br> Exemplo: `"segmentNamespaceAllowList": ["AudienceManager"]` permitirá que os usuários mapeiem apenas os públicos-alvo da `AudienceManager` para este destino. <br> <br> Para permitir que os usuários exportem qualquer público para o seu destino, você pode ignorar esse parâmetro. <br> <br> Se ambos `segmentNamespaceAllowList` e `segmentNamespaceDenyList` estiverem ausentes na sua configuração, os usuários só poderão exportar públicos-alvo originários da [Serviço de segmentação](../../../../segmentation/home.md). |
| `segmentNamespaceDenyList` | Matriz | Opcional | Restringe os usuários no mapeamento de públicos-alvo para o destino, a partir dos namespaces de público-alvo definidos na matriz. Não pode ser usado com `segmentNamespaceAllowed`. <br> <br> Exemplo: `"segmentNamespaceDenyList": ["AudienceManager"]` bloquearão os usuários de mapear públicos-alvo da `AudienceManager` para este destino. <br> <br> Para permitir que os usuários exportem qualquer público para o seu destino, você pode ignorar esse parâmetro. <br> <br> Se ambos `segmentNamespaceAllowed` e `segmentNamespaceDenyList` estiverem ausentes na sua configuração, os usuários só poderão exportar públicos-alvo originários da [Serviço de segmentação](../../../../segmentation/home.md). <br> <br> Para permitir a exportação de todos os públicos-alvo, independentemente da origem, defina `"segmentNamespaceDenyList":[]`. |

{style="table-layout:auto"}

A experiência de interface do usuário resultante é mostrada nas imagens abaixo.

Quando os usuários selecionam o target mapping, eles podem ver os campos definidos no `profileFields` matriz.

![Imagem da interface do usuário mostrando a tela de atributos de destino.](../../assets/functionality/destination-configuration/select-attributes.png)

Após selecionar os atributos, eles podem vê-los na coluna do campo de destino.

![Imagem da interface do usuário mostrando um esquema de destino estático com atributos](../../assets/functionality/destination-configuration/static-schema-attributes.png)

## Criar um esquema dinâmico {#dynamic-schema-configuration}

O Destination SDK oferece suporte à criação de esquemas de parceiros dinâmicos. Ao contrário de um esquema estático, um esquema dinâmico não usa um `profileFields` matriz. Em vez disso, os esquemas dinâmicos usam um servidor de esquema dinâmico que se conecta à sua própria API de onde recupera a configuração do esquema.

>[!IMPORTANT]
>
>Antes de criar um esquema dinâmico, você deve [criar um servidor de esquema dinâmico](../../authoring-api/destination-server/create-destination-server.md#dynamic-schema-servers).

Em uma configuração de esquema dinâmico, a variável `profileFields` matriz é substituída pela variável `dynamicSchemaConfig` conforme mostrado abaixo.

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

| Parâmetro | Tipo | Obrigatório / Opcional | Descrição |
|---------|----------|------|---|
| `dynamicEnum.authenticationRule` | String | Obrigatório | Indica como [!DNL Platform] Os clientes do se conectam ao seu destino. Os valores aceitos são `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Uso `CUSTOMER_AUTHENTICATION` se os clientes da Platform fizerem logon no sistema por meio de qualquer um dos métodos de autenticação descritos [aqui](customer-authentication.md). </li><li> Uso `PLATFORM_AUTHENTICATION` se houver um sistema de autenticação global entre o Adobe e seu destino e a [!DNL Platform] O cliente não precisa fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve [criar um objeto de credenciais](../../credentials-api/create-credential-configuration.md) usando a API de credenciais do. </li><li>Uso `NONE` se nenhuma autenticação for necessária para enviar dados para a plataforma de destino. </li></ul> |
| `dynamicEnum.destinationServerId` | String | Obrigatório | A variável `instanceId` do seu servidor de esquema dinâmico. Esse servidor de destino inclui o endpoint da API que o Experience Platform chamará para recuperar o esquema dinâmico. |
| `dynamicEnum.value` | String | Obrigatório | O nome do esquema dinâmico, conforme definido na configuração do servidor do esquema dinâmico. |
| `dynamicEnum.responseFormat` | String | Obrigatório | Sempre definida como `SCHEMA` ao definir um schema dinâmico. |
| `profileRequired` | Booleano | Opcional | Uso `true` se os usuários precisarem mapear atributos de perfil do Experience Platform para atributos personalizados na plataforma de destino. |
| `segmentRequired` | Booleano | Obrigatório | Este parâmetro é requerido pelo Destination SDK e sempre deve ser definido como `true`. |
| `identityRequired` | Booleano | Obrigatório | Defina como `true` se os usuários devem ser capazes de mapear [tipos de identidade](identity-namespace-configuration.md) de Experience Platform para os atributos definidos na variável `profileFields` matriz . |

{style="table-layout:auto"}

## Mapeamentos necessários {#required-mappings}

Na configuração do esquema, além do esquema estático ou dinâmico, você tem a opção de adicionar mapeamentos necessários (ou predefinidos). Esses são mapeamentos que os usuários podem visualizar na interface do usuário da Platform, mas não podem modificá-los ao configurar uma conexão com o seu destino.

Por exemplo, é possível impor que o campo de endereço de email sempre seja enviado ao destino.

>[!NOTE]
>
>As seguintes combinações de mapeamentos necessários são compatíveis no momento:
>* Você pode configurar um campo de origem e um campo de destino obrigatórios. Nesse caso, os usuários não podem editar ou selecionar nenhum dos dois campos e só podem visualizar a seleção.
>* Você pode configurar apenas um campo de destino obrigatório. Nesse caso, os usuários poderão selecionar um campo de origem para mapear para o destino.
>
> No momento, está configurando apenas um campo de origem obrigatório *não* compatível.

Veja abaixo dois exemplos de uma configuração de esquema com mapeamentos necessários e como eles se parecem na etapa de mapeamento do [ativar dados para fluxo de trabalho de destinos em lote](../../../ui/activate-batch-profile-destinations.md).


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

| Parâmetro | Tipo | Obrigatório / Opcional | Descrição |
|---|---|---|---|
| `requiredMappingsOnly` | Booleano | Opcional | Quando definido como true , os usuários não poderão mapear outros atributos e identidades no fluxo de ativação, além dos mapeamentos necessários definidos na variável `requiredMappings` matriz. |
| `requiredMappings.sourceType` | String | Obrigatório | Indica o tipo de `source` campo. Valores compatíveis: <ul><li>`text/x.schema-path`: Use esse valor quando a variável `source` é um atributo de perfil de um esquema XDM.</li><li>`text/x.aep-xl`: Use esse valor quando `source` O campo é definido por uma expressão regular. Exemplo: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`</li><li>`text/plain`: Use esse valor quando `source` O campo é definido por um modelo de macro. No momento, o único modelo de macro compatível é `metadata.segment.alias`.</li></ul> |
| `requiredMappings.source` | String | Obrigatório | Indica o valor do campo de origem. Tipos de valores suportados: <ul><li>Atributos do perfil XDM. Exemplo: `personalEmail.address`. Quando o atributo de origem for um atributo de perfil XDM, defina o `sourceType` parâmetro para `text/x.schema-path`.</li><li>Expressões regulares. Exemplo: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`. Quando o atributo de origem for uma expressão regular, defina o `sourceType` parâmetro para `text/x.aep-xl`.</li><li>Modelos de macro. Exemplo:`metadata.segment.alias`. Quando o atributo de origem for um modelo de macro, defina o `sourceType` parâmetro para `text/plain`. No momento, o único modelo de macro compatível é `metadata.segment.alias`.</li></ul> |
| `requiredMappings.destination` | String | Obrigatório | Indica o valor do campo de destino. Quando os campos de origem e de destino são especificados como mapeamentos obrigatórios, os usuários não podem selecionar ou editar nenhum dos dois campos e só podem exibir a seleção. |

{style="table-layout:auto"}

Como resultado, tanto o **[!UICONTROL Campo de origem]** e **[!UICONTROL Campo de destino]** As seções na interface do usuário da Platform estão esmaecidas.

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

| Parâmetro | Tipo | Obrigatório / Opcional | Descrição |
|---|---|---|---|
| `requiredMappingsOnly` | Booleano | Opcional | Quando definido como true , os usuários não poderão mapear outros atributos e identidades no fluxo de ativação, além dos mapeamentos necessários definidos na variável `requiredMappings` matriz. |
| `requiredMappings.destination` | String | Obrigatório | Indica o valor do campo de destino. Quando apenas o campo de destino é especificado, os usuários podem selecionar um campo de origem para mapear para o destino. |
| `mandatoryRequired` | Booleano | Opcional | Indica se o mapeamento deve ser marcado como um [atributo obrigatório](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `primaryKeyRequired` | Booleano | Opcional | Indica se o mapeamento deve ser marcado como um [chave de desduplicação](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |

{style="table-layout:auto"}

Como resultado, a **[!UICONTROL Campo de destino]** na interface do usuário da Platform estiver esmaecida, enquanto a variável **[!UICONTROL Campo de origem]** A seção está ativa e os usuários podem interagir com ela. A variável **[!UICONTROL Chave obrigatória]** e **[!UICONTROL Chave de desduplicação]** opções estão ativas e os usuários não podem alterá-las.

![Imagem dos mapeamentos necessários no fluxo de ativação da interface do usuário.](../../assets/functionality/destination-configuration/required-mappings-1.png)

>[!ENDTABS]

## Próximas etapas {#next-steps}

Depois de ler este artigo, você deve entender melhor quais tipos de esquema são compatíveis com o Destination SDK e como você pode configurar seu esquema.

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
