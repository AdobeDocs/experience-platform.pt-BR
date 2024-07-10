---
title: Conexão SAP Commerce
description: Use o conector de destino do SAP Commerce para atualizar os registros do cliente em sua conta SAP.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 3bd1a2a7-fb56-472d-b9bd-603b94a8937e
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '2246'
ht-degree: 3%

---

# [!DNL SAP Commerce] conexão

[!DNL SAP Commerce], anteriormente conhecido como [[!DNL Hybris]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html)O, é uma solução de plataforma de comércio eletrônico baseada em nuvem para empresas B2B e B2C e está disponível como parte do portfólio SAP Customer Experience. [[!DNL SAP] Cobrança da assinatura](https://www.sap.com/products/financial-management/subscription-billing.html) O é um produto do portfólio e permite o gerenciamento completo do ciclo de vida da assinatura com vendas simplificadas e experiências de pagamento por meio de integrações padronizadas.

Este [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) usa o [[!DNL SAP Subscription Billing] API de gerenciamento de clientes](https://api.sap.com/api/BusinessPartner_APIs/path/PUT_customers-customerNumber), para atualizar os detalhes do cliente no [!DNL SAP Commerce] de um público-alvo Experience Platform existente após a ativação.

Instruções para autenticar em seu [!DNL SAP Commerce] exemplo, são apresentados mais abaixo, no [Autenticar para destino](#authenticate) seção.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o [!DNL SAP Commerce] destino, este é um exemplo de caso de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

[!DNL SAP Commerce] Os clientes do armazenam informações sobre indivíduos ou entidades organizacionais que interagem com sua empresa. Sua equipe usa os clientes existentes no [!DNL SAP Commerce] para criar os públicos-alvo do Experience Platform. Depois de enviar esses públicos-alvo para o [!DNL SAP Commerce], as informações são atualizadas e cada cliente recebe uma propriedade com o respectivo valor como o nome do público-alvo que indica a qual público-alvo o cliente pertence.

## Pré-requisitos {#prerequisites}

Consulte as seções abaixo para obter os pré-requisitos que você deve configurar no Experience Platform e [!DNL SAP Commerce] e para informações que você deve coletar antes de trabalhar com a [!DNL SAP Commerce] destino.

### Pré-requisitos do Experience Platform {#prerequisites-in-experience-platform}

Antes de ativar os dados para o [!DNL SAP Commerce] destino, você deve ter um [schema](/help/xdm/schema/composition.md), um [conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html), e [públicos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) criado em [!DNL Experience Platform].

Consulte a documentação do Experience Platform para [Grupo de campos de esquema Detalhes da associação do público](/help/xdm/field-groups/profile/segmentation.md) se precisar de orientação sobre os status do público-alvo.

### Pré-requisitos para a [!DNL SAP Commerce] destino {#prerequisites-destination}

Observe os seguintes pré-requisitos para exportar dados da Platform para o seu [!DNL SAP Commerce] conta:

#### Você deve ter um [!DNL SAP Subscription Billing] account {#prerequisites-account}

Para exportar dados da Platform para o seu [!DNL SAP Commerce] conta, é necessário ter uma [!DNL SAP Subscription Billing] conta. Se você não tiver uma conta de faturamento válida, entre em contato com [!DNL SAP] gerente de conta. Consulte a [[!DNL SAP] Configuração da plataforma](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) para obter detalhes adicionais.

#### Gerar uma chave de serviço {#prerequisites-service-key}

* A variável [!DNL SAP Commerce] a chave de serviço permite acessar a variável [!DNL SAP Subscription Billing] API por meio do Experience Platform. Consulte a [!DNL SAP Commerce] [criar uma Chave de serviço com a ID do cliente e o Segredo do cliente](https://help.sap.com/docs/CLOUD_TO_CASH_OD/1216e7b79c984675b0a6f0005e351c74/87c11a0f5dc3494eaf3baa355925c030.html#create-a-service-key-with-client-id-and-client-secret) para criar uma chave de serviço. O [!DNL SAP Commerce] exige o seguinte:
   * ID de cliente
   * Segredo do cliente
   * URL. O padrão de URL é o seguinte: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Esse valor será usado posteriormente para obter valores para `Region` e `Endpoint`.

+++Selecione para ver um exemplo da chave de serviço

```json
{ 
    "url": "https://eu10.revenue.cloud.sap/api",
    "uaa": {
        "clientid": "XXX",
        "clientsecret": "XXX",
        "url": "https://subscriptionbilling.authentication.eu10.hana.ondemand.com",
        "identityzone": "subscriptionbilling",
        "identityzoneid": "XXX",
        "tenantid": "XXX",
        "tenantmode": "dedicated",
        "sburl": "https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
        "apiurl": "https://api.authentication.eu10.hana.ondemand.com",
        "verificationkey": "XXX",
        "xsappname": "XXX",
        "subaccountid": "XXX",
        "uaadomain": "authentication.eu10.hana.ondemand.com",
        "zoneid": "XXX",
        "credential-type": "binding-secret"
    },
    "vendor": "SAP"
}
```

+++

#### Criar referências personalizadas no [!DNL SAP Subscription Billing] {#prerequisites-custom-reference}

Para atualizar o status do público-alvo do Experience Platform no [!DNL SAP Subscription Billing], é necessário um campo de referência personalizado para cada público selecionado na Platform.

Para criar as referências personalizadas, faça logon no [!DNL SAP Subscription Billing] e navegue até a página **[Configuração e dados mestres]** > **[Referências personalizadas]** página. Em seguida, selecione **[!UICONTROL Criar]** para adicionar uma nova referência para cada público selecionado na Platform. Esses nomes de campos de referência serão necessários nos próximos [Agendar exportação de público e exemplo](#schedule-segment-export-example) etapa.

Um exemplo de como criar um personalizado **[!UICONTROL Tipo de referência]** no prazo de [!DNL SAP Subscription Billing] é mostrado abaixo:
![Imagem que mostra onde criar uma referência personalizada no Faturamento de assinatura SAP.](../../assets/catalog/ecommerce/sap-commerce/create-custom-reference.png)

Para obter orientação adicional, consulte o [!DNL SAP Subscription Billing] [referências personalizadas](https://help.sap.com/docs/CLOUD_TO_CASH_OD/80d121f216af43648e79664efe5595f7/85696a63c8d8453a934e86c9413a25cf.html?version=2023-11-27) documentação.

### Coletar credenciais necessárias {#gather-credentials}

Para conectar [!DNL SAP Commerce] para Experience Platform, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| ID de cliente | O valor de `clientId` da chave de serviço. |
| Segredo do cliente | O valor de `clientSecret` da chave de serviço. |
| Endpoint | O valor de `url` na chave de serviço, é semelhante a `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| Região | O local do data center. A região está presente no `url` e tem um valor semelhante a `eu10` ou `us10`. Por exemplo, se a variável `url` é `https://eu10.revenue.cloud.sap/api` você precisa `eu10`. |

## Medidas de proteção {#guardrails}

Solicitações de API para o [!DNL SAP Cloud Management service] estão sujeitos a [Limites de taxa](https://help.sap.com/docs/btp/sap-business-technology-platform/account-administration-rate-limiting). Quando o limite de taxa for excedido, você encontrará uma `HTTP 429 Too Many Requests` código do status da resposta .

## Identidades suportadas {#supported-identities}

[!DNL SAP Commerce] O oferece suporte à atualização de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidade de destino | Descrição | Considerações |
| --- | --- | --- |
| `customerNumberSAP` | Um identificador do cliente individual ou corporativo já presente em seu [!DNL SAP Commerce] conta. | Obrigatório |

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve todos os públicos-alvo que você pode exportar para esse destino.

Esse destino suporta a ativação de todos os públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md).

Esse destino também suporta a ativação dos públicos-alvo descritos na tabela abaixo.

| Tipo de público | Suportado | Descrição |
| ------------- | --------- | ----------- |
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo Experience Platform [Serviço de segmentação](../../../segmentation/home.md). |
| Uploads personalizados | ✓ | Públicos-alvo [importado](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | <ul><li>Você está exportando todos os membros de um público-alvo, juntamente com os campos de esquema desejados *(por exemplo: endereço de email, número de telefone, sobrenome)*, de acordo com o mapeamento de campo.</li><li> Para cada público selecionado na Platform, a variável correspondente [!DNL SAP Commerce] O atributo adicional é atualizado com o status de público-alvo da Platform.</li></ul> |
| Frequência de exportação | **[!UICONTROL Streaming]** | <ul><li>Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Quando um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

Dentro de **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, pesquisar [!DNL SAP Commerce]. Como alternativa, você pode localizá-lo na **[!UICONTROL comércio eletrônico]** categoria.

### Autenticar para o destino {#authenticate}

Preencha os campos obrigatórios abaixo. Consulte a [Gerar uma chave de serviço](#prerequisites-service-key) para obter orientação.

| Campo | Descrição |
| --- | --- |
| **[!UICONTROL ID do cliente]** | O valor de `clientId` da chave de serviço. |
| **[!UICONTROL Client secret]** | O valor de `clientSecret` da chave de serviço. |
| **[!UICONTROL Endpoint]** | O valor de `url` na chave de serviço, é semelhante a `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| **[!UICONTROL Região]** | O local do data center. A região está presente no `url` e tem um valor semelhante a `eu10` ou `us10`. Por exemplo, se a variável `url` é `https://eu10.revenue.cloud.sap/api` você precisa `eu10`. |

Para autenticar no destino, selecione **[!UICONTROL Conectar ao destino]**.
![Imagem da interface do usuário da Platform mostrando como autenticar no destino.](../../assets/catalog/ecommerce/sap-commerce/authenticate-destination.png)

Se os detalhes fornecidos forem válidos, a interface exibirá uma **[!UICONTROL Conectado]** com uma marca de seleção verde. Você pode prosseguir para a próxima etapa.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.
![Imagem da interface do Platform mostrando os detalhes de destino a serem preenchidos após a autenticação.](../../assets/catalog/ecommerce/sap-commerce/destination-details.png)

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.
* **[!UICONTROL Tipo de cliente]**: selecione ***Indivíduo*** ou ***Corporativo*** dependendo das entidades no seu público-alvo. A variável [!DNL SAP Subscription Billing] [schema](https://api.sap.com/api/BusinessPartner_APIs/schema) alterna os campos obrigatórios dependendo desta seleção, que é mapeada para a variável `customerType` atributo. Se a seleção for ***Corporativo***, em seguida, os mapeamentos obrigatórios como `firstName` e `lastName` necessário para um cliente individual será ignorado e `company` torna-se obrigatório e vice-versa.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar os dados, é necessário **[!UICONTROL Exibir destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}

Ler [Ativar perfis e públicos para destinos de exportação de público de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Mapear atributos e identidades {#map}

Para enviar corretamente os dados do público-alvo do Adobe Experience Platform para a [!DNL SAP Commerce] destino, você deve passar pela etapa de mapeamento de campos. O mapeamento consiste em criar um link entre os campos do esquema do Experience Data Model (XDM) na sua conta da Platform e seus equivalentes correspondentes no destino. Para mapear corretamente os campos XDM para o [!DNL SAP Commerce] campos de destino, siga as etapas abaixo:

#### Mapeie o `customerNumberSAP` identidade

A variável `customerNumberSAP` a identidade é um mapeamento obrigatório para este destino. Siga as etapas abaixo para mapeá-la:
1. No **[!UICONTROL Mapeamento]** etapa, selecione **[!UICONTROL Adicionar novo mapeamento]**. Agora você pode ver uma nova linha de mapeamento na tela.
   ![Captura de tela da interface do usuário da plataforma com o botão adicionar novo mapeamento realçado.](../../assets/catalog/ecommerce/sap-commerce/mapping-add-new-mapping.png)
1. No **[!UICONTROL Selecionar campo de origem]** escolha a **[!UICONTROL Selecionar namespace de identidade]** e selecione `customerNumberSAP`.
   ![Captura de tela da interface do usuário da plataforma selecionando o email como um atributo de origem a ser mapeado como identidade.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-source-identity.png)
1. No **[!UICONTROL Selecionar campo de destino]** escolha a **[!UICONTROL Selecionar namespace de identidade]** e selecione o `customerNumber` identidade.
   ![Captura de tela da interface do usuário da plataforma selecionando o email como um atributo de destino a ser mapeado como identidade.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-target-identity.png)

| Campo de origem | Campo de público alvo | Obrigatório |
| --- | --- | --- |
| `IdentityMap: customerNumberSAP` | `Identity: customerNumber` | Sim |

Um exemplo com o mapeamento de identidade é mostrado abaixo:
![Imagem da interface do usuário da Platform mostrando um exemplo de mapeamento de identidade de customerNumber.](../../assets/catalog/ecommerce/sap-commerce/mapping-identities.png)

#### Mapeamento de atributos

Para adicionar outros atributos que você deseja atualizar entre o esquema de perfil XDM e o [!DNL SAP Subscription Billing] repita as etapas abaixo:
1. No **[!UICONTROL Mapeamento]** etapa, selecione **[!UICONTROL Adicionar novo mapeamento]**. Agora você pode ver uma nova linha de mapeamento na tela.
   ![Captura de tela da interface do usuário da plataforma com o botão adicionar novo mapeamento realçado.](../../assets/catalog/ecommerce/sap-commerce/mapping-add-new-mapping.png)
1. No **[!UICONTROL Selecionar campo de origem]** escolha a **[!UICONTROL Selecionar atributos]** e selecione o atributo XDM.
   ![Captura de tela da interface do usuário da plataforma selecionando o Sobrenome como um atributo de origem.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-source-attribute.png)
1. No **[!UICONTROL Selecionar campo de destino]** escolha **[!UICONTROL Selecionar atributos personalizados]** categoria e digite o nome do [!DNL SAP Subscription Billing] atributo da lista de clientes [schema](https://api.sap.com/api/BusinessPartner_APIs/schema) atributos.
   ![Captura de tela da interface do usuário da plataforma em que lastName é definido como o atributo de destino.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-target-attribute.png)

>[!IMPORTANT]
>
> Os nomes de campos de destino diferenciam maiúsculas de minúsculas e devem corresponder à variável [!DNL SAP Subscription Billing] nomes de atributo. A única exceção para isso é `country` onde você deve usar `countryCode` em vez disso. [!DNL SAP Subscription Billing] suporta códigos de país alfa-2 (ISO 3166). O valor diferencia maiúsculas de minúsculas e deve ter entre 0 e 3 caracteres, portanto, certifique-se de fornecer exatamente como definido caso encontre erros: `The country code {} does not exist` ou `size must be between 0 and 3`.

#### Mapa `mandatory` atributos para o tipo de cliente selecionado

Os mapeamentos de atributos obrigatórios dependem do **[!UICONTROL Tipo de cliente]** que você selecionou. Para mapear os atributos obrigatórios, selecione uma das opções abaixo:

>[!BEGINTABS]

>[!TAB Cliente individual]

| Campo de origem | Campo de público alvo | Obrigatório |
| --- | --- | --- |
| `xdm: person.lastName` | `Attribute: lastName` | Sim |
| `xdm: workAddress.countryCode` | `Attribute: countryCode` | Sim |

>[!TAB Cliente corporativo]

| Campo de origem | Campo de público alvo | Obrigatório |
| --- | --- | --- |
| `xdm: b2b.companyName` | `Attribute: company` | Sim |
| `xdm: workAddress.countryCode` | `Attribute: countryCode` | Sim |

>[!ENDTABS]

#### Mapeamento de atributos adicionais

Em seguida, você pode adicionar mapeamentos adicionais entre o esquema de perfil XDM e a variável [!DNL SAP Subscription Billing] [schema](https://api.sap.com/api/BusinessPartner_APIs/schema) atributos para um cliente, conforme mostrado abaixo:

>[!BEGINTABS]

>[!TAB Cliente individual]

| Campo de origem | Campo de público alvo | Obrigatório |
| --- | --- | --- |
| `xdm: person.name.firstName` | `Attribute: firstName` | Não |
| `xdm: workAddress.street1` | `Attribute: street` | Não |
| `xdm: workAddress.city` | `Attribute: city` | Não |

Um exemplo com mapeamentos de atributos obrigatórios e opcionais, em que o cliente é um indivíduo, é mostrado abaixo:
![Imagem da interface do usuário da Platform mostrando um exemplo com mapeamentos de atributos obrigatórios e opcionais, em que o cliente é um indivíduo.](../../assets/catalog/ecommerce/sap-commerce/mapping-attributes-individual.png)

>[!TAB Cliente corporativo]

| Campo de origem | Campo de público alvo | Obrigatório |
| --- | --- | --- |
| `xdm: workAddress.street1` | `Attribute: street` | Não |
| `xdm: workAddress.city` | `Attribute: city` | Não |

Um exemplo com mapeamentos de atributos obrigatórios e opcionais em que o cliente é uma empresa é mostrado abaixo:
![Imagem da interface do usuário da Platform mostrando um exemplo com mapeamentos de atributos obrigatórios e opcionais, em que o cliente é uma empresa.](../../assets/catalog/ecommerce/sap-commerce/mapping-attributes-corporate.png)

>[!ENDTABS]

Quando terminar de fornecer os mapeamentos para sua conexão de destino, selecione **[!UICONTROL Próxima]**.

### Agendar exportação de público e exemplo {#schedule-segment-export-example}

Ao executar a [Agendar exportação de público](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) etapa, você deve mapear manualmente os públicos-alvo da Platform para a [atributos](#prerequisites-attribute) in [!DNL SAP Subscription Billing].

Um exemplo da etapa de exportação Programar público, com a localização do [!DNL SAP Commerce] **[!UICONTROL ID do mapeamento]** destacado, é mostrado abaixo:
![Imagem da Platform mostrando a programação de exportação de público-alvo com IDs de mapeamento preenchidas.](../../assets/catalog/ecommerce/sap-commerce/schedule-segment-export.png)

Para fazer isso, selecione cada segmento e insira o nome da referência personalizada em [!DNL SAP Subscription Billing] no [!DNL SAP Commerce] **[!UICONTROL ID do mapeamento]** campo do conector de destino. Para obter orientação sobre como criar referências personalizadas, consulte o [Criar referências personalizadas no [!DNL SAP Subscription Billing]](#prerequisites-custom-reference) seção.

>[!IMPORTANT]
>
> Não use o rótulo de referência personalizado como o valor.
>![Imagem que indica que você não deve usar o valor do rótulo de referência personalizado para mapeamento.](../../assets/catalog/ecommerce/sap-commerce/custom-reference-dont-use-label-for-mapping.png)

Por exemplo, se o público-alvo de Experience Platform selecionado for `sap_audience1` e quiser que seu status seja atualizado para o [!DNL SAP Subscription Billing] referência personalizada `SAP_1`, especifique esse valor no campo [!DNL SAP_Commerce] **[!UICONTROL ID do mapeamento]** campo.

Um exemplo **[!UICONTROL Tipo de referência]** de [!DNL SAP Subscription Billing] é mostrado abaixo:
![Imagem que mostra onde criar uma referência personalizada no Faturamento de assinatura SAP.](../../assets/catalog/ecommerce/sap-commerce/create-custom-reference.png)

Um exemplo da etapa Agendar exportação de público, com um público selecionado e seu correspondente [!DNL SAP Commerce] **[!UICONTROL ID do mapeamento]** destacado, é mostrado abaixo:
![Imagem da Platform mostrando a programação de exportação de público-alvo com IDs de mapeamento preenchidas.](../../assets/catalog/ecommerce/sap-commerce/schedule-segment-export-example.png)

Como mostrado, o valor dentro do **[!UICONTROL ID do mapeamento]** o campo deve corresponder exatamente ao [!DNL SAP Subscription Billing] **[!UICONTROL Tipo de referência]** valor .

Repita esta seção para cada público-alvo ativado da Platform.

Com base na imagem mostrada acima em que você selecionou dois públicos-alvo, o mapeamento seria o seguinte: | [!DNL SAP Commerce] nome do público | [!DNL SAP Subscription Billing] **[!UICONTROL Tipo de referência]** | [!DNL SAP Commerce] **[!UICONTROL ID do mapeamento]** value | | — | — | — | | sap_audience1 | `SAP_1` | `SAP_1` | | Público-alvo SAP2 | `SAP_2` | `SAP_2` |

## Validar exportação de dados {#exported-data}

Para validar se você configurou o destino corretamente, siga as etapas abaixo:

Faça logon no [!DNL SAP Subscription Billing] e navegue até o **[!UICONTROL Contatos]** página para verificar os status do público-alvo. A lista pode ser configurada para exibir colunas para as referências personalizadas e exibir os status de público correspondentes.
![Imagem de Faturamento de assinatura SAP mostrando a página de visão geral do cliente com cabeçalhos de coluna mostrando o nome do público-alvo e os status do público-alvo das células](../../assets/catalog/ecommerce/sap-commerce/customer-overview.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte o [Visão geral da governança de dados](/help/data-governance/home.md).

## Erros e solução de problemas {#errors-and-troubleshooting}

Consulte a [[!DNL SAP Subscription Billing] Tipos de erro](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/1a6a0dd6129c48e8b235190a1b5409fa.html) página da documentação para obter uma lista de possíveis tipos de erros e seus códigos de resposta.

## Recursos adicionais {#additional-resources}

Informações adicionais úteis do [!DNL SAP] A documentação do está abaixo:
* [Cobrança de assinatura SAP integrada](https://help.sap.com/docs/CLOUD_TO_CASH_OD/1216e7b79c984675b0a6f0005e351c74/e4b8badf7d124026991e4ab6b57d2a33.html)

### Changelog

Esta seção captura a funcionalidade e as atualizações de documentação significativas feitas neste conector de destino.

+++ Exibir changelog

| Mês de lançamento | Tipo de atualização | Descrição |
|---|---|---|
| Janeiro de 2024 | Versão inicial | Versão inicial de destino e publicação da documentação. |

{style="table-layout:auto"}

+++
