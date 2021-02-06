---
keywords: móvel; brasa; Mensagens;
title: Destino da conexão Braze
description: O Brasil é uma plataforma abrangente de envolvimento do cliente que potencializa experiências relevantes e memoráveis entre os clientes e as marcas que eles adoram.
translation-type: tm+mt
source-git-commit: f4095a90ff70e8d054bae4f3b0f884552ffd30df
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 1%

---


# (Beta) [!DNL Braze] conexão

>[!IMPORTANT]
>
>O destino brasileiro no Adobe Experience Platform está atualmente em Beta. A documentação e a funcionalidade estão sujeitas a alterações.

O destino [!DNL Braze] ajuda a enviar dados de perfil para [!DNL Braze].

[!DNL Braze] é uma plataforma abrangente de envolvimento do cliente que fornece experiências relevantes e memoráveis entre os clientes e as marcas que eles adoram.

Para enviar dados de perfil para [!DNL Braze], primeiro conecte-se ao destino.

## Especificações de destino {#destination-specs}

Observe os seguintes detalhes específicos do destino [!DNL Braze]:

* Você pode enviar qualquer [identidade](../../../identity-service/namespaces.md) para o destino [!DNL Braze], desde que mapeie-o para [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation).
* [!DNL Adobe Experience Platform] segmentos são exportados para  [!DNL Braze] sob o  `AdobeExperiencePlatformSegments` atributo.

>[!NOTE]
>
>Lembre-se de que o envio de atributos personalizados adicionais para [!DNL Braze] pode causar aumento no consumo de [!DNL Braze] ponto de dados. Consulte seu [!DNL Braze] gerente de conta antes de enviar atributos personalizados adicionais.

## Casos de uso {#use-cases}

Como comerciante, quero público alvo os usuários em um destino de envolvimento móvel, com segmentos criados [!DNL Adobe Experience Platform]. Além disso, desejo fornecer experiências personalizadas a elas, com base em atributos de seus perfis [!DNL Adobe Experience Platform], assim que os segmentos e perfis forem atualizados em [!DNL Adobe Experience Platform].

## Tipo de exportação {#export-type}

**[!DNL Profile-based]** - você está exportando todos os membros de um segmento, juntamente com os campos de schema desejados (por exemplo: endereço de email, número de telefone, sobrenome) e/ou identidades, de acordo com o mapeamento de campo.
[!DNL Adobe Experience Platform] segmentos são exportados para  [!DNL Braze] sob o  `AdobeExperiencePlatformSegments` atributo.


## Conectar ao destino {#connect-destination}

Em **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]**, selecione [!DNL Braze] e **[!UICONTROL Configurar]**.

![Configurar Destino do Brasil](../../assets/catalog/mobile-engagement/braze/configure.png)

>[!NOTE]
>
>Se já existir uma conexão com esse destino, você poderá ver um botão **[!UICONTROL Ativar]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Ativate]** e **[!UICONTROL Configure]**, consulte a seção [Catalog](../../ui/destinations-workspace.md#catalog) da documentação da área de trabalho de destino.
>
>![Ativar Destino do Brasil](../../assets/catalog/mobile-engagement/braze/activate.png)

Na etapa [!UICONTROL Account], é necessário fornecer o token da conta [!DNL Braze]. Esta é sua chave [!DNL Braze] [!DNL API]. Você pode encontrar instruções detalhadas sobre como obter sua chave [!DNL API] aqui: [Visão geral da chave da API REST](https://www.braze.com/docs/api/api_key/). Digite o token e clique em **[!UICONTROL Conectar ao destino]**.

![Etapa da Conta de Destino Brasileira](../../assets/catalog/mobile-engagement/braze/account.png)

Clique em **[!UICONTROL Próximo]**. Na etapa [!UICONTROL Authentication], é necessário inserir os detalhes da conexão [!DNL Braze]:
* **[!UICONTROL Nome]**: insira um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: insira uma descrição que o ajudará a identificar esse destino no futuro.
* **[!UICONTROL Instância]** do Ponto de Extremidade: pergunte ao seu  [!DNL Braze] representante qual instância de endpoint você deve usar.
* **[!UICONTROL Caso]** de uso de marketing: os casos de uso de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar de casos de uso de marketing definidos pelo Adobe ou criar seu próprio caso de uso de marketing. Para obter mais informações sobre casos de uso de marketing, consulte a página [Data Governance no Adobe Experience Platform](../../../data-governance/policies/overview.md). Para obter informações sobre casos individuais de uso de marketing definidos pelo Adobe, consulte [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

![Etapa de autenticação do site](../../assets/catalog/mobile-engagement/braze/authentication.png)

Clique em **[!UICONTROL Criar destino]**. Seu destino agora é criado. Você pode clicar em **[!UICONTROL Salvar e Sair]** se quiser ativar segmentos posteriormente, ou selecionar **[!UICONTROL Próximo]** para continuar o fluxo de trabalho e selecionar segmentos para ativação. Em ambos os casos, consulte a próxima seção, [Ativar segmentos](#activate-segments), para o restante do fluxo de trabalho.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](../../ui/activate-destinations.md#select-attributes) para obter informações sobre o fluxo de trabalho da ativação de segmentos.

## Mapeamento de campos {#field-mapping}

Para enviar corretamente seus dados de audiência de [!DNL Adobe Experience Platform] para o destino [!DNL Braze], é necessário percorrer a etapa de mapeamento de campo.

O mapeamento consiste em criar um link entre os campos do schema [!DNL Experience Data Model] (XDM) na conta [!DNL Platform] e seus equivalentes correspondentes do destino do público alvo.

Para mapear corretamente seus campos XDM para os campos de destino [!DNL Braze], siga estas etapas:

Na etapa [!UICONTROL Mapeamento], clique em **[!UICONTROL Adicionar novo mapeamento]**.

![Mapeamento de adição de destino de brasileiro](../../assets/catalog/mobile-engagement/braze/mapping.png)

Na seção [!UICONTROL Campo de origem], clique no botão de seta ao lado do campo vazio.

![Mapeamento de origem de destino do Brasil](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

Na janela [!UICONTROL Selecionar campo de origem], você pode escolher entre duas categorias de campos XDM:
* [!UICONTROL Selecionar atributos]: use essa opção para mapear um campo específico do seu schema XDM para um  [!DNL Braze] atributo.

![Atributo de Origem do Mapeamento de Destino Brasileiro](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Selecionar namespace] de identidade: Use esta opção para mapear uma namespace de  [!DNL Platform] identidade para uma  [!DNL Braze] namespace.

![Namespace de Origem do Mapeamento de Destino Brasileiro](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Escolha o campo de origem e clique em **[!UICONTROL Selecionar]**.

Na seção [!UICONTROL Campo de Público alvo], clique no ícone de mapeamento à direita do campo.

![Target mapping de Destino Brasileiro](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

Na janela [!UICONTROL Selecionar campo de público alvo], você pode escolher entre três categorias de campos de público alvo:
* [!UICONTROL Selecionar atributos]: Use essa opção para mapear seus atributos XDM para  [!DNL Braze] atributos padrão.
* [!UICONTROL Selecionar namespace] de identidade: Use esta opção para mapear namespaces  [!DNL Platform] de identidade para namespaces  [!DNL Braze] de identidade.
* [!UICONTROL Selecionar atributos] personalizados: Use essa opção para mapear atributos XDM para  [!DNL Braze] atributos personalizados que você definiu em sua  [!DNL Braze] conta.
* Você também pode usar essa opção para renomear atributos XDM existentes em [!DNL Braze]. Por exemplo, o mapeamento de um atributo `lastName` XDM para um atributo `Last_Name` personalizado em [!DNL Braze] criará o atributo `Last_Name` em [!DNL Braze], caso ele ainda não exista, e mapeará o atributo `lastName` XDM para ele.

![Campos de Target mapping de Destino Brasileiro](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Escolha o campo público alvo e clique em **[!UICONTROL Selecionar]**.

Agora você deve ver o mapeamento de campo na lista.

![Mapeamento de Destino da Brasileira Concluído](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Para adicionar mais mapeamentos, repita as etapas anteriores.

### Exemplo {#mapping-example}

Digamos que seu schema de perfil XDM e sua instância [!DNL Braze] contenham os seguintes atributos e identidades:

|  | Schema de Perfil XDM | [!DNL Braze] Instância |
|---|---|---|
| Atributos | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>PhoneNumber</code></li></ul> |
| Identidades | <ul><li>Email</code></li><li>ID de anúncio do Google (GAID)</code></li><li>ID da Apple para anunciantes (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

O mapeamento correto seria semelhante a:

![Exemplo de mapeamento de destino do Brasil](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para o destino [!DNL Braze], verifique sua conta [!DNL Braze]. [!DNL Adobe Experience Platform] segmentos são exportados para  [!DNL Braze] sob o  `AdobeExperiencePlatformSegments` atributo.

## Uso e controle de dados {#data-usage-governance}

Todos os destinos [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral do controle de dados](../../../data-governance/home.md).

