---
keywords: Experience Platform;página inicial;IAB;IAB 2.0;consentimento;Consentimento
solution: Experience Platform
title: Suporte IAB TCF 2.0 no Experience Platform
description: Saiba como configurar suas operações de dados e esquemas para transmitir as opções de consentimento do cliente ao ativar segmentos para destinos no Adobe Experience Platform.
role: Developer
feature: Consent
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '2509'
ht-degree: 0%

---

# Suporte IAB TCF 2.0 no Experience Platform

O [!DNL Transparency & Consent Framework] (TCF), conforme descrito pelo [!DNL Interactive Advertising Bureau] (IAB) é uma estrutura técnica de padrão aberto destinada a permitir que as organizações obtenham, registrem e atualizem o consentimento do consumidor para o processamento de seus dados pessoais, em conformidade com o [!DNL General Data Protection Regulation] (GDPR) da União Europeia. A segunda iteração da estrutura, TCF 2.0, concede mais flexibilidade para a forma como os consumidores podem fornecer ou não o consentimento, incluindo se e como os fornecedores podem usar determinadas características do processamento de dados, como a geolocalização precisa.

>[!NOTE]
>
>Mais informações sobre o TCF 2.0 podem ser encontradas no [site do IAB Europa](https://iabeurope.eu/), incluindo material de suporte e especificações técnicas.

O Adobe Experience Platform faz parte da [lista de fornecedores IAB TCF 2.0](https://iabeurope.eu/vendor-list-tcf/) registrada, com a ID **565**. Em conformidade com os requisitos do TCF 2.0, o Experience Platform permite coletar dados de consentimento do cliente e integrá-los aos perfis de clientes armazenados. Esses dados de consentimento podem ser fatorados se os perfis são incluídos em segmentos de público exportados, dependendo do caso de uso.

>[!IMPORTANT]
>
>O Experience Platform só pode estar em conformidade com a versão 2.0 do TCF (ou posterior). Não há suporte para versões anteriores do TCF.

Este documento fornece uma visão geral de como configurar suas operações de dados e esquemas de perfil para aceitar dados de consentimento do cliente gerados pela sua Plataforma de gerenciamento de consentimento (CMP). Também aborda como o Experience Platform transmite opções de consentimento do usuário ao exportar segmentos.

## Pré-requisitos

Para seguir este guia, você deve usar uma CMP, comercial ou própria, integrada e compatível com a TCF do IAB. Consulte a [lista de CMPs compatíveis](https://iabeurope.eu/cmp-list/) para obter mais informações.

>[!IMPORTANT]
>
>Se a ID da CMP for inválida, a Experience Platform continuará processando seus dados como estão. Para aplicar o TCF 2.0, você deve confirmar se o CMP tem uma ID válida que foi registrada com o TCF 2.0 do IAB antes de enviar dados para o Experience Platform.

Este guia também requer uma compreensão funcional dos seguintes serviços da Experience Platform:

* [Experience Data Model (XDM)](/help/xdm/home.md): a estrutura padronizada pela qual a Experience Platform organiza os dados de experiência do cliente.
* [Adobe Experience Platform Identity Service](/help/identity-service/home.md): resolve o desafio fundamental colocado pela fragmentação dos dados de experiência do cliente ao unir as identidades de vários dispositivos e sistemas.
* [Perfil de cliente em tempo real](/help/profile/home.md): usa o [!DNL Identity Service] para criar perfis de cliente detalhados a partir dos seus conjuntos de dados em tempo real. [!DNL Real-Time Customer Profile] extrai dados do Data Lake e mantém perfis de clientes em seu próprio armazenamento de dados separado.
* [Adobe Experience Platform Web SDK](/help/collection/js/js-overview.md): uma biblioteca JavaScript do lado do cliente que permite integrar vários serviços Experience Platform ao seu site voltado para o cliente.
   * [Comandos de consentimento do SDK](/help/collection/js/commands/setconsent.md): uma visão geral dos casos de uso dos comandos do SDK relacionados ao consentimento mostrados neste guia.
* [Serviço de Segmentação do Adobe Experience Platform](/help/segmentation/home.md): permite dividir os dados do [!DNL Real-Time Customer Profile] em grupos de indivíduos que compartilham características semelhantes e respondem de forma semelhante às estratégias de marketing.

Além dos serviços Experience Platform listados acima, você também deve se familiarizar com os [destinos](/help/data-governance/home.md) e sua função no ecossistema do Experience Platform.

## Resumo do fluxo de consentimento do cliente {#summary}

As seções a seguir descrevem como os dados de consentimento são coletados e aplicados após o sistema ser configurado corretamente.

### Coleta de dados de consentimento

O Experience Platform permite coletar dados de consentimento do cliente por meio do seguinte processo:

1. Um cliente fornece suas preferências de consentimento para a coleta de dados por meio de uma caixa de diálogo no site.
1. Seu CMP detecta a alteração de preferência de consentimento e gera os dados de consentimento TCF de acordo.
1. Usando a Experience Platform Web SDK, os dados de consentimento gerados (retornados pela CMP) são enviados para a Adobe Experience Platform.
1. Os dados de consentimento coletados são assimilados em um conjunto de dados habilitado para [!DNL Profile] cujo esquema contém campos de consentimento TCF.

Além dos comandos do SDK acionados pelos ganchos de alteração de consentimento do CMP, os dados de consentimento também podem fluir para o Experience Platform por meio de quaisquer dados XDM gerados pelo cliente que são carregados diretamente para um conjunto de dados habilitado para [!DNL Profile].

Qualquer segmento compartilhado com o Experience Platform pela Adobe Audience Manager (por meio do conector de origem [!DNL Audience Manager] ou de outra forma) também poderá conter dados de consentimento se os campos apropriados tiverem sido aplicados a esses segmentos por meio de [!DNL Experience Cloud Identity Service]. Para obter mais informações sobre como coletar dados de consentimento em [!DNL Audience Manager], consulte o documento no [plug-in do Adobe Audience Manager para TCF do IAB](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=pt-BR).

### Imposição de consentimento downstream

Depois que os dados de consentimento da TCF forem assimilados com êxito, os seguintes processos ocorrerão nos serviços downstream da Experience Platform:

1. [!DNL Real-Time Customer Profile] atualiza os dados de consentimento armazenados para o perfil desse cliente.
1. A Experience Platform processará as IDs do cliente somente se a permissão do fornecedor para o Experience Platform (565) for fornecida para cada ID em um cluster.
1. Ao exportar segmentos para destinos pertencentes a membros da lista de fornecedores do TCF 2.0, o Experience Platform só incluirá perfis se as permissões de fornecedor do Experience Platform (565) *e* fornecerem o destino individual para cada ID em um cluster.

O restante das seções neste documento fornece orientação sobre como configurar o Experience Platform e suas operações de dados para atender aos requisitos de coleta e imposição descritos acima.

## Determine como gerar dados de consentimento do cliente na CMP {#consent-data}

Como cada sistema CMP é exclusivo, você deve determinar a melhor maneira de permitir que seus clientes forneçam consentimento enquanto interagem com seu serviço. Uma caixa de diálogo de consentimento de cookie é uma maneira comum de obter o consentimento do cliente. Um exemplo de caixa de diálogo CMP é visto abaixo.

![Um exemplo de caixa de diálogo da Plataforma de Gerenciamento de Consentimento.](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

Essa caixa de diálogo deve permitir que o cliente aceite ou não as seguintes opções:

| Opção de consentimento | Descrição |
| --- | --- |
| **Finalidades** | Finalidades definem para quais fins de publicidade uma marca pode usar os dados de um cliente. A seguinte finalidade deve ser escolhida para que o Experience Platform processe IDs do cliente: <ul><li>**Finalidade 1**: armazenar e/ou acessar informações em um dispositivo</li><li>**Propósito 10**: desenvolver e melhorar produtos</li></ul> |
| **Permissões de fornecedor** | Além dos objetivos tecnológicos do anúncio, o diálogo também deve permitir que o cliente opte por aceitar ou não ter seus dados usados por fornecedores específicos, incluindo o Adobe Experience Platform (565). |

### Strings de consentimento {#consent-strings}

Independentemente do método usado para coletar os dados, o objetivo é gerar um valor de sequência de caracteres com base nas opções de consentimento escolhidas pelo cliente, chamado de sequência de consentimento.

Na especificação do TCF, as cadeias de consentimento são usadas para codificar detalhes relevantes sobre as configurações de consentimento de um cliente, em termos de finalidades de marketing específicas, conforme definido por políticas e fornecedores. O Experience Platform usa essas cadeias de caracteres para armazenar as configurações de consentimento de cada cliente e, portanto, uma nova cadeia de caracteres de consentimento deve ser gerada sempre que essas configurações forem alteradas.

As sequências de consentimento só podem ser criadas por um CMP registrado com a TCF do IAB. Para obter mais informações sobre como gerar cadeias de consentimento usando seu CMP específico, consulte o [guia de formatação da cadeia de consentimento](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) no repositório GitHub da TCF do IAB.

## Criar conjuntos de dados com campos de consentimento TCF {#datasets}

Os dados de consentimento do cliente devem ser enviados para conjuntos de dados cujos esquemas contêm campos de consentimento TCF. Consulte o tutorial sobre [criação de conjuntos de dados para capturar o consentimento do TCF 2.0](./dataset.md) para saber como criar o conjunto de dados de perfil necessário (e um conjunto de dados opcional de Evento de Experiência) antes de continuar com este guia.

## Atualizar as políticas de mesclagem [!DNL Profile] para incluir dados de consentimento {#merge-policies}

Depois de criar um conjunto de dados habilitado para [!DNL Profile] para coletar dados de consentimento, você deve garantir que suas políticas de mesclagem tenham sido configuradas para sempre incluir campos de consentimento TCF em seus perfis de cliente. Isso envolve definir a precedência do conjunto de dados para que ele seja priorizado em relação a outros conjuntos de dados potencialmente conflitantes.

Para obter mais informações sobre como trabalhar com políticas de mesclagem, consulte a [visão geral das políticas de mesclagem](/help/profile/merge-policies/overview.md). Ao configurar suas políticas de mesclagem, você deve garantir que seus segmentos incluam todos os atributos de consentimento necessários fornecidos pelo [grupo de campos de esquema de privacidade XDM](./dataset.md#privacy-field-group), conforme descrito no guia sobre preparação de conjuntos de dados.

## Integrar o Experience Platform Web SDK para coletar dados de consentimento do cliente {#sdk}

>[!NOTE]
>
>O uso do Experience Platform Web SDK é necessário para processar dados de consentimento diretamente no Adobe Experience Platform. Não há suporte para [!DNL Experience Cloud Identity Service].
>
>No entanto, [!DNL Experience Cloud Identity Service] ainda é compatível com o processamento de consentimento no Adobe Audience Manager, e a conformidade com TCF 2.0 requer apenas que a biblioteca seja atualizada para [versão 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Depois de configurar o CMP para gerar cadeias de consentimento, é necessário integrar o Experience Platform Web SDK para coletar essas cadeias de caracteres e enviá-las para o Experience Platform. O Experience Platform SDK fornece dois comandos que podem ser usados para enviar dados de consentimento de TCF para o Experience Platform (explicados nas subseções abaixo). Esses comandos devem ser usados quando um cliente fornecer informações de consentimento pela primeira vez e sempre que o consentimento for alterado posteriormente.

**A SDK não faz interface com nenhum CMP pronto para uso**. Cabe a você determinar como integrar o SDK ao seu site, acompanhar as alterações de consentimento no CMP e chamar o comando apropriado.

### Criar um fluxo de dados

Para que o SDK envie dados para o Experience Platform, primeiro você deve criar um fluxo de dados para o Experience Platform. Etapas específicas sobre como criar uma sequência de dados são fornecidas na [documentação do SDK](/help/datastreams/overview.md).

Depois de fornecer um nome exclusivo para a sequência de dados, selecione o botão de alternância ao lado de **[!UICONTROL Adobe Experience Platform]**. Em seguida, use os seguintes valores para preencher o restante do formulário:

| Campo de sequência de dados | Valor |
| --- | --- |
| [!UICONTROL Sandbox] | O nome da [sandbox](/help/sandboxes/home.md) da Experience Platform que contém a conexão de transmissão e os conjuntos de dados necessários para configurar a sequência de dados. |
| [!UICONTROL Streaming Inlet] | Uma conexão de transmissão válida para o Experience Platform. Consulte o tutorial em [criando uma conexão de streaming](/help/ingestion/tutorials/create-streaming-connection-ui.md) se você não tiver uma entrada de streaming existente. |
| [!UICONTROL Event Dataset] | Selecione o conjunto de dados [!DNL XDM ExperienceEvent] criado na [etapa anterior](#datasets). Se você incluiu o grupo de campos [[!UICONTROL IAB TCF 2.0 Consent] &#x200B;](/help/xdm/field-groups/event/iab.md) no esquema deste conjunto de dados, é possível rastrear eventos de alteração de consentimento ao longo do tempo usando o comando [`sendEvent`](#sendEvent), armazenando esses dados nesse conjunto de dados. Lembre-se de que os valores de consentimento armazenados neste conjunto de dados são **não** usados em fluxos de trabalho de imposição automática. |
| [!UICONTROL Profile Dataset] | Selecione o conjunto de dados [!DNL XDM Individual Profile] criado na [etapa anterior](#datasets). Ao responder aos ganchos de alteração de consentimento CMP usando o comando [`setConsent`](#setConsent), os dados coletados são armazenados nesse conjunto de dados. Como esse conjunto de dados é habilitado para perfil, os valores de consentimento armazenados nesse conjunto de dados são honrados durante os workflows de imposição automática. |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Quando terminar, selecione **[!UICONTROL Save]** na parte inferior da tela e continue seguindo os prompts adicionais para concluir a configuração.

### Execução de comandos de alteração de consentimento

Depois de criar o fluxo de dados descrito na seção anterior, você pode começar a usar os comandos do SDK para enviar dados de consentimento para a Experience Platform. As seções abaixo fornecem exemplos de como cada comando do SDK pode ser usado em cenários diferentes.

#### Uso de ganchos de alteração de consentimento CMP {#setConsent}

Muitos CMPs fornecem ganchos prontos para uso que ouvem eventos de alteração de consentimento. Quando esses eventos ocorrerem, você poderá usar o comando [`setConsent`](/help/collection/js/commands/setconsent.md) para atualizar os dados de consentimento desse cliente.

O comando `setConsent` espera dois argumentos:

1. Uma string que indica o tipo de comando (neste caso, &quot;setConsent&quot;).
1. Uma carga que contém uma matriz `consent`. A matriz deve conter pelo menos um objeto que forneça os campos de consentimento necessários.

O comando `setConsent` é exibido abaixo:

```js
alloy("setConsent", {
  consent: [{
    standard: "IAB TCF",
    version: "2.0",
    value: "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
    gdprApplies: "true"
  }]
});
```

| Propriedade de carga útil | Descrição |
| --- | --- |
| `standard` | O padrão de consentimento que está sendo usado. Esse valor deve ser definido como `IAB` para processamento de consentimento do TCF 2.0. |
| `version` | O número da versão do padrão de consentimento indicado em `standard`. Esse valor deve ser definido como `2.0` para processamento de consentimento do TCF 2.0. |
| `value` | A cadeia de consentimento codificada na base 64 gerada pelo CMP. |
| `gdprApplies` | Um valor booliano que indica se o GDPR se aplica ao cliente conectado no momento. Para que o TCF 2.0 seja aplicado a esse cliente, o valor deve ser definido como `true`. O padrão é `true`, se não estiver definido. |

O comando `setConsent` deve ser usado como parte de um gancho CMP que detecta alterações nas configurações de consentimento. O JavaScript a seguir fornece um exemplo de como o comando `setConsent` pode ser usado para o gancho `OnConsentChanged` do OneTrust:

```js
OneTrust.OnConsentChanged(function () {
  // Retrieve the TCF 2.0 consent data generated by the CMP, and pass it to Alloy. 
  __tcfapi("getTCData", 2, function (data, success) {
    if (success) {
      var tcString = data.tcString;
      var gdpr = data.gdprApplies;

      alloy("setConsent", {
        consent: [{
          standard: "IAB TCF",
          version: "2.0",
          value: tcString,
          gdprApplies: gdpr
        }]
      });
    }
  });
});
```

#### Uso de eventos {#sendEvent}

Você também pode coletar dados de consentimento TCF 2.0 em cada evento acionado no Experience Platform usando o comando `sendEvent`.

>[!NOTE]
>
>Para usar este método, você deve ter adicionado o grupo de campos Privacidade de eventos de experiência ao esquema [!DNL Profile] habilitado para [!DNL XDM ExperienceEvent]. Consulte a seção sobre [atualização do esquema ExperienceEvent](./dataset.md#event-schema) no guia de preparação do conjunto de dados para obter etapas sobre como configurar isso.

O comando `sendEvent` deve ser usado como um retorno de chamada em ouvintes de eventos apropriados em seu site. O comando espera dois argumentos: (1) uma cadeia de caracteres que indica o tipo de comando (neste caso, `sendEvent`) e (2) uma carga contendo um objeto `xdm` que fornece os campos de consentimento necessários como JSON:

```js
alloy("sendEvent", {
  xdm: {
    "consentStrings": [{
      "consentStandard": "IAB TCF",
      "consentStandardVersion": "2.0",
      "consentStringValue": "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
      "gdprApplies": true
    }]
  }
});
```

| Propriedade de carga útil | Descrição |
| --- | --- |
| `xdm.consentStrings` | Uma matriz que deve conter pelo menos um objeto que forneça os campos de consentimento necessários. |
| `consentStandard` | O padrão de consentimento que está sendo usado. Esse valor deve ser definido como `IAB` para processamento de consentimento do TCF 2.0. |
| `consentStandardVersion` | O número da versão do padrão de consentimento indicado em `standard`. Esse valor deve ser definido como `2.0` para processamento de consentimento do TCF 2.0. |
| `consentStringValue` | A cadeia de consentimento codificada na base 64 gerada pelo CMP. |
| `gdprApplies` | Um valor booliano que indica se o GDPR se aplica ao cliente conectado no momento. Para que o TCF 2.0 seja aplicado a esse cliente, o valor deve ser definido como `true`. O padrão é `true`, se não estiver definido. |

### Tratamento de respostas do SDK

Muitos comandos do Web SDK retornam promessas que indicam se a chamada foi bem-sucedida ou falhou. Em seguida, você pode usar essas respostas para obter lógica adicional, como exibir mensagens de confirmação ao cliente. Consulte [Respostas de comando](/help/collection/js/commands/command-responses.md) para obter mais informações.

## Exportar segmentos {#export}

>[!NOTE]
>
>Antes de começar a exportar segmentos, você deve garantir que seus segmentos incluam todos os campos de consentimento necessários. Consulte a seção em [configurando políticas de mesclagem](#merge-policies) para obter mais informações.

Depois de coletar dados de consentimento do cliente e criar segmentos de público-alvo contendo os atributos de consentimento necessários, é possível impor a conformidade com TCF 2.0 ao exportar esses segmentos para destinos downstream.

Se a configuração de consentimento `gdprApplies` estiver definida como `true` para um conjunto de perfis de clientes, todos os dados desses perfis exportados para destinos downstream serão filtrados com base nas preferências de consentimento de TCF para cada perfil. Qualquer perfil que não atenda às preferências de consentimento necessárias é ignorado durante o processo de exportação.

Os clientes devem consentir com as seguintes finalidades (conforme descrito pelas [políticas do TCF 2.0](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) para que seus perfis sejam incluídos em segmentos exportados para destinos:

* **Finalidade 1**: armazenar e/ou acessar informações em um dispositivo
* **Propósito 10**: desenvolver e melhorar produtos

O TCF 2.0 também exige que a fonte de dados verifique a permissão do fornecedor do destino antes de enviar os dados para esse destino. Dessa forma, a Experience Platform verifica se a permissão do fornecedor do destino está ativada para todas as IDs no cluster antes de incluir os dados vinculados a esse destino.

>[!NOTE]
>
>Qualquer segmento compartilhado com o Adobe Audience Manager contém os mesmos valores de consentimento TCF 2.0 que seus equivalentes do Experience Platform. Como [!DNL Audience Manager] compartilha a mesma ID de fornecedor do Experience Platform (565), as mesmas finalidades e permissões de fornecedor são necessárias. Consulte o documento no [plug-in do Adobe Audience Manager para TCF do IAB](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=pt-BR) para obter mais informações.

## Testar sua implementação {#test-implementation}

Depois de configurar a implementação do TCF 2.0 e exportar segmentos para destinos, os dados que não atenderem aos requisitos de consentimento não serão exportados. Para ver se os perfis corretos do cliente foram filtrados durante a exportação, verifique manualmente os armazenamentos de dados nos destinos para ver se o consentimento foi aplicado corretamente.

>[!IMPORTANT]
>
>Se várias IDs formarem um cluster e TCF 2.0 for aplicado, todo o cluster será excluído se mesmo uma única ID não contiver as finalidades corretas e as permissões do fornecedor.

## Próximas etapas

Esse documento abordou o processo de configuração das operações de dados do Experience Platform para atender às suas obrigações comerciais, conforme descrito pelo TCF 2.0. Consulte a visão geral sobre [governança, privacidade e segurança](../../overview.md) para obter mais informações sobre os recursos relacionados à privacidade da Experience Platform.
