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

Para que a Adobe Experience Platform processe os dados de consentimento do cliente de acordo com o IAB [!DNL Transparency & Consent Framework] (TCF) 2.0, esses dados devem ser enviados para conjuntos de dados cujos esquemas contêm campos de consentimento TCF 2.0.

Especificamente, dois conjuntos de dados são necessários para capturar dados de consentimento do TCF 2.0:

* Um conjunto de dados com base na variável [!DNL XDM Individual Profile] classe, ativada para uso em [!DNL Real-Time Customer Profile].
* Um conjunto de dados com base na variável [!DNL XDM ExperienceEvent] classe.

>[!IMPORTANT]
>
>A Platform só impõe as cadeias de caracteres TCF coletadas no conjunto de dados do Perfil individual. Embora um conjunto de dados ExperienceEvent ainda seja necessário para criar um fluxo de dados como parte desse fluxo de trabalho, você só precisa assimilar dados no conjunto de dados do perfil. O conjunto de dados ExperienceEvent ainda pode ser usado se você quiser rastrear eventos de alteração de consentimento ao longo do tempo, mas esses valores não são usados ao impor na ativação do segmento.

Este documento fornece etapas para configurar esses dois conjuntos de dados. Para obter uma visão geral do workflow completo para configurar as operações de dados da Platform para TCF 2.0, consulte o [Visão geral da conformidade com a TCF 2.0 do IAB](./overview.md).

## Pré-requisitos

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Experience Data Model (XDM)](../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM.
* [Serviço de identidade da Adobe Experience Platform](../../../../identity-service/home.md): permite conectar as identidades dos clientes a partir de diferentes fontes de dados em dispositivos e sistemas.
   * [Namespaces de identidade](../../../../identity-service/features/namespaces.md): os dados de identidade do cliente devem ser fornecidos em um namespace de identidade específico reconhecido pelo Serviço de identidade.
* [Perfil do cliente em tempo real](../../../../profile/home.md): Aproveita [!DNL Identity Service] para permitir que você crie perfis detalhados do cliente a partir de seus conjuntos de dados em tempo real. [!DNL Real-Time Customer Profile] O extrai dados do Data Lake e mantém perfis de clientes em seu próprio armazenamento de dados separado.

## Grupos de campos TCF 2.0 {#field-groups}

A variável [!UICONTROL Detalhes do consentimento da TCF 2.0 do IAB] O grupo de campos de esquema fornece campos de consentimento do cliente necessários para o suporte ao TCF 2.0. Há duas versões desse grupo de campos: uma compatível com a variável [!DNL XDM Individual Profile] e a outra com a variável [!DNL XDM ExperienceEvent] classe.

As seções abaixo explicam a estrutura de cada um desses grupos de campos, incluindo os dados esperados durante a assimilação.

### Grupo de campos de perfil {#profile-field-group}

Para esquemas baseados em [!DNL XDM Individual Profile], o [!UICONTROL Detalhes do consentimento da TCF 2.0 do IAB] o grupo de campos fornece um único campo do tipo mapa, `identityPrivacyInfo`, que mapeia as identidades dos clientes de acordo com as preferências de consentimento da TCF. Esse grupo de campos deve ser incluído em um esquema baseado em registro habilitado para o Perfil do cliente em tempo real para que a imposição automática ocorra.

Consulte a [guia de referência](../../../../xdm/field-groups/profile/iab.md) para que este grupo de campos saiba mais sobre a estrutura e o caso de uso.

### Grupo de campos de evento {#event-field-group}

Se você quiser rastrear eventos de alteração de consentimento ao longo do tempo, poderá adicionar o [!UICONTROL Detalhes do consentimento da TCF 2.0 do IAB] grupo de campos para o seu [!UICONTROL XDM ExperienceEvent] esquema.

Se você não planeja rastrear os eventos de alteração de consentimento ao longo do tempo, não é necessário incluir esse grupo de campos no esquema do evento. Ao aplicar automaticamente os valores de consentimento da TCF, o Experience Platform usa apenas as informações de consentimento mais recentes assimiladas na [grupo de campos de perfil](#profile-field-group). Os valores de consentimento capturados pelos eventos não participam dos fluxos de trabalho de aplicação automática.

Consulte a [guia de referência](../../../../xdm/field-groups/event/iab.md) para este grupo de campos para obter mais informações sobre sua estrutura e caso de uso.

## Criar esquemas de consentimento do cliente {#create-schemas}

Para criar conjuntos de dados que capturem dados de consentimento, primeiro você deve criar esquemas XDM para basear esses conjuntos de dados.

Como mencionado na seção anterior, um schema que usa o [!UICONTROL Perfil individual XDM] A classe é necessária para impor o consentimento em workflows downstream da Platform. Opcionalmente, também é possível criar um esquema separado com base em [!UICONTROL XDM ExperienceEvent] se desejar rastrear as alterações de consentimento ao longo do tempo. Ambos os esquemas devem conter um `identityMap` e um grupo de campos TCF 2.0 apropriado.

Na interface do usuário da Platform, selecione **[!UICONTROL Esquemas]** na navegação à esquerda, para abrir a [!UICONTROL Esquemas] espaço de trabalho. Aqui, siga as etapas nas seções abaixo para criar cada schema necessário.

>[!NOTE]
>
>Se, em vez disso, você tiver esquemas XDM existentes que deseja usar para capturar dados de consentimento, poderá editar esses esquemas em vez de criar novos. No entanto, se um esquema existente tiver sido ativado para uso no Perfil do cliente em tempo real, sua identidade principal não poderá ser um campo diretamente identificável que esteja proibido de usar em anúncios baseados em interesses, como um endereço de email. Consulte seu advogado se não tiver certeza de quais campos são restritos.
>
>Além disso, ao editar esquemas existentes, somente alterações aditivas (não separáveis) podem ser feitas. Consulte a seção sobre o [princípios da evolução do schema](../../../../xdm/schema/composition.md#evolution) para obter mais informações.

### Criar um esquema de consentimento de perfil {#profile-schema}

Selecionar **[!UICONTROL Criar esquema]** e escolha **[!UICONTROL Perfil individual XDM]** no menu suspenso.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

A variável **[!UICONTROL Adicionar grupos de campos]** será exibida, permitindo que você comece a adicionar grupos de campos ao esquema imediatamente. Aqui, selecione **[!UICONTROL Detalhes do consentimento da TCF 2.0 do IAB]** da lista. Opcionalmente, é possível usar a barra de pesquisa para restringir os resultados e localizar o grupo de campos com mais facilidade.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

Em seguida, localize o **[!UICONTROL IdentityMap]** grupo de campos na lista e selecione-o também. Depois que ambos os grupos de campos forem listados no painel direito, selecione **[!UICONTROL Adicionar grupos de campos]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-identitymap.png)

A tela será exibida novamente, mostrando que a variável `identityPrivacyInfo` e `identityMap` Os campos foram adicionados à estrutura do esquema.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

Antes de adicionar mais campos ao esquema, selecione o campo raiz a ser revelado **[!UICONTROL Propriedades do esquema]** no painel direito, onde você pode fornecer um nome e uma descrição para o esquema.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-profile.png)

Depois de fornecer um nome e uma descrição, você pode adicionar mais campos ao esquema selecionando **[!UICONTROL Adicionar]** no **[!UICONTROL Grupos de campos]** no lado esquerdo da tela.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-profile.png)

Se você estiver editando um esquema existente que já foi ativado para uso no [!DNL Real-Time Customer Profile], selecione **[!UICONTROL Salvar]** para confirmar as alterações antes de pular para a seção sobre [criar um conjunto de dados com base no seu esquema de consentimento](#dataset). Se estiver criando um novo schema, continue seguindo as etapas descritas na subseção abaixo.

#### Ativar o esquema para uso no [!DNL Real-Time Customer Profile]

Para que a Platform associe os dados de consentimento que recebe a perfis de clientes específicos, o esquema de consentimento deve ser ativado para uso no [!DNL Real-Time Customer Profile].

>[!NOTE]
>
>O schema de exemplo mostrado nesta seção usa suas `identityMap` como sua identidade principal. Se quiser definir outro campo como identidade primária, certifique-se de que você esteja usando um identificador indireto, como uma ID de cookie, e não um campo diretamente identificável que esteja proibido de usar em publicidade baseada em interesses, como um endereço de email. Consulte seu advogado se não tiver certeza de quais campos são restritos.
>
>As etapas sobre como definir um campo de identidade principal para um esquema podem ser encontradas no [[!UICONTROL Esquemas] Guia da interface do usuário](../../../../xdm/ui/fields/identity.md).

Para ativar o esquema para [!DNL Profile], selecione o nome do esquema no painel à esquerda para abrir a **[!UICONTROL Propriedades do esquema]** seção. Aqui, selecione a variável **[!UICONTROL Perfil]** botão de alternância.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

Um popover é exibido, indicando uma identidade principal ausente. Marque a caixa de seleção para usar uma identidade principal alternativa, pois a identidade principal estará contida na `identityMap` campo.

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

Finalmente, selecione **[!UICONTROL Salvar]** para confirmar as alterações.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### Criar um esquema de consentimento de evento {#event-schema}

>[!NOTE]
>
>Os esquemas de consentimento de evento são usados apenas para rastrear eventos de alteração de consentimento ao longo do tempo e não participam de workflows de imposição de downstream. Se você não quiser rastrear as alterações de consentimento ao longo do tempo, pule para a próxima seção em [criação de conjuntos de dados de consentimento](#datasets).

No **[!UICONTROL Esquemas]** espaço de trabalho, selecione **[!UICONTROL Criar esquema]** e escolha **[!UICONTROL XDM ExperienceEvent]** na lista suspensa.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

A variável **[!UICONTROL Adicionar grupos de campos]** será exibida. Aqui, selecione **[!UICONTROL Detalhes do consentimento da TCF 2.0 do IAB]** da lista. Opcionalmente, é possível usar a barra de pesquisa para restringir os resultados e localizar o grupo de campos com mais facilidade.


![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

Em seguida, localize o **[!UICONTROL IdentityMap]** grupo de campos na lista e selecione-o também. Depois que ambos os grupos de campos forem listados no painel direito, selecione **[!UICONTROL Adicionar grupos de campos]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-identitymap.png)

A tela será exibida novamente, mostrando que a variável `consentStrings` e `identityMap` Os campos foram adicionados à estrutura do esquema.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

Antes de adicionar mais campos ao esquema, selecione o campo raiz a ser revelado **[!UICONTROL Propriedades do esquema]** no painel direito, onde você pode fornecer um nome e uma descrição para o esquema.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-event.png)

Depois de fornecer um nome e uma descrição, você pode adicionar mais campos ao esquema selecionando **[!UICONTROL Adicionar]** no **[!UICONTROL Grupos de campos]** no lado esquerdo da tela.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-event.png)

Depois que os grupos de campos necessários tiverem sido adicionados, conclua selecionando **[!UICONTROL Salvar]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-field-groups.png)

## Criar conjuntos de dados com base em seus esquemas de consentimento {#datasets}

Para cada um dos esquemas necessários descritos acima, você deve criar um conjunto de dados que assimilará os dados de consentimento dos clientes. O conjunto de dados com base no esquema de registro deve ser ativado para [!DNL Real-Time Customer Profile], enquanto o conjunto de dados com base no esquema de série temporal **não deve** ser [!DNL Profile]-habilitado.

Para começar, selecione **[!UICONTROL Conjuntos de dados]** na navegação à esquerda, selecione **[!UICONTROL Criar conjunto de dados]** no canto superior direito.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create.png)

Na próxima página, selecione **[!UICONTROL Criar conjunto de dados a partir do esquema]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create-from-schema.png)

A variável **[!UICONTROL Criar conjunto de dados a partir do esquema]** workflow aparece, começando no **[!UICONTROL Selecionar esquema]** etapa. Na lista fornecida, localize um dos esquemas de consentimento criados anteriormente. Opcionalmente, é possível usar a barra de pesquisa para restringir os resultados e localizar seu esquema com mais facilidade. Selecione o botão de opção ao lado do esquema desejado e selecione **[!UICONTROL Próxima]** para continuar.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-select-schema.png)

A variável **[!UICONTROL Configurar conjunto de dados]** é exibida. Forneça um nome e uma descrição exclusivos e de fácil identificação para o conjunto de dados antes de selecionar **[!UICONTROL Concluir]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-configure.png)

A página de detalhes do conjunto de dados recém-criado é exibida. Se o conjunto de dados for baseado no esquema de série temporal, o processo será concluído. Se o conjunto de dados for baseado no esquema de registro, a etapa final do processo será ativar o conjunto de dados para uso no [!DNL Real-Time Customer Profile].

No painel direito, selecione a variável **[!UICONTROL Perfil]** alterne, selecione **[!UICONTROL Ativar]** no popover de confirmação para ativar o esquema para [!DNL Profile].

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

Siga as etapas acima novamente para criar um conjunto de dados baseado em eventos se você tiver criado um esquema para ele.

## Próximas etapas

Seguindo este tutorial, você criou pelo menos um conjunto de dados que agora pode ser usado para coletar dados de consentimento do cliente:

* Um conjunto de dados baseado em registro que é ativado para uso no Perfil do cliente em tempo real. **(Obrigatório)**
* Um conjunto de dados baseado em séries temporais que não está habilitado para [!DNL Profile]. (Opcional)

Agora você pode retornar ao [Visão geral do IAB TCF 2.0](./overview.md#merge-policies) para continuar o processo de configuração da conformidade da Platform for TCF 2.0.
