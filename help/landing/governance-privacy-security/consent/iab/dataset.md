---
keywords: Experience Platform; home; IAB; IAB 2.0; consentimento; Consentimento
solution: Experience Platform
title: Criar conjuntos de dados para capturar dados de consentimento do IAB TCF 2.0
description: Este documento fornece etapas para configurar os dois conjuntos de dados necessários para coletar dados de consentimento do IAB TCF 2.0.
exl-id: 36b2924d-7893-4c55-bc33-2c0234f1120e
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1655'
ht-degree: 0%

---

# Criar conjuntos de dados para capturar dados de consentimento do IAB TCF 2.0

Para que a Adobe Experience Platform processe os dados de consentimento do cliente de acordo com o IAB [!DNL Transparency & Consent Framework] (TCF) 2.0, esses dados devem ser enviados para conjuntos de dados cujos esquemas contêm campos de consentimento TCF 2.0.

Especificamente, dois conjuntos de dados são necessários para capturar dados de consentimento do TCF 2.0:

* Um conjunto de dados com base na variável [!DNL XDM Individual Profile] classe, habilitada para uso em [!DNL Real-Time Customer Profile].
* Um conjunto de dados com base na variável [!DNL XDM ExperienceEvent] classe .

>[!IMPORTANT]
>
>A Platform aplica somente as cadeias de caracteres TCF coletadas no conjunto de dados Perfil individual . Embora um conjunto de dados ExperienceEvent ainda seja necessário para criar um conjunto de dados como parte desse fluxo de trabalho, é necessário assimilar dados somente no conjunto de dados do perfil. O conjunto de dados ExperienceEvent ainda pode ser usado se você deseja rastrear eventos de alteração de consentimento ao longo do tempo, mas esses valores não são usados em ao impor na ativação do segmento.

Este documento fornece etapas para configurar esses dois conjuntos de dados. Para obter uma visão geral do fluxo de trabalho completo para configurar as operações de dados da plataforma para TCF 2.0, consulte [Visão geral de conformidade do TCF 2.0 do IAB](./overview.md).

## Pré-requisitos

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Experience Data Model (XDM)](../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../xdm/schema/composition.md): Saiba mais sobre os componentes básicos dos esquemas XDM.
* [Serviço de identidade da Adobe Experience Platform](../../../../identity-service/home.md): Permite que você conecte identidades de clientes de suas diferentes fontes de dados entre dispositivos e sistemas.
   * [Namespaces de identidade](../../../../identity-service/namespaces.md): Os dados de identidade do cliente devem ser fornecidos em um namespace de identidade específico reconhecido pelo Serviço de identidade.
* [Perfil do cliente em tempo real](../../../../profile/home.md): Aproveitamento [!DNL Identity Service] para permitir que você crie perfis de clientes detalhados a partir de seus conjuntos de dados em tempo real. [!DNL Real-Time Customer Profile] extrai dados do Data Lake e mantém perfis de clientes em seu próprio armazenamento de dados separado.

## Grupos de campos TCF 2.0 {#field-groups}

O [!UICONTROL Detalhes do consentimento da TCF do IAB 2.0] grupo de campos schema fornece campos de consentimento do cliente necessários para o suporte ao TCF 2.0. Há duas versões desse grupo de campos: compatível com o [!DNL XDM Individual Profile] classe e a outra com a [!DNL XDM ExperienceEvent] classe .

As seções abaixo explicam a estrutura de cada um desses grupos de campos, incluindo os dados esperados durante a assimilação.

### Grupo de campos de perfil {#profile-field-group}

Para esquemas baseados em [!DNL XDM Individual Profile], o [!UICONTROL Detalhes do consentimento da TCF do IAB 2.0] grupo de campos fornece um único campo do tipo mapa, `identityPrivacyInfo`, que mapeia as identidades do cliente para suas preferências de consentimento da TCF. Esse grupo de campos deve ser incluído em um schema baseado em registro habilitado para o Perfil do cliente em tempo real para que a imposição automática ocorra.

Consulte a [guia de referência](../../../../xdm/field-groups/profile/iab.md) para que esse grupo de campos saiba mais sobre sua estrutura e caso de uso.

### Grupo de campos Evento {#event-field-group}

Se quiser rastrear eventos de alteração de consentimento ao longo do tempo, é possível adicionar a variável [!UICONTROL Detalhes do consentimento da TCF do IAB 2.0] grupo de campos para sua [!UICONTROL ExperiênciaEvento XDM] esquema.

Se você não planeja rastrear eventos de alteração de consentimento ao longo do tempo, não é necessário incluir esse grupo de campos no esquema de evento. Ao impor automaticamente valores de consentimento da TCF, o Experience Platform só usa as informações de consentimento mais recentes assimiladas na variável [grupo de campos de perfil](#profile-field-group). Os valores de consentimento capturados pelos eventos não participam dos workflows de imposição automática.

Consulte a [guia de referência](../../../../xdm/field-groups/event/iab.md) para esse grupo de campos para obter mais informações sobre sua estrutura e caso de uso.

## Criar esquemas de consentimento do cliente {#create-schemas}

Para criar conjuntos de dados que capturam dados de consentimento, primeiro crie esquemas XDM para basear esses conjuntos de dados.

Conforme mencionado na seção anterior, um schema que usa a variável [!UICONTROL Perfil individual XDM] A classe é necessária para impor o consentimento em workflows da plataforma downstream. Opcionalmente, também é possível criar um schema separado com base em [!UICONTROL ExperiênciaEvento XDM] se desejar rastrear as alterações de consentimento ao longo do tempo. Ambos os schemas devem conter um `identityMap` e um grupo de campos TCF 2.0 apropriado.

Na interface do usuário da plataforma, selecione **[!UICONTROL Esquemas]** na navegação à esquerda para abrir o [!UICONTROL Esquemas] espaço de trabalho. A partir daqui, siga as etapas nas seções abaixo para criar cada schema necessário.

>[!NOTE]
>
>Se você tiver esquemas XDM existentes que deseja usar para capturar dados de consentimento, edite esses esquemas em vez de criar novos. No entanto, se um esquema existente tiver sido ativado para uso no Perfil do cliente em tempo real, sua identidade primária não poderá ser um campo diretamente identificável que seja proibido de usar em publicidade com base em interesses, como um endereço de email. Consulte seu consultor jurídico se não tiver certeza de quais campos são restritos.
>
>Além disso, ao editar schemas existentes, somente alterações aditivas (ininterruptas) podem ser feitas. Consulte a seção sobre o [princípios da evolução do schema](../../../../xdm/schema/composition.md#evolution) para obter mais informações.

### Criar um esquema de consentimento de perfil {#profile-schema}

Selecionar **[!UICONTROL Criar esquema]** e escolha **[!UICONTROL Perfil individual XDM]** no menu suspenso.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-profile.png)

O **[!UICONTROL Adicionar grupos de campos]** for exibida, permitindo que você comece a adicionar grupos de campos ao esquema imediatamente. Aqui, selecione **[!UICONTROL Detalhes do consentimento da TCF do IAB 2.0]** na lista. Como opção, você pode usar a barra de pesquisa para restringir os resultados para localizar o grupo de campos mais facilmente.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-privacy.png)

Em seguida, encontre a **[!UICONTROL IdentityMap]** grupo de campos na lista e selecione-o também. Depois que ambos os grupos de campos estiverem listados no painel direito, selecione **[!UICONTROL Adicionar grupos de campos]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-profile-identitymap.png)

A tela reaparece, mostrando que a variável `identityPrivacyInfo` e `identityMap` foram adicionados à estrutura do schema.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-privacy-structure.png)

Antes de adicionar mais campos ao schema, selecione o campo raiz a ser revelado **[!UICONTROL Propriedades do schema]** no painel direito, onde é possível fornecer um nome e uma descrição para o schema.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-profile.png)

Após fornecer um nome e uma descrição, é possível adicionar mais campos ao schema selecionando **[!UICONTROL Adicionar]** nos termos do **[!UICONTROL Grupos de campos]** no lado esquerdo da tela.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-profile.png)

Se você estiver editando um esquema existente que já foi ativado para uso no [!DNL Real-Time Customer Profile], selecione **[!UICONTROL Salvar]** para confirmar as alterações antes de pular para a seção em [criação de um conjunto de dados com base em seu esquema de consentimento](#dataset). Se estiver criando um novo schema, continue seguindo as etapas descritas na subseção abaixo.

#### Ative o esquema para usar em [!DNL Real-Time Customer Profile]

Para que a Platform associe os dados de consentimento que recebe a perfis de clientes específicos, o schema de consentimento deve ser ativado para uso em [!DNL Real-Time Customer Profile].

>[!NOTE]
>
>O schema de exemplo mostrado nesta seção usa seu `identityMap` como sua identidade primária. Se desejar definir outro campo como uma identidade primária, verifique se você está usando um identificador indireto como uma ID de cookie e não um campo diretamente identificável que é proibido de usar em publicidade com base em interesses, como um endereço de email. Consulte seu consultor jurídico se não tiver certeza de quais campos são restritos.
>
>As etapas sobre como definir um campo de identidade primário para um schema podem ser encontradas no [[!UICONTROL Esquemas] Guia da interface do usuário](../../../../xdm/ui/fields/identity.md).

Para habilitar o esquema para [!DNL Profile], selecione o nome do schema no painel esquerdo para abrir o **[!UICONTROL Propriedades do schema]** seção. Aqui, selecione o **[!UICONTROL Perfil]** botão de alternância.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-enable-profile.png)

Um provedor é exibido, indicando uma identidade primária ausente. Marque a caixa de seleção para usar uma identidade primária alternativa, pois a identidade primária estará contida no `identityMap` campo.

![](../../../images/governance-privacy-security/consent/iab/dataset/missing-primary-identity.png)

Finalmente, selecione **[!UICONTROL Salvar]** para confirmar as alterações.

![](../../../images/governance-privacy-security/consent/iab/dataset/profile-save.png)

### Criar um esquema de consentimento de evento {#event-schema}

>[!NOTE]
>
>Os esquemas de consentimento do evento são usados apenas para rastrear eventos de alteração de consentimento ao longo do tempo e não participam de workflows de imposição de downstream. Se não quiser rastrear as alterações de consentimento ao longo do tempo, ignore a próxima seção em [criar conjuntos de dados de consentimento](#datasets).

No **[!UICONTROL Esquemas]** espaço de trabalho, selecione **[!UICONTROL Criar esquema]** e escolha **[!UICONTROL ExperiênciaEvento XDM]** na lista suspensa.

![](../../../images/governance-privacy-security/consent/iab/dataset/create-schema-event.png)

O **[!UICONTROL Adicionar grupos de campos]** será exibida. Aqui, selecione **[!UICONTROL Detalhes do consentimento da TCF do IAB 2.0]** na lista. Como opção, você pode usar a barra de pesquisa para restringir os resultados para localizar o grupo de campos mais facilmente.


![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-privacy.png)

Em seguida, encontre a **[!UICONTROL IdentityMap]** grupo de campos na lista e selecione-o também. Depois que ambos os grupos de campos estiverem listados no painel direito, selecione **[!UICONTROL Adicionar grupos de campos]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-event-identitymap.png)

A tela reaparece, mostrando que a variável `consentStrings` e `identityMap` foram adicionados à estrutura do schema.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-privacy-structure.png)

Antes de adicionar mais campos ao schema, selecione o campo raiz a ser revelado **[!UICONTROL Propriedades do schema]** no painel direito, onde é possível fornecer um nome e uma descrição para o schema.

![](../../../images/governance-privacy-security/consent/iab/dataset/schema-details-event.png)

Após fornecer um nome e uma descrição, é possível adicionar mais campos ao schema selecionando **[!UICONTROL Adicionar]** nos termos do **[!UICONTROL Grupos de campos]** no lado esquerdo da tela.

![](../../../images/governance-privacy-security/consent/iab/dataset/add-field-group-event.png)

Depois que os grupos de campos necessários tiverem sido adicionados, conclua selecionando **[!UICONTROL Salvar]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/event-all-field-groups.png)

## Criar conjuntos de dados com base em seus esquemas de consentimento {#datasets}

Para cada um dos esquemas obrigatórios descritos acima, você deve criar um conjunto de dados que, em última análise, assimilará os dados de consentimento de seus clientes. O conjunto de dados baseado no esquema de registro deve ser habilitado para [!DNL Real-Time Customer Profile], enquanto o conjunto de dados se baseia no esquema da série de tempo **não deve** be [!DNL Profile]habilitado para .

Para começar, selecione **[!UICONTROL Conjuntos de dados]** na navegação à esquerda, selecione **[!UICONTROL Criar conjunto de dados]** no canto superior direito.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create.png)

Na próxima página, selecione **[!UICONTROL Criar conjunto de dados a partir do esquema]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-create-from-schema.png)

O **[!UICONTROL Criar conjunto de dados a partir do esquema]** for exibido, começando no **[!UICONTROL Selecionar esquema]** etapa. Na lista fornecida, localize um dos esquemas de consentimento criados anteriormente. Como opção, você pode usar a barra de pesquisa para restringir os resultados e localizar o esquema mais fácil. Selecione o botão de opção ao lado do esquema desejado e selecione **[!UICONTROL Próximo]** para continuar.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-select-schema.png)

O **[!UICONTROL Configurar conjunto de dados]** será exibida. Fornecer um nome e uma descrição exclusivos e facilmente identificáveis para o conjunto de dados antes de selecionar **[!UICONTROL Concluir]**.

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-configure.png)

A página de detalhes do conjunto de dados recém-criado é exibida. Se o conjunto de dados se basear no esquema da série de tempo, o processo será concluído. Se o conjunto de dados se basear no esquema de registro, a etapa final no processo será habilitar o conjunto de dados para uso em [!DNL Real-Time Customer Profile].

No painel direito, selecione o **[!UICONTROL Perfil]** alternar e selecionar **[!UICONTROL Habilitar]** no provedor de confirmação para habilitar o schema de [!DNL Profile].

![](../../../images/governance-privacy-security/consent/iab/dataset/dataset-enable-profile.png)

Siga as etapas acima novamente para criar um conjunto de dados baseado em eventos se você tiver criado um esquema para ele.

## Próximas etapas

Ao seguir este tutorial, você criou pelo menos um conjunto de dados que pode ser usado para coletar dados de consentimento do cliente:

* Um conjunto de dados baseado em registros habilitado para uso no Perfil do cliente em tempo real. **(Obrigatório)**
* Um conjunto de dados baseado em séries de tempo que não está habilitado para [!DNL Profile]. (Opcional)

Agora você pode retornar ao [Visão geral do TCF do IAB 2.0](./overview.md#merge-policies) para continuar o processo de configuração da plataforma para conformidade com o TCF 2.0.
