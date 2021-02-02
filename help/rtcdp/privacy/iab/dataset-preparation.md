---
keywords: Experience Platform;home;IAB;IAB 2.0;consentimento;Consentimento
solution: Experience Platform
title: Criar conjuntos de dados para capturar dados de consentimento do IAB TCF 2.0
topic: privacy events
description: Este documento fornece etapas para configurar os dois conjuntos de dados necessários para coletar dados de consentimento do IAB TCF 2.0.
translation-type: tm+mt
source-git-commit: 0fea6c4d215e16941010e59817a2a099d775d2cd
workflow-type: tm+mt
source-wordcount: '1653'
ht-degree: 0%

---


# Criar conjuntos de dados para capturar dados de consentimento do IAB TCF 2.0

Para que [!DNL Real-time Customer Data Platform] processe os dados de consentimento do cliente em conformidade com o IAB [!DNL Transparency & Consent Framework] (TCF) 2.0, esses dados devem ser enviados para conjuntos de dados cujos schemas contêm campos de consentimento TCF 2.0.

Especificamente, dois conjuntos de dados são necessários para capturar dados de consentimento do TCF 2.0:

* Um conjunto de dados baseado na classe [!DNL XDM Individual Profile], habilitado para uso em [!DNL Real-time Customer Profile].
* Um conjunto de dados baseado na classe [!DNL XDM ExperienceEvent].

Este documento fornece etapas para configurar esses dois conjuntos de dados para coletar dados de consentimento do IAB TCF 2.0. Para obter uma visão geral do fluxo de trabalho completo para configurar [!DNL Real-time CDP] para TCF 2.0, consulte a [visão geral de conformidade do IAB TCF 2.0](./overview.md).

## Pré-requisitos

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Modelo de dados de experiência (XDM)](../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos schemas XDM.
   * [Crie um schema na interface do usuário](../../../xdm/tutorials/create-schema-ui.md): Um tutorial que aborda as noções básicas de como trabalhar com o Editor de Schemas.
* [Serviço](../../../identity-service/home.md) de identidade Adobe Experience Platform: Permite que você conecte identidades de clientes de suas diferentes fontes de dados entre dispositivos e sistemas.
   * [Namespaces](../../../identity-service/namespaces.md) de identidade: Os dados de identidade do cliente devem ser fornecidos sob uma namespace de identidade específica reconhecida pelo Serviço de identidade.
* [Perfil](../../../profile/home.md) do cliente em tempo real: Aproveita  [!DNL Identity Service] para permitir que você crie perfis detalhados do cliente a partir de seus conjuntos de dados em tempo real. [!DNL Real-time Customer Profile] extrai dados do Data Lake e persiste em perfis do cliente em seu próprio armazenamento de dados separado.

## [!UICONTROL Estrutura ] Detalhada da Privacidade  {#structure}

A combinação [!UICONTROL Detalhes de privacidade] fornece campos de consentimento do cliente necessários para o suporte ao TCF 2.0. Há duas versões desta combinação: um compatível com a classe [!DNL XDM Individual Profile] e o outro com a classe [!DNL XDM ExperienceEvent].

As seções seguintes explicam a estrutura de cada uma destas misturas, incluindo os dados que esperam durante a ingestão.

### Mistura de perfis {#profile-mixin}

Para schemas baseados em [!DNL XDM Individual Profile], a combinação [!UICONTROL Detalhes de Privacidade] fornece um único campo tipo mapa, `xdm:identityPrivacyInfo`, que mapeia as identidades do cliente para suas preferências de consentimento IAB. O JSON a seguir é um exemplo do tipo de dados `xdm:identityPrivacyInfo` esperados após a ingestão dos dados:

```json
{
  "xdm:identityPrivacyInfo": {
      "ECID": {
        "13782522493631189": {
          "xdm:identityIABConsent": {
            "xdm:consentTimestamp": "2020-04-11T05:05:05Z",
            "xdm:consentString": {
              "xdm:consentStandard": "IAB TCF",
              "xdm:consentStandardVersion": "2.0",
              "xdm:consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
              "xdm:gdprApplies": true,
              "xdm:containsPersonalData": false
            }
          }
        }
      }
    }
}
```

Como mostra o exemplo, cada chave de nível raiz de `xdm:identityPrivacyInfo` corresponde a uma namespace de identidade reconhecida pelo Serviço de identidade. Por sua vez, cada propriedade de namespace deve ter pelo menos uma subpropriedade cuja chave corresponde ao valor de identidade correspondente do cliente para essa namespace. Neste exemplo, o cliente é identificado com um valor de ID de Experience Cloud (`ECID`) de `13782522493631189`.

>[!NOTE]
>
>Embora o exemplo acima use um único par de namespace/valor para representar a identidade do cliente, você pode adicionar chaves adicionais para outras namespaces, e cada namespace pode ter vários valores de identidade, cada um com seu próprio conjunto de preferências de consentimento IAB.

No objeto de valor de identidade há um único campo, `xdm:identityIABConsent`. Esse objeto captura os valores de consentimento IAB do cliente para a namespace de identidade e o valor especificados. As subpropriedades contidas neste campo estão listadas abaixo:

| Propriedade | Descrição |
| --- | --- |
| `xdm:consentTimestamp` | Um carimbo de data e hora [ISO 8601](https://www.ietf.org/rfc/rfc3339.txt) de quando os valores de consentimento IAB foram alterados. |
| `xdm:consentString` | Um objeto que contém os dados de consentimento atualizados do cliente e outras informações contextuais. Consulte a seção sobre [propriedades da cadeia de caracteres de consentimento](#consent-string) para saber mais sobre as subpropriedades necessárias deste objeto. |

### Mistura de eventos {#event-mixin}

Para schemas baseados em [!DNL XDM ExperienceEvent], a combinação [!UICONTROL Detalhes de privacidade] fornece um único campo do tipo array: `xdm:consentStrings`. Cada item nesta matriz deve ser um objeto que contenha as propriedades necessárias para uma sequência de caracteres de consentimento IAB, semelhantes ao campo `xdm:consentString` na combinação de perfis. Para obter mais informações sobre essas subpropriedades, consulte a [próxima seção](#consent-string).

```json
{
  "xdm:consentStrings": [
    {
      "xdm:consentStandard": "IAB TCF",
      "xdm:consentStandardVersion": "2.0",
      "xdm:consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
      "xdm:gdprApplies": true,
      "xdm:containsPersonalData": false
    }
  ]
}
```

### Propriedades da string de consentimento {#consent-string}

Ambas as versões da combinação [!UICONTROL Detalhes de privacidade] exigem pelo menos um objeto que capture os campos necessários que descrevem a sequência de caracteres de consentimento IAB para o cliente. Essas propriedades são explicadas abaixo:

| Propriedade | Descrição |
| --- | --- |
| `xdm:consentStandard` | A estrutura de consentimento à qual os dados se aplicam. Para conformidade com TCF, o valor deve ser `IAB TCF`. |
| `xdm:consentStandardVersion` | O número da versão da estrutura de consentimento indicado por `xdm:consentStandard`. Para conformidade com TCF 2.0, o valor deve ser `2.0`. |
| `xdm:consentStringValue` | A cadeia de caracteres de consentimento que foi gerada pela plataforma de gerenciamento de consentimento (CMP) com base nas configurações selecionadas do cliente. |
| `xdm:gdprApplies` | Um valor booliano que indica se o RGPD se aplica ou não a este cliente. O valor deve ser definido como `true` para que a aplicação do TCF 2.0 ocorra. O padrão é `false` se não estiver incluído. |
| `xdm:containsPersonalData` | Um valor booliano que indica se a atualização de consentimento contém ou não dados pessoais. O padrão é `false` se não estiver incluído. |

## Criar schemas de consentimento do cliente {#create-schemas}

Para criar conjuntos de dados que capturam dados de consentimento, é necessário primeiro criar schemas XDM para basear esses conjuntos de dados.

Na interface do usuário da plataforma, selecione **[!UICONTROL Schemas]** no painel de navegação esquerdo para abrir o espaço de trabalho [!UICONTROL Schemas]. Aqui, siga as etapas nas seções abaixo para criar cada schema necessário.

>[!NOTE]
>
>Se você tiver schemas XDM existentes que deseja usar para capturar dados de consentimento, edite esses schemas em vez de criar novos. No entanto, se um schema existente tiver sido habilitado para uso no Perfil do cliente em tempo real, sua identidade primária não poderá ser um campo diretamente identificável que esteja proibido de usar em publicidade com base em interesses, como um endereço de email. Consulte seu consultor jurídico se não tiver certeza sobre quais campos estão restritos.
>
>Além disso, ao editar schemas existentes, somente alterações aditivas (não quebráveis) podem ser feitas. Consulte a seção sobre os princípios [da evolução do schema](../../../xdm/schema/composition.md#evolution) para obter mais informações.

### Criar um schema de consentimento baseado em registros {#profile-schema}

Na área de trabalho **[!UICONTROL Schemas]**, selecione **[!UICONTROL Criar schema]** e escolha **[!UICONTROL Perfil Individual XDM]** na lista suspensa.

![](../assets/iab/create-schema-profile.png)

O [!DNL Schema Editor] é exibido, mostrando a estrutura do schema na tela. Use o painel direito para fornecer um nome e uma descrição para o schema, em seguida, selecione **[!UICONTROL Adicionar]** na seção **[!UICONTROL Mixins]** no lado esquerdo da tela.

![](../assets/iab/add-mixin-profile.png)

A caixa de diálogo **[!UICONTROL Adicionar mixin]** é exibida. Aqui, selecione **[!UICONTROL Detalhes de privacidade]** na lista. Como opção, você pode usar a barra de pesquisa para restringir os resultados para localizar a mistura mais fácil. Depois que a mistura for selecionada, selecione **[!UICONTROL Adicionar mistura]**.

![](../assets/iab/add-profile-privacy.png)

A tela de desenho é exibida novamente, mostrando que o campo `identityPrivacyInfo` foi adicionado à estrutura do schema.

![](../assets/iab/profile-privacy-structure.png)

Daqui, repita as etapas acima para adicionar as seguintes combinações adicionais ao schema:

* [!UICONTROL IdentityMap]
* [!UICONTROL Região de captura de dados para o Perfil]
* [!UICONTROL Detalhes demográficos]
* [!UICONTROL Detalhes do contato pessoal]

![](../assets/iab/profile-all-mixins.png)

Se você estiver editando um schema existente que já foi habilitado para uso em [!DNL Real-time Customer Profile], selecione **[!UICONTROL Salvar]** para confirmar suas alterações antes de pular para a seção em [criar um conjunto de dados com base no seu schema de consentimento](#dataset). Se você estiver criando um novo schema, continue seguindo as etapas descritas na subseção abaixo.

#### Ative o schema para uso em [!DNL Real-time Customer Profile]

Para que [!DNL Real-time CDP] associe os dados de consentimento que recebe a perfis de clientes específicos, o schema de consentimento deve ser habilitado para uso em [!DNL Real-time Customer Profile].

>[!NOTE]
>
>O schema de exemplo mostrado nesta seção usa seu campo `identityMap` como sua identidade primária. Se desejar definir outro campo como uma identidade primária, certifique-se de que está usando um identificador indireto, como uma ID de cookie, e não um campo diretamente identificável que está proibido de usar em publicidade com base em interesses, como um endereço de email. Consulte seu consultor jurídico se não tiver certeza sobre quais campos estão restritos.
>
>As etapas sobre como definir um campo de identidade principal para um schema podem ser encontradas no [tutorial de criação do schema](../../../xdm/tutorials/create-schema-ui.md#identity-field).

Para ativar o schema para [!DNL Profile], selecione o nome do schema no painel esquerdo para abrir a caixa de diálogo **[!UICONTROL propriedades do Schema]** no painel direito. Aqui, selecione o botão de alternância **[!UICONTROL Perfil]**.

![](../assets/iab/profile-enable-profile.png)

Um provedor é exibido, indicando uma identidade primária ausente. Marque a caixa de seleção para usar uma identidade primária alternativa, já que a identidade primária estará contida no campo `identityMap`.

![](../assets/iab/missing-primary-identity.png)

Finalmente, selecione **[!UICONTROL Salvar]** para confirmar suas alterações.

![](../assets/iab/profile-save.png)

### Criar um schema de consentimento baseado em séries de tempo {#event-schema}

Na área de trabalho **[!UICONTROL Schemas]**, selecione **[!UICONTROL Criar schema]** e escolha **[!UICONTROL XDM ExperienceEvent]** na lista suspensa.

![](../assets/iab/create-schema-event.png)

O [!DNL Schema Editor] é exibido, mostrando a estrutura do schema na tela. Use o painel direito para fornecer um nome e uma descrição para o schema, em seguida, selecione **[!UICONTROL Adicionar]** na seção **[!UICONTROL Mixins]** no lado esquerdo da tela.

![](../assets/iab/add-mixin-event.png)

A caixa de diálogo **[!UICONTROL Adicionar mixin]** é exibida. Aqui, selecione **[!UICONTROL Detalhes de privacidade]** na lista. Como opção, você pode usar a barra de pesquisa para restringir os resultados para localizar a mistura mais fácil. Depois de escolher uma mistura, selecione **[!UICONTROL Adicionar mistura]**.

![](../assets/iab/add-event-privacy.png)

A tela de desenho é exibida novamente, mostrando que a matriz `consentStrings` foi adicionada à estrutura do schema.

![](../assets/iab/event-privacy-structure.png)

Daqui, repita as etapas acima para adicionar as seguintes combinações adicionais ao schema:

* [!UICONTROL IdentityMap]
* [!UICONTROL Detalhes do ambiente]
* [!UICONTROL Detalhes da Web]
* [!UICONTROL Detalhes da implementação]

Depois que as misturas forem adicionadas, conclua selecionando **[!UICONTROL Salvar]**.

![](../assets/iab/event-all-mixins.png)

## Crie conjuntos de dados com base em seus schemas de consentimento {#datasets}

Para cada um dos schemas obrigatórios descritos acima, você deve criar um conjunto de dados que acabará assimilando os dados de consentimento dos clientes. O conjunto de dados com base no schema de registro deve ser ativado para [!DNL Real-time Customer Profile], enquanto o conjunto de dados com base no schema de séries de tempo **não deve** estar [!DNL Profile] habilitado.

Para começar, selecione **[!UICONTROL Conjuntos de dados]** no painel de navegação esquerdo, em seguida, selecione **[!UICONTROL Criar conjunto de dados]** no canto superior direito.

![](../assets/iab/dataset-create.png)

Na próxima página, selecione **[!UICONTROL Criar conjunto de dados a partir do schema]**.

![](../assets/iab/dataset-create-from-schema.png)

O fluxo de trabalho **[!UICONTROL Criar conjunto de dados a partir do schema]** é exibido, começando na etapa **[!UICONTROL Selecionar schema]**. Na lista fornecida, localize um dos schemas de consentimento criados anteriormente. Como opção, você pode usar a barra de pesquisa para restringir os resultados e localizar seu schema mais facilmente. Selecione o botão de opção ao lado do schema desejado e selecione **[!UICONTROL Próximo]** para continuar.

![](../assets/iab/dataset-select-schema.png)

A etapa **[!UICONTROL Configurar conjunto de dados]** é exibida. Forneça um nome e uma descrição exclusivos e facilmente identificáveis para o conjunto de dados antes de selecionar **[!UICONTROL Concluir]**.

![](../assets/iab/dataset-configure.png)

A página de detalhes do conjunto de dados recém-criado é exibida. Se o conjunto de dados for baseado no schema da série de tempo, o processo será concluído. Se o conjunto de dados for baseado no schema de registro, a etapa final do processo é habilitar o conjunto de dados para uso em [!DNL Real-time Customer Profile].

No painel direito, selecione a alternância **[!UICONTROL Perfil]** e, em seguida, selecione **[!UICONTROL Ativar]** no módulo de confirmação para ativar o schema para [!DNL Profile].

![](../assets/iab/dataset-enable-profile.png)

Siga as etapas acima novamente para criar o outro conjunto de dados necessário para conformidade com o TCF 2.0.

## Próximas etapas

Seguindo este tutorial, você criou dois conjuntos de dados que agora podem ser usados para coletar dados de consentimento do cliente:

* Um conjunto de dados baseado em registros habilitado para uso no Perfil do cliente em tempo real.
* Um conjunto de dados baseado em séries de tempo que não está habilitado para [!DNL Profile].

Agora você pode retornar à [visão geral do IAB TCF 2.0](./overview.md#merge-policies) para continuar o processo de configuração [!DNL Real-time CDP] para conformidade com o TCF 2.0.