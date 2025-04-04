---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Configurar um conjunto de dados para capturar dados de consentimento e preferência
description: Saiba como configurar um esquema e um conjunto de dados do Experience Data Model (XDM) para capturar dados de consentimento e preferência no Adobe Experience Platform.
role: Developer
feature: Consent, Schemas, Datasets
exl-id: 61ceaa2a-c5ac-43f5-b118-502bdc432234
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 0%

---

# Configurar um conjunto de dados para capturar dados de consentimento e preferência

Para que o Adobe Experience Platform processe os dados de consentimento/preferência do cliente, esses dados devem ser enviados para um conjunto de dados cujo esquema contém campos relacionados a consentimentos e outras permissões. Especificamente, esse conjunto de dados deve ser baseado na classe [!DNL XDM Individual Profile] e habilitado para uso em [!DNL Real-Time Customer Profile].

Este documento fornece etapas para configurar um conjunto de dados para processar dados de consentimento no Experience Platform. Para obter uma visão geral do fluxo de trabalho completo para processar dados de consentimento/preferência no Experience Platform, consulte a [visão geral do processamento de consentimento](./overview.md).

>[!IMPORTANT]
>
>Os exemplos neste guia usam um conjunto padronizado de campos para representar os valores de consentimento do cliente, conforme definido pelo [[!UICONTROL Grupo de campos de esquema de Detalhes de Consentimento e Preferência]](../../../../xdm/field-groups/profile/consents.md). A estrutura desses campos tem como objetivo fornecer um modelo de dados eficiente para abranger muitos casos de uso comuns de coleta de consentimento.
>
>No entanto, você também pode definir seus próprios grupos de campos para representar o consentimento de acordo com seus próprios modelos de dados. Consulte sua equipe jurídica para obter aprovação para um modelo de dados de consentimento que atenda às suas necessidades comerciais, com base nas seguintes opções:
>
>* O grupo de campos de consentimento padronizado
>* Um grupo de campos de consentimento personalizado criado pela sua organização
>* Uma combinação do grupo de campos de consentimento padronizado e campos adicionais fornecidos por um grupo de campos de consentimento personalizado

## Pré-requisitos

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Experience Data Model (XDM)](../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM.
* [Perfil do cliente em tempo real](../../../../profile/home.md): consolida os dados do cliente de diferentes fontes em uma exibição completa e unificada, enquanto oferece uma conta acionável com carimbo de data e hora de cada interação com o cliente.

>[!IMPORTANT]
>
>Este tutorial pressupõe que você conheça o esquema [!DNL Profile] no Experience Platform que deseja usar para capturar informações de atributos do cliente. Independentemente do método usado para coletar dados de consentimento, esse esquema deve ser [habilitado para o Perfil de Cliente em Tempo Real](../../../../xdm/ui/resources/schemas.md#profile). Além disso, a identidade primária do schema não pode ser um campo diretamente identificável que esteja proibido de usar em anúncios baseados em interesses, como um endereço de email. Consulte seu advogado se não tiver certeza de quais campos são restritos.

## Estrutura do grupo de campos [!UICONTROL Detalhes sobre consentimento e preferência] {#structure}

O grupo de campos [!UICONTROL Detalhes sobre Consentimento e Preferência] fornece campos de consentimento padronizados para um esquema. Atualmente, este grupo de campos é compatível apenas com esquemas baseados na classe [!DNL XDM Individual Profile].

O grupo de campos fornece um único campo de tipo de objeto, `consents`, cujas subpropriedades capturam um conjunto de campos de consentimento padronizados. O JSON a seguir é um exemplo do tipo de dados que `consents` espera na assimilação de dados:

```json
{
  "consents": {
    "collect": {
      "val": "y",
    },
    "share": {
      "val": "y",
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "y"
      },
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
      }
    },
    "idSpecific": {
      "email": {
        "jdoe@example.com": {
          "marketing": {
            "email": {
              "val": "n"
            }
          }
        }
      }
    }
  },
  "metadata": {
    "time": "2019-01-01T15:52:25+00:00"
  }
}
```

>[!NOTE]
>
>Para obter mais informações sobre a estrutura e o significado das subpropriedades em `consents`, consulte a visão geral no grupo de campos [[!UICONTROL Detalhes sobre consentimento e preferência]](../../../../xdm/field-groups/profile/consents.md).

## Adicionar grupos de campos obrigatórios ao esquema [!DNL Profile] {#add-field-group}

Para coletar dados de consentimento usando o padrão Adobe, é necessário ter um esquema habilitado para Perfil que contenha os dois grupos de campos a seguir:

* [[!UICONTROL Detalhes sobre consentimento e preferência]](../../../../xdm/field-groups/profile/consents.md)
* [[!UICONTROL IdentityMap]](../../../../xdm/field-groups/profile/identitymap.md) (necessário se estiver usando o Experience Platform Web ou o Mobile SDK para enviar sinais de consentimento)

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Esquemas]** na navegação à esquerda e selecione a guia **[!UICONTROL Procurar]** para exibir uma lista de esquemas existentes. Aqui, selecione o nome do esquema habilitado para [!DNL Profile] ao qual você deseja adicionar campos de consentimento. As capturas de tela nesta seção usam o esquema &quot;Membros de Fidelidade&quot; criado no [tutorial de criação de esquema](../../../../xdm/tutorials/create-schema-ui.md), como exemplo.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-schema.png)

>[!TIP]
>
>Você pode usar os recursos de pesquisa e filtragem do espaço de trabalho para ajudar a encontrar seu esquema com mais facilidade. Consulte o guia em [explorando recursos XDM](../../../../xdm/ui/explore.md) para obter mais informações.

A [!DNL Schema Editor] é exibida, mostrando a estrutura do esquema na tela. No lado esquerdo da tela, selecione **[!UICONTROL Adicionar]** na seção **[!UICONTROL Grupos de campos]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-field-group.png)

A caixa de diálogo **[!UICONTROL Adicionar grupo de campos]** é exibida. Aqui, selecione **[!UICONTROL Detalhes de consentimento e preferência]** na lista. Opcionalmente, é possível usar a barra de pesquisa para restringir os resultados e localizar o grupo de campos com mais facilidade.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-group-dialog.png)

Em seguida, localize o grupo de campos **[!UICONTROL IdentityMap]** na lista e selecione-o também. Depois que ambos os grupos de campos forem listados no painel direito, selecione **[!UICONTROL Adicionar grupos de campos]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/identitymap.png)

A tela será exibida novamente, mostrando que os campos `consents` e `identityMap` foram adicionados à estrutura do esquema. Se você precisar de campos de consentimento e preferência adicionais não capturados pelo grupo de campos padrão, consulte a seção do apêndice sobre [adição de campos de consentimento e preferência personalizados ao esquema](#custom-consent). Caso contrário, selecione **[!UICONTROL Salvar]** para finalizar as alterações no esquema.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/save-schema.png)

>[!IMPORTANT]
>
>Se você estiver criando um novo esquema ou editando um esquema existente que não foi habilitado para o Perfil, deverá [habilitar o esquema para o Perfil](../../../../xdm/ui/resources/schemas.md#profile) antes de salvar.

Se o esquema editado for usado pelo [!UICONTROL Conjunto de dados do perfil] especificado na sequência de dados do Experience Platform Web SDK, esse conjunto de dados incluirá os novos campos de consentimento. Agora você pode retornar ao [guia de processamento de consentimento](./overview.md#merge-policies) para continuar o processo de configuração do Experience Platform para processar dados de consentimento. Se você não tiver criado um conjunto de dados para esse esquema, siga as etapas na próxima seção.

## Criar um conjunto de dados com base no seu esquema de consentimento {#dataset}

Depois de criar um esquema com campos de consentimento, você deve criar um conjunto de dados que assimilará os dados de consentimento dos clientes. Este conjunto de dados deve ser habilitado para [!DNL Real-Time Customer Profile].

Para começar, selecione **[!UICONTROL Conjuntos de dados]** na navegação à esquerda e selecione **[!UICONTROL Criar conjunto de dados]** no canto superior direito.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/create-dataset.png)

Na próxima página, selecione **[!UICONTROL Criar conjunto de dados do esquema]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/from-schema.png)

O fluxo de trabalho **[!UICONTROL Criar conjunto de dados a partir do esquema]** aparece, começando na etapa **[!UICONTROL Selecionar esquema]**. Na lista fornecida, localize um dos esquemas de consentimento criados anteriormente. Opcionalmente, é possível usar a barra de pesquisa para restringir os resultados e localizar seu esquema com mais facilidade. Selecione o botão de opção ao lado do esquema desejado e selecione **[!UICONTROL Avançar]** para continuar.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-dataset-schema.png)

A etapa **[!UICONTROL Configurar conjunto de dados]** é exibida. Forneça um nome e uma descrição exclusivos e de fácil identificação para o conjunto de dados antes de selecionar **[!UICONTROL Concluir]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/dataset-details.png)

A página de detalhes do conjunto de dados recém-criado é exibida. Se o conjunto de dados for baseado no esquema de série temporal, o processo será concluído. Se o conjunto de dados for baseado no esquema do seu registro, a etapa final no processo será habilitar o conjunto de dados para uso no [!DNL Real-Time Customer Profile].

No painel direito, selecione a opção de alternância **[!UICONTROL Perfil]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/profile-toggle.png)

Finalmente, selecione **[!UICONTROL Habilitar]** no popover de confirmação para habilitar o esquema para [!DNL Profile].

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/enable-dataset.png)

O conjunto de dados foi salvo e habilitado para uso em [!DNL Profile]. Se você estiver planejando usar o Experience Platform Web SDK para enviar dados de consentimento para o Perfil, selecione esse conjunto de dados como o [!UICONTROL Conjunto de dados do perfil] ao configurar sua [sequência de dados](../../../../datastreams/overview.md).

## Próximas etapas

Ao seguir este tutorial, você adicionou campos de consentimento a um esquema habilitado para [!DNL Profile], cujo conjunto de dados será usado para assimilar dados de consentimento usando o Experience Platform Web SDK ou assimilação XDM direta.

Agora você pode retornar à [visão geral do processamento de consentimento](./overview.md#merge-policies) para continuar configurando o Experience Platform para processar dados de consentimento.

## Apêndice

A seção a seguir contém informações adicionais sobre a criação de um conjunto de dados para assimilar dados de consentimento e preferência do cliente.

### Adicionar campos personalizados de consentimento e preferência ao esquema {#custom-consent}

Se você precisar capturar sinais de consentimento adicionais além daqueles representados pelo grupo de campos [!UICONTROL Detalhes de consentimento e preferência] padrão, poderá usar componentes XDM personalizados para aprimorar seu esquema de consentimento para atender às suas necessidades comerciais específicas. Esta seção descreve os princípios básicos de como personalizar o esquema de consentimento para assimilar esses sinais no Perfil.

>[!IMPORTANT]
>
>Os SDKs da Web e móvel da Experience Platform não são compatíveis com campos personalizados em seus comandos de alteração de consentimento. Atualmente, a única maneira de assimilar campos de consentimento personalizados no Perfil é por meio de [assimilação em lote](../../../../ingestion/batch-ingestion/overview.md) ou uma [conexão de origem](../../../../sources/home.md).

É altamente recomendável usar o grupo de campos [!UICONTROL Detalhes sobre consentimento e preferência] como uma linha de base para a estrutura dos dados de consentimento e adicionar outros campos conforme necessário, em vez de tentar criar toda a estrutura do zero.

Para adicionar campos personalizados à estrutura de um grupo de campos padrão, primeiro crie um grupo de campos personalizado. Depois de adicionar o grupo de campos [!UICONTROL Detalhes de consentimento e preferência] ao esquema, selecione o ícone **de adição (+)** na seção **[!UICONTROL Grupos de campos]** e selecione **[!UICONTROL Criar novo grupo de campos]**. Forneça um nome e uma descrição opcional para o grupo de campos e selecione **[!UICONTROL Adicionar grupo de campos]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field-group.png)

O [!DNL Schema Editor] reaparece com o novo grupo de campos personalizado selecionado no painel esquerdo. Na tela, são exibidos controles que permitem adicionar campos personalizados à estrutura do esquema. Para adicionar um novo campo de consentimento ou preferência, selecione o ícone **de adição (+)** ao lado do objeto `consents`.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field.png)

Um novo campo aparece dentro do objeto `consents`. Como você está adicionando um campo personalizado a um objeto XDM padrão, o novo campo é criado em um objeto com namespace para sua ID de locatário.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/nested-tenantId.png)

No painel direito, em **[!UICONTROL Propriedades do campo]**, forneça um nome e uma descrição para o campo. Ao selecionar o **[!UICONTROL Tipo]** do campo, você deve usar o tipo de dados padrão apropriado para um consentimento personalizado ou campo de preferência:

* [[!UICONTROL Campo de consentimento genérico]](../../../../xdm/data-types/consent-field.md)
* [[!UICONTROL Campo de preferência de marketing genérico]](../../../../xdm/data-types/marketing-field.md)
* [[!UICONTROL Campo de Preferência de Marketing Genérico com Assinaturas]](../../../../xdm/data-types/marketing-field-subscriptions.md)
* [[!UICONTROL Campo de Preferência de Personalization Genérico]](../../../../xdm/data-types/personalization-field.md)

Quando terminar, selecione **[!UICONTROL Aplicar]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-properties.png)

O campo de consentimento ou preferência é adicionado à estrutura do esquema. Observe que o [!UICONTROL Caminho] exibido no painel direito contém o namespace `_tenantId`. Esse namespace deve ser incluído sempre que você fizer referência ao caminho para esse campo em suas operações de dados.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-added.png)

Siga as etapas acima para continuar adicionando os campos de consentimento e preferência necessários. Quando terminar, selecione **[!UICONTROL Salvar]** para confirmar as alterações.

Se você não criou um conjunto de dados para este esquema, continue para a seção sobre [criação de um conjunto de dados](#dataset).
