---
keywords: atributos do dirigível;destino do dirigível
title: Conexão com os atributos do dirigível
description: Transmita dados de público-alvo do Adobe para o dirigível como atributos de público-alvo para direcionamento no dirigível.
exl-id: bfc1b52f-2d68-40d6-9052-c2ee1e877961
source-git-commit: 34ae6f0f791a40584c2d476ed715bb7c5b733c42
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 2%

---

# [!DNL Airship Attributes] conexão {#airship-attributes-destination}

## Visão geral {#overview}

[!DNL Airship] O é a principal plataforma de engajamento do cliente, ajudando você a fornecer mensagens omnicanais relevantes e personalizadas aos seus usuários em cada estágio do ciclo de vida do cliente.

Essa integração transmite dados de perfil de Adobe para [!DNL Airship] as [Atributos](https://docs.airship.com/guides/audience/attributes/) para direcionamento ou acionamento.

Para saber mais sobre [!DNL Airship], consulte o [Documentação do dirigível](https://docs.airship.com).

>[!TIP]
>
>Esse conector de destino e a página de documentação são criados e mantidos pelo [!DNL Airship] equipe. Para qualquer consulta ou solicitação de atualização, entre em contato diretamente em [support.airship.com](https://support.airship.com/).

## Pré-requisitos {#prerequisites}

Antes de enviar os públicos-alvo para [!DNL Airship], você deve:

* Habilitar atributos no [!DNL Airship] projeto.
* Gerar um token de portador para autenticação.

>[!TIP]
>
>Criar um [!DNL Airship] conta via [este link de inscrição](https://go.airship.eu/accounts/register/plan/starter/) caso ainda não o tenha feito.

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
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome) e/ou identidades, de acordo com o mapeamento de campos. |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Ativar atributos {#enable-attributes}

Os atributos de perfil do Adobe Experience Platform são semelhantes ao [!DNL Airship] atributos e podem ser facilmente mapeados na Platform usando a ferramenta de mapeamento demonstrada mais abaixo nesta página.

[!DNL Airship] Os projetos do têm vários atributos predefinidos e padrão. Se você tiver um atributo personalizado, deverá defini-lo em [!DNL Airship] primeiro. Consulte [Configurar e gerenciar atributos](https://docs.airship.com/tutorials/audience/attributes/) para obter detalhes.

## Gerar token de portador {#bearer-token}

Ir para **[!UICONTROL Configurações]** &quot; **[!UICONTROL APIs e integrações]** no [Painel do dirigível](https://go.airship.com) e selecione **[!UICONTROL Tokens]** no menu à esquerda.

Clique em **[!UICONTROL Criar token]**.

Forneça um nome amigável para o token, por exemplo, &quot;Destino dos atributos de Adobe&quot;, e selecione &quot;Acesso integral&quot; para a função.

Clique em **[!UICONTROL Criar token]** e salve os detalhes como confidenciais.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o [!DNL Airship Attributes] destino, aqui estão exemplos de casos de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso #1

Aproveite os dados de perfil coletados no Adobe Experience Platform para personalização da mensagem e conteúdo avançado em qualquer um dos [!DNL Airship]dos canais. Por exemplo, aproveitar [!DNL Experience Platform] dados de perfil para definir atributos de localização dentro de [!DNL Airship]. Isso permitirá que uma marca de hotel exiba uma imagem para a localização do hotel mais próxima para cada usuário.

### Caso de uso #2

Aproveite os atributos do Adobe Experience Platform para enriquecer ainda mais [!DNL Airship] perfis e combine-os com o SDK ou [!DNL Airship] dados preditivos. Por exemplo, um varejista pode criar um público-alvo com dados de status de fidelidade e localização (atributos da Platform) e [!DNL Airship] A previsão é de que os dados de churn enviem mensagens altamente direcionadas a usuários no status de fidelidade ouro que vivem em Las Vegas, Nova York e têm uma alta probabilidade de churn.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

### Autenticar para o destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios e selecione **[!UICONTROL Conectar ao destino]**.

* **[!UICONTROL Token de portador]**: o token do portador gerado pelo [!DNL Airship] painel.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.

* **[!UICONTROL Nome]**: digite um nome que ajudará a identificar esse destino.
* **[!UICONTROL Descrição]**: digite uma descrição para esse destino.
* **[!UICONTROL Domínio]**: selecione um data center dos EUA ou da UE, dependendo de qual [!DNL Airship] o data center se aplica a esse destino.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}

Consulte [Ativar dados do público-alvo para streaming de destinos de exportação de público](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

## Considerações de mapeamento {#mapping-considerations}

[!DNL Airship] os atributos podem ser definidos em um canal, que representa a instância do dispositivo, por exemplo, iPhone, ou em um usuário nomeado, que mapeia todos os dispositivos de um usuário para um identificador comum, como uma ID de cliente. Se você tiver endereços de email de texto sem formatação (com hash) como identidade principal no esquema, selecione o campo de email no **[!UICONTROL Atributos de origem]** e mapear para o [!DNL Airship] usuário nomeado na coluna à direita em **[!UICONTROL Identidades do Target]**, conforme mostrado abaixo.

![Mapeamento de usuário nomeado](../../assets/catalog/mobile-engagement/airship/mapping.png)

Para identificadores que devem ser mapeados para um canal, ou seja, um dispositivo, mapeie para o canal apropriado com base na origem. As imagens a seguir mostram como dois mapeamentos são criados:

* ID de publicidade do IDFA iOS para um [!DNL Airship] Canal do iOS
* Adobe `fullName` atributo para [!DNL Airship] Atributo &quot;Nome completo&quot;

>[!NOTE]
>
>Use o nome amigável que aparece no campo [!DNL Airship] painel ao selecionar o campo alvo para o mapeamento de atributo.

**Mapear identidade**

Selecionar campo de origem:

![Conectar-se aos atributos do dirigível](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Selecionar campo de destino:

![Conectar-se aos atributos do dirigível](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**Mapear atributo**

Selecionar atributo de origem:

![Selecionar campo de origem](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Selecionar atributo de destino:

![Selecionar campo de destino](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Verificar mapeamento:

![Mapeamento de canal](../../assets/catalog/mobile-engagement/airship/mapping.png)


## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte o [Visão geral da governança de dados](../../../data-governance/home.md).
