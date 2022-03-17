---
keywords: móvel; brasa; Mensagens;
title: Ligação de brasa
description: O Brasil é uma plataforma abrangente de engajamento do cliente que possibilita experiências relevantes e memoráveis entre os clientes e as marcas que eles adoram.
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: c5d2427635d90f3a9551e2a395d01d664005e8bc
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 2%

---

# [!DNL Braze] conexão

## Visão geral {#overview}

O [!DNL Braze] O destino ajuda a enviar dados de perfil para o [!DNL Braze].

[!DNL Braze] é uma plataforma abrangente de engajamento do cliente que possibilita experiências relevantes e memoráveis entre os clientes e as marcas que eles adoram.

Para enviar dados de perfil para o [!DNL Braze], primeiro você deve se conectar ao destino.

## Especificações do destino {#specifics}

Observe os detalhes a seguir que são específicos da variável [!DNL Braze] destino:

* [!DNL Adobe Experience Platform] segmentos são exportados para [!DNL Braze] nos termos do `AdobeExperiencePlatformSegments` atributo.

>[!NOTE]
>
>Lembre-se de enviar atributos personalizados adicionais para [!DNL Braze] pode causar aumento na [!DNL Braze] consumo de ponto de dados. Consulte seu [!DNL Braze] gerente de conta antes de enviar atributos personalizados adicionais.

## Casos de uso {#use-cases}

Como profissional de marketing, desejo direcionar usuários em um destino de envolvimento móvel, com segmentos incorporados [!DNL Adobe Experience Platform]. Além disso, quero oferecer experiências personalizadas a elas, com base em atributos de seus [!DNL Adobe Experience Platform] assim que os segmentos e perfis forem atualizados em [!DNL Adobe Experience Platform].

## Identidades suportadas {#supported-identities}

[!DNL Braze] O suporta a ativação de identidades descritas na tabela abaixo.

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| external_id | Personalizado [!DNL Braze] identificador que suporta o mapeamento de qualquer identidade. | Você pode enviar qualquer [identidade](../../../identity-service/namespaces.md) para [!DNL Braze] destino, desde que você o mapeie para a variável [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome) e/ou identidades, de acordo com o mapeamento de campo.[!DNL Adobe Experience Platform] segmentos são exportados para [!DNL Braze] nos termos do `AdobeExperiencePlatformSegments` atributo. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* **[!UICONTROL Token de conta do Brasil]**: Este é o seu [!DNL Braze] [!DNL API] chave. Você pode encontrar instruções detalhadas sobre como obter seu [!DNL API] Chave aqui: [Visão geral da chave de API REST](https://www.braze.com/docs/api/api_key/).
* **[!UICONTROL Nome]**: insira um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: insira uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL Instância do ponto de extremidade]**: pergunte ao seu [!DNL Braze] representante de qual instância de ponto de extremidade você deve usar.

## Ativar segmentos para este destino {#activate}

Consulte [Ativar os dados do público-alvo para os destinos de exportação do segmento de fluxo](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Considerações de mapeamento {#mapping-considerations}

Para enviar corretamente os dados de público-alvo do [!DNL Adobe Experience Platform] para [!DNL Braze] , é necessário percorrer a etapa de mapeamento de campo .

O mapeamento consiste na criação de um link entre os [!DNL Experience Data Model] (XDM) campos do esquema no [!DNL Platform] e seus equivalentes correspondentes do destino-alvo.

Para mapear corretamente os campos XDM para a variável [!DNL Braze] campos de destino, siga estas etapas:

No [!UICONTROL Mapeamento] etapa , clique em **[!UICONTROL Adicionar novo mapeamento]**.

![Mapeamento de adição de destino de site](../../assets/catalog/mobile-engagement/braze/mapping.png)

No [!UICONTROL Campo de origem] , clique no botão de seta ao lado do campo vazio.

![Mapeamento de Origem de Destino Brasileiro](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

No [!UICONTROL Selecionar campo de origem] você pode escolher entre duas categorias de campos XDM:
* [!UICONTROL Selecionar atributos]: use esta opção para mapear um campo específico do esquema XDM para um [!DNL Braze] atributo.

![Atributo da Fonte de Mapeamento de Destino Brasileiro](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Selecionar namespace de identidade]: Use esta opção para mapear uma [!DNL Platform] namespace de identidade para um [!DNL Braze] namespace.

![Namespace da Fonte do Mapeamento de Destino Brasileiro](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Escolha o campo de origem e clique em **[!UICONTROL Selecionar]**.

No [!UICONTROL Campo de destino] , clique no ícone mapping à direita do campo .

![Mapeamento de Destino da Brasileira](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

No [!UICONTROL Selecionar campo de destino] você pode escolher entre duas categorias de campos de destino:
* [!UICONTROL Selecionar namespace de identidade]: Usar esta opção para mapear [!DNL Platform] namespaces de identidade para [!DNL Braze] namespaces de identidade.
* [!UICONTROL Selecionar atributos personalizados]: Use esta opção para mapear atributos XDM para personalizados [!DNL Braze] os atributos definidos na [!DNL Braze] conta. <br> Também é possível usar essa opção para renomear atributos XDM existentes para [!DNL Braze]. Por exemplo, mapear uma `lastName` Atributo XDM a um `Last_Name` atributo em [!DNL Braze], criará o `Last_Name` atributo em [!DNL Braze], se ainda não existir, e mapeie a variável `lastName` Atributo XDM a ele.

![Campos de mapeamento de destino do site](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Escolha o campo de destino e clique em **[!UICONTROL Selecionar]**.

Agora, você deve ver o mapeamento de campo na lista.

![Mapeamento de Destino de Brasileira Concluído](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Para adicionar mais mapeamentos, repita as etapas anteriores.

## Exemplo de mapeamento {#mapping-example}

Digamos que seu esquema de perfil XDM e seu [!DNL Braze] A instância contém os seguintes atributos e identidades:

|  | Esquema de perfil do XDM | [!DNL Braze] Instância |
|---|---|---|
| Atributos | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>Número de telefone</code></li></ul> |
| Identidades | <ul><li>Email</code></li><li>Google Ad ID (GAID)</code></li><li>Apple ID para anunciantes (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

O mapeamento correto seria semelhante a:

![Exemplo de mapeamento de destino de site](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para a [!DNL Braze] destino, verifique seu [!DNL Braze] conta. [!DNL Adobe Experience Platform] segmentos são exportados para [!DNL Braze] nos termos do `AdobeExperiencePlatformSegments` atributo.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](../../../data-governance/home.md).
