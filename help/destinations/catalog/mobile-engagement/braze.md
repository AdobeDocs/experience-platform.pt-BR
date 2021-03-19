---
keywords: móvel; brasa; Mensagens;
title: Ligação de brasa
description: O Brasil é uma plataforma abrangente de engajamento do cliente que possibilita experiências relevantes e memoráveis entre os clientes e as marcas que eles adoram.
translation-type: tm+mt
source-git-commit: 0759919dc458798ca4bc5f233a9cb319194ea534
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 2%

---


# (Beta) [!DNL Braze] conexão

>[!IMPORTANT]
>
>O destino da brasileira no Adobe Experience Platform está atualmente na versão beta. A documentação e a funcionalidade estão sujeitas a alterações.

O destino [!DNL Braze] ajuda a enviar os dados do perfil para [!DNL Braze].

[!DNL Braze] é uma plataforma abrangente de engajamento do cliente que possibilita experiências relevantes e memoráveis entre os clientes e as marcas que eles adoram.

Para enviar dados de perfil para [!DNL Braze], primeiro você deve se conectar ao destino.

## Especificações de destino {#destination-specs}

Observe os seguintes detalhes que são específicos ao destino [!DNL Braze]:

* [!DNL Adobe Experience Platform] segmentos são exportados para o  [!DNL Braze] sob o  `AdobeExperiencePlatformSegments` atributo .

>[!NOTE]
>
>Lembre-se de que o envio de atributos personalizados adicionais para [!DNL Braze] pode causar aumento no consumo de [!DNL Braze] ponto de dados. Consulte seu [!DNL Braze] gerente de conta antes de enviar atributos personalizados adicionais.

## Casos de uso {#use-cases}

Como comerciante, desejo direcionar usuários em um destino de envolvimento móvel, com segmentos criados em [!DNL Adobe Experience Platform]. Além disso, desejo fornecer experiências personalizadas a elas, com base em atributos de seus perfis [!DNL Adobe Experience Platform], assim que os segmentos e perfis forem atualizados em [!DNL Adobe Experience Platform].

### Identidades suportadas {#supported-identities}

[!DNL Google Ad Manager] O suporta a ativação de identidades descritas na tabela abaixo.

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| external_id | Identificador [!DNL Braze] personalizado que suporta o mapeamento de qualquer identidade. | Você pode enviar qualquer [identidade](../../../identity-service/namespaces.md) para o destino [!DNL Braze], desde que mapeie-o para [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

## Tipo de exportação {#export-type}

**[!DNL Profile-based]** - estiver exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome) e/ou identidades, de acordo com o mapeamento de campo.
[!DNL Adobe Experience Platform] segmentos são exportados para o  [!DNL Braze] sob o  `AdobeExperiencePlatformSegments` atributo .


## Conecte-se ao destino {#connect-destination}

Em **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selecione [!DNL Braze] e selecione **[!UICONTROL Configure]**.

![Configurar Destino da Brasileira](../../assets/catalog/mobile-engagement/braze/configure.png)

>[!NOTE]
>
>Se uma conexão com esse destino já existir, você poderá ver um botão **[!UICONTROL Activate]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consulte a seção [Catálogo](../../ui/destinations-workspace.md#catalog) da documentação do espaço de trabalho de destino.
>
>![Ativar Destino da Brasileira](../../assets/catalog/mobile-engagement/braze/activate.png)

Na etapa [!UICONTROL Account], é necessário fornecer o token de conta [!DNL Braze]. Esta é sua chave [!DNL Braze] [!DNL API]. Você pode encontrar instruções detalhadas sobre como obter sua chave [!DNL API] aqui: [Visão geral da chave da API REST](https://www.braze.com/docs/api/api_key/). Insira o token e clique em **[!UICONTROL Connect to destination]**.

![Etapa da Conta de Destino Brasileira](../../assets/catalog/mobile-engagement/braze/account.png)

Clique em **[!UICONTROL Next]**. Na etapa [!UICONTROL Authentication], é necessário inserir os detalhes da conexão [!DNL Braze]:
* **[!UICONTROL Name]**: insira um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Description]**: insira uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL Endpoint Instance]**: pergunte ao seu  [!DNL Braze] representante qual instância de ponto de extremidade você deve usar.
* **[!UICONTROL Marketing action]**: as ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte a página [Governança de dados no Adobe Experience Platform](../../../data-governance/policies/overview.md) . Para obter informações sobre as ações de marketing individuais definidas pelo Adobe, consulte a [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

![Etapa de Autenticação Brasileira](../../assets/catalog/mobile-engagement/braze/authentication.png)

Clique em **[!UICONTROL Create destination]**. Seu destino foi criado. Você pode clicar em **[!UICONTROL Save & Exit]** se desejar ativar segmentos posteriormente, ou selecionar **[!UICONTROL Next]** para continuar o fluxo de trabalho e selecionar segmentos para ativar. Em ambos os casos, consulte a próxima seção, [Ativar segmentos](#activate-segments), para o restante do fluxo de trabalho.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos para um destino](../../ui/activate-destinations.md#select-attributes) para obter informações sobre o fluxo de trabalho de ativação de segmentos.

## Mapeamento de campo {#field-mapping}

Para enviar corretamente os dados do público-alvo de [!DNL Adobe Experience Platform] para o destino [!DNL Braze], é necessário percorrer a etapa de mapeamento de campo.

O mapeamento consiste em criar um link entre os campos do esquema [!DNL Experience Data Model] (XDM) na conta [!DNL Platform] e os equivalentes correspondentes do destino.

Para mapear corretamente os campos XDM para os campos de destino [!DNL Braze], siga estas etapas:

Na etapa [!UICONTROL Mapping], clique em **[!UICONTROL Add new mapping]**.

![Mapeamento de adição de destino de site](../../assets/catalog/mobile-engagement/braze/mapping.png)

Na seção [!UICONTROL Source Field], clique no botão de seta ao lado do campo vazio.

![Mapeamento de Origem de Destino Brasileiro](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

Na janela [!UICONTROL Select source field], é possível escolher entre duas categorias de campos XDM:
* [!UICONTROL Select attributes]: use essa opção para mapear um campo específico do esquema XDM para um  [!DNL Braze] atributo.

![Atributo da Fonte de Mapeamento de Destino Brasileiro](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Select identity namespace]: Use esta opção para mapear um namespace de  [!DNL Platform] identidade para um  [!DNL Braze] namespace.

![Namespace da Fonte do Mapeamento de Destino Brasileiro](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Escolha o campo de origem e clique em **[!UICONTROL Select]**.

Na seção [!UICONTROL Target Field], clique no ícone de mapeamento à direita do campo.

![Mapeamento de Destino da Brasileira](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

Na janela [!UICONTROL Select target field], é possível escolher entre três categorias de campos de destino:
* [!UICONTROL Select attributes]: Use essa opção para mapear os atributos XDM para  [!DNL Braze] atributos padrão.
* [!UICONTROL Select identity namespace]: Use esta opção para mapear namespaces de  [!DNL Platform] identidade para namespaces de  [!DNL Braze] identidade.
* [!UICONTROL Select custom attributes]: Use esta opção para mapear atributos XDM para  [!DNL Braze] atributos personalizados que você definiu em sua  [!DNL Braze] conta.
* Também é possível usar essa opção para renomear atributos XDM existentes em [!DNL Braze]. Por exemplo, mapear um atributo `lastName` XDM para um atributo `Last_Name` personalizado em [!DNL Braze], criará o atributo `Last_Name` em [!DNL Braze], se ele ainda não existir, e mapeará o atributo `lastName` XDM para ele.

![Campos de mapeamento de destino do site](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Escolha o campo de destino e clique em **[!UICONTROL Select]**.

Agora, você deve ver o mapeamento de campo na lista.

![Mapeamento de Destino de Brasileira Concluído](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Para adicionar mais mapeamentos, repita as etapas anteriores.

### Exemplo {#mapping-example}

Digamos que seu esquema de perfil XDM e sua instância [!DNL Braze] contenham os seguintes atributos e identidades:

|  | Esquema de perfil do XDM | [!DNL Braze] Instância |
|---|---|---|
| Atributos | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>PhoneNumber</code></li></ul> |
| Identidades | <ul><li>Email</code></li><li>ID de anúncio do Google (GAID)</code></li><li>Apple ID para anunciantes (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

O mapeamento correto seria semelhante a:

![Exemplo de mapeamento de destino de site](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para o destino [!DNL Braze], verifique sua conta [!DNL Braze]. [!DNL Adobe Experience Platform] segmentos são exportados para o  [!DNL Braze] sob o  `AdobeExperiencePlatformSegments` atributo .

## Uso e governança de dados {#data-usage-governance}

Todos os destinos [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](../../../data-governance/home.md).

