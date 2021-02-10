---
keywords: atributos do dirigível;destino do dirigível
title: Ligação de atributos de dirigível
description: Transmita dados de Audiência para o Airship sem problemas como atributos de Audiência para definição de metas dentro do Airship.
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 0%

---


# (Beta) [!DNL Airship Attributes] conexão {#airship-attributes-destination}

>[!IMPORTANT]
>
>O destino [!DNL Airship Attributes] no Adobe Experience Platform está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

[!DNL Airship] é a plataforma líder de envolvimento do cliente, ajudando você a fornecer mensagens de canal significativas e personalizadas para seus usuários em cada estágio do ciclo de vida do cliente.

Essa integração envia dados de perfil de Adobe para [!DNL Airship] como [Atributos](https://docs.airship.com/guides/audience/attributes/) para direcionamento ou acionamento.

Para saber mais sobre [!DNL Airship], consulte [Documentos do Airship](https://docs.airship.com).


>[!TIP]
>
>Esta página de documentação foi criada pela equipe [!DNL Airship]. Para obter quaisquer perguntas ou solicitações de atualização, entre em contato diretamente com elas em [support.airship.com](https://support.airship.com/).

## Pré-requisitos {#prerequisites}

Antes de enviar seus segmentos de audiência para [!DNL Airship], você deve:

* Ative os atributos no projeto [!DNL Airship].
* Gere um token do portador para autenticação.

>[!TIP]
>
>Crie uma conta [!DNL Airship] por meio de [este link de inscrição](https://go.airship.eu/accounts/register/plan/starter/), caso ainda não o tenha feito.

### Ativar atributos {#enable-attributes}

Os atributos do perfil Adobe Experience Platform são semelhantes aos atributos [!DNL Airship] e podem ser facilmente mapeados uns para os outros na Plataforma usando a ferramenta de mapeamento mostrada mais abaixo nesta página.

[!DNL Airship] projetos têm vários atributos predefinidos e padrão. Se você tiver um atributo personalizado, deverá defini-lo em [!DNL Airship] primeiro. Consulte [Configurar e gerenciar atributos](https://docs.airship.com/tutorials/audience/attributes/) para obter detalhes.

### Token do portador {#bearer-token}

Vá para **[!UICONTROL Settings]**&quot; **[!UICONTROL APIs &amp; Integrations]** no [painel Airship](https://go.airship.com) e selecione **[!UICONTROL Tokens]** no menu à esquerda.

Clique em **[!UICONTROL Criar token]**.

Forneça um nome amigável para o seu token, por exemplo, &quot;Destino de atributos de Adobe&quot; e selecione &quot;Todo acesso&quot; para a função.

Clique em **[!UICONTROL Criar token]** e salve os detalhes como confidenciais.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o destino [!DNL Airship Attributes], veja a seguir exemplos de casos de uso que os clientes da Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso nº 1

Aproveite os dados do perfil coletados no Adobe Experience Platform para personalização da mensagem e conteúdo avançado em qualquer um dos canais de [!DNL Airship]. Por exemplo, aproveite os dados do perfil [!DNL Experience Platform] para definir atributos de localização em [!DNL Airship]. Isso permitirá que uma marca de hotel exiba uma imagem para o local de hotel mais próximo para cada usuário.

### Caso de uso nº 2

Aproveite os atributos do Adobe Experience Platform para enriquecer ainda mais os perfis [!DNL Airship] e combiná-los com SDK ou [!DNL Airship] dados preditivos. Por exemplo, um varejista pode criar um segmento com status de fidelidade e dados de localização (atributos da Plataforma) e [!DNL Airship] com previsão de gerar dados para enviar mensagens altamente direcionadas aos usuários no status de fidelidade dourada que vivem em Las Vegas, NV, e têm uma alta probabilidade de se movimentar.

## Conectar-se a [!DNL Airship Attributes] {#connect-airship-attributes}

Em **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, role até a categoria **[!UICONTROL Mobile Engagement]**. Selecione **[!DNL Airship Attributes]** e selecione **[!UICONTROL Configurar]**.

>[!NOTE]
>
>Se já existir uma conexão com esse destino, você poderá ver um botão **[!UICONTROL Ativar]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Ativate]** e **[!UICONTROL Configure]**, consulte a seção [Catalog](../../ui/destinations-workspace.md#catalog) da documentação da área de trabalho de destino.

![Conectar-se aos atributos do aeróstato](../../assets/catalog/mobile-engagement/airship/catalog.png)

Na etapa **Account**, se você já tiver configurado uma conexão com o destino [!DNL Airship Attributes], selecione **[!UICONTROL Conta existente]** e selecione a conexão existente. Ou você pode selecionar **[!UICONTROL Nova conta]** para configurar uma nova conexão com [!DNL Airship Attributes]. Selecione **[!UICONTROL Ligar ao destino]** para ligar o Adobe Experience Platform ao seu projeto [!DNL Airship] utilizando o token portador que gerou a partir do painel [!DNL Airship].

>[!NOTE]
>
>A Adobe Experience Platform oferece suporte à validação de credenciais no processo de autenticação e exibe uma mensagem de erro se você inserir credenciais incorretas na conta [!DNL Airship]. Isso garante que você não conclua o fluxo de trabalho com credenciais incorretas.

![Conectar-se aos atributos do aeróstato](../../assets/catalog/mobile-engagement/airship/connect.png)

Depois que suas credenciais forem confirmadas e a Adobe Experience Platform estiver conectada ao projeto [!DNL Airship], você poderá selecionar **[!UICONTROL Próximo]** para prosseguir para a etapa **[!UICONTROL Configuração]**.

Na etapa **[!UICONTROL Authentication]**, digite um **[!UICONTROL Name]** e um **[!UICONTROL Description]** para o fluxo de ativação.

Também nesta etapa, você pode selecionar data center dos EUA ou da UE, dependendo de qual data center [!DNL Airship] se aplica a esse destino. Por fim, selecione um ou mais casos de uso de marketing para os quais os dados serão exportados para o destino. Você pode selecionar entre casos de uso de marketing definidos pelo Adobe ou criar os seus próprios. Para obter mais informações sobre casos de uso de marketing, consulte [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

Selecione **[!UICONTROL Criar destino]** depois de preencher os campos acima.

![Conectar-se aos atributos do aeróstato](../../assets/catalog/mobile-engagement/airship/select-domain.png)

Seu destino agora é criado. Você pode selecionar **[!UICONTROL Salvar e Sair]** se quiser ativar segmentos posteriormente ou selecionar **[!UICONTROL Próximo]** para continuar o fluxo de trabalho e selecionar segmentos para ativação. Em ambos os casos, consulte a próxima seção, [Ativar segmentos](#activate-segments), para o restante do fluxo de trabalho.

## Ativar segmentos {#activate-segments}

Para ativar segmentos em [!DNL Airship Attributes], siga as etapas abaixo:

Em **[!UICONTROL Destinos > Procurar]**, selecione o destino [!DNL Airship Attributes] onde deseja ativar seus segmentos.

![ativar fluxo](../../assets/catalog/mobile-engagement/airship/browse.png)

Clique no nome do destino. Isso leva você ao fluxo Ativar.

Observe que se já existir um fluxo de ativação para um destino, você poderá ver os segmentos que estão sendo enviados para o destino. Selecione **[!UICONTROL Editar ativação]** no painel direito e siga as etapas abaixo para modificar os detalhes da ativação.

![ativar fluxo](../../assets/catalog/mobile-engagement/airship/activate.png)

Selecione **[!UICONTROL Ativar]**. No fluxo de trabalho **[!UICONTROL Ativar destino]**, na página **[!UICONTROL Selecionar segmentos]**, selecione quais segmentos enviar para [!DNL Airship Attributes].

![segmentos para destino](../../assets/catalog/mobile-engagement/airship/select-segments.png)

Na etapa **[!UICONTROL Mapeamento]**, selecione quais atributos e identidades do schema [XDM](../../../xdm/home.md) serão mapeados para o schema de destino. Selecione **[!UICONTROL Adicionar novo mapeamento]** para navegar pelo seu schema e mapeá-lo para a identidade do público alvo correspondente.

![tela inicial do mapeamento de identidade](../../assets/catalog/mobile-engagement/airship/identity-mapping.png)

[!DNL Airship] os atributos podem ser definidos em um canal, que representa a instância do dispositivo, por exemplo, iPhone, ou um usuário nomeado, que mapeia todos os dispositivos de um usuário para um identificador comum, como uma ID do cliente. Se você tiver endereços de email de texto simples (sem hash) como identidade primária em seu schema, selecione o campo de email em **[!UICONTROL Atributos de origem]** e mapeie para o usuário nomeado [!DNL Airship] na coluna direita em **[!UICONTROL Identidades de Público alvo]**, conforme mostrado abaixo.

![Mapeamento de usuário nomeado](../../assets/catalog/mobile-engagement/airship/mapping.png)

Para identificadores que devem ser mapeados para um canal, ou seja, um dispositivo, mapeie para o canal apropriado com base na fonte. As imagens a seguir mostram como dois mapeamentos são criados:

* ID de anúncio do iOS IDFA para um canal do iOS [!DNL Airship]
* Atributo Adobe `fullName` para atributo [!DNL Airship] &quot;Full Name&quot;

>[!NOTE]
>
>Use o nome amigável que aparece no painel [!DNL Airship] ao selecionar o campo de público alvo para o mapeamento do atributo.

**Identidade do mapa**

Selecionar campo de origem:

![Conectar-se aos atributos do aeróstato](../../assets/catalog/mobile-engagement/airship/select-source-identity.png)

Selecione o campo público alvo:

![Conectar-se aos atributos do aeróstato](../../assets/catalog/mobile-engagement/airship/select-target-identity.png)

**Atributo do mapa**

Selecionar atributo de origem:

![Selecionar campo de origem](../../assets/catalog/mobile-engagement/airship/select-source-attributes.png)

Selecione o atributo do público alvo:

![Selecionar campo público alvo](../../assets/catalog/mobile-engagement/airship/select-target-attribute.png)

Verificar mapeamento:

![Mapeamento de canais](../../assets/catalog/mobile-engagement/airship/mapping.png)

Na página **[!UICONTROL Agendamento do segmento]**, o agendamento está desabilitado no momento. Clique em **[!UICONTROL Avançar]** para continuar com a etapa de revisão.

![Agendamento atualmente desabilitado](../../assets/catalog/mobile-engagement/airship/scheduling.png)

Na página **[!UICONTROL Revisar]**, você pode ver um resumo de sua seleção. Selecione **[!UICONTROL Cancelar]** para interromper o fluxo, **[!UICONTROL Voltar]** para modificar as definições, ou **[!UICONTROL Concluir]** para confirmar a seleção e o start que envia dados para o destino.

>[!IMPORTANT]
>
>Nesta etapa, a Adobe Experience Platform verifica violações da política de uso de dados. Abaixo está um exemplo de violação de uma política. Não é possível concluir o fluxo de trabalho da ativação de segmentos até que você tenha resolvido a violação. Para obter informações sobre como resolver violações de política, consulte [Aplicação de política](../../../data-governance/enforcement/auto-enforcement.md) na seção de documentação de controle de dados.

![confirmação de seleção](../../assets/common/data-policy-violation.png)

Se nenhuma violação de política tiver sido detectada, selecione **[!UICONTROL Concluir]** para confirmar sua seleção e start enviando dados para o destino.

![revisão](../../assets/catalog/mobile-engagement/airship/review.png)

## Uso e controle de dados {#data-usage-governance}

Todos os destinos [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral do controle de dados](../../../data-governance/home.md).
