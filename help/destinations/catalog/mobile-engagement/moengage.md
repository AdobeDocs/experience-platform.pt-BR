---
title: Conexão Moengage
description: A Moengage é uma plataforma de engajamento do cliente que promove interações centradas no cliente entre consumidores e marcas em tempo real.
last-substantial-update: 2023-10-11T00:00:00Z
source-git-commit: 6a80089f404057b5c98764b5e0166b9afaf1a7e4
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 0%

---


# Conexão com o [!DNL Moengage]

## Visão geral {#overview}

Use o [!DNL Moengage] destino para conectar e mapear seus dados do Adobe (atributos de usuário, segmentos e eventos) para o MoEngage em tempo real. Os clientes podem então agir com base nesses dados, fornecendo experiências personalizadas e direcionadas.

Com o Adobe, a integração é muito simples e intuitiva. Basta pegar qualquer perfil de usuário Adobe e mapeá-lo para um atributo de usuário MoEngage.

>[!IMPORTANT]
>
>Esse conector de destino e a página de documentação são criados e mantidos pelo *Moengage* equipe. Para qualquer consulta ou solicitação de atualização, entre em contato diretamente em *`https://help.moengage.com/hc/en-us`.*

## Casos de uso {#use-cases}

Um profissional de marketing deseja direcionar um segmento de usuário (integrado no Adobe Experience Platform) por meio de [!DNL Moengage] campanhas. Além disso, eles querem personalizar o conteúdo da campanha com base nos atributos dos perfis do Adobe Experience Platform. Com essa integração, os usuários e atributos são atualizados no MoEngage assim que os segmentos e perfis são atualizados no Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

Antes de enviar os dados do Adobe Experience Platform para o [!DNL Moengage], observe os seguintes pré-requisitos:

* Para usar o destino MoEngage com o Adobe Experience Platform, os usuários devem primeiro ter acesso aos seus [!DNL Moengage] Conta. Visite a seguinte página para se inscrever ou fazer logon em sua conta do MoEngage: https://app.moengage.com


## Identidades suportadas {#supported-identities}

[!DNL Moengage] O oferece suporte à ativação das identidades descritas na tabela abaixo.

| Identidade de destino | Descrição | Considerações |
|---|------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| user_id | Identificador exclusivo que identifica exclusivamente um perfil de usuário na [!DNL Moengage] sistema. | Esse identificador oferece suporte ao tipo de sequência de caracteres. É necessário um user_id ou anonymous_id |
| anonymous_id | Outro identificador para um perfil de usuário desconhecido, ou seja, um perfil que não existe no sistema. | Esse identificador oferece suporte ao tipo de sequência de caracteres. É necessário um user_id ou anonymous_id |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento (público-alvo) com os identificadores (user_id, anonymous_id) junto com os atributos personalizados definidos por você exportados para [!DNL Moengage]. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Conectar ao destino]**.

![Autenticação de destino Moengage](../../assets/catalog/mobile-engagement/moengage/authentication.png)

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.
![Autenticação de destino Moengage](../../assets/catalog/mobile-engagement/moengage/settings.png)
* **[!UICONTROL NOME DE USUÁRIO]**: ID DO APLICATIVO DE DADOS da página de configurações de [!DNL Moengage] painel.
* **[!UICONTROL SENHA]**: CHAVE DE APLICATIVO DE DADOS da página de configurações de [!DNL Moengage] painel.

![Autenticação de destino Moengage](../../assets/catalog/mobile-engagement/moengage/destination_details.png)

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL Região]**: Seu aplicativo *data center*.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados do público-alvo para destinos de exportação de segmento de transmissão](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino.

### Mapear atributos e identidades {#map}

Para enviar corretamente os dados do público-alvo de [!DNL Adobe Experience Platform] para o [!DNL Moengage] destino, é necessário passar pela etapa de mapeamento de campos.

O mapeamento consiste na criação de um link entre as [!DNL Experience Data Model] Campos de esquema do (XDM) no [!DNL Platform] conta e seus equivalentes correspondentes no destino.

Para mapear corretamente os campos XDM para o [!DNL Moengage] campos de destino, siga estas etapas:

No [!UICONTROL Mapeamento] etapa, selecione **[!UICONTROL Caixa de seleção]**.

![Moengage Destination Adicionar mapeamento](../../assets/catalog/mobile-engagement/moengage/segments.png)

No [!UICONTROL Mapeamento] etapa, selecione **[!UICONTROL Adicionar novo mapeamento]**.

![Moengage Destination Adicionar mapeamento](../../assets/catalog/mobile-engagement/moengage/mapping.png)

No [!UICONTROL Campo de origem] selecione o botão de seta ao lado do campo vazio.

![Moengage Destination Source Mapping](../../assets/catalog/mobile-engagement/moengage/mapping-source.png)

No [!UICONTROL Selecionar campo de origem] você pode escolher entre duas categorias de campos XDM:
* [!UICONTROL Selecionar atributos]: use essa opção para mapear um campo específico do esquema XDM para [!DNL Moengage] atributo.

![Atributo de Origem do Mapeamento de Destino Moengage](../../assets/catalog/mobile-engagement/moengage/mapping-attributes.png)

Escolha o campo de origem e selecione **[!UICONTROL Selecionar]**.

No [!UICONTROL Campo de destino] selecione o ícone de mapeamento à direita do campo.

![Moengage Target Mapping](../../assets/catalog/mobile-engagement/moengage/mapping-target.png)

No [!UICONTROL Selecionar campo de destino] você pode escolher entre duas categorias de campos de destino:
* [!UICONTROL Selecionar namespace de identidade]: use esta opção para mapear [!DNL Platform] namespaces de identidade para [!DNL Moengage] namespaces de identidade.
* [!UICONTROL Selecionar atributos personalizados]: use essa opção para mapear atributos XDM para personalizados [!DNL Moengage] atributos definidos no [!DNL Moengage] conta. <br> Também é possível usar essa opção para renomear atributos XDM existentes em [!DNL Moengage]. Por exemplo, mapear um `lastName` Atributo XDM para um personalizado `Last_Name` atributo em [!DNL Moengage], criará o `Last_Name` atributo em [!DNL Moengage], se ainda não existir, e mapear o `lastName` Atributo XDM a ele.

![Moengage Destination Mapping Fields (Moengajar campos de mapeamento de destino)](../../assets/catalog/mobile-engagement/moengage/mapping-target-fields.png)

Escolha o campo de destino e selecione **[!UICONTROL Selecionar]**.

Agora você deve ver o mapeamento de campos na lista.

![Mapeamento De Destino Moengage Concluído](../../assets/catalog/mobile-engagement/moengage/mapping-complete.png)

Para adicionar mais mapeamentos, repita as etapas anteriores.

## Dados exportados / Validar exportação de dados {#exported-data}

Para verificar se os dados foram exportados com êxito para o [!DNL Moengage] destino, vá para o perfil de usuário em seu [!DNL Moengage] conta. Você verá um atributo de usuário chamado Segmento AEP.

![Mapeamento De Destino Moengage Concluído](../../assets/catalog/mobile-engagement/moengage/validation.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia o [Visão geral da governança de dados](/help/data-governance/home.md).

