---
keywords: mobile; braze; mensagens;
title: Conexão Braze
description: O Brasil é uma plataforma abrangente de engajamento do cliente que promove experiências relevantes e memoráveis entre os clientes e as marcas que eles adoram.
last-substantial-update: 2024-08-20T00:00:00Z
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 3%

---

# [!DNL Braze] conexão

## Visão geral {#overview}

O destino [!DNL Braze] ajuda a enviar dados de perfil para [!DNL Braze].

O [!DNL Braze] é uma plataforma abrangente de engajamento do cliente que possibilita experiências relevantes e memoráveis entre os clientes e as marcas que eles adoram.

Para enviar dados de perfil para [!DNL Braze], primeiro você deve se conectar ao destino.

## Especificações do destino {#specifics}

Observe os seguintes detalhes que são específicos para o destino [!DNL Braze]:

* [!DNL Adobe Experience Platform] públicos-alvo são exportados para [!DNL Braze] sob o atributo `AdobeExperiencePlatformSegments`.

>[!NOTE]
>
>Lembre-se de que o envio de atributos personalizados adicionais para [!DNL Braze] pode causar um aumento no consumo de pontos de dados de [!DNL Braze]. Consulte seu gerente de conta [!DNL Braze] antes de enviar outros atributos personalizados.

## Casos de uso {#use-cases}

Como profissional de marketing, quero direcionar usuários em um destino de engajamento móvel, com públicos-alvo integrados no [!DNL Adobe Experience Platform]. Além disso, desejo entregar experiências personalizadas a eles, com base em atributos de seus perfis do [!DNL Adobe Experience Platform], assim que os públicos-alvo e perfis forem atualizados no [!DNL Adobe Experience Platform].

## Identidades suportadas {#supported-identities}

[!DNL Braze] dá suporte à ativação das identidades descritas na tabela abaixo.

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| external_id | Identificador [!DNL Braze] personalizado que oferece suporte ao mapeamento de qualquer identidade. | Você pode enviar qualquer [identidade](../../../identity-service/features/namespaces.md) para o destino [!DNL Braze], desde que mapeie-a para o [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Uploads personalizados | ✓ | Públicos [importados](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Profile-based]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome) e/ou identidades, de acordo com o mapeamento de campos.[!DNL Adobe Experience Platform] públicos-alvo são exportados para [!DNL Braze] sob o atributo `AdobeExperiencePlatformSegments`. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa das **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Braze account token]**: Esta é sua chave [!DNL Braze] [!DNL API]. Você pode encontrar instruções detalhadas sobre como obter sua chave [!DNL API] aqui: [Visão geral da chave de API REST](https://www.braze.com/docs/api/api_key/).

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Name]**: digite um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Description]**: insira uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL Endpoint Instance]**: pergunte ao representante do [!DNL Braze] qual instância de ponto de extremidade você deve usar.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Consulte [Ativar dados de público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

## Considerações de mapeamento {#mapping-considerations}

Para enviar corretamente os dados de público-alvo de [!DNL Adobe Experience Platform] para o destino [!DNL Braze], é necessário passar pela etapa de mapeamento de campos.

O mapeamento consiste na criação de um vínculo entre os campos do esquema [!DNL Experience Data Model] (XDM) na conta [!DNL Experience Platform] e seus equivalentes correspondentes no destino.

Para mapear corretamente os campos XDM para os campos de destino [!DNL Braze], siga estas etapas:

Na etapa [!UICONTROL Mapping], clique em **[!UICONTROL Add new mapping]**.

![Adicionar mapeamento de destino](../../assets/catalog/mobile-engagement/braze/mapping.png)

Na seção [!UICONTROL Source Field], clique no botão de seta ao lado do campo vazio.

![Mapeamento de Source de Destino do Brasil](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

Na janela [!UICONTROL Select source field], você pode escolher entre duas categorias de campos XDM:

* [!UICONTROL Select attributes]: use esta opção para mapear um campo específico do esquema XDM para um atributo [!DNL Braze].

![Mapeamento de Destino do Atributo Source](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Select identity namespace]: Use esta opção para mapear um namespace de identidade [!DNL Experience Platform] para um namespace [!DNL Braze].

![Namespace Source de Mapeamento de Destino](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Escolha seu campo de origem e clique em **[!UICONTROL Select]**.

Na seção [!UICONTROL Target Field], clique no ícone de mapeamento à direita do campo.

![Mapeamento de Destino Brasileiro](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

Na janela [!UICONTROL Select target field], você pode escolher entre duas categorias de campos de destino:

* [!UICONTROL Select identity namespace]: Use esta opção para mapear [!DNL Experience Platform] namespaces de identidade para [!DNL Braze] namespaces de identidade.
* [!UICONTROL Select custom attributes]: use esta opção para mapear atributos XDM para atributos [!DNL Braze] personalizados que você definiu em sua conta [!DNL Braze]. <br> Também é possível usar essa opção para renomear atributos XDM existentes em [!DNL Braze]. Por exemplo, mapear um atributo XDM `lastName` para um atributo personalizado `Last_Name` em [!DNL Braze] criará o atributo `Last_Name` em [!DNL Braze], se ele ainda não existir, e mapeará o atributo XDM `lastName` para ele.

![Descobrir Campos De Mapeamento De Destino](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Escolha seu campo de destino e clique em **[!UICONTROL Select]**.

Agora você deve ver o mapeamento de campos na lista.

![Mapeamento de Destino Concluído](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Para adicionar mais mapeamentos, repita as etapas anteriores.

## Exemplo de mapeamento {#mapping-example}

Digamos que o esquema de perfil XDM e a instância [!DNL Braze] contenham os seguintes atributos e identidades:

|  | Esquema de perfil XDM | [!DNL Braze] Instância |
|---|---|---|
| Atributos | <ul><li><code>person.name.firstName</code></li><li><code>pessoa.nome.sobrenome</code></li><li><code>mobilePhone.number</code></li></ul> | <ul><li><code>Nome</code></li><li><code>Sobrenome</code></li><li><code>NúmeroTelefone</code></li></ul> |
| Identidades | <ul><li><code>Email</code></li><li><code>ID do Google Ad (GAID)</code></li><li><code>Apple ID para anunciantes (IDFA)</code></li></ul> | <ul><li><code>external_id</code></li></ul> |

O mapeamento correto seria semelhante a:

![Exemplo de Mapeamento de Destino](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para o destino [!DNL Braze], verifique sua conta [!DNL Braze]. [!DNL Adobe Experience Platform] públicos-alvo são exportados para [!DNL Braze] sob o atributo `AdobeExperiencePlatformSegments`.

## Resolução de problemas {#troubleshooting}

**Recebi um erro de tempo limite ao ativar meus públicos para este destino. O que devo fazer?**

Ocasionalmente, a ativação do público-alvo para esse destino pode resultar em um erro de tempo limite. Esse erro nem sempre indica um problema de ativação.

Se você receber um erro de tempo limite, verifique o tamanho do público na plataforma de destino. Se o tamanho do público-alvo estiver correto, a integração está funcionando como esperado.

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] impõe a governança de dados, consulte [Visão geral da Governança de Dados](../../../data-governance/home.md).
