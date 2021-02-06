---
keywords: Experience Platform;home;IAB;IAB 2.0;consentimento;Consentimento
solution: Experience Platform
title: Suporte a IAB TCF 2.0 no Experience Platform
topic: privacy events
description: Saiba como configurar suas operações e schemas de dados para transmitir opções de consentimento do cliente ao ativar segmentos para destinos no Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: b0af9d49f6cfe50f6dff745dfac174dbaa76d070
workflow-type: tm+mt
source-wordcount: '2458'
ht-degree: 0%

---


# Suporte a IAB TCF 2.0 no Experience Platform

O [!DNL Transparency & Consent Framework] (TCF), conforme descrito pelo [!DNL Interactive Advertising Bureau] (IAB), é um quadro técnico de padrão aberto destinado a permitir que as organizações obtenham, registrem e atualizem o consentimento do consumidor para o processamento dos seus dados pessoais, em conformidade com a União Europeia [!DNL General Data Protection Regulation] (RGPD). A segunda iteração da estrutura, TCF 2.0, concede mais flexibilidade para a forma como os consumidores podem fornecer ou recusar o consentimento, incluindo se e como os fornecedores podem utilizar determinados recursos do processamento de dados, como geolocalização precisa.

>[!NOTE]
>
>Mais informações sobre o TCF 2.0 podem ser encontradas no [site IAB Europe](https://iabeurope.eu/tcf-2-0/), incluindo materiais de suporte e especificações técnicas.

A Adobe Experience Platform faz parte da lista registrada [IAB TCF 2.0 do fornecedor](https://iabeurope.eu/vendor-list-tcf-v2-0/), na ID **565**. Em conformidade com os requisitos do TCF 2.0, a Plataforma permite coletar dados de consentimento do cliente e integrá-los aos perfis armazenados do cliente. Esses dados de consentimento podem ser tidos em conta se os perfis são incluídos nos segmentos de audiência exportados, dependendo de seu caso de uso.

>[!IMPORTANT]
>
>A plataforma só é capaz de cumprir com a versão 2.0 do TCF (ou superior). As versões anteriores do TCF não são suportadas.

Este documento fornece uma visão geral de como configurar suas operações de dados e schemas de perfis para aceitar dados de consentimento do cliente gerados pelo CMP e como a Plataforma transmite as opções de consentimento do usuário ao exportar segmentos.

## Pré-requisitos

Para seguir este guia, você deve usar uma Plataforma de gerenciamento de consentimento (CMP), comercial ou própria, integrada e compatível com o TCF da IAB. Consulte a lista [de CMPs](https://iabeurope.eu/cmp-list/) compatíveis para obter mais informações.

>[!IMPORTANT]
>
>Se a ID do CMP for inválida, a Plataforma continuará processando seus dados como estão. Para aplicar o TCF 2.0, você deve confirmar que o CMP tem uma ID válida que foi registrada com o IAB TCF 2.0 antes de enviar os dados para a Plataforma.

Este guia também requer um entendimento prático dos seguintes serviços da plataforma:

* [Modelo de dados de experiência (XDM)](../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [Serviço](../../../../identity-service/home.md) de identidade Adobe Experience Platform: Resolve o desafio fundamental colocado pela fragmentação dos dados de experiência do cliente ao unir identidades entre dispositivos e sistemas.
* [Perfil](../../../../profile/home.md) do cliente em tempo real: Aproveita  [!DNL Identity Service] para criar perfis detalhados do cliente a partir de seus conjuntos de dados em tempo real. [!DNL Real-time Customer Profile] extrai dados do Data Lake e persiste em perfis do cliente em seu próprio armazenamento de dados separado.
* [Adobe Experience Platform Web SDK](../../../../edge/home.md): Uma biblioteca JavaScript do lado do cliente que permite integrar vários serviços da plataforma ao seu site voltado para o cliente.
   * [Comandos](../../../../edge/consent/supporting-consent.md) de consentimento do SDK: Uma visão geral de caso de uso dos comandos SDK relacionados ao consentimento mostrados neste guia.
* [Serviço](../../../../segmentation/home.md) de segmentação do Adobe Experience Platform: Permite dividir  [!DNL Real-time Customer Profile] dados em grupos de indivíduos que compartilham características semelhantes e responderão de forma semelhante às estratégias de marketing.

Além dos serviços da plataforma listados acima, você também deve estar familiarizado com [destinos](../../../../data-governance/home.md) e com sua função no ecossistema da plataforma.

## Resumo do fluxo de consentimento do cliente {#summary}

As seções a seguir descrevem como os dados de consentimento são coletados e aplicados depois que o sistema é configurado corretamente.

### Consentir coleta de dados

A plataforma permite coletar dados de consentimento do cliente por meio do seguinte processo:

1. Um cliente fornece suas preferências de consentimento para a coleta de dados por meio de uma caixa de diálogo em seu site.
1. Seu CMP detecta a alteração da preferência de consentimento e gera dados de consentimento TCF de acordo.
1. Usando o SDK da Web da plataforma, os dados de consentimento gerados (retornados pelo CMP) são enviados para a Adobe Experience Platform.
1. Os dados de consentimento coletados são ingeridos em um conjunto de dados habilitado para [!DNL Profile] cujo schema contém campos de consentimento TCF.

Além dos comandos do SDK acionados por ganchos de consentimento de alteração do CMP, os dados de consentimento também podem fluir para o Experience Platform por meio de quaisquer dados XDM gerados pelo cliente que sejam carregados diretamente para um conjunto de dados habilitado para [!DNL Profile].

Qualquer segmento compartilhado com a Plataforma pela Adobe Audience Manager (por meio do conector de origem [!DNL Audience Manager] ou de outra forma) também pode conter dados de consentimento, desde que os campos apropriados tenham sido aplicados a esses segmentos por meio de [!DNL Experience Cloud Identity Service]. Para obter mais informações sobre como coletar dados de consentimento em [!DNL Audience Manager], consulte o documento no [plug-in Adobe Audience Manager para IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

### Execução de consentimento a jusante

Depois que os dados de consentimento do TCF forem assimilados com êxito, os seguintes processos ocorrerão nos serviços da plataforma downstream:

1. [!DNL Real-time Customer Profile] atualiza os dados de consentimento armazenados para o perfil desse cliente.
1. A plataforma processa as IDs do cliente somente se a permissão do fornecedor para a Plataforma (565) for fornecida para cada ID em um cluster.
1. Ao exportar segmentos para destinos pertencentes aos membros da lista do fornecedor TCF 2.0, a Plataforma inclui apenas perfis se as permissões do fornecedor para a Plataforma (565) *e* o destino individual forem fornecidas para cada ID em um cluster.

O restante das seções deste documento fornecem orientações sobre como configurar a Plataforma e suas operações de dados para atender aos requisitos de coleta e aplicação descritos acima.

## Determine como gerar dados de consentimento do cliente em seu CMP {#consent-data}

Como cada sistema CMP é único, você deve determinar a melhor maneira de permitir que seus clientes forneçam consentimento à medida que interagem com seu serviço. Uma maneira comum de conseguir isso é usando uma caixa de diálogo de consentimento de cookie, semelhante ao exemplo a seguir:

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

Essa caixa de diálogo deve permitir que o cliente opt in ou saia do seguinte:

| Opção de consentimento | Descrição |
| --- | --- |
| **Finalidades** | Finalidades definem para quais fins de publicidade uma marca pode usar os dados de um cliente. As seguintes finalidades devem ser aceitas para que a Plataforma processe as IDs do cliente: <ul><li>**Finalidade 1**: Armazenar e/ou acessar informações em um dispositivo</li><li>**Finalidade 10**: Desenvolver e melhorar produtos</li></ul> |
| **Permissões do fornecedor** | Além dos fins técnicos do anúncio, a caixa de diálogo também deve permitir que o cliente opt in ou não ter seus dados usados por fornecedores específicos, incluindo a Adobe Experience Platform (565). |

### Strings de consentimento {#consent-strings}

Independentemente do método usado para coletar os dados, o objetivo é gerar um valor de sequência de caracteres com base nas opções de consentimento escolhidas pelo cliente, chamadas de sequência de caracteres de consentimento.

Na especificação TCF, as strings de consentimento são usadas para codificar detalhes relevantes sobre as configurações de consentimento de um cliente, em termos de finalidades de marketing específicas, conforme definido pelas políticas e fornecedores. A plataforma utiliza essas sequências de caracteres para armazenar as configurações de consentimento para cada cliente e, portanto, uma nova sequência de caracteres de consentimento deve ser gerada sempre que essas configurações forem alteradas.

As strings de consentimento só podem ser criadas por um CMP registrado no IAB TCF. Para obter mais informações sobre como gerar sequências de caracteres de consentimento usando seu CMP específico, consulte o [guia de formatação de sequência de caracteres de consentimento](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) no acordo IAB TCF GitHub.

## Criar conjuntos de dados com campos de consentimento TCF {#datasets}

Os dados de consentimento do cliente devem ser enviados para conjuntos de dados cujos schemas contenham campos de consentimento TCF. Consulte o tutorial em [criar conjuntos de dados para capturar o consentimento do TCF 2.0](./dataset.md) para saber como criar os dois conjuntos de dados necessários antes de continuar com este guia.

## Atualize [!DNL Profile] as políticas de mesclagem para incluir dados de consentimento {#merge-policies}

Depois de criar um conjunto de dados habilitado para [!DNL Profile] para coletar dados de consentimento, verifique se as políticas de mesclagem foram configuradas para incluir sempre campos de consentimento TCF nos perfis do cliente. Isso envolve configurar a precedência do conjunto de dados para que seu conjunto de dados de consentimento seja priorizado em relação a outros conjuntos de dados potencialmente conflitantes.

Para obter mais informações sobre como trabalhar com políticas de mesclagem, consulte o [guia do usuário das políticas de mesclagem](../../../../profile/ui/merge-policies.md). Ao configurar suas políticas de mesclagem, você deve garantir que seus segmentos incluam todos os atributos de consentimento necessários fornecidos pelo [mixin de privacidade XDM](./dataset.md#privacy-mixin), conforme descrito no guia sobre a preparação do conjunto de dados.

## Integre o SDK da Web do Experience Platform para coletar dados de consentimento do cliente {#sdk}

>[!NOTE]
>
>O uso do Experience Platform Web SDK é necessário para processar dados de consentimento diretamente no Adobe Experience Platform. [!DNL Experience Cloud Identity Service] não é suportado no momento.
>
>[!DNL Experience Cloud Identity Service] no entanto, ainda há suporte para o processamento de consentimento no Adobe Audience Manager, e a conformidade com o TCF 2.0 exige apenas que a biblioteca seja atualizada para a  [versão 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Depois de configurar seu CMP para gerar strings de consentimento, você deve integrar o SDK da Web do Experience Platform para coletar essas strings e enviá-las para a Plataforma. O SDK da plataforma fornece dois comandos que podem ser usados para enviar dados de consentimento do TCF para a Plataforma (explicado nas subseções abaixo) e devem ser usados quando um cliente fornece informações de consentimento pela primeira vez e a qualquer momento que o consentimento for alterado posteriormente.

**O SDK não faz interface com nenhum CMP pronto para usar**. Cabe a você determinar como integrar o SDK ao seu site, acompanhar as mudanças de consentimento no CMP e chamar o comando apropriado.

### Criar uma nova configuração de borda

Para que o SDK envie dados para o Experience Platform, é necessário primeiro criar uma nova configuração de borda para a Plataforma em [!DNL Adobe Experience Platform Launch]. Etapas específicas para criar uma nova configuração são fornecidas na [documentação do SDK](../../../../edge/fundamentals/edge-configuration.md).

Depois de fornecer um nome exclusivo para a configuração, selecione o botão de alternância ao lado de **[!UICONTROL Adobe Experience Platform]**. Em seguida, use os seguintes valores para preencher o restante do formulário:

| Campo de configuração do Edge | Valor |
| --- | --- |
| [!UICONTROL Sandbox] | O nome da plataforma [sandbox](../../../../sandboxes/home.md) que contém a conexão de streaming e os conjuntos de dados necessários para configurar a configuração de borda. |
| [!UICONTROL Entrada de fluxo] | Uma conexão de streaming válida para Experience Platform. Consulte o tutorial em [criar uma conexão de streaming](../../../../ingestion/tutorials/create-streaming-connection-ui.md) se você não tiver uma entrada de streaming existente. |
| [!UICONTROL Conjunto de dados do evento] | Selecione o conjunto de dados [!DNL XDM ExperienceEvent] criado na etapa [anterior](#datasets). |
| [!UICONTROL Conjunto de dados do perfil] | Selecione o conjunto de dados [!DNL XDM Individual Profile] criado na etapa [anterior](#datasets). |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Quando terminar, selecione **[!UICONTROL Salvar]** na parte inferior da tela e continue seguindo quaisquer prompts adicionais para concluir a configuração.

### Como fazer comandos de alteração de consentimento

Depois de criar a configuração de borda descrita na seção anterior, você pode fazer start usando comandos do SDK para enviar dados de consentimento para a Plataforma. As seções abaixo fornecem exemplos de como cada comando do SDK pode ser usado em diferentes cenários.

>[!NOTE]
>
>Para obter uma introdução à sintaxe comum de todos os comandos do SDK da plataforma, consulte o documento em [executar comandos](../../../../edge/fundamentals/executing-commands.md).

#### Uso de ganchos de alteração de consentimento do CMP

Muitos CMPs fornecem ganchos prontos para uso que escutam eventos de mudança de consentimento. Quando esses eventos ocorrem, você pode usar o comando `setConsent` para atualizar os dados de consentimento do cliente.

O comando `setConsent` espera dois argumentos: (1) uma string que indica o tipo de comando (neste caso, &quot;setConsent&quot;) e (2) uma carga que contém uma matriz `consent`, que deve conter pelo menos um objeto que fornece os campos de consentimento necessários, conforme mostrado abaixo:

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

| Propriedade Payload | Descrição |
| --- | --- |
| `standard` | O padrão de consentimento sendo usado. Esse valor deve ser definido como `IAB` para processamento de consentimento TCF 2.0. |
| `version` | O número da versão do padrão de consentimento indicado em `standard`. Esse valor deve ser definido como `2.0` para processamento de consentimento TCF 2.0. |
| `value` | A string de consentimento codificada em base 64 gerada pelo CMP. |
| `gdprApplies` | Um valor booliano que indica se o RGPD se aplica ao cliente conectado no momento. Para que o TCF 2.0 seja aplicado a este cliente, o valor deve ser definido como `true`. |

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

#### Uso de eventos

Você também pode coletar dados de consentimento do TCF 2.0 em cada evento acionado na Plataforma usando o comando `sendEvent`.

>[!NOTE]
>
>Para usar esse método, você deve ter adicionado o [!DNL Experience Event Privacy mixin] ao schema [!DNL Profile] habilitado para [!DNL XDM ExperienceEvent]. Consulte a seção sobre [atualização do schema ExperienceEvent](./dataset.md#event-schema) no guia de preparação do conjunto de dados para obter as etapas sobre como configurar isso.

O comando `sendEvent` deve ser usado como um retorno de chamada nos ouvintes de evento apropriados do seu site. O comando espera dois argumentos: (1) uma string que indica o tipo de comando (neste caso, `sendEvent`) e (2) uma carga que contém um objeto `xdm` que fornece os campos de consentimento necessários como JSON:

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

| Propriedade Payload | Descrição |
| --- | --- |
| `xdm.consentStrings` | Uma matriz que deve conter pelo menos um objeto que fornece os campos de consentimento necessários. |
| `consentStandard` | O padrão de consentimento sendo usado. Esse valor deve ser definido como `IAB` para processamento de consentimento TCF 2.0. |
| `consentStandardVersion` | O número da versão do padrão de consentimento indicado em `standard`. Esse valor deve ser definido como `2.0` para processamento de consentimento TCF 2.0. |
| `consentStringValue` | A string de consentimento codificada em base 64 gerada pelo CMP. |
| `gdprApplies` | Um valor booliano que indica se o RGPD se aplica ao cliente conectado no momento. Para que o TCF 2.0 seja aplicado a este cliente, o valor deve ser definido como `true`. |

### Tratamento de respostas do SDK

Todos os comandos [!DNL Platform SDK] retornam promessas que indicam se a chamada foi bem-sucedida ou falhou. Você pode usar essas respostas para uma lógica adicional, como a exibição de mensagens de confirmação para o cliente. Consulte a seção sobre [como lidar com sucesso ou falha](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) no guia sobre a execução de comandos do SDK para obter exemplos específicos.

## Exportar segmentos {#export}

>[!NOTE]
>
>Antes de start na exportação de segmentos, verifique se os segmentos incluem todos os campos de consentimento necessários. Consulte a seção sobre [como configurar as políticas de mesclagem](#merge-policies) para obter mais informações.

Depois de coletar os dados de consentimento do cliente e criar segmentos de audiência contendo os atributos de consentimento necessários, você poderá aplicar a conformidade do TCF 2.0 ao exportar esses segmentos para destinos downstream.

Desde que a configuração de consentimento `gdprApplies` esteja definida como `true` para um conjunto de perfis do cliente, todos os dados desses perfis exportados para destinos downstream serão filtrados com base nas preferências de consentimento para cada perfil. Qualquer perfil que não atender às preferências de consentimento necessário será ignorado durante o processo de exportação.

Os clientes devem consentir nos seguintes fins (conforme descrito por [políticas TCF 2.0](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) para que seus perfis sejam incluídos nos segmentos que são exportados para destinos:

* **Finalidade 1**: Armazenar e/ou acessar informações em um dispositivo
* **Finalidade 10**: Desenvolver e melhorar produtos

O TCF 2.0 também exige que a fonte de dados verifique a permissão do fornecedor de destino antes de enviar dados para esse destino. Dessa forma, a Plataforma verifica se a permissão do fornecedor de destino está opt in para todas as IDs no cluster antes de incluir os dados vinculados a esse destino.

>[!NOTE]
>
>Todos os segmentos compartilhados com a Adobe Audience Manager conterão os mesmos valores de consentimento do TCF 2.0 que seus parceiros da plataforma. Como [!DNL Audience Manager] compartilha a mesma ID de fornecedor que a Plataforma (565), os mesmos objetivos e permissões de fornecedor são necessários. Consulte o documento no [plug-in Adobe Audience Manager para IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) para obter mais informações.

## Testar sua implementação {#test-implementation}

Após configurar sua implementação do TCF 2.0 e ter exportado segmentos para destinos, todos os dados que não atenderem aos requisitos de consentimento não serão exportados. No entanto, para verificar se os perfis certos do cliente foram filtrados durante a exportação, verifique manualmente os armazenamentos de dados em seus destinos para ver se o consentimento foi aplicado corretamente.

É importante observar que se várias IDs formarem um cluster e o TCF 2.0 for aplicado, todo o cluster será excluído se mesmo uma única ID não contiver os objetivos corretos e as permissões do fornecedor.

## Próximas etapas

Este documento cobriu o processo de configuração das operações de dados da plataforma para atender às suas obrigações comerciais, conforme descrito pelo TCF 2.0. Consulte a visão geral sobre [governança, privacidade e segurança](../../overview.md) para obter mais informações sobre os recursos relacionados à privacidade da plataforma.