---
title: Conexão com o Snowflake
description: Exporte dados para sua conta da Snowflake usando listas privadas.
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="Informative"
exl-id: 4a00e46a-dedb-4dd3-b496-b0f4185ea9b0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 4%

---

# Conexão com o Snowflake {#snowflake-destination}

>[!IMPORTANT]
>
>Este conector de destino está na versão beta e só está disponível para clientes selecionados. Para solicitar acesso, entre em contato com o representante da Adobe.

## Visão geral {#overview}

Exporte dados para sua conta da Snowflake usando listas privadas.

## Pré-requisitos {#prerequisites}

Antes de configurar a conexão do Snowflake, verifique se os seguintes pré-requisitos estão sendo atendidos:

* Você tem acesso a uma conta [!DNL Snowflake].
* Sua conta do Snowflake tem inscrições em listas privadas. Você ou alguém em sua empresa que tenha privilégios de administrador de conta no Snowflake pode configurar isso.

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
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Exportação de público-alvo]** | Você está exportando todos os membros de um público com os identificadores (nome, número de telefone ou outros) usados no destino [!DNL Snowflake]. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil for atualizado no Experience Platform com base na avaliação do público-alvo, o conector enviará a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar Destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, selecione **[!UICONTROL Conectar ao destino]**.

![Captura de tela de exemplo mostrando como autenticar no destino](../../assets/catalog/cloud-storage/snowflake/authenticate-destination.png)

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

![Captura de tela de exemplo mostrando como preencher detalhes para o seu destino](../../assets/catalog/cloud-storage/snowflake/configure-destination-details.png)

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá este destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar este destino no futuro.
* **[!UICONTROL ID da Conta da Snowflake]**: sua ID da conta da Snowflake. Exemplo: `adobe-123456`.
* **[!UICONTROL Confirmação da conta]**: alterne a confirmação da ID de conta da Snowflake para confirmar se a ID de conta está correta e se pertence a você.

>[!IMPORTANT]
>
> Caracteres especiais usados no nome de destino e no nome da sandbox do Experience Platform são convertidos automaticamente em sublinhados (`_`) no Snowflake. Para evitar confusão, não use caracteres especiais no destino e no nome da sandbox.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, leia o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Avançar]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Leia [Ativar perfis e públicos-alvo para destinos de exportação de público-alvo de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para este destino.

### Mapear atributos {#map}

O destino do Snowflake oferece suporte ao mapeamento de atributos de perfil para atributos personalizados.

![Imagem da interface do usuário do Experience Platform mostrando a tela de mapeamento para o destino do Snowflake.](../../assets/catalog/cloud-storage/snowflake/mapping.png)

Os atributos de destino são criados automaticamente no Snowflake usando o nome do atributo fornecido no campo **[!UICONTROL Nome do atributo]**.

## Dados exportados / Validar exportação de dados {#exported-data}

Verifique sua conta do Snowflake para verificar se os dados foram exportados corretamente.

## Uso e governança de dados {#data-usage-governance}

Todos os destinos do [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como o [!DNL Adobe Experience Platform] fiscaliza a governança de dados, leia a [Visão geral da Governança de Dados](/help/data-governance/home.md).
