---
keywords: Experience Platform;inicial;IAB;IAB 2.0;consentimento;Consentimento
solution: Experience Platform
title: Criar conjuntos de dados para capturar dados de consentimento da TCF 2.0 do IAB
description: Este documento fornece etapas para configurar os dois conjuntos de dados necessários para coletar dados de consentimento da TCF 2.0 do IAB.
exl-id: 36b2924d-7893-4c55-bc33-2c0234f1120e
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1674'
ht-degree: 0%

---

# Criar conjuntos de dados para capturar dados de consentimento da TCF 2.0 do IAB

Para que o Adobe Experience Platform processe dados de consentimento do cliente de acordo com o IAB [!DNL Transparency & Consent Framework] (TCF) 2.0, esses dados devem ser enviados para conjuntos de dados cujos esquemas contêm campos de consentimento TCF 2.0.

Especificamente, dois conjuntos de dados são necessários para capturar dados de consentimento do TCF 2.0:

* Um conjunto de dados baseado na classe [!DNL XDM Individual Profile], habilitado para uso em [!DNL Real-Time Customer Profile].
* Um conjunto de dados baseado na classe [!DNL XDM ExperienceEvent].

>[!IMPORTANT]
>
>A Platform só impõe as cadeias de caracteres TCF coletadas no conjunto de dados do Perfil individual. Embora um conjunto de dados ExperienceEvent ainda seja necessário para criar um fluxo de dados como parte desse fluxo de trabalho, você só precisa assimilar dados no conjunto de dados do perfil. O conjunto de dados ExperienceEvent ainda pode ser usado se você quiser rastrear eventos de alteração de consentimento ao longo do tempo, mas esses valores não são usados ao impor na ativação do segmento.

Este documento fornece etapas para configurar esses dois conjuntos de dados. Para obter uma visão geral do fluxo de trabalho completo para configurar as operações de dados da Platform para TCF 2.0, consulte a [visão geral de conformidade do IAB TCF 2.0](./overview.md).

## Pré-requisitos

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Experience Data Model (XDM)](../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM.
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md): permite conectar as identidades dos clientes de suas diferentes fontes de dados em dispositivos e sistemas.
   * [Namespaces de identidade](../../../../identity-service/features/namespaces.md): os dados de identidade do cliente devem ser fornecidos em um namespace de identidade específico reconhecido pelo Serviço de Identidade.
* [Perfil do cliente em tempo real](../../../../profile/home.md): aproveita o [!DNL Identity Service] para permitir que você crie perfis detalhados do cliente a partir dos seus conjuntos de dados em tempo real. [!DNL Real-Time Customer Profile] extrai dados do Data Lake e mantém perfis de clientes em seu próprio armazenamento de dados separado.

## Grupos de campos TCF 2.0 {#field-groups}

O grupo de campos de esquema [!UICONTROL Detalhes do consentimento] da TCF 2.0 do IAB fornece campos de consentimento do cliente necessários para o suporte à TCF 2.0. Há duas versões deste grupo de campos: uma compatível com a classe [!DNL XDM Individual Profile] e a outra com a classe [!DNL XDM ExperienceEvent].

As seções abaixo explicam a estrutura de cada um desses grupos de campos, incluindo os dados esperados durante a assimilação.

### Grupo de campos de perfil {#profile-field-group}

Para esquemas baseados em [!DNL XDM Individual Profile], o grupo de campos [!UICONTROL Detalhes do Consentimento da TCF 2.0 do IAB] fornece um único campo do tipo mapa, `identityPrivacyInfo`, que mapeia as identidades do cliente para suas preferências de consentimento da TCF. Esse grupo de campos deve ser incluído em um esquema baseado em registro habilitado para o Perfil do cliente em tempo real para que a imposição automática ocorra.

Consulte o [guia de referência](../../../../xdm/field-groups/profile/iab.md) deste grupo de campos para saber mais sobre sua estrutura e caso de uso.

### Grupo de campos de evento {#event-field-group}

Se você quiser rastrear eventos de alteração de consentimento ao longo do tempo, poderá adicionar o grupo de campos [!UICONTROL Detalhes do consentimento] da TCF do IAB ao seu esquema [!UICONTROL XDM ExperienceEvent].

Se você não planeja rastrear os eventos de alteração de consentimento ao longo do tempo, não é necessário incluir esse grupo de campos no esquema do evento. Ao impor automaticamente valores de consentimento TCF, o Experience Platform usa apenas as informações de consentimento mais recentes assimiladas no [grupo de campos de perfil](#profile-field-group). Os valores de consentimento capturados pelos eventos não participam dos fluxos de trabalho de aplicação automática.

Consulte o [guia de referência](../../../../xdm/field-groups/event/iab.md) deste grupo de campos para obter mais informações sobre sua estrutura e caso de uso.

## Criar esquemas de consentimento do cliente {#create-schemas}

Para criar conjuntos de dados que capturem dados de consentimento, primeiro você deve criar esquemas XDM para basear esses conjuntos de dados.

Conforme mencionado na seção anterior, um esquema que usa a classe [!UICONTROL Perfil Individual XDM] é necessário para impor o consentimento em fluxos de trabalho de plataforma downstream. Opcionalmente, também é possível criar um esquema separado com base no [!UICONTROL XDM ExperienceEvent] se desejar rastrear as alterações de consentimento ao longo do tempo. Ambos os esquemas devem conter um campo `identityMap` e um grupo de campos TCF 2.0 apropriado.

Na interface da Platform, selecione **[!UICONTROL Esquemas]** na navegação à esquerda para abrir o espaço de trabalho [!UICONTROL Esquemas]. Aqui, siga as etapas nas seções abaixo para criar cada schema necessário.

>[!NOTE]
>
>Se, em vez disso, você tiver esquemas XDM existentes que deseja usar para capturar dados de consentimento, poderá editar esses esquemas em vez de criar novos. No entanto, se um esquema existente tiver sido ativado para uso no Perfil do cliente em tempo real, sua identidade principal não poderá ser um campo diretamente identificável que esteja proibido de usar em anúncios baseados em interesses, como um endereço de email. Consulte seu advogado se não tiver certeza de quais campos são restritos.
>
>Além disso, ao editar esquemas existentes, somente alterações aditivas (não separáveis) podem ser feitas. Consulte a seção sobre os [princípios da evolução do esquema](../../../../xdm/schema/composition.md#evolution) para obter mais informações.

### Criar um esquema de consentimento de perfil {#profile-schema}

Selecione **[!UICONTROL Criar esquema]** e escolha **[!UICONTROL Perfil Individual XDM]** no menu suspenso.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

A caixa de diálogo **[!UICONTROL Adicionar grupos de campos]** é exibida, permitindo que você comece a adicionar grupos de campos ao esquema imediatamente. Aqui, selecione **[!UICONTROL Detalhes do consentimento da TCF 2.0 do IAB]** na lista. Opcionalmente, é possível usar a barra de pesquisa para restringir os resultados e localizar o grupo de campos com mais facilidade.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

Em seguida, localize o grupo de campos **[!UICONTROL IdentityMap]** na lista e selecione-o também. Depois que ambos os grupos de campos forem listados no painel direito, selecione **[!UICONTROL Adicionar grupos de campos]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-identitymap.png)

A tela será exibida novamente, mostrando que os campos `identityPrivacyInfo` e `identityMap` foram adicionados à estrutura do esquema.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

Antes de adicionar mais campos ao esquema, selecione o campo raiz para revelar **[!UICONTROL propriedades do esquema]** no painel direito, onde você pode fornecer um nome e uma descrição para o esquema.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-profile.png)

Depois de fornecer um nome e uma descrição, você pode, opcionalmente, adicionar mais campos ao esquema selecionando **[!UICONTROL Adicionar]** na seção **[!UICONTROL Grupos de campos]** no lado esquerdo da tela.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-profile.png)

Se você estiver editando um esquema existente que já foi habilitado para uso em [!DNL Real-Time Customer Profile], selecione **[!UICONTROL Salvar]** para confirmar suas alterações antes de avançar para a seção sobre [criação de um conjunto de dados com base no seu esquema de consentimento](#dataset). Se estiver criando um novo schema, continue seguindo as etapas descritas na subseção abaixo.

#### Habilitar o esquema para uso em [!DNL Real-Time Customer Profile]

Para que a Platform associe os dados de consentimento que recebe a perfis de clientes específicos, o esquema de consentimento deve ser habilitado para uso em [!DNL Real-Time Customer Profile].

>[!NOTE]
>
>O esquema de exemplo mostrado nesta seção usa seu campo `identityMap` como sua identidade primária. Se quiser definir outro campo como identidade primária, certifique-se de que você esteja usando um identificador indireto, como uma ID de cookie, e não um campo diretamente identificável que esteja proibido de usar em publicidade baseada em interesses, como um endereço de email. Consulte seu advogado se não tiver certeza de quais campos são restritos.
>
>As etapas sobre como definir um campo de identidade principal para um esquema podem ser encontradas no [[!UICONTROL guia da interface do usuário de Esquemas]](../../../../xdm/ui/fields/identity.md).

Para habilitar o esquema para [!DNL Profile], selecione o nome do esquema no painel esquerdo para abrir a seção **[!UICONTROL Propriedades do esquema]**. Aqui, selecione o botão de alternância **[!UICONTROL Perfil]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

Um popover é exibido, indicando uma identidade principal ausente. Marque a caixa de seleção para usar uma identidade principal alternativa, pois a identidade principal estará contida no campo `identityMap`.

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

Finalmente, selecione **[!UICONTROL Salvar]** para confirmar as alterações.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### Criar um esquema de consentimento de evento {#event-schema}

>[!NOTE]
>
>Os esquemas de consentimento de evento são usados apenas para rastrear eventos de alteração de consentimento ao longo do tempo e não participam de workflows de imposição de downstream. Se você não quiser rastrear as alterações de consentimento ao longo do tempo, pule para a próxima seção sobre [criação de conjuntos de dados de consentimento](#datasets).

No espaço de trabalho **[!UICONTROL Esquemas]**, selecione **[!UICONTROL Criar esquema]** e escolha **[!UICONTROL XDM ExperienceEvent]** na lista suspensa.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

A caixa de diálogo **[!UICONTROL Adicionar grupos de campos]** é exibida. Aqui, selecione **[!UICONTROL Detalhes do consentimento da TCF 2.0 do IAB]** na lista. Opcionalmente, é possível usar a barra de pesquisa para restringir os resultados e localizar o grupo de campos com mais facilidade.


![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

Em seguida, localize o grupo de campos **[!UICONTROL IdentityMap]** na lista e selecione-o também. Depois que ambos os grupos de campos forem listados no painel direito, selecione **[!UICONTROL Adicionar grupos de campos]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-identitymap.png)

A tela será exibida novamente, mostrando que os campos `consentStrings` e `identityMap` foram adicionados à estrutura do esquema.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

Antes de adicionar mais campos ao esquema, selecione o campo raiz para revelar **[!UICONTROL propriedades do esquema]** no painel direito, onde você pode fornecer um nome e uma descrição para o esquema.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-event.png)

Depois de fornecer um nome e uma descrição, você pode, opcionalmente, adicionar mais campos ao esquema selecionando **[!UICONTROL Adicionar]** na seção **[!UICONTROL Grupos de campos]** no lado esquerdo da tela.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-event.png)

Após adicionar os grupos de campos necessários, conclua selecionando **[!UICONTROL Salvar]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-field-groups.png)

## Criar conjuntos de dados com base em seus esquemas de consentimento {#datasets}

Para cada um dos esquemas necessários descritos acima, você deve criar um conjunto de dados que assimilará os dados de consentimento dos clientes. O conjunto de dados baseado no esquema de registro deve ser habilitado para [!DNL Real-Time Customer Profile], enquanto o conjunto de dados baseado no esquema de série temporal **não deve** ser habilitado para [!DNL Profile].

Para começar, selecione **[!UICONTROL Conjuntos de dados]** na navegação à esquerda e selecione **[!UICONTROL Criar conjunto de dados]** no canto superior direito.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create.png)

Na próxima página, selecione **[!UICONTROL Criar conjunto de dados do esquema]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create-from-schema.png)

O fluxo de trabalho **[!UICONTROL Criar conjunto de dados a partir do esquema]** aparece, começando na etapa **[!UICONTROL Selecionar esquema]**. Na lista fornecida, localize um dos esquemas de consentimento criados anteriormente. Opcionalmente, é possível usar a barra de pesquisa para restringir os resultados e localizar seu esquema com mais facilidade. Selecione o botão de opção ao lado do esquema desejado e selecione **[!UICONTROL Avançar]** para continuar.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-select-schema.png)

A etapa **[!UICONTROL Configurar conjunto de dados]** é exibida. Forneça um nome e uma descrição exclusivos e de fácil identificação para o conjunto de dados antes de selecionar **[!UICONTROL Concluir]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-configure.png)

A página de detalhes do conjunto de dados recém-criado é exibida. Se o conjunto de dados for baseado no esquema de série temporal, o processo será concluído. Se o conjunto de dados for baseado no esquema do seu registro, a etapa final no processo será habilitar o conjunto de dados para uso no [!DNL Real-Time Customer Profile].

No painel direito, selecione a opção de alternância **[!UICONTROL Perfil]** e selecione **[!UICONTROL Habilitar]** no popover de confirmação para habilitar o esquema para [!DNL Profile].

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

Siga as etapas acima novamente para criar um conjunto de dados baseado em eventos se você tiver criado um esquema para ele.

## Próximas etapas

Seguindo este tutorial, você criou pelo menos um conjunto de dados que agora pode ser usado para coletar dados de consentimento do cliente:

* Um conjunto de dados baseado em registro que é ativado para uso no Perfil do cliente em tempo real. **(Obrigatório)**
* Um conjunto de dados baseado em série temporal que não está habilitado para [!DNL Profile]. (Opcional)

Agora você pode retornar à [visão geral do IAB TCF 2.0](./overview.md#merge-policies) para continuar o processo de configuração da Platform para conformidade com o TCF 2.0.
