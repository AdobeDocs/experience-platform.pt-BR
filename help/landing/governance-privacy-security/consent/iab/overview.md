---
keywords: Experience Platform, home, IAB, IAB 2.0, consentimento, Consentimento
solution: Experience Platform
title: Suporte ao IAB TCF 2.0 na Experience Platform
topic: privacy events
description: Saiba como configurar operações de dados e esquemas para transmitir opções de consentimento do cliente ao ativar segmentos para destinos na Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: a845ade0fc1e6e18c36b5f837fe7673a976f01c7
workflow-type: tm+mt
source-wordcount: '2472'
ht-degree: 0%

---


# Suporte ao IAB TCF 2.0 na Experience Platform

O [!DNL Transparency & Consent Framework] (TCF), conforme descrito pelo [!DNL Interactive Advertising Bureau] (IAB), é uma estrutura técnica de padrão aberto destinada a permitir que as organizações obtenham, registrem e atualizem o consentimento do consumidor para o processamento de seus dados pessoais, em conformidade com o [!DNL General Data Protection Regulation] (GDPR) da União Europeia. A segunda iteração da estrutura, TCF 2.0, concede mais flexibilidade para como os consumidores podem fornecer ou reter consentimento, incluindo se e como os fornecedores podem usar determinados recursos de processamento de dados, como a geolocalização precisa.

>[!NOTE]
>
>Mais informações sobre o TCF 2.0 podem ser encontradas no [site IAB Europe](https://iabeurope.eu/tcf-2-0/), incluindo materiais de suporte e especificações técnicas.

A Adobe Experience Platform faz parte da lista de fornecedores do IAB TCF 2.0 registrada](https://iabeurope.eu/vendor-list-tcf-v2-0/), na ID **565**. [ Em conformidade com os requisitos do TCF 2.0, o Platform permite coletar dados de consentimento do cliente e integrá-los aos perfis de clientes armazenados. Esses dados de consentimento podem ser fatorado para determinar se os perfis estão incluídos em segmentos de público-alvo exportados, dependendo do caso de uso.

>[!IMPORTANT]
>
>A Platform só pode estar em conformidade com a versão 2.0 do TCF (ou posterior). As versões anteriores da TCF não são compatíveis.

Este documento fornece uma visão geral de como configurar as operações de dados e os esquemas de perfil para aceitar os dados de consentimento do cliente gerados pelo CMP e como a Platform transmite as opções de consentimento do usuário ao exportar segmentos.

## Pré-requisitos

Para seguir este guia, você deve usar uma Plataforma de gerenciamento de consentimento (CMP), comercial ou própria, integrada e compatível com a TCF do IAB. Consulte a [lista de CMPs compatíveis](https://iabeurope.eu/cmp-list/) para obter mais informações.

>[!IMPORTANT]
>
>Se a ID do CMP for inválida, a Platform continuará processando os dados como estão. Para aplicar o TCF 2.0, você deve confirmar que o CMP tem uma ID válida que foi registrada no IAB TCF 2.0 antes de enviar dados ao Platform.

Este guia também requer uma compreensão funcional dos seguintes serviços da plataforma:

* [Modelo de dados de experiência (XDM)](../../../../xdm/home.md): A estrutura padronizada pela qual a Experience Platform organiza os dados de experiência do cliente.
* [Serviço de identidade da Adobe Experience Platform](../../../../identity-service/home.md): Resolve o desafio fundamental colocado pela fragmentação dos dados de experiência do cliente ao unir identidades entre dispositivos e sistemas.
* [Perfil](../../../../profile/home.md) do cliente em tempo real: Aproveitamento  [!DNL Identity Service] para criar perfis detalhados do cliente a partir de seus conjuntos de dados em tempo real. [!DNL Real-time Customer Profile] extrai dados do Data Lake e mantém perfis de clientes em seu próprio armazenamento de dados separado.
* [SDK](../../../../edge/home.md) da Web da Adobe Experience Platform: Uma biblioteca JavaScript do lado do cliente que permite integrar vários serviços da plataforma ao seu site voltado para o cliente.
   * [Comandos](../../../../edge/consent/supporting-consent.md) de consentimento do SDK: Uma visão geral do caso de uso dos comandos SDK relacionados ao consentimento mostrados neste guia.
* [Serviço de segmentação da Adobe Experience Platform](../../../../segmentation/home.md): Permite dividir  [!DNL Real-time Customer Profile] dados em grupos de indivíduos que compartilham características semelhantes e responderão de forma semelhante às estratégias de marketing.

Além dos serviços da plataforma listados acima, você também deve estar familiarizado com [destinos](../../../../data-governance/home.md) e sua função no ecossistema da plataforma.

## Resumo do fluxo de consentimento do cliente {#summary}

As seções a seguir descrevem como os dados de consentimento são coletados e aplicados depois que o sistema é configurado corretamente.

### Coleta de dados de consentimento

A Platform permite coletar dados de consentimento do cliente por meio do seguinte processo:

1. Um cliente fornece suas preferências de consentimento para a coleta de dados por meio de uma caixa de diálogo no site.
1. O CMP detecta a alteração da preferência de consentimento e gera os dados de consentimento do TCF de acordo.
1. Usando o SDK da Web da plataforma, os dados de consentimento gerados (retornados pela CMP) são enviados para a Adobe Experience Platform.
1. Os dados de consentimento coletados são assimilados em um conjunto de dados habilitado para [!DNL Profile] cujo esquema contém campos de consentimento TCF.

Além dos comandos do SDK acionados por ganchos de alteração de consentimento da CMP, os dados de consentimento também podem fluir para a Experience Platform por meio de quaisquer dados XDM gerados pelo cliente que sejam carregados diretamente para um conjunto de dados habilitado para [!DNL Profile].

Qualquer segmento compartilhado com a Platform pelo Adobe Audience Manager (por meio do [!DNL Audience Manager] conector de origem ou de outro modo) também pode conter dados de consentimento, desde que os campos apropriados tenham sido aplicados a esses segmentos por meio de [!DNL Experience Cloud Identity Service]. Para obter mais informações sobre como coletar dados de consentimento em [!DNL Audience Manager], consulte o documento no [plug-in do Adobe Audience Manager para TCF do IAB](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

### Execução de consentimento a jusante

Depois que os dados de consentimento da TCF forem assimilados com êxito, os seguintes processos ocorrerão nos serviços downstream da plataforma:

1. [!DNL Real-time Customer Profile] atualiza os dados de consentimento armazenados para o perfil do cliente.
1. A Platform processa as IDs do cliente somente se a permissão do fornecedor para a Plataforma (565) for fornecida para cada ID em um cluster.
1. Ao exportar segmentos para destinos pertencentes aos membros da lista de fornecedores TCF 2.0, a Platform inclui apenas perfis se as permissões do fornecedor para a Plataforma (565) *e* o destino individual for fornecido para cada ID em um cluster.

O restante das seções neste documento fornecem orientação sobre como configurar a Platform e suas operações de dados para atender aos requisitos de coleta e aplicação descritos acima.

## Determine como gerar dados de consentimento do cliente em seu CMP {#consent-data}

Como cada sistema CMP é exclusivo, você deve determinar a melhor maneira de permitir que seus clientes forneçam consentimento à medida que interagirem com seu serviço. Uma maneira comum de fazer isso é usando uma caixa de diálogo de consentimento de cookie, semelhante ao seguinte exemplo:

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

Essa caixa de diálogo deve permitir que o cliente aceite ou saia do seguinte:

| Opção de consentimento | Descrição |
| --- | --- |
| **Finalidades** | Finalidades definem para quais finalidades de tecnologia de anúncios uma marca pode usar os dados de um cliente. As seguintes finalidades devem ser aceitas para que a Platform processe as IDs do cliente: <ul><li>**Finalidade 1**: Armazenar e/ou acessar informações em um dispositivo</li><li>**Finalidade 10**: Desenvolver e melhorar produtos</li></ul> |
| **Permissões do fornecedor** | Além de fins de tecnologia de anúncios, a caixa de diálogo também deve permitir que o cliente opte por aceitar ou não a utilização de seus dados por fornecedores específicos, incluindo a Adobe Experience Platform (565). |

### Sequências de consentimento {#consent-strings}

Independentemente do método usado para coletar os dados, o objetivo é gerar um valor de string com base nas opções de consentimento escolhidas pelo cliente, chamadas de string de consentimento.

Na especificação da TCF, as cadeias de consentimento são usadas para codificar detalhes relevantes sobre as configurações de consentimento de um cliente, em termos de finalidades de marketing específicas, conforme definido por políticas e fornecedores. A Platform usa essas cadeias de caracteres para armazenar as configurações de consentimento para cada cliente e, portanto, uma nova cadeia de consentimento deve ser gerada sempre que essas configurações forem alteradas.

As cadeias de caracteres de consentimento só podem ser criadas por uma CMP registrada junto à TCF do IAB. Para obter mais informações sobre como gerar cadeias de consentimento usando seu CMP específico, consulte o [guia de formatação da cadeia de consentimento](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) no repositório GitHub da TCF do IAB .

## Criar conjuntos de dados com campos de consentimento da TCF {#datasets}

Os dados de consentimento do cliente devem ser enviados para conjuntos de dados cujos esquemas contêm campos de consentimento da TCF. Consulte o tutorial em [criar conjuntos de dados para capturar o consentimento do TCF 2.0](./dataset.md) para saber como criar os dois conjuntos de dados necessários antes de continuar com este guia.

## Atualize [!DNL Profile] as políticas de mesclagem para incluir dados de consentimento {#merge-policies}

Depois de criar um conjunto de dados habilitado para [!DNL Profile] para coletar dados de consentimento, você deve garantir que suas políticas de mesclagem tenham sido configuradas para sempre incluir campos de consentimento TCF nos perfis do cliente. Isso envolve definir a precedência do conjunto de dados para que seu conjunto de dados de consentimento seja priorizado em relação a outros conjuntos de dados potencialmente conflitantes.

Para obter mais informações sobre como trabalhar com políticas de mesclagem, consulte o [guia do usuário de políticas de mesclagem](../../../../profile/ui/merge-policies.md). Ao configurar suas políticas de mesclagem, você deve garantir que seus segmentos incluam todos os atributos de consentimento necessários fornecidos pelo [XDM privacy mixin](./dataset.md#privacy-mixin), conforme descrito no guia sobre a preparação do conjunto de dados.

## Integre o SDK da Web da Experience Platform para coletar dados de consentimento do cliente {#sdk}

>[!NOTE]
>
>O uso do SDK da Web da Experience Platform é necessário para processar dados de consentimento diretamente na Adobe Experience Platform. [!DNL Experience Cloud Identity Service] no momento não é compatível.
>
>[!DNL Experience Cloud Identity Service] O ainda é compatível com o processamento de consentimento no Adobe Audience Manager, no entanto, e a conformidade com o TCF 2.0 exige apenas que a biblioteca seja atualizada para a  [versão 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Depois de configurar o CMP para gerar cadeias de consentimento, você deve integrar o SDK da Web da Experience Platform para coletar essas cadeias de caracteres e enviá-las para a Platform. O SDK da plataforma fornece dois comandos que podem ser usados para enviar dados de consentimento da TCF para a Plataforma (explicados nas subseções abaixo) e devem ser usados quando um cliente fornecer informações de consentimento pela primeira vez e a qualquer momento em que o consentimento for alterado posteriormente.

**O SDK não faz interface com nenhum CMPs pronto para uso**. Cabe a você determinar como integrar o SDK ao seu site, acompanhar as alterações de consentimento no CMP e chamar o comando apropriado.

### Criar uma nova configuração de borda

Para que o SDK envie dados para a Experience Platform, primeiro você deve criar uma nova configuração de borda para a Platform em [!DNL Adobe Experience Platform Launch]. Etapas específicas para criar uma nova configuração são fornecidas na [documentação do SDK](../../../../edge/fundamentals/edge-configuration.md).

Depois de fornecer um nome exclusivo para a configuração, selecione o botão de alternância ao lado de **[!UICONTROL Adobe Experience Platform]**. Em seguida, use os seguintes valores para preencher o restante do formulário:

| Campo de configuração da borda | Valor |
| --- | --- |
| [!UICONTROL Sandbox] | O nome da plataforma [sandbox](../../../../sandboxes/home.md) que contém a conexão de transmissão e os conjuntos de dados necessários para configurar a configuração de borda. |
| [!UICONTROL Entrada de transmissão] | Uma conexão de transmissão válida para a Experience Platform. Consulte o tutorial em [criar uma conexão de transmissão](../../../../ingestion/tutorials/create-streaming-connection-ui.md) se você não tiver uma entrada de transmissão existente. |
| [!UICONTROL Conjunto de dados do evento] | Selecione o conjunto de dados [!DNL XDM ExperienceEvent] criado na [etapa anterior](#datasets). |
| [!UICONTROL Conjunto de dados de perfil] | Selecione o conjunto de dados [!DNL XDM Individual Profile] criado na [etapa anterior](#datasets). |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Quando terminar, selecione **[!UICONTROL Save]** na parte inferior da tela e continue a seguir quaisquer prompts adicionais para concluir a configuração.

### Comandos de alteração de consentimento

Depois de criar a configuração de borda descrita na seção anterior, você pode começar a usar comandos do SDK para enviar dados de consentimento para a Platform. As seções abaixo fornecem exemplos de como cada comando do SDK pode ser usado em diferentes cenários.

>[!NOTE]
>
>Para obter uma introdução à sintaxe comum para todos os comandos do SDK da plataforma, consulte o documento em [executar comandos](../../../../edge/fundamentals/executing-commands.md).

#### Uso de ganchos de alteração de consentimento da CMP

Muitas CMPs fornecem ganchos prontos para uso que ouvem eventos de alteração de consentimento. Quando esses eventos ocorrem, você pode usar o comando `setConsent` para atualizar os dados de consentimento desse cliente.

O comando `setConsent` espera dois argumentos: (1) uma string que indica o tipo de comando (neste caso, &quot;setConsent&quot;) e (2) uma carga útil que contém uma matriz `consent`, que deve conter pelo menos um objeto que forneça os campos de consentimento necessários, conforme mostrado abaixo:

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

| Propriedade da carga útil | Descrição |
| --- | --- |
| `standard` | O padrão de consentimento que está sendo usado. Esse valor deve ser definido como `IAB` para processamento de consentimento TCF 2.0. |
| `version` | O número da versão do padrão de consentimento indicado em `standard`. Esse valor deve ser definido como `2.0` para processamento de consentimento TCF 2.0. |
| `value` | A cadeia de consentimento codificado em base 64 gerada pelo CMP. |
| `gdprApplies` | Um valor booleano que indica se o GDPR se aplica ao cliente conectado no momento. Para que o TCF 2.0 seja aplicado a este cliente, o valor deve ser definido como `true`. O padrão é `true` se não estiver definido. |

O comando `setConsent` deve ser usado como parte de um gancho de CMP que detecta alterações nas configurações de consentimento. O JavaScript a seguir fornece um exemplo de como o comando `setConsent` pode ser usado para o gancho `OnConsentChanged` do OneTrust:

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

Você também pode coletar dados de consentimento do TCF 2.0 em cada evento acionado na plataforma usando o comando `sendEvent`.

>[!NOTE]
>
>Para usar esse método, você deve ter adicionado o [!DNL Experience Event Privacy mixin] ao esquema [!DNL Profile] habilitado para [!DNL XDM ExperienceEvent]. Consulte a seção sobre [atualização do esquema ExperienceEvent](./dataset.md#event-schema) no guia de preparação do conjunto de dados para obter etapas sobre como configurar isso.

O comando `sendEvent` deve ser usado como um retorno de chamada em ouvintes de eventos apropriados em seu site. O comando espera dois argumentos: (1) uma string que indica o tipo de comando (neste caso, `sendEvent`) e (2) uma carga contendo um objeto `xdm` que fornece os campos de consentimento necessários como JSON:

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

| Propriedade da carga útil | Descrição |
| --- | --- |
| `xdm.consentStrings` | Uma matriz que deve conter pelo menos um objeto que forneça os campos de consentimento necessários. |
| `consentStandard` | O padrão de consentimento que está sendo usado. Esse valor deve ser definido como `IAB` para processamento de consentimento TCF 2.0. |
| `consentStandardVersion` | O número da versão do padrão de consentimento indicado em `standard`. Esse valor deve ser definido como `2.0` para processamento de consentimento TCF 2.0. |
| `consentStringValue` | A cadeia de consentimento codificado em base 64 gerada pelo CMP. |
| `gdprApplies` | Um valor booleano que indica se o GDPR se aplica ao cliente conectado no momento. Para que o TCF 2.0 seja aplicado a este cliente, o valor deve ser definido como `true`. O padrão é `true` se não estiver definido. |

### Tratamento de respostas do SDK

Todos os comandos [!DNL Platform SDK] retornam promessas que indicam se a chamada foi bem-sucedida ou falhou. Em seguida, você pode usar essas respostas para obter uma lógica adicional, como exibir mensagens de confirmação para o cliente. Consulte a seção [manuseando o sucesso ou a falha](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) no guia sobre a execução de comandos do SDK para obter exemplos específicos.

## Exportar segmentos {#export}

>[!NOTE]
>
>Antes de começar a exportar segmentos, você deve garantir que seus segmentos incluam todos os campos de consentimento necessários. Consulte a seção [configurando políticas de mesclagem](#merge-policies) para obter mais informações.

Depois de coletar os dados de consentimento do cliente e criar segmentos de público-alvo contendo os atributos de consentimento necessários, você pode impor a conformidade com o TCF 2.0 ao exportar esses segmentos para destinos downstream.

Desde que a configuração de consentimento `gdprApplies` esteja definida como `true` para um conjunto de perfis de cliente, todos os dados desses perfis exportados para destinos downstream serão filtrados com base nas preferências de consentimento da TCF para cada perfil. Qualquer perfil que não atende às preferências de consentimento necessárias é ignorado durante o processo de exportação.

Os clientes devem consentir com as seguintes finalidades (conforme descrito por [Políticas TCF 2.0](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) para que seus perfis sejam incluídos em segmentos que são exportados para destinos:

* **Finalidade 1**: Armazenar e/ou acessar informações em um dispositivo
* **Finalidade 10**: Desenvolver e melhorar produtos

O TCF 2.0 também exige que a fonte de dados verifique a permissão de fornecedor do destino antes de enviar dados para esse destino. Dessa forma, a Platform verifica se a permissão do fornecedor do destino foi aceita para todas as IDs no cluster antes de incluir dados vinculados a esse destino.

>[!NOTE]
>
>Qualquer segmento compartilhado com o Adobe Audience Manager conterá os mesmos valores de consentimento da TCF 2.0 que seus equivalentes da plataforma. Como [!DNL Audience Manager] compartilha a mesma ID de fornecedor que a Plataforma (565), as mesmas finalidades e permissões de fornecedor são necessárias. Consulte o documento no plug-in do Adobe Audience Manager para IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) para obter mais informações.[

## Teste sua implementação {#test-implementation}

Depois de configurar a implementação do TCF 2.0 e exportar segmentos para destinos, os dados que não atenderem aos requisitos de consentimento não serão exportados. No entanto, para ver se os perfis do cliente certos foram filtrados durante a exportação, você deve verificar manualmente os armazenamentos de dados em seus destinos para ver se o consentimento foi empregado corretamente.

É importante observar que, se várias IDs formarem um cluster e o TCF 2.0 se aplicar, todo o cluster será excluído se mesmo uma única ID não contiver os objetivos corretos e as permissões do fornecedor.

## Próximas etapas

Este documento cobriu o processo de configuração das operações de dados da plataforma para atender às suas obrigações comerciais, conforme descrito pelo TCF 2.0. Consulte a visão geral sobre [governança, privacidade e segurança](../../overview.md) para obter mais informações sobre os recursos relacionados à privacidade da plataforma.