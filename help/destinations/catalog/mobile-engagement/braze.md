---
keywords: móvel; brasa; Mensagens;
title: Ligação de brasa
description: O Brasil é uma plataforma abrangente de engajamento do cliente que possibilita experiências relevantes e memoráveis entre os clientes e as marcas que eles adoram.
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 2%

---

# (Beta) [!DNL Braze] conexão

>[!IMPORTANT]
>
>O destino da brasileira no Adobe Experience Platform está atualmente na versão beta. A documentação e a funcionalidade estão sujeitas a alterações.

## Visão geral {#overview}

O destino [!DNL Braze] ajuda a enviar os dados do perfil para [!DNL Braze].

[!DNL Braze] é uma plataforma abrangente de engajamento do cliente que possibilita experiências relevantes e memoráveis entre os clientes e as marcas que eles adoram.

Para enviar dados de perfil para [!DNL Braze], primeiro você deve se conectar ao destino.

## Especificações do destino {#specifics}

Observe os seguintes detalhes que são específicos ao destino [!DNL Braze]:

* [!DNL Adobe Experience Platform] segmentos são exportados para o  [!DNL Braze] sob o  `AdobeExperiencePlatformSegments` atributo .

>[!NOTE]
>
>Lembre-se de que o envio de atributos personalizados adicionais para [!DNL Braze] pode causar aumento no consumo de [!DNL Braze] ponto de dados. Consulte seu [!DNL Braze] gerente de conta antes de enviar atributos personalizados adicionais.

## Casos de uso {#use-cases}

Como comerciante, desejo direcionar usuários em um destino de envolvimento móvel, com segmentos criados em [!DNL Adobe Experience Platform]. Além disso, desejo fornecer experiências personalizadas a elas, com base em atributos de seus perfis [!DNL Adobe Experience Platform], assim que os segmentos e perfis forem atualizados em [!DNL Adobe Experience Platform].

## Identidades suportadas {#supported-identities}

[!DNL Braze] O suporta a ativação de identidades descritas na tabela abaixo.

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| external_id | Identificador [!DNL Braze] personalizado que suporta o mapeamento de qualquer identidade. | Você pode enviar qualquer [identidade](../../../identity-service/namespaces.md) para o destino [!DNL Braze], desde que mapeie-o para [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

## Tipo de exportação {#export-type}

**[!DNL Profile-based]** - estiver exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome) e/ou identidades, de acordo com o mapeamento de campo.
[!DNL Adobe Experience Platform] segmentos são exportados para o  [!DNL Braze] sob o  `AdobeExperiencePlatformSegments` atributo .

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Enquanto [configurar](../../ui/connect-destination.md) esse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Token]** da conta do Brasil: Essa é a sua  [!DNL Braze] [!DNL API] chave. Você pode encontrar instruções detalhadas sobre como obter sua chave [!DNL API] aqui: [Visão geral da chave da API REST](https://www.braze.com/docs/api/api_key/).
* **[!UICONTROL Nome]**: insira um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: insira uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL Instância]** do ponto de extremidade: pergunte ao seu  [!DNL Braze] representante qual instância de ponto de extremidade você deve usar.

## Ativar segmentos para este destino {#activate}

Consulte [Ativar perfis e segmentos para um destino](../../ui/activate-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para destinos.

## Considerações de mapeamento {#mapping-considerations}

Para enviar corretamente os dados do público-alvo de [!DNL Adobe Experience Platform] para o destino [!DNL Braze], é necessário percorrer a etapa de mapeamento de campo.

O mapeamento consiste em criar um link entre os campos do esquema [!DNL Experience Data Model] (XDM) na conta [!DNL Platform] e os equivalentes correspondentes do destino.

Para mapear corretamente os campos XDM para os campos de destino [!DNL Braze], siga estas etapas:

Na etapa [!UICONTROL Mapeamento], clique em **[!UICONTROL Adicionar novo mapeamento]**.

![Mapeamento de adição de destino de site](../../assets/catalog/mobile-engagement/braze/mapping.png)

Na seção [!UICONTROL Source Field], clique no botão de seta ao lado do campo vazio.

![Mapeamento de Origem de Destino Brasileiro](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

Na janela [!UICONTROL Select source field], você pode escolher entre duas categorias de campos XDM:
* [!UICONTROL Selecionar atributos]: use essa opção para mapear um campo específico do esquema XDM para um  [!DNL Braze] atributo.

![Atributo da Fonte de Mapeamento de Destino Brasileiro](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Selecionar namespace] de identidade: Use esta opção para mapear um namespace de  [!DNL Platform] identidade para um  [!DNL Braze] namespace.

![Namespace da Fonte do Mapeamento de Destino Brasileiro](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Escolha o campo de origem e clique em **[!UICONTROL Select]**.

Na seção [!UICONTROL Campo de destino], clique no ícone de mapeamento à direita do campo.

![Mapeamento de Destino da Brasileira](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

Na janela [!UICONTROL Select target field], é possível escolher entre três categorias de campos de destino:
* [!UICONTROL Selecionar atributos]: Use essa opção para mapear os atributos XDM para  [!DNL Braze] atributos padrão.
* [!UICONTROL Selecionar namespace] de identidade: Use esta opção para mapear namespaces de  [!DNL Platform] identidade para namespaces de  [!DNL Braze] identidade.
* [!UICONTROL Selecionar atributos] personalizados: Use esta opção para mapear atributos XDM para  [!DNL Braze] atributos personalizados que você definiu em sua  [!DNL Braze] conta.
* Também é possível usar essa opção para renomear atributos XDM existentes em [!DNL Braze]. Por exemplo, mapear um atributo `lastName` XDM para um atributo `Last_Name` personalizado em [!DNL Braze], criará o atributo `Last_Name` em [!DNL Braze], se ele ainda não existir, e mapeará o atributo `lastName` XDM para ele.

![Campos de mapeamento de destino do site](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Escolha o campo de destino e clique em **[!UICONTROL Select]**.

Agora, você deve ver o mapeamento de campo na lista.

![Mapeamento de Destino de Brasileira Concluído](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Para adicionar mais mapeamentos, repita as etapas anteriores.

## Exemplo de mapeamento {#mapping-example}

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
