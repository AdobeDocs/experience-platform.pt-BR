---
keywords: Experience Platform;inicial;IAB;IAB 2.0;consentimento;Consentimento
solution: Experience Platform
title: Suporte IAB TCF 2.0 no Experience Platform
description: Saiba como configurar suas operações de dados e esquemas para transmitir as opções de consentimento do cliente ao ativar segmentos para destinos no Adobe Experience Platform.
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 1%

---

# Suporte IAB TCF 2.0 no Experience Platform

A variável [!DNL Transparency & Consent Framework] (TCF), tal como sublinhado pela [!DNL Interactive Advertising Bureau] (IAB), é uma estrutura técnica de padrão aberto destinada a permitir que as organizações obtenham, registrem e atualizem o consentimento do consumidor para o processamento de seus dados pessoais, em conformidade com a legislação da União Europeia [!DNL General Data Protection Regulation] (RGPD). A segunda iteração da estrutura, TCF 2.0, concede mais flexibilidade para a forma como os consumidores podem fornecer ou não o consentimento, incluindo se e como os fornecedores podem usar determinadas características do processamento de dados, como a geolocalização precisa.

>[!NOTE]
>
>Mais informações sobre o TCF 2.0 podem ser encontradas no [Site do IAB na Europa](https://iabeurope.eu/tcf-2-0/), incluindo materiais de suporte e especificações técnicas.

O Adobe Experience Platform faz parte da [Lista de fornecedores do IAB TCF 2.0](https://iabeurope.eu/vendor-list-tcf-v2-0/), na ID **565**. Em conformidade com os requisitos do TCF 2.0, a Platform permite coletar dados de consentimento do cliente e integrá-los aos perfis de clientes armazenados. Esses dados de consentimento podem ser fatorados se os perfis são incluídos em segmentos de público exportados, dependendo do caso de uso.

>[!IMPORTANT]
>
>A Platform só pode estar em conformidade com a versão 2.0 do TCF (ou posterior). Não há suporte para versões anteriores do TCF.

Este documento fornece uma visão geral de como configurar suas operações de dados e esquemas de perfil para aceitar dados de consentimento do cliente gerados pelo CMP e como o Platform transmite opções de consentimento do usuário ao exportar segmentos.

## Pré-requisitos

Para seguir este guia, você deve usar uma Plataforma de gerenciamento de consentimento (CMP), comercial ou própria, integrada e compatível com a TCF do IAB. Consulte a [lista de CMPs compatíveis](https://iabeurope.eu/cmp-list/) para obter mais informações.

>[!IMPORTANT]
>
>Se a ID da CMP for inválida, a Platform continuará processando seus dados como estão. Para aplicar o TCF 2.0, você deve confirmar se o CMP tem uma ID válida que foi registrada com o TCF 2.0 do IAB antes de enviar dados para a Platform.

Este guia também requer uma compreensão funcional dos seguintes serviços da plataforma:

* [Experience Data Model (XDM)](../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [Serviço de identidade da Adobe Experience Platform](../../../../identity-service/home.md): soluciona o desafio fundamental apresentado pela fragmentação dos dados de experiência do cliente, unindo identidades em dispositivos e sistemas.
* [Perfil do cliente em tempo real](../../../../profile/home.md): Aproveita [!DNL Identity Service] para criar perfis detalhados do cliente a partir de seus conjuntos de dados em tempo real. [!DNL Real-Time Customer Profile] O extrai dados do Data Lake e mantém perfis de clientes em seu próprio armazenamento de dados separado.
* [Adobe Experience Platform Web SDK](../../../../edge/home.md): uma biblioteca JavaScript do lado do cliente que permite integrar vários serviços da plataforma ao seu site voltado para o cliente.
   * [Comandos de consentimento do SDK](../../../../edge/consent/supporting-consent.md): uma visão geral dos casos de uso dos comandos do SDK relacionados a consentimento mostrados neste guia.
* [Serviço de segmentação do Adobe Experience Platform](../../../../segmentation/home.md): permite dividir [!DNL Real-Time Customer Profile] em grupos de indivíduos que compartilham características semelhantes e responderão de forma semelhante às estratégias de marketing.

Além dos serviços da Platform listados acima, você também deve estar familiarizado com [destinos](../../../../data-governance/home.md) e seu papel no ecossistema da plataforma.

## Resumo do fluxo de consentimento do cliente {#summary}

As seções a seguir descrevem como os dados de consentimento são coletados e aplicados após o sistema ser configurado corretamente.

### Coleta de dados de consentimento

A Platform permite coletar dados de consentimento do cliente por meio do seguinte processo:

1. Um cliente fornece suas preferências de consentimento para a coleta de dados por meio de uma caixa de diálogo no site.
1. Seu CMP detecta a alteração de preferência de consentimento e gera os dados de consentimento TCF de acordo.
1. Usando o SDK da Web da Platform, os dados de consentimento gerados (retornados pela CMP) são enviados para a Adobe Experience Platform.
1. Os dados de consentimento coletados são assimilados em um [!DNL Profile]Conjunto de dados habilitado para cujo esquema contém campos de consentimento TCF.

Além dos comandos do SDK acionados pelos ganchos de alteração de consentimento do CMP, os dados de consentimento também podem fluir para o Experience Platform por meio de quaisquer dados XDM gerados pelo cliente que são carregados diretamente em um [!DNL Profile]conjunto de dados habilitado para.

Quaisquer segmentos compartilhados com a Platform pela Adobe Audience Manager (por meio da [!DNL Audience Manager] conector de origem ou outro) também podem conter dados de consentimento, desde que os campos apropriados tenham sido aplicados a esses segmentos por meio de [!DNL Experience Cloud Identity Service]. Para obter mais informações sobre como coletar dados de consentimento no [!DNL Audience Manager], consulte o documento no [Plug-in do Adobe Audience Manager para IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=pt-BR).

### Imposição de consentimento downstream

Depois que os dados de consentimento da TCF forem assimilados com êxito, os seguintes processos ocorrerão nos serviços downstream da plataforma:

1. [!DNL Real-Time Customer Profile] O atualiza os dados de consentimento armazenados para o perfil desse cliente.
1. A Platform processará as IDs do cliente somente se a permissão do fornecedor para a Platform (565) for fornecida para cada ID em um cluster.
1. Ao exportar segmentos para destinos pertencentes a membros da lista de fornecedores do TCF 2.0, o Platform incluirá perfis somente se as permissões do fornecedor forem para ambas as plataformas (565) *e* o destino individual é fornecido para cada ID em um cluster.

O restante das seções neste documento fornece orientação sobre como configurar a Platform e suas operações de dados para atender aos requisitos de coleta e aplicação descritos acima.

## Determine como gerar dados de consentimento do cliente na CMP {#consent-data}

Como cada sistema CMP é exclusivo, você deve determinar a melhor maneira de permitir que seus clientes forneçam consentimento enquanto interagem com seu serviço. Uma maneira comum de fazer isso é usando uma caixa de diálogo de consentimento de cookie, semelhante ao seguinte exemplo:

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

Essa caixa de diálogo deve permitir que o cliente aceite ou não as seguintes opções:

| Opção de consentimento | Descrição |
| --- | --- |
| **Finalidades** | Finalidades definem para quais fins de publicidade uma marca pode usar os dados de um cliente. Os seguintes objetivos devem ser aceitos para que a Platform processe as IDs do cliente: <ul><li>**Finalidade 1**: armazenar e/ou acessar informações em um dispositivo</li><li>**Propósito 10**: desenvolver e melhorar produtos</li></ul> |
| **Permissões de fornecedor** | Além dos objetivos tecnológicos do anúncio, o diálogo também deve permitir que o cliente opte por aceitar ou não ter seus dados usados por fornecedores específicos, incluindo o Adobe Experience Platform (565). |

### Strings de consentimento {#consent-strings}

Independentemente do método usado para coletar os dados, o objetivo é gerar um valor de sequência de caracteres com base nas opções de consentimento escolhidas pelo cliente, chamado de sequência de consentimento.

Na especificação do TCF, as cadeias de consentimento são usadas para codificar detalhes relevantes sobre as configurações de consentimento de um cliente, em termos de finalidades de marketing específicas, conforme definido por políticas e fornecedores. A Platform utiliza essas cadeias de caracteres para armazenar as configurações de consentimento de cada cliente e, portanto, uma nova cadeia de caracteres de consentimento deve ser gerada sempre que essas configurações forem alteradas.

As sequências de consentimento só podem ser criadas por um CMP registrado com a TCF do IAB. Para obter mais informações sobre como gerar sequências de consentimento usando seu CMP específico, consulte o [guia de formatação da sequência de consentimento](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) no repositório GitHub da TCF do IAB.

## Criar conjuntos de dados com campos de consentimento TCF {#datasets}

Os dados de consentimento do cliente devem ser enviados para conjuntos de dados cujos esquemas contêm campos de consentimento TCF. Consulte o tutorial em [criação de conjuntos de dados para capturar o consentimento do TCF 2.0](./dataset.md) para saber como criar o conjunto de dados de perfil necessário (e um conjunto de dados opcional de Evento de experiência) antes de continuar com este guia.

## Atualizar [!DNL Profile] políticas de mesclagem para incluir dados de consentimento {#merge-policies}

Depois de criar um [!DNL Profile]Conjunto de dados habilitado para coletar dados de consentimento, você deve garantir que suas políticas de mesclagem tenham sido configuradas para sempre incluir campos de consentimento TCF nos perfis do cliente. Isso envolve definir a precedência do conjunto de dados para que ele seja priorizado em relação a outros conjuntos de dados potencialmente conflitantes.

Para obter mais informações sobre como trabalhar com políticas de mesclagem, consulte [visão geral das políticas de mesclagem](../../../../profile/merge-policies/overview.md). Ao configurar suas políticas de mesclagem, você deve garantir que seus segmentos incluam todos os atributos de consentimento necessários fornecidos pela [Grupo de campos de esquema de privacidade XDM](./dataset.md#privacy-field-group), conforme descrito no guia sobre preparação de conjuntos de dados.

## Integre o SDK da Web do Experience Platform para coletar dados de consentimento do cliente {#sdk}

>[!NOTE]
>
>É necessário usar o SDK da Web do Experience Platform para processar dados de consentimento diretamente no Adobe Experience Platform. [!DNL Experience Cloud Identity Service] não é compatível no momento.
>
>[!DNL Experience Cloud Identity Service] O ainda é compatível com o processamento de consentimento no Adobe Audience Manager, no entanto, e a conformidade com o TCF 2.0 exige apenas que a biblioteca seja atualizada para [versão 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Depois de configurar o CMP para gerar cadeias de consentimento, você deve integrar o SDK da Web do Experience Platform para coletar essas cadeias de caracteres e enviá-las para a Platform. O SDK da Platform fornece dois comandos que podem ser usados para enviar dados de consentimento de TCF para a Platform (explicados nas subseções abaixo) e devem ser usados quando um cliente fornecer informações de consentimento pela primeira vez e sempre que o consentimento for alterado posteriormente.

**O SDK não faz interface com nenhum CMP pronto para uso**. Cabe a você determinar como integrar o SDK ao seu site, acompanhar as alterações de consentimento no CMP e chamar o comando apropriado.

### Criar um novo fluxo de dados

Para que o SDK envie dados para o Experience Platform, primeiro você deve criar um novo fluxo de dados para a Platform. Etapas específicas para criar um novo fluxo de dados são fornecidas na [Documentação do SDK](../../../../edge/datastreams/overview.md).

Depois de fornecer um nome exclusivo para o fluxo de dados, selecione o botão de alternância ao lado de **[!UICONTROL Adobe Experience Platform]**. Em seguida, use os seguintes valores para preencher o restante do formulário:

| Campo de sequência de dados | Valor |
| --- | --- |
| [!UICONTROL Sandbox] | O nome da plataforma [sandbox](../../../../sandboxes/home.md) que contém a conexão de transmissão e os conjuntos de dados necessários para configurar o fluxo de dados. |
| [!UICONTROL Entrada de transmissão] | Uma conexão de transmissão válida para o Experience Platform. Veja o tutorial sobre [criação de uma conexão de transmissão](../../../../ingestion/tutorials/create-streaming-connection-ui.md) se você não tiver uma entrada de transmissão existente. |
| [!UICONTROL Conjunto de dados do evento] | Selecione o [!DNL XDM ExperienceEvent] conjunto de dados criado na [etapa anterior](#datasets). Se você incluiu a variável [[!UICONTROL Consentimento IAB TCF 2.0] grupo de campos](../../../../xdm/field-groups/event/iab.md) neste esquema do conjunto de dados, você pode rastrear eventos de alteração de consentimento ao longo do tempo usando o [`sendEvent`](#sendEvent) , armazenando esses dados nesse conjunto de dados. Lembre-se de que os valores de consentimento armazenados neste conjunto de dados são **não** usado em workflows de imposição automática. |
| [!UICONTROL Conjunto de dados do perfil] | Selecione o [!DNL XDM Individual Profile] conjunto de dados criado na [etapa anterior](#datasets). Ao responder aos ganchos de alteração de consentimento do CMP usando o [`setConsent`](#setConsent) , os dados coletados serão armazenados nesse conjunto de dados. Como esse conjunto de dados é habilitado para perfil, os valores de consentimento armazenados nesse conjunto de dados são honrados durante os workflows de imposição automática. |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Quando terminar, selecione **[!UICONTROL Salvar]** na parte inferior da tela e continue seguindo os prompts adicionais para concluir a configuração.

### Execução de comandos de alteração de consentimento

Depois de criar o fluxo de dados descrito na seção anterior, você pode começar a usar comandos do SDK para enviar dados de consentimento para a Platform. As seções abaixo fornecem exemplos de como cada comando do SDK pode ser usado em cenários diferentes.

>[!NOTE]
>
>Para obter uma introdução à sintaxe comum para todos os comandos do SDK da Platform, consulte o documento em [execução de comandos](../../../../edge/fundamentals/executing-commands.md).

#### Uso de ganchos de alteração de consentimento CMP {#setConsent}

Muitos CMPs fornecem ganchos prontos para uso que ouvem eventos de alteração de consentimento. Quando esses eventos ocorrerem, você poderá usar o `setConsent` para atualizar os dados de consentimento desse cliente.

A variável `setConsent` O comando espera dois argumentos: (1) uma string que indica o tipo de comando (neste caso, &quot;setConsent&quot;) e (2) uma carga que contém um `consent` que deve conter pelo menos um objeto que forneça os campos de consentimento obrigatórios, conforme mostrado abaixo:

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
| `standard` | O padrão de consentimento que está sendo usado. Esse valor deve ser definido como `IAB` para processamento de consentimento TCF 2.0. |
| `version` | O número da versão do padrão de consentimento indicado em `standard`. Esse valor deve ser definido como `2.0` para processamento de consentimento TCF 2.0. |
| `value` | A cadeia de consentimento codificada na base 64 gerada pelo CMP. |
| `gdprApplies` | Um valor booliano que indica se o GDPR se aplica ao cliente conectado no momento. Para que o TCF 2.0 seja aplicado a esse cliente, o valor deve ser definido como `true`. O padrão é `true` se não estiver definido. |

A variável `setConsent` deve ser usado como parte de um gancho CMP que detecta alterações nas configurações de consentimento. O JavaScript a seguir fornece um exemplo de como a variável `setConsent` comando pode ser usado para o OneTrust `OnConsentChanged` gancho:

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

Você também pode coletar dados de consentimento do TCF 2.0 em cada evento acionado na Plataforma usando o `sendEvent` comando.

>[!NOTE]
>
>Para usar esse método, é necessário ter adicionado o grupo de campos Privacidade de evento de experiência ao [!DNL Profile]-habilitado [!DNL XDM ExperienceEvent] esquema. Consulte a seção sobre [atualização do esquema ExperienceEvent](./dataset.md#event-schema) no guia de preparação do conjunto de dados, para obter etapas sobre como configurar isso.

A variável `sendEvent` deve ser usado como um retorno de chamada nos ouvintes de eventos apropriados do seu site. O comando espera dois argumentos: (1) uma string que indica o tipo de comando (nesse caso, `sendEvent`), e (2) uma carga útil contendo um `xdm` que fornece os campos de consentimento necessários como JSON:

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
| `consentStandard` | O padrão de consentimento que está sendo usado. Esse valor deve ser definido como `IAB` para processamento de consentimento TCF 2.0. |
| `consentStandardVersion` | O número da versão do padrão de consentimento indicado em `standard`. Esse valor deve ser definido como `2.0` para processamento de consentimento TCF 2.0. |
| `consentStringValue` | A cadeia de consentimento codificada na base 64 gerada pelo CMP. |
| `gdprApplies` | Um valor booliano que indica se o GDPR se aplica ao cliente conectado no momento. Para que o TCF 2.0 seja aplicado a esse cliente, o valor deve ser definido como `true`. O padrão é `true` se não estiver definido. |

### Tratamento de respostas do SDK

Todos [!DNL Platform SDK] Os comandos do retornam promessas que indicam se a chamada foi bem-sucedida ou falhou. Em seguida, você pode usar essas respostas para obter lógica adicional, como exibir mensagens de confirmação ao cliente. Consulte a seção sobre [lidando com sucesso ou falha](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) no guia sobre a execução de comandos do SDK para obter exemplos específicos.

## Exportar segmentos {#export}

>[!NOTE]
>
>Antes de começar a exportar segmentos, você deve garantir que seus segmentos incluam todos os campos de consentimento necessários. Consulte a seção sobre [configuração de políticas de mesclagem](#merge-policies) para obter mais informações.

Depois de coletar dados de consentimento do cliente e criar segmentos de público-alvo contendo os atributos de consentimento necessários, é possível impor a conformidade com TCF 2.0 ao exportar esses segmentos para destinos downstream.

Desde que a configuração de consentimento `gdprApplies` está definida como `true` para um conjunto de perfis de clientes, todos os dados desses perfis exportados para destinos downstream são filtrados com base nas preferências de consentimento da TCF para cada perfil. Qualquer perfil que não atenda às preferências de consentimento necessárias é ignorado durante o processo de exportação.

Os clientes devem consentir com os seguintes objetivos (conforme descrito pelo [Políticas do TCF 2.0](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) para que seus perfis sejam incluídos em segmentos exportados para destinos:

* **Finalidade 1**: armazenar e/ou acessar informações em um dispositivo
* **Finalidade 10**: desenvolver e melhorar produtos

O TCF 2.0 também exige que a fonte de dados verifique a permissão do fornecedor do destino antes de enviar os dados para esse destino. Dessa forma, a Platform verifica se a permissão do fornecedor do destino é aceita para todas as IDs no cluster antes de incluir dados vinculados a esse destino.

>[!NOTE]
>
>Quaisquer segmentos compartilhados com o Adobe Audience Manager conterão os mesmos valores de consentimento TCF 2.0 que seus equivalentes da Platform. Desde [!DNL Audience Manager] O compartilha a mesma ID de fornecedor da Plataforma (565), as mesmas finalidades e permissões de fornecedor são necessárias. Consulte o documento no [Plug-in do Adobe Audience Manager para IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=pt-BR) para obter mais informações.

## Testar sua implementação {#test-implementation}

Depois de configurar a implementação do TCF 2.0 e exportar segmentos para destinos, os dados que não atenderem aos requisitos de consentimento não serão exportados. No entanto, para ver se os perfis certos do cliente foram filtrados durante a exportação, você deve verificar manualmente os armazenamentos de dados em seus destinos para ver se o consentimento foi aplicado corretamente.

É importante observar que, se várias IDs compuserem um cluster e o TCF 2.0 for aplicado, todo o cluster será excluído se mesmo uma única ID não contiver as finalidades corretas e as permissões do fornecedor.

## Próximas etapas

Esse documento abordou o processo de configuração das operações de dados da Platform para atender às suas obrigações comerciais, conforme descrito pelo TCF 2.0. Consulte a visão geral em [governança, privacidade e segurança](../../overview.md) para obter mais informações sobre os recursos relacionados à privacidade da Platform.
