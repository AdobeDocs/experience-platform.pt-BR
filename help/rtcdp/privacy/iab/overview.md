---
keywords: Experience Platform;home;IAB;IAB 2.0;
solution: Experience Platform
title: Suporte ao IAB TCF 2.0 na Plataforma de dados do cliente em tempo real
topic: privacy events
translation-type: tm+mt
source-git-commit: 1bb896f7629d7b71b94dd107eeda87701df99208
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 1%

---


# Suporte a IAB TCF 2.0 em [!DNL Real-time Customer Data Platform]

O [!DNL Transparency & Consent Framework] (TCF), tal como delineado pelo [!DNL Interactive Advertising Bureau] (IAB), é um quadro técnico de padrão aberto destinado a permitir que as organizações obtenham, registrem e atualizem o consentimento do consumidor para o tratamento dos seus dados pessoais, em conformidade com o RGPD [!DNL General Data Protection Regulation] (European União). A segunda iteração da estrutura, TCF 2.0, concede mais flexibilidade para a forma como os consumidores podem fornecer ou recusar o consentimento, incluindo se e como os fornecedores podem utilizar determinados recursos do processamento de dados, como geolocalização precisa.

>[!NOTE]
>
>Para mais informações sobre o TCF 2.0, consultar o sítio Web [da](https://iabeurope.eu/tcf-2-0/)IAB Europe, incluindo materiais de suporte e especificações técnicas.

[!DNL Real-time Customer Data Platform (Real-time CDP)] faz parte da lista [registrada do fornecedor](https://iabeurope.eu/vendor-list-tcf-v2-0/)IAB TCF 2.0, com a ID **565**. Em conformidade com os requisitos do TCF 2.0, [!DNL Real-time CDP] permite coletar dados de consentimento do cliente e integrá-los aos perfis armazenados do cliente. Esses dados de consentimento podem ser tidos em conta se os perfis são incluídos nos segmentos de audiência exportados, dependendo de seu caso de uso.

>[!IMPORTANT]
>
>[!DNL Real-time CDP] só é capaz de cumprir com a versão 2.0 do TCF (ou superior). As versões anteriores do TCF não são suportadas.

Este documento fornece uma visão geral de como configurar suas operações de dados e schemas de perfis para aceitar dados de consentimento do cliente gerados pelo CMP e como [!DNL Real-time CDP] transmitir as opções de consentimento do usuário ao exportar segmentos.

## Pré-requisitos

Para seguir este guia, você deve usar uma Plataforma de gerenciamento de consentimento (CMP), comercial ou própria, integrada e compatível com o TCF da IAB. Consulte a [lista de CMPs](https://iabeurope.eu/cmp-list/) compatíveis para obter mais informações.

>[!IMPORTANT]
>
>Se a ID do CMP for inválida, [!DNL Real-time CDP] continuará processando os dados como estão. Para aplicar o TCF 2.0, você deve confirmar que o CMP tem uma ID válida que foi registrada no IAB TCF 2.0 antes de enviar os dados para [!DNL Experience Platform].

Este guia também requer uma compreensão prática dos seguintes serviços da Adobe Experience Platform:

* [Modelo de dados de experiência (XDM)](../../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
* [Serviço](../../../identity-service/home.md)de identidade Adobe Experience Platform: Resolve o desafio fundamental colocado pela fragmentação dos dados de experiência do cliente ao unir identidades entre dispositivos e sistemas.
* [Perfil](../../../profile/home.md)do cliente em tempo real: Aproveita [!DNL Identity Service] para criar perfis detalhados do cliente a partir de seus conjuntos de dados em tempo real. [!DNL Real-time Customer Profile] extrai dados do Data Lake e persiste em perfis do cliente em seu próprio armazenamento de dados separado.
* [Adobe Experience Platform Web SDK](../../../edge/home.md): Uma biblioteca JavaScript do lado do cliente que permite integrar vários [!DNL Platform] serviços ao seu site voltado para o cliente.
   * [Comandos](../../../edge/fundamentals/supporting-consent.md)de consentimento do SDK: Uma visão geral de caso de uso dos comandos SDK relacionados ao consentimento mostrados neste guia.
* [Serviço](../../../segmentation/home.md)de segmentação do Adobe Experience Platform: Permite dividir [!DNL Real-time Customer Profile] dados em grupos de indivíduos que compartilham características semelhantes e responderão de forma semelhante às estratégias de marketing.

Além dos [!DNL Platform] serviços listados acima, você também deve estar familiarizado com os [destinos](../../destinations/destinations-overview.md) e seu uso em [!DNL Real-time CDP].

## Resumo do fluxo de consentimento do cliente {#summary}

As seções a seguir descrevem como os dados de consentimento são coletados e aplicados depois que o sistema é configurado corretamente.

### Consentir coleta de dados

[!DNL Real-time CDP] permite coletar dados de consentimento do cliente por meio do seguinte processo:

1. Um cliente fornece suas preferências de consentimento para a coleta de dados por meio de uma caixa de diálogo em seu site.
1. Seu CMP detecta a alteração da preferência de consentimento e gera dados de consentimento IAB de acordo.
1. Usando o [!DNL Experience Platform Web SDK], os dados de consentimento gerados (retornados pelo CMP) são enviados para a Adobe Experience Platform.
1. Os dados de consentimento coletados são ingeridos em um conjunto de dados [!DNL Profile]habilitado cujo schema contém campos de consentimento IAB.

Além dos comandos do SDK acionados por ganchos de alteração de consentimento do CMP, os dados de consentimento também podem fluir para [!DNL Experience Platform] qualquer dado XDM gerado pelo cliente que é carregado diretamente para um conjunto de dados [!DNL Profile]habilitado.

Qualquer segmento compartilhado com a Adobe Audience Manager (por meio do conector de [!DNL Platform] origem ou de outra forma) também pode conter dados de consentimento, desde que os campos apropriados tenham sido aplicados a esses segmentos por meio [!DNL Audience Manager] [!DNL Experience Cloud Identity Service]. Para obter mais informações sobre como coletar dados de consentimento no, consulte [!DNL Audience Manager]o documento no plug-in [Adobe Audience Manager para IAB TCF](https://docs.adobe.com/help/pt-BR/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

### Execução de consentimento a jusante

Depois que os dados de consentimento do IAB forem assimilados com êxito, os seguintes processos ocorrerão nos [!DNL Real-time CDP] serviços de downstream:

1. [!DNL Real-time Customer Profile] atualiza os dados de consentimento armazenados para o perfil desse cliente.
1. [!DNL Real-time CDP] processa as IDs do cliente somente se a permissão do fornecedor para [!DNL Real-time CDP] (565) for fornecida para cada ID em um cluster.
1. Ao exportar segmentos para destinos pertencentes aos membros da lista do fornecedor TCF 2.0, [!DNL Real-time CDP] só inclui perfis se as permissões do fornecedor para [!DNL Real-time CDP] (565) *e destino forem fornecidas para cada ID em um cluster* .

O restante das seções deste documento fornecem orientações sobre como configurar [!DNL Real-time CDP] e suas operações de dados para atender aos requisitos de coleta e aplicação descritos acima.

## Determine como gerar dados de consentimento do cliente em seu CMP {#consent-data}

Como cada sistema CMP é único, você deve determinar a melhor maneira de permitir que seus clientes forneçam consentimento à medida que interagem com seu serviço. Uma maneira comum de conseguir isso é usando uma caixa de diálogo de consentimento de cookie, semelhante ao exemplo a seguir:

![](../assets/iab/cmp-dialog.png)

Essa caixa de diálogo deve permitir que o cliente opt in ou saia do seguinte:

| Opção de consentimento | Descrição |
| --- | --- |
| **Finalidades** | Finalidades definem para quais fins de publicidade uma marca pode usar os dados de um cliente. As seguintes finalidades devem ser aceitas para [!DNL Real-time CDP] processar IDs de clientes: <ul><li>**Finalidade 1**: Armazenar e/ou acessar informações em um dispositivo</li><li>**Finalidade 10**: Desenvolver e melhorar produtos</li></ul> |
| **Permissões do fornecedor** | Além dos fins técnicos do anúncio, a caixa de diálogo também deve permitir que o cliente opt in ou não ter seus dados usados por fornecedores específicos, inclusive [!DNL  Real-time CDP] (565). |

### Strings de consentimento {#consent-strings}

Independentemente do método usado para coletar os dados, o objetivo é gerar um valor de sequência de caracteres com base nas opções de consentimento escolhidas pelo cliente, chamadas de sequência de caracteres **de** consentimento.

Na especificação TCF, as strings de consentimento são usadas para codificar detalhes relevantes sobre as configurações de consentimento de um cliente, em termos de finalidades de marketing específicas, conforme definido pelas políticas e fornecedores. [!DNL Real-time CDP] utiliza essas sequências de caracteres para armazenar as configurações de consentimento para cada cliente e, portanto, uma nova sequência de caracteres de consentimento deve ser gerada sempre que essas configurações forem alteradas.

As strings de consentimento só podem ser criadas por um CMP registrado no IAB TCF. Para obter mais informações sobre como gerar sequências de caracteres de consentimento usando seu CMP específico, consulte o guia [de formatação da sequência de caracteres de](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) consentimento no acordo IAB TCF GitHub.

## Criar conjuntos de dados com campos de consentimento IAB {#datasets}

Os dados de consentimento do cliente devem ser enviados para um conjunto de dados cujo schema contenha campos de consentimento IAB. Consulte o tutorial sobre como [criar conjuntos de dados para capturar o consentimento](./dataset-preparation.md) do TCF 2.0 para saber como criar os dois conjuntos de dados necessários antes de continuar com este guia.

## Atualizar [!DNL Profile] políticas de mesclagem para incluir dados de consentimento {#merge-policies}

Depois de criar um conjunto de dados [!DNL Profile]habilitado para coletar dados de consentimento, verifique se as políticas de mesclagem foram configuradas para sempre incluir campos de consentimento IAB nos perfis do cliente. Isso envolve configurar a precedência do conjunto de dados para que seu conjunto de dados de consentimento seja priorizado em relação a outros conjuntos de dados potencialmente conflitantes.

Para obter mais informações sobre como trabalhar com políticas de mesclagem, consulte o guia [do usuário das políticas de](../../../profile/ui/merge-policies.md)mesclagem. Ao configurar suas políticas de mesclagem, você deve garantir que seus segmentos incluam todos os atributos de consentimento necessários fornecidos pela mixina [de privacidade do](./dataset-preparation.md#privacy-mixin)XDM, conforme descrito no guia sobre a preparação do conjunto de dados.

## Integrar o SDK da [!DNL Experience Platform] Web para coletar dados de consentimento do cliente {#sdk}

>[!NOTE]
>
>O uso do SDK da [!DNL Experience Platform] Web é necessário para processar dados de consentimento diretamente no Adobe Experience Platform. [!DNL Experience Cloud Identity Service] não é suportado no momento.
>
>[!DNL Experience Cloud Identity Service] no entanto, ainda há suporte para o processamento de consentimento no Adobe Audience Manager, e a conformidade com o TCF 2.0 exige apenas que a biblioteca seja atualizada para a [versão 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Depois de configurar seu CMP para gerar strings de consentimento, você deve integrar o SDK da [!DNL Experience Platform] Web para coletar essas strings e enviá-las para [!DNL Platform]. O [!DNL Platform] SDK fornece dois comandos que podem ser usados para enviar dados de consentimento IAB para a Plataforma (explicado nas subseções abaixo), e devem ser usados quando um cliente fornece informações de consentimento pela primeira vez e a qualquer momento que o consentimento for alterado posteriormente.

**O SDK não faz interface com nenhum CMP pronto para usar**. Cabe a você determinar como integrar o SDK ao seu site, acompanhar as mudanças de consentimento no CMP e chamar o comando apropriado.

### Criar uma nova configuração de borda

Para que o SDK envie dados para [!DNL Experience Platform], é necessário primeiro criar uma nova configuração de borda para [!DNL Platform] o [!DNL Adobe Experience Platform Launch]. Etapas específicas para criar uma nova configuração são fornecidas na documentação [do](../../../edge/fundamentals/edge-configuration.md)SDK.

Depois de fornecer um nome exclusivo para a configuração, selecione o botão de alternância ao lado do **[!UICONTROL Adobe Experience Platform]**. Em seguida, use os seguintes valores para preencher o restante do formulário:

| Campo de configuração do Edge | Valor |
| --- | --- |
| [!UICONTROL Sandbox] | O nome da [!DNL Platform] caixa de proteção [](../../../sandboxes/home.md) que contém a conexão de streaming e os conjuntos de dados necessários para configurar a configuração de borda. |
| [!UICONTROL Entrada de fluxo] | Uma conexão de streaming válida para [!DNL Experience Platform]. Consulte o tutorial sobre como [criar uma conexão](../../../ingestion/tutorials/create-streaming-connection-ui.md) de streaming se você não tiver uma entrada de streaming existente. |
| [!UICONTROL Conjunto de dados do evento] | Selecione o [!DNL XDM ExperienceEvent] conjunto de dados criado na etapa [](#datasets)anterior. |
| [!UICONTROL Conjunto de dados do perfil] | Selecione o [!DNL XDM Individual Profile] conjunto de dados criado na etapa [](#datasets)anterior. |

![](../assets/iab/edge-config.png)

Quando terminar, clique em **[!UICONTROL Salvar]** na parte inferior da tela e continue seguindo os prompts adicionais para concluir a configuração.

### Como fazer comandos de alteração de consentimento

Depois de criar a configuração de borda descrita na seção anterior, você pode fazer start usando comandos do SDK para enviar dados de consentimento [!DNL Platform]. As seções abaixo fornecem exemplos de como cada comando do SDK pode ser usado em diferentes cenários.

>[!NOTE]
>
>Para obter uma introdução à sintaxe comum para todos os comandos [!DNL Platform] do SDK, consulte o documento sobre como [executar comandos](../../../edge/fundamentals/executing-commands.md).

#### Uso de ganchos de alteração de consentimento do CMP

Muitos CMPs fornecem ganchos prontos para uso que escutam eventos de mudança de consentimento. Quando esses eventos ocorrem, você pode usar o `setConsent` comando para atualizar os dados de consentimento do cliente.

O `setConsent` comando espera dois argumentos: (1) uma string que indica o tipo de comando (neste caso, &quot;setConsent&quot;) e (2) uma carga que contém uma `consent` matriz, que deve conter pelo menos um objeto que fornece os campos de consentimento necessários, conforme mostrado abaixo:

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
| `standard` | O padrão de consentimento sendo usado. Esse valor deve ser definido como &quot;IAB&quot; para processamento de consentimento TCF 2.0. |
| `version` | O número da versão da norma de consentimento indicada em `standard`. Esse valor deve ser definido como &quot;2.0&quot; para o processamento de consentimento TCF 2.0. |
| `value` | A string de consentimento codificada em base 64 gerada pelo CMP. |
| `gdprApplies` | Um valor booliano que indica se o RGPD se aplica ao cliente conectado no momento. Para que o TCF 2.0 seja aplicado a este cliente, o valor deve ser definido como &quot;true&quot;. |

O `setConsent` comando deve ser usado como parte de um gancho CMP que detecta alterações nas configurações de consentimento. O JavaScript a seguir fornece um exemplo de como o `setConsent` comando pode ser usado para o `OnConsentChanged` gancho do OneTrust:

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

Você também pode coletar dados de consentimento do TCF 2.0 em cada evento acionado [!DNL Platform] usando o `sendEvent` comando.

>[!NOTE]
>
>Para usar esse método, você deve ter adicionado o [!DNL Experience Event Privacy mixin] ao seu [!DNL Profile]schema [!DNL XDM ExperienceEvent] habilitado. Consulte a seção sobre como [atualizar o schema](./dataset-preparation.md#event-schema) ExperienceEvent no guia de preparação do conjunto de dados para obter etapas sobre como configurar isso.

O `sendEvent` comando deve ser usado como um retorno de chamada em ouvintes de evento apropriados em seu site. O comando espera dois argumentos: (1) uma string que indica o tipo de comando (neste caso, &quot;sendEvent&quot;) e (2) uma carga que contém um `xdm` objeto que fornece os campos de consentimento necessários como JSON:

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
| `consentStandard` | O padrão de consentimento sendo usado. Esse valor deve ser definido como &quot;IAB&quot; para processamento de consentimento TCF 2.0. |
| `consentStandardVersion` | O número da versão da norma de consentimento indicada em `standard`. Esse valor deve ser definido como &quot;2.0&quot; para o processamento de consentimento TCF 2.0. |
| `consentStringValue` | A string de consentimento codificada em base 64 gerada pelo CMP. |
| `gdprApplies` | Um valor booliano que indica se o RGPD se aplica ao cliente conectado no momento. Para que o TCF 2.0 seja aplicado a este cliente, o valor deve ser definido como &quot;true&quot;. |

### Tratamento de respostas do SDK

Todos os [!DNL Platform SDK] comandos retornam promessas que indicam se a chamada foi bem-sucedida ou falhou. Você pode usar essas respostas para uma lógica adicional, como a exibição de mensagens de confirmação para o cliente. Consulte a seção sobre como [lidar com o sucesso ou a falha](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) no guia sobre a execução de comandos do SDK para obter exemplos específicos.

## Exportar segmentos {#export}

>[!NOTE]
>
>Antes de start na exportação de segmentos, verifique se os segmentos incluem todos os campos de consentimento necessários. Consulte a seção sobre como [configurar políticas](#merge-policies) de mesclagem para obter mais informações.

Depois de coletar os dados de consentimento do cliente e criar segmentos de audiência contendo os atributos de consentimento necessários, você poderá aplicar a conformidade do TCF 2.0 ao exportar esses segmentos para destinos downstream.

Desde que a configuração de consentimento `gdprApplies` esteja definida como `true` para um conjunto de perfis do cliente, todos os dados desses perfis exportados para destinos a jusante serão filtrados com base nas preferências de consentimento para cada perfil. Qualquer perfil que não atender às preferências de consentimento necessário será ignorado durante o processo de exportação.

Os clientes devem consentir nos seguintes fins (conforme descrito pelas políticas [do](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)TCF 2.0) para que seus perfis sejam incluídos nos segmentos exportados para destinos:

* **Finalidade 1**: Armazenar e/ou acessar informações em um dispositivo
* **Finalidade 10**: Desenvolver e melhorar produtos

O TCF 2.0 também exige que a fonte de dados verifique a permissão do fornecedor de destino antes de enviar dados para esse destino. Dessa forma, [!DNL Real-time CDP] verifica se a permissão do fornecedor de destino está opt in para todas as IDs no cluster antes de incluir os dados vinculados a esse destino.

>[!NOTE]
>
>Todos os segmentos compartilhados com a Adobe Audience Manager conterão os mesmos valores de consentimento do TCF 2.0 que seus [!DNL Platform] homólogos. Como [!DNL Audience Manager] compartilha a mesma ID de fornecedor [!DNL Real-time CDP] (565), os mesmos objetivos e a mesma permissão de fornecedor são necessários. Consulte o documento no plug-in do [Adobe Audience Manager para IAB TCF](https://docs.adobe.com/help/pt-BR/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) para obter mais informações.

## Test your implementation {#test-implementation}

Após configurar sua implementação do TCF 2.0 e ter exportado segmentos para destinos, todos os dados que não atenderem aos requisitos de consentimento não serão exportados. No entanto, para verificar se os perfis certos do cliente foram filtrados durante a exportação, verifique manualmente os armazenamentos de dados em seus destinos para ver se o consentimento foi aplicado corretamente.

É importante observar que se várias IDs formarem um cluster e o TCF 2.0 for aplicado, todo o cluster será excluído se mesmo uma única ID não contiver os objetivos corretos e as permissões do fornecedor.

## Próximas etapas

Este documento cobriu o processo de configuração das operações de dados para [!DNL Real-time CDP] ser compatível com o TCF 2.0. Para obter mais informações sobre os outros recursos de privacidade fornecidos por [!DNL Real-time CDP], consulte a seguinte documentação:

* [Privacidade na CDP em tempo real](../privacy-overview.md)
* [Controle de dados em CDP em tempo real](../data-governance-overview.md)