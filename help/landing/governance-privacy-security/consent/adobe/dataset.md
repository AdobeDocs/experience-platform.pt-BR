---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Configurar um conjunto de dados para capturar o consentimento e os dados de preferência
topic-legacy: getting started
description: Saiba como configurar um esquema e conjunto de dados do Experience Data Model (XDM) para capturar dados de consentimento e preferência no Adobe Experience Platform.
exl-id: 61ceaa2a-c5ac-43f5-b118-502bdc432234
translation-type: tm+mt
source-git-commit: 30a2ddb875b035b4509b4be3692b95d0d3ef50b3
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 0%

---

# Configurar um conjunto de dados para capturar dados de consentimento e preferência

Para que o Adobe Experience Platform processe seus dados de consentimento/preferência do cliente, esses dados devem ser enviados para um conjunto de dados cujo esquema contenha campos relacionados a consentimentos e outras permissões. Especificamente, esse conjunto de dados deve ser baseado na classe [!DNL XDM Individual Profile] e habilitado para uso em [!DNL Real-time Customer Profile].

Este documento fornece etapas para configurar um conjunto de dados para processar dados de consentimento no Experience Platform. Para obter uma visão geral do fluxo de trabalho completo para processar dados de consentimento/preferência no Platform, consulte a [visão geral do processamento de consentimento](./overview.md).

>[!IMPORTANT]
>
>Os exemplos neste guia usam um conjunto padronizado de campos para representar valores de consentimento do cliente, conforme definido pelo tipo de dados [Consents &amp; Preferences XDM](../../../../xdm/data-types/consents.md). A estrutura desses campos tem como objetivo fornecer um modelo de dados eficiente para abranger muitos casos de uso comuns de coleta de consentimento.
>
>No entanto, também é possível definir seus próprios grupos de campos para representar o consentimento de acordo com seus próprios modelos de dados. Consulte sua equipe jurídica para obter aprovação de um modelo de dados de consentimento que atenda às suas necessidades comerciais, com base nas seguintes opções:
>
>* O grupo de campos de consentimento padronizado
>* Um grupo de campos de consentimento personalizado criado pela organização
>* Uma combinação do grupo de campos de consentimento padronizado e campos adicionais fornecidos por um grupo de campos de consentimento personalizado


## Pré-requisitos

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Modelo de dados de experiência (XDM)](../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os componentes básicos dos esquemas XDM.
* [Perfil](../../../../profile/home.md) do cliente em tempo real: Consolida dados de clientes de fontes diferentes em uma visualização completa e unificada, oferecendo uma conta acionável e com carimbos de data e hora de cada interação com o cliente.

>[!IMPORTANT]
>
>Este tutorial pressupõe que você saiba o schema [!DNL Profile] na Plataforma que deseja usar para capturar informações de atributos do cliente. Independentemente do método usado para coletar dados de consentimento, esse schema deve estar [ativado para o Perfil do cliente em tempo real](../../../../xdm/ui/resources/schemas.md#profile). Além disso, a identidade primária do esquema não pode ser um campo diretamente identificável que é proibido de usar em publicidade com base em interesses, como um endereço de email. Consulte seu consultor jurídico se não tiver certeza de quais campos são restritos.

## Estrutura do grupo de campos Consentimentos e Preferências {#structure}

O grupo de campos [!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)] (a seguir denominado &quot;grupo de campos Consentes e Preferências&quot;) fornece campos de consentimento padronizados para um esquema. No momento, esse grupo de campos é compatível apenas com schemas com base na classe [!DNL XDM Individual Profile].

O grupo de campos fornece um único campo do tipo de objeto, `consents`, cujas subpropriedades capturam um conjunto de campos de consentimento padronizados. O JSON a seguir é um exemplo do tipo de dados que `consents` espera ao assimilar dados:

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
>Para obter mais informações sobre a estrutura e o significado das sub-propriedades em `consents`, consulte a visão geral no [Tipo de dados de Consentimentos e Preferências](../../../../xdm/data-types/consents.md).

## Adicione o grupo de campos Consents &amp; Preferências ao esquema [!DNL Profile] {#add-field-group}

Na interface do usuário da plataforma, selecione **[!UICONTROL Schemas]** na navegação à esquerda e selecione a guia **[!UICONTROL Browse]** para exibir uma lista de esquemas existentes. Aqui, selecione o nome do schema habilitado para [!DNL Profile] ao qual deseja adicionar campos de consentimento. As capturas de tela nesta seção usam o schema &quot;Membros de fidelidade&quot; criado no [tutorial de criação de schema](../../../../xdm/tutorials/create-schema-ui.md) como exemplo.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-schema.png)

>[!TIP]
>
>Você pode usar os recursos de pesquisa e filtragem do espaço de trabalho para ajudar a encontrar o esquema mais fácil. Consulte o guia sobre [exploração de recursos XDM](../../../../xdm/ui/explore.md) para obter mais informações.

O [!DNL Schema Editor] é exibido, mostrando a estrutura do schema na tela. No lado esquerdo da tela, selecione **[!UICONTROL Add]** na seção **[!UICONTROL Field groups]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-field-group.png)

A caixa de diálogo **[!UICONTROL Add field group]** é exibida. Aqui, selecione **[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)]** na lista. Como opção, você pode usar a barra de pesquisa para restringir os resultados para localizar o grupo de campos mais facilmente. Depois que o grupo de campos for selecionado, selecione **[!UICONTROL Add field group]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-group-dialog.png)

A tela é exibida novamente, mostrando que o objeto `consents` foi adicionado à estrutura do schema. Se você precisar de mais campos de consentimento e preferência não capturados pelo grupo de campos padrão, consulte a seção de apêndice em [adicionar campos de consentimento e preferência personalizados ao schema](#custom-consent). Caso contrário, selecione **[!UICONTROL Save]** para finalizar as alterações no schema.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/save-schema.png)

Se o esquema editado for usado pelo [!UICONTROL Profile Dataset] especificado na configuração de borda do SDK da Web da plataforma, esse conjunto de dados agora incluirá os novos campos de consentimento. Agora você pode retornar ao [guia de processamento de consentimento](./overview.md#merge-policies) para continuar o processo de configuração do Experience Platform para processar dados de consentimento.

Se não tiver criado um conjunto de dados para esse esquema, siga as etapas na próxima seção.

## Crie um conjunto de dados com base no seu esquema de consentimento {#dataset}

Depois de criar um schema com campos de consentimento, você deve criar um conjunto de dados que, em última análise, assimilará os dados de consentimento dos clientes. Este conjunto de dados deve ser ativado para [!DNL Real-time Customer Profile].

Para começar, selecione **[!UICONTROL Datasets]** na navegação à esquerda e selecione **[!UICONTROL Create dataset]** no canto superior direito.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/create-dataset.png)

Na próxima página, selecione **[!UICONTROL Create dataset from schema]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/from-schema.png)

O workflow **[!UICONTROL Create dataset from schema]** é exibido, começando na etapa **[!UICONTROL Select schema]**. Na lista fornecida, localize um dos esquemas de consentimento criados anteriormente. Como opção, você pode usar a barra de pesquisa para restringir os resultados e localizar o esquema mais fácil. Selecione o botão de opção ao lado do schema desejado e selecione **[!UICONTROL Next]** para continuar.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-dataset-schema.png)

A etapa **[!UICONTROL Configure dataset]** é exibida. Forneça um nome e uma descrição exclusivos e facilmente identificáveis para o conjunto de dados antes de selecionar **[!UICONTROL Finish]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/dataset-details.png)

A página de detalhes do conjunto de dados recém-criado é exibida. Se o conjunto de dados se basear no esquema da série de tempo, o processo será concluído. Se o conjunto de dados se baseia no esquema de registro, a etapa final no processo é habilitar o conjunto de dados para uso em [!DNL Real-time Customer Profile].

No painel direito, selecione a opção **[!UICONTROL Profile]** .

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/profile-toggle.png)

Finalmente, selecione **[!UICONTROL Enable]** no provedor de confirmação para habilitar o schema para [!DNL Profile].

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/enable-dataset.png)

O conjunto de dados agora é salvo e ativado para uso em [!DNL Profile]. Se você estiver planejando usar o SDK da Web da plataforma para enviar dados de consentimento ao Perfil, deverá selecionar esse conjunto de dados como o [!UICONTROL Profile Dataset] ao configurar sua [configuração de borda](../../../../edge/fundamentals/edge-configuration.md).

## Próximas etapas

Ao seguir este tutorial, você adicionou campos de consentimento a um esquema habilitado para [!DNL Profile], cujo conjunto de dados será usado para assimilar dados de consentimento usando o SDK da Web da plataforma ou a assimilação direta do XDM.

Agora você pode retornar para a [visão geral do processamento de consentimento](./overview.md#merge-policies) para continuar configurando o Experience Platform para processar dados de consentimento.

## Apêndice

A seção a seguir contém informações adicionais sobre como criar um conjunto de dados para assimilar dados de consentimento e preferência do cliente.

### Adicionar consentimento personalizado e campos de preferência ao esquema {#custom-consent}

Se você precisar capturar sinais de consentimento adicionais fora daqueles representados pelo grupo de campos padrão [!DNL Consents & Preferences] , poderá usar componentes XDM personalizados para aprimorar seu esquema de consentimento para atender às necessidades específicas dos negócios. Esta seção descreve os princípios básicos de como personalizar o esquema de consentimento de uma maneira compatível com os comandos de alteração de consentimento feitos pelos SDKs do Adobe Experience Platform Mobile e da Web.

>[!IMPORTANT]
>
>Você deve usar o grupo de campos [!DNL Consents & Preferences] como uma linha de base para a estrutura dos dados de consentimento e adicionar campos adicionais, conforme necessário, em vez de tentar criar toda a estrutura do zero.

Para adicionar campos personalizados à estrutura de um grupo de campos padrão, primeiro crie um grupo de campos personalizado. Depois de adicionar o grupo de campos [!DNL Consents & Preferences] ao schema, selecione o ícone de **mais (+)** na seção **[!UICONTROL Field groups]** e selecione **[!UICONTROL Create new field group]**. Forneça um nome e uma descrição opcional para o grupo de campos e selecione **[!UICONTROL Add field group]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field-group.png)

O [!DNL Schema Editor] é exibido novamente com o novo grupo de campos personalizados selecionado no painel à esquerda. Na tela, são exibidos controles que permitem adicionar campos personalizados à estrutura do esquema. Para adicionar um novo consentimento ou campo de preferência, selecione o ícone de adição (+)**ao lado do objeto `consents`.**

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field.png)

Um novo campo é exibido dentro do objeto `consents`. Como você está adicionando um campo personalizado a um objeto XDM padrão, o novo campo é criado em um objeto com namespaco para a ID do locatário.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/nested-tenantId.png)

No painel direito em **[!UICONTROL Field properties]**, forneça um nome e uma descrição para o campo. Ao selecionar o **[!UICONTROL Type]** do campo, você deve usar o tipo de dados padrão apropriado para um consentimento ou campo de preferência personalizado:

* [[!UICONTROL Generic Consent Field]](../../../../xdm/data-types/consent-field.md)
* [[!UICONTROL Generic Marketing Preference Field]](../../../../xdm/data-types/marketing-field.md)
* [[!UICONTROL Generic Marketing Preference Field with Subscriptions]](../../../../xdm/data-types/marketing-field-subscriptions.md)
* [[!UICONTROL Generic Personalization Preference Field]](../../../../xdm/data-types/personalization-field.md)

Quando terminar, selecione **[!UICONTROL Apply]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-properties.png)

O campo de consentimento ou preferência é adicionado à estrutura do schema. Observe que [!UICONTROL Path] exibido no painel direito contém o namespace `_tenantId`. Esse namespace deve ser incluído sempre que você fizer referência ao caminho para esse campo em suas operações de dados.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-added.png)

Siga as etapas acima para continuar adicionando os campos de consentimento e preferência necessários. Quando terminar, selecione **[!UICONTROL Save]** para confirmar as alterações.

Se o esquema editado for usado pelo [!UICONTROL Profile Dataset] especificado na configuração de borda do SDK da Web da plataforma, esse conjunto de dados agora incluirá os novos campos de consentimento. Agora você pode retornar ao [guia de processamento de consentimento](./overview.md#merge-policies) para continuar o processo de configuração do Experience Platform para processar dados de consentimento.

Se você não tiver criado um conjunto de dados para esse esquema, continue para a seção em [criar um conjunto de dados](#dataset).
