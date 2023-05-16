---
description: Saiba como configurar o schema do parceiro para destinos criados com o Destination SDK.
title: Configuração do esquema do parceiro
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 5%

---


# Configuração do esquema do parceiro

A Experience Platform utiliza esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Quando os dados são assimilados na Platform, ela é estruturada de acordo com um esquema XDM. Para obter mais informações sobre o modelo de composição de schema, incluindo princípios de design e práticas recomendadas, consulte o [noções básicas da composição do schema](../../../../xdm/schema/composition.md).

Ao criar um destino com o Destination SDK, você pode definir seu próprio schema de parceiros a ser usado pela plataforma de destino. Isso dá aos usuários a capacidade de mapear atributos de perfil da Platform para campos específicos que sua plataforma de destino reconhece, tudo dentro da interface do usuário da plataforma.

Ao configurar o schema do parceiro para seu destino, você pode ajustar o mapeamento de campo suportado pela plataforma de destino, como:

* Permitir que os usuários mapeiem um `phoneNumber` Atributo XDM a um `phone` atributo suportado pela plataforma de destino.
* Crie esquemas de parceiros dinâmicos que o Experience Platform pode chamar dinamicamente para recuperar uma lista de todos os atributos suportados no destino.
* Defina os mapeamentos de campo obrigatórios necessários para a plataforma de destino.

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama no [opções de configuração](../configuration-options.md) ou consulte o guia sobre como [use o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

É possível definir as configurações do esquema por meio da variável `/authoring/destinations` endpoint . Consulte as páginas de referência da API a seguir para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Atualizar uma configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artigo descreve todas as opções de configuração de esquema compatíveis que podem ser usadas para o seu destino e mostra o que os clientes verão na interface do usuário da plataforma.

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações oferecem suporte à funcionalidade descrita nesta página.

| Tipo de integração | Oferece suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (em lote) | Sim |

## Configuração de esquema compatível {#supported-schema-types}

O Destination SDK suporta várias configurações de esquema:

* Os esquemas estáticos são definidos por meio da variável `profileFields` no `schemaConfig` seção. Em um schema estático, você define cada atributo de target que deve ser mostrado na interface do usuário do Experience Platform no `profileFields` matriz. Se precisar atualizar o esquema, [atualizar a configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md).
* Os esquemas dinâmicos usam um tipo de servidor de destino adicional, chamado de [servidor de esquema dinâmico](../../authoring-api/destination-server/create-destination-server.md), para gerar esquemas dinamicamente com base em sua própria API. Os esquemas dinâmicos não usam o `profileFields` matriz. Se precisar atualizar o esquema, não é necessário [atualizar a configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md). Em vez disso, o servidor de esquema dinâmico recupera o esquema atualizado da sua API.
* Na configuração do schema, você tem a opção de adicionar mapeamentos necessários (ou predefinidos). Esses são mapeamentos que os usuários podem visualizar na interface do usuário da plataforma, mas que não podem modificá-los ao configurar uma conexão com seu destino. Por exemplo, você pode impor o campo de endereço de email a ser sempre enviado para o destino.

O `schemaConfig` A seção usa vários parâmetros de configuração, dependendo do tipo de schema necessário, conforme mostrado nas seções abaixo.

## Criar um esquema estático {#attributes-schema}

Para criar um schema estático com atributos de perfil, defina os atributos de target no `profileFields` conforme mostrado abaixo.

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
      "identityRequired":true
}
```

| Parâmetro | Tipo | Obrigatório / Opcional | Descrição |
|---------|----------|------|---|
| `profileFields` | Matriz | Opcional | Define a matriz de atributos de destino aceitos pela sua plataforma de destino para a qual os clientes podem mapear seus atributos de perfil. Ao usar um `profileFields` matriz, você pode omitir a variável `useCustomerSchemaForAttributeMapping` totalmente. |
| `useCustomerSchemaForAttributeMapping` | Booleano | Opcional | Ativa ou desativa o mapeamento de atributos do schema do cliente para os atributos que você define na variável `profileFields` matriz. <ul><li>Se estiver definido como `true`, os usuários só veem a coluna de origem no campo de mapeamento. `profileFields` não são aplicáveis neste caso.</li><li>Se estiver definido como `false`, os usuários podem mapear atributos de origem de seu esquema para os atributos definidos na variável `profileFields` matriz.</li></ul> O valor padrão é `false`. |
| `profileRequired` | Booleano | Opcional | Use `true` se os usuários forem capazes de mapear atributos de perfil do Experience Platform para atributos personalizados na plataforma de destino. |
| `segmentRequired` | Booleano | Obrigatório | Esse parâmetro é exigido pelo Destination SDK e deve sempre ser definido como `true`. |
| `identityRequired` | Booleano | Obrigatório | Defina como `true` se os usuários devem ser capazes de mapear [tipos de identidade](identity-namespace-configuration.md) do Experience Platform para os atributos definidos na variável `profileFields` array . |

{style="table-layout:auto"}

A experiência resultante da interface do usuário é mostrada nas imagens abaixo.

Quando os usuários selecionam o target mapping, eles podem ver os campos definidos na variável `profileFields` matriz.

![Imagem da interface do usuário que mostra a tela de atributos de destino.](../../assets/functionality/destination-configuration/select-attributes.png)

Após selecionar os atributos, eles podem vê-los na coluna de campo de destino.

![Imagem da interface do usuário mostrando um esquema de destino estático com atributos](../../assets/functionality/destination-configuration/static-schema-attributes.png)

## Criar um esquema dinâmico {#dynamic-schema-configuration}

O Destination SDK suporta a criação de esquemas de parceiros dinâmicos. Ao contrário de um schema estático, um schema dinâmico não usa um `profileFields` matriz. Em vez disso, os esquemas dinâmicos usam um servidor de esquema dinâmico que se conecta à sua própria API de onde recupera a configuração do esquema.

>[!IMPORTANT]
>
>Antes de criar um esquema dinâmico, é necessário [criar um servidor de esquema dinâmico](../../authoring-api/destination-server/create-destination-server.md).

Em uma configuração de esquema dinâmico, a variável `profileFields` é substituída pela variável `dynamicSchemaConfig` conforme mostrado abaixo.

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
| `dynamicEnum.authenticationRule` | String | Obrigatório | Indica como [!DNL Platform] Os clientes do se conectam ao seu destino. Os valores aceitos são `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Use `CUSTOMER_AUTHENTICATION` se os clientes da Platform fizerem logon em seu sistema por meio de qualquer um dos métodos de autenticação descritos [here](customer-authentication.md). </li><li> Use `PLATFORM_AUTHENTICATION` se houver um sistema de autenticação global entre o Adobe e seu destino e o [!DNL Platform] o cliente não precisa fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve [criar um objeto de credenciais](../../credentials-api/create-credential-configuration.md) usando a API de credenciais. </li><li>Use `NONE` se nenhuma autenticação for necessária para enviar dados para a plataforma de destino. </li></ul> |
| `dynamicEnum.destinationServerId` | String | Obrigatório | O `instanceId` do servidor de esquema dinâmico. Esse servidor de destino inclui o ponto de extremidade da API que o Experience Platform chamará para recuperar o esquema dinâmico. |
| `dynamicEnum.value` | String | Obrigatório | O nome do schema dinâmico, conforme definido na configuração do servidor de esquema dinâmico. |
| `dynamicEnum.responseFormat` | String | Obrigatório | Sempre defina como `SCHEMA` ao definir um esquema dinâmico. |
| `profileRequired` | Booleano | Opcional | Use `true` se os usuários forem capazes de mapear atributos de perfil do Experience Platform para atributos personalizados na plataforma de destino. |
| `segmentRequired` | Booleano | Obrigatório | Esse parâmetro é exigido pelo Destination SDK e deve sempre ser definido como `true`. |
| `identityRequired` | Booleano | Obrigatório | Defina como `true` se os usuários devem ser capazes de mapear [tipos de identidade](identity-namespace-configuration.md) do Experience Platform para os atributos definidos na variável `profileFields` array . |

{style="table-layout:auto"}

## Mapeamentos necessários {#required-mappings}

Na configuração do esquema, além do esquema estático ou dinâmico, você tem a opção de adicionar mapeamentos necessários (ou predefinidos). Esses são mapeamentos que os usuários podem visualizar na interface do usuário da plataforma, mas que não podem modificá-los ao configurar uma conexão com seu destino.

Por exemplo, você pode impor o campo de endereço de email a ser sempre enviado para o destino.

>[!NOTE]
>
>Atualmente, as seguintes combinações de mapeamentos necessários são suportadas:
>* Você pode configurar um campo de origem obrigatório e um campo de destino obrigatório. Nesse caso, os usuários não podem editar ou selecionar nenhum dos dois campos e só podem exibir a seleção.
>* Você pode configurar apenas um campo de destino obrigatório. Nesse caso, os usuários poderão selecionar um campo de origem para mapear para o destino.
>
> A configuração de apenas um campo de origem obrigatório está atualmente *not* suportado.

Veja abaixo dois exemplos de uma configuração de esquema com mapeamentos necessários e como eles se parecem na etapa de mapeamento da variável [fluxo de trabalho ativar dados para destinos em lote](../../../ui/activate-batch-profile-destinations.md).


>[!BEGINTABS]

>[!TAB Mapeamentos de origem e de destino necessários]

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
| `requiredMappings.sourceType` | String | Obrigatório | Indica o tipo de `source` campo. Valores compatíveis: <ul><li>`text/x.schema-path`: Use esse valor quando a variável `source` é um atributo de perfil de um esquema XDM.</li><li>`text/x.aep-xl`: Use esse valor ao `source` é definido por uma expressão regular. Exemplo: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`</li><li>`text/plain`: Use esse valor ao `source` é definido por um modelo de macro. Atualmente, o único modelo de macro compatível é `metadata.segment.alias`.</li></ul> |
| `requiredMappings.source` | String | Obrigatório | Indica o valor do campo de origem. Tipos de valor compatíveis: <ul><li>Atributos de perfil XDM. Exemplo: `personalEmail.address`. Quando o atributo de origem for um atributo de perfil XDM, defina a variável `sourceType` para `text/x.schema-path`.</li><li>Expressões regulares. Exemplo: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`. Quando o atributo de origem for uma expressão regular, defina a variável `sourceType` para `text/x.aep-xl`.</li><li>Modelos de macro. Exemplo:`metadata.segment.alias`. Quando o atributo de origem for um modelo de macro, defina a variável `sourceType` para `text/plain`. Atualmente, o único modelo de macro compatível é `metadata.segment.alias`.</li></ul> |
| `requiredMappings.destination` | String | Obrigatório | Indica o valor do campo de destino. Quando os campos de origem e de destino são especificados como mapeamentos obrigatórios, os usuários não podem selecionar ou editar nenhum dos dois campos e só podem exibir a seleção. |

{style="table-layout:auto"}

Como resultado, ambas as variáveis **[!UICONTROL Campo de origem]** e **[!UICONTROL Campo de destino]** Na interface do usuário da plataforma, as seções estão esmaecidas.

![Imagem dos mapeamentos necessários no fluxo de ativação da interface do usuário.](../../assets/functionality/destination-configuration/required-mappings-2.png)

>[!TAB Mapeamento de destino necessário]

O exemplo abaixo mostra um mapeamento de destino necessário. Se somente o campo de destino for especificado como obrigatório, os usuários poderão selecionar o campo de origem para mapear para ele.

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
| `requiredMappings.destination` | String | Obrigatório | Indica o valor do campo de destino. Quando apenas o campo de destino for especificado, os usuários poderão selecionar um campo de origem para mapear para o destino. |
| `mandatoryRequired` | Booleano | Opcional | Indica se o mapeamento deve ser marcado como um [atributo obrigatório](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `primaryKeyRequired` | Booleano | Opcional | Indica se o mapeamento deve ser marcado como um [chave de desduplicação](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |

{style="table-layout:auto"}

Como resultado, a variável **[!UICONTROL Campo de destino]** na interface do usuário da plataforma fica acinzentada, enquanto a variável **[!UICONTROL Campo de origem]** está ativa e os usuários podem interagir com ela. O **[!UICONTROL Chave obrigatória]** e **[!UICONTROL Chave de desduplicação]** As opções estão ativas e os usuários não podem alterá-las.

![Imagem dos mapeamentos necessários no fluxo de ativação da interface do usuário.](../../assets/functionality/destination-configuration/required-mappings-1.png)

>[!ENDTABS]

## Próximas etapas {#next-steps}

Após a leitura deste artigo, você deve ter uma melhor compreensão de quais tipos de esquema são aceitos pelo Destination SDK e como pode configurar seu esquema.

Para saber mais sobre os outros componentes de destino, consulte os seguintes artigos:

* [Autenticação do cliente](customer-authentication.md)
* [Autenticação OAuth2](oauth2-authentication.md)
* [Atributos da interface do usuário](ui-attributes.md)
* [Campos de dados do cliente](customer-data-fields.md)
* [Configuração do namespace de identidade](identity-namespace-configuration.md)
* [Configurações de mapeamento suportadas](supported-mapping-configurations.md)
* [Delivery de destino](destination-delivery.md)
* [Configuração de metadados de público-alvo](audience-metadata-configuration.md)
* [Política de agregação](aggregation-policy.md)
* [Configuração em lote](batch-configuration.md)
* [Qualificações de perfil histórico](historical-profile-qualifications.md)