---
keywords: mobile; braze; mensagens;
title: Conexão Braze
description: O Brasil é uma plataforma abrangente de engajamento do cliente que promove experiências relevantes e memoráveis entre os clientes e as marcas que eles adoram.
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 3%

---

# [!DNL Braze] conexão

## Visão geral {#overview}

A variável [!DNL Braze] O destino ajuda a enviar dados de perfil para o [!DNL Braze].

[!DNL Braze] O é uma plataforma abrangente de engajamento do cliente que promove experiências relevantes e memoráveis entre os clientes e as marcas que eles adoram.

Para enviar dados de perfil para [!DNL Braze], você deve primeiro se conectar ao destino.

## Especificações do destino {#specifics}

Observe os seguintes detalhes específicos do [!DNL Braze] destino:

* [!DNL Adobe Experience Platform] os públicos são exportados para [!DNL Braze] no `AdobeExperiencePlatformSegments` atributo.

>[!NOTE]
>
>Lembre-se de que enviar atributos personalizados adicionais para o [!DNL Braze] pode causar aumentos nas [!DNL Braze] consumo de ponto de dados. Consulte seu [!DNL Braze] gerente de conta antes de enviar atributos personalizados adicionais.

## Casos de uso {#use-cases}

Como profissional de marketing, desejo direcionar os usuários em um destino de envolvimento móvel, com públicos-alvo integrados [!DNL Adobe Experience Platform]. Além disso, desejo oferecer experiências personalizadas a eles, com base nos atributos de seus [!DNL Adobe Experience Platform] perfis, assim que públicos-alvo e perfis forem atualizados no [!DNL Adobe Experience Platform].

## Identidades suportadas {#supported-identities}

[!DNL Braze] O oferece suporte à ativação das identidades descritas na tabela abaixo.

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| external_id | Personalizado [!DNL Braze] identificador que oferece suporte ao mapeamento de qualquer identidade. | Você pode enviar qualquer [identidade](../../../identity-service/features/namespaces.md) para o [!DNL Braze] destino, contanto que você o mapeie para a variável [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

{style="table-layout:auto"}

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md). |
| Uploads personalizados | ✓ | Públicos-alvo [importado](../../../segmentation/ui/overview.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome) e/ou identidades, de acordo com o mapeamento de campos.[!DNL Adobe Experience Platform] os públicos são exportados para [!DNL Braze] no `AdobeExperiencePlatformSegments` atributo. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Exibir destinos]** e **[!UICONTROL Gerenciar destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Conectar ao destino]**.

* **[!UICONTROL Token da conta brasileira]**: Este é o seu [!DNL Braze] [!DNL API] chave. Você pode encontrar instruções detalhadas sobre como obter o seu [!DNL API] chave aqui: [Visão geral da chave REST API](https://www.braze.com/docs/api/api_key/).

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: digite um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: insira uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL Instância de Ponto de Extremidade]**: pergunte ao seu [!DNL Braze] representante qual instância de endpoint você deve usar.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar os dados, é necessário **[!UICONTROL Exibir destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}

Consulte [Ativar dados do público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

## Considerações de mapeamento {#mapping-considerations}

Para enviar corretamente os dados do público-alvo de [!DNL Adobe Experience Platform] para o [!DNL Braze] destino, é necessário passar pela etapa de mapeamento de campos.

O mapeamento consiste na criação de um link entre as [!DNL Experience Data Model] Campos de esquema do (XDM) no [!DNL Platform] conta e seus equivalentes correspondentes no destino.

Para mapear corretamente os campos XDM para o [!DNL Braze] campos de destino, siga estas etapas:

No [!UICONTROL Mapeamento] clique em **[!UICONTROL Adicionar novo mapeamento]**.

![Adicionar mapeamento de destino brasileiro](../../assets/catalog/mobile-engagement/braze/mapping.png)

No [!UICONTROL Campo de origem] clique no botão de seta ao lado do campo vazio.

![Mapeamento de origem de destino do Brasil](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

No [!UICONTROL Selecionar campo de origem] você pode escolher entre duas categorias de campos XDM:
* [!UICONTROL Selecionar atributos]: use essa opção para mapear um campo específico do esquema XDM para um campo [!DNL Braze] atributo.

![Atributos da Origem de Mapeamento de Destino Brasileiro](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Selecionar namespace de identidade]: use essa opção para mapear um [!DNL Platform] namespace de identidade para um [!DNL Braze] namespace.

![Namespace de Origem do Mapeamento de Destino Brasileiro](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Escolha o campo de origem e clique em **[!UICONTROL Selecionar]**.

No [!UICONTROL Campo de destino] clique no ícone de mapeamento à direita do campo.

![Mapeamento de Destino Brasileiro](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

No [!UICONTROL Selecionar campo de destino] você pode escolher entre duas categorias de campos de destino:
* [!UICONTROL Selecionar namespace de identidade]: use esta opção para mapear [!DNL Platform] namespaces de identidade para [!DNL Braze] namespaces de identidade.
* [!UICONTROL Selecionar atributos personalizados]: use essa opção para mapear atributos XDM para personalizados [!DNL Braze] atributos definidos no [!DNL Braze] conta. <br> Também é possível usar essa opção para renomear atributos XDM existentes em [!DNL Braze]. Por exemplo, mapear um `lastName` Atributo XDM para um personalizado `Last_Name` atributo em [!DNL Braze], criará o `Last_Name` atributo em [!DNL Braze], se ainda não existir, e mapear o `lastName` Atributo XDM a ele.

![Campos de Mapeamento de Destino Brasileiro](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Escolha o campo de destino e clique em **[!UICONTROL Selecionar]**.

Agora você deve ver o mapeamento de campos na lista.

![Mapeamento de Destinos Brasileiros Concluído](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Para adicionar mais mapeamentos, repita as etapas anteriores.

## Exemplo de mapeamento {#mapping-example}

Digamos que seu esquema de perfil XDM e seu [!DNL Braze] instância contém os seguintes atributos e identidades:

|  | Esquema de perfil XDM | [!DNL Braze] Instância |
|---|---|---|
| Atributos | <ul><li><code>person.name.firstName</code></li><li><code>person.name.lastName</code></li><li><code>mobilePhone.number</code></li></ul> | <ul><li><code>Nome</code></li><li><code>Sobrenome</code></li><li><code>PhoneNumber</code></li></ul> |
| Identidades | <ul><li><code>E-mail</code></li><li><code>ID de anúncio do Google (GAID)</code></li><li><code>Apple ID para anunciantes (IDFA)</code></li></ul> | <ul><li><code>external_id</code></li></ul> |

O mapeamento correto seria semelhante a:

![Exemplo de mapeamento de destino brasileiro](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para o [!DNL Braze] destino, verifique seu [!DNL Braze] conta. [!DNL Adobe Experience Platform] os públicos são exportados para [!DNL Braze] no `AdobeExperiencePlatformSegments` atributo.

## Solução de problemas {#troubleshooting}

**Recebi um erro de tempo limite ao ativar meus públicos-alvo para esse destino. O que devo fazer?**

Ocasionalmente, a ativação do público-alvo para esse destino pode resultar em um erro de tempo limite. Esse erro nem sempre indica um problema de ativação.

Se você receber um erro de tempo limite, verifique o tamanho do público na plataforma de destino. Se o tamanho do público-alvo estiver correto, a integração está funcionando como esperado.

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte [Visão geral da governança de dados](../../../data-governance/home.md).
