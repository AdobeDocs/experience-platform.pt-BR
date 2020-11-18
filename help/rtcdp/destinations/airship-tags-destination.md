---
keywords: airship tags;airship destination
title: Destino das Etiquetas de Avião
seo-title: Destino das Etiquetas de Avião
description: Transmita dados de Audiência para o Airship sem problemas como Etiquetas de Audiência para definição de metas dentro do Airship.
seo-description: Transmita dados de Audiência para o Airship sem problemas como Etiquetas de Audiência para definição de metas dentro do Airship.
translation-type: tm+mt
source-git-commit: 4b1bf5bbce57a22529c5d025c5bae10557400d54
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 1%

---


# (Beta) [!DNL Airship Tags] destino {#airship-tags-destination}

>[!IMPORTANT]
>
>O [!DNL Airship Tags] destino no Adobe Experience Platform está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

## Visão geral

[!DNL Airship] é a plataforma líder de envolvimento do cliente, ajudando você a fornecer mensagens de canal significativas e personalizadas para seus usuários em cada estágio do ciclo de vida do cliente.

Essa integração transmite os dados de segmento do Adobe Experience Platform [!DNL Airship] como [Tags](https://docs.airship.com/guides/audience/tags/) para definição de metas ou acionamento.

Para saber mais sobre [!DNL Airship], consulte os [Documentos](https://docs.airship.com)do Airship.


>[!TIP]
>
>Esta página de documentação foi criada pela [!DNL Airship] equipe. Para obter informações ou solicitações de atualização, entre em contato diretamente com [support.airship.com](https://support.airship.com/).

## Pré-requisitos

Antes de enviar seus segmentos do Adobe Experience Platform para [!DNL Airship], você deve:

* Crie um grupo de tags em seu [!DNL Airship] projeto.
* Gere um token do portador para autenticação.

>[!TIP]
> 
>Crie uma [!DNL Airship] conta por meio [deste link](https://go.airship.eu/accounts/register/plan/starter/) de inscrição, caso ainda não o tenha feito.

### Grupos de tags

O conceito de segmentos na plataforma Adobe Experience é semelhante às [Tags](https://docs.airship.com/guides/audience/tags/) no Airship, com pequenas diferenças na implementação. Essa integração mapeia o status da [associação de um usuário em um segmento](https://experienceleague.adobe.com/docs/experience-platform/xdm/mixins/profile/segmentation.html?lang=en#mixins) Experience Platform para a presença ou não de uma [!DNL Airship] tag. Por exemplo, em um segmento de Plataforma no qual o `xdm:status` muda para `realized`, a tag é adicionada ao [!DNL Airship] canal ou ao usuário nomeado para o qual esse perfil é mapeado. Se a tag for `xdm:status` alterada para `exited`, ela será removida.

Para habilitar essa integração, crie um grupo *de* tags com [!DNL Airship] nome `adobe-segments`.

>[!IMPORTANT]
>
>Ao criar seu novo grupo de tags, **não marque** o botão de opção que diz &quot;[!DNL Allow these tags to be set only from your server]&quot;. Isso fará com que a integração de tags Adobe falhe.

Consulte [Gerenciar grupos](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) de tags para obter instruções sobre como criar o grupo de tags.

### Token do portador

1. Vá para **[!UICONTROL Configurações]** &quot; **[!UICONTROL APIs e integrações]** no painel [](https://go.airship.com) Airship e selecione **[!UICONTROL Tokens]** no menu esquerdo.
1. Clique em **[!UICONTROL Criar token]**.
1. Forneça um nome fácil de usar para o seu token, por exemplo, &quot;Destino de tags de Adobe&quot; e selecione &quot;Todo acesso&quot; para a função.
1. Clique em **[!UICONTROL Criar token]** e salve os detalhes como confidenciais.


## Casos de uso

Para ajudá-lo a entender melhor como e quando você deve usar o [!DNL Airship Tags] destino, veja a seguir exemplos de casos de uso que os clientes da Adobe Experience Platform podem resolver usando esse destino.

### Caso de uso nº 1

Os varejistas ou as plataformas de entretenimento podem criar perfis de usuários em seus clientes de fidelidade e passar esses segmentos [!DNL Airship] para direcionamento de mensagens em campanhas móveis.

### Caso de uso nº 2

Acione mensagens de um para um em tempo real quando os usuários caírem em ou saírem de segmentos específicos no Adobe Experience Platform.

Por exemplo, um varejista configura um segmento específico da marca jeans na Plataforma. Esse varejista agora pode disparar uma mensagem móvel assim que alguém define sua preferência por jeans para uma marca específica.

## Conectar-se a [!DNL Airship Tags] {#connect-airship-tags}

1. Em **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, navegue até a categoria de envolvimento **[!UICONTROL do]** Mobile. Selecione **[!DNL Airship Tags]**, em seguida, **[!UICONTROL Configurar]**.

   >[!NOTE]
   >
   >Se já existir uma conexão com esse destino, você poderá ver um botão **[!UICONTROL Ativar]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Ativar]** e **[!UICONTROL Configurar]**, consulte a seção [Catálogo](/help/rtcdp/destinations/destinations-workspace.md#catalog) da documentação da área de trabalho de destino.

   ![Conectar-se às Tags de nave](/help/rtcdp/destinations/assets/airship-tags-in-catalog.png)

2. Na etapa **Conta** , se você já tiver configurado uma conexão com seu [!DNL Airship Tags] destino, selecione Conta **** existente e selecione sua conexão existente. Ou você pode selecionar **[!UICONTROL Nova conta]** para configurar uma nova conexão com [!DNL Airship Tags]. Selecione **[!UICONTROL Conectar-se ao destino]** para conectar o Adobe Experience Platform ao seu [!DNL Airship] projeto usando o token do portador que você gerou a partir do [!DNL Airship] painel.

   >[!NOTE]
   >
   >A Adobe Experience Platform oferece suporte à validação de credenciais no processo de autenticação e exibe uma mensagem de erro se você inserir credenciais incorretas em sua [!DNL Airship] conta. Isso garante que você não conclua o fluxo de trabalho com credenciais incorretas.

   ![Conectar-se às Tags de nave](/help/rtcdp/destinations/assets/airshiptags1-connect-account.png)

3. Depois que suas credenciais forem confirmadas e a Adobe Experience Platform estiver conectada ao seu [!DNL Airship] projeto, você poderá selecionar **[!UICONTROL Avançar]** para prosseguir para a etapa **[!UICONTROL de configuração]** .

4. Na etapa **[!UICONTROL Autenticação]** , digite um **[!UICONTROL Nome]** e uma **[!UICONTROL Descrição]** para o fluxo de ativação. <br> Também nesta etapa, você pode selecionar data center dos EUA ou da UE, dependendo de qual data center se aplica a esse destino. [!DNL Airship] Por fim, selecione um ou mais casos de uso de marketing para os quais os dados serão exportados para o destino. Você pode selecionar entre casos de uso de marketing definidos pelo Adobe ou criar os seus próprios. Para obter mais informações sobre casos de uso de marketing, consulte a página [Data Governance em CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) em tempo real. Para obter informações sobre casos individuais de uso de marketing definidos pelo Adobe, consulte a visão geral [das políticas de uso de](/help/data-governance/policies/overview.md#core-actions)dados. <br> Selecione **[!UICONTROL Criar destino]** depois de preencher os campos acima.

   ![Conectar-se às Tags de nave](/help/rtcdp/destinations/assets/airshiptags2-select-domain.png)

5. Seu destino agora é criado. Você pode selecionar **[!UICONTROL Salvar e sair]** se quiser ativar segmentos posteriormente ou selecionar **[!UICONTROL Próximo]** para continuar o fluxo de trabalho e selecionar segmentos para ativar. Em ambos os casos, consulte a próxima seção, [Ativar segmentos](#activate-segments), para o restante do fluxo de trabalho.

## Ativar segmentos {#activate-segments}

Para ativar segmentos para [!DNL Airship Tags], siga as etapas abaixo:

1. Em **[!UICONTROL Destinos > Procurar]**, selecione o [!DNL Airship Tags] destino onde deseja ativar seus segmentos. ![ativar fluxo](/help/rtcdp/destinations/assets/airship-tags-activate1.png)
2. Clique no nome do destino. Isso leva você ao fluxo Ativar.
Observe que se já existir um fluxo de ativação para um destino, você poderá ver os segmentos que estão sendo enviados para o destino. Selecione **[!UICONTROL Editar ativação]** no painel direito e siga as etapas abaixo para modificar os detalhes da ativação.  ![ativar fluxo](/help/rtcdp/destinations/assets/airship-tags-activate2.png)
3. Selecione **[!UICONTROL Ativar]**;
4. No fluxo de trabalho **[!UICONTROL Ativar destino]** , na página **[!UICONTROL Selecionar segmentos]** , selecione para quais segmentos enviar [!DNL Airship Tags].
   ![segmentos para destino](/help/rtcdp/destinations/assets/airshiptags3-select-segments.png)
5. Na etapa **[!UICONTROL Mapeamento]** , selecione quais atributos e identidades do schema [XDM](https://docs.adobe.com/content/help/pt-BR/experience-platform/xdm/home.html) serão mapeados para o schema de destino. Selecione **[!UICONTROL Adicionar novo mapeamento]** para navegar pelo schema e mapeá-lo para a identidade do público alvo correspondente.
   ![tela inicial do mapeamento de identidade](/help/rtcdp/destinations/assets/gcm-identity-mapping.png)
   [!DNL Airship] as tags podem ser definidas em um canal, que representa a instância do dispositivo, por exemplo, iPhone ou um usuário nomeado, que mapeia todos os dispositivos de um usuário para um identificador comum, como uma ID do cliente. Se você tiver endereços de email de texto simples (sem hash) como identidade primária em seu schema, selecione o campo de email em seus Atributos **[!UICONTROL de]** origem e mapeie para o usuário [!DNL Airship] nomeado na coluna direita em Identidades **[!UICONTROL de]**Público alvo, como mostrado abaixo.
   ![Mapeamento](/help/rtcdp/destinations/assets/airshiptags7-mappingoption2.png)de usuário nomeado Para identificadores que devem ser mapeados para um canal, ou seja, um dispositivo, mapeie para o canal apropriado com base na fonte. As imagens a seguir mostram como mapear uma ID de anúncio do Google para um canal [!DNL Airship] Android.
   ![Conectar-se às Tags de nave](/help/rtcdp/destinations/assets/airshiptags4-select-source-identity.png)
   ![Conectar-se às Tags de nave](/help/rtcdp/destinations/assets/airshiptags5-select-target-identity.png)
   ![Mapeamento de canais](/help/rtcdp/destinations/assets/airshiptags6-mappingoption1.png)

6. Na página Agendamento **[!UICONTROL do]** segmento, o agendamento está desativado no momento. Clique em **[!UICONTROL Avançar]** para continuar com a etapa de revisão.
7. Na página **[!UICONTROL Revisar]** , você pode ver um resumo de sua seleção. Selecione **[!UICONTROL Cancelar]** para quebrar o fluxo, **[!UICONTROL Voltar]** para modificar suas configurações ou **[!UICONTROL Concluir]** para confirmar sua seleção e start enviando dados para o destino.

>[!IMPORTANT]
>
>Nesta etapa, a Adobe Experience Platform verifica violações da política de uso de dados. Abaixo está um exemplo de violação de uma política. Não é possível concluir o fluxo de trabalho da ativação de segmentos até que você tenha resolvido a violação. Para obter informações sobre como resolver violações de política, consulte Aplicação de [política](/help/rtcdp/privacy/data-governance-overview.md#enforcement) na seção de documentação de controle de dados.

![confirmação de seleção](/help/rtcdp/destinations/assets/data-policy-violation.png)

Se nenhuma violação de política tiver sido detectada, selecione **[!UICONTROL Concluir]** para confirmar sua seleção e start enviando dados para o destino.

![confirmação de seleção](/help/rtcdp/destinations/assets/Airship-tags-review.png)


## Uso e governança de dados {#data-usage-governance}

Todos os [!DNL Adobe Experience Platform] destinos são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplicar o controle de dados, consulte [Controle de dados em CDP](/help/rtcdp/privacy/data-governance-overview.md)em tempo real.

