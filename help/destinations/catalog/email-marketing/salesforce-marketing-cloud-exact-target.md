---
keywords: email;Email;e-mail;email targets;salesforce;api salesforce marketing cloud destination
title: (API) Conexão do Salesforce Marketing Cloud
description: O destino do Marketing Cloud do Salesforce (anteriormente conhecido como ExactTarget) permite exportar os dados da sua conta e ativá-los no Marketing Cloud do Salesforce para as suas necessidades comerciais.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: d1bfd85bf7a318692fb6ae87e163dca105d531c6
workflow-type: tm+mt
source-wordcount: '2924'
ht-degree: 1%

---

# [!DNL (API) Salesforce Marketing Cloud] conexão

## Visão geral {#overview}

[[!DNL (API) Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/engagement/) (anteriormente conhecido como [!DNL ExactTarget]) é uma suíte de marketing digital que permite criar e personalizar jornadas para visitantes e clientes personalizarem suas experiências.

>[!IMPORTANT]
>
>Observe a diferença entre essa conexão e a outra [[!DNL Salesforce Marketing Cloud] conexão](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) que existe na seção Catálogo de marketing por email. A outra conexão do Salesforce Marketing Cloud permite exportar arquivos para um local de armazenamento especificado, enquanto essa é uma conexão de transmissão baseada em API.

Comparado a [!DNL Salesforce Marketing Cloud Account Engagement] mais orientada para a **B2B** marketing, a [!DNL (API) Salesforce Marketing Cloud] destino é ideal para **B2C** Casos de uso do com ciclos mais curtos de tomada de decisão transacional. Você pode consolidar conjuntos de dados maiores representando o comportamento do público-alvo para ajustar e melhorar as campanhas de marketing, priorizando e segmentando contatos, especialmente de conjuntos de dados externos [!DNL Salesforce]. *Observe que o Experience Platform também tem uma conexão para o [[!DNL Salesforce Marketing Cloud Account Engagement]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md).*

Este [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) utiliza o [!DNL Salesforce Marketing Cloud] [atualizar contatos](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) API, que permite **adicionar contatos e atualizar dados de contato** para as suas necessidades de negócios depois de ativá-las em um novo [!DNL Salesforce Marketing Cloud] segmento.

[!DNL Salesforce Marketing Cloud] O usa o OAuth 2 com credenciais de cliente como o mecanismo de autenticação para se comunicar com o [!DNL Salesforce Marketing Cloud] API. Instruções para autenticar em seu [!DNL Salesforce Marketing Cloud] exemplo, são apresentados mais abaixo, no [Autenticar para destino](#authenticate) seção.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar o [!DNL (API) Salesforce Marketing Cloud] destino, este é um exemplo de caso de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Enviar emails para contatos de campanhas de marketing {#use-case-send-emails}

O departamento de vendas de uma plataforma de aluguel de residências quer transmitir um email de marketing para um público-alvo de clientes direcionado. A equipe de marketing da plataforma pode adicionar novos contatos / atualizar contatos existentes *(e seus endereços de email)* no Adobe Experience Platform, crie públicos-alvo a partir de seus próprios dados offline e envie esses públicos-alvo para [!DNL Salesforce Marketing Cloud], que pode ser usado para enviar o email da campanha de marketing.

## Pré-requisitos {#prerequisites}

### Pré-requisitos no Experience Platform {#prerequisites-in-experience-platform}

Antes de ativar os dados para o [!DNL (API) Salesforce Marketing Cloud] destino, você deve ter um [schema](/help/xdm/schema/composition.md), um [conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), e [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) criado em [!DNL Experience Platform].

### Pré-requisitos no [!DNL (API) Salesforce Marketing Cloud] {#prerequisites-destination}

Observe os seguintes pré-requisitos para exportar dados da Platform para o seu [!DNL Salesforce Marketing Cloud] conta:

#### Você precisa ter um [!DNL Salesforce Marketing Cloud] account {#prerequisites-account}

A [!DNL Salesforce Marketing Cloud] conta com uma assinatura do [[!DNL Marketing Cloud Engagement]](https://www.salesforce.com/products/marketing-cloud/engagement/) o produto é obrigatório para continuar.

Entre em contato com [[!DNL Salesforce] Suporte](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) se você não tiver uma [!DNL Salesforce Marketing Cloud] ou sua conta não tem a variável [!DNL Marketing Cloud Engagement] assinatura do produto.

#### Criar atributos em [!DNL Salesforce Marketing Cloud] {#prerequisites-attribute}

Ao ativar públicos-alvo para a variável [!DNL (API) Salesforce Marketing Cloud] destino, você deve inserir um valor no campo **[!UICONTROL ID do mapeamento]** para cada público-alvo ativado, no campo **[Programação de público](#schedule-segment-export-example)** etapa.

[!DNL Salesforce] exige que esse valor leia e interprete corretamente os públicos-alvo provenientes do Experience Platform e atualize o status dos públicos-alvo dentro de [!DNL Salesforce Marketing Cloud]. Consulte a documentação do Experience Platform para [Grupo de campos de esquema Detalhes da associação do público](/help/xdm/field-groups/profile/segmentation.md) se precisar de orientação sobre os status do público-alvo.

Para cada público-alvo que você ativar da Platform para o [!DNL Salesforce Marketing Cloud], é necessário criar um atributo do tipo `Text` no prazo de [!DNL Salesforce]. Use o [!DNL Salesforce Marketing Cloud] [!DNL Contact Builder] para criar atributos. Os nomes de campo de atributo são usados para a variável [!DNL (API) Salesforce Marketing Cloud] campo de destino durante o **[!UICONTROL Mapeamento]** etapa. Você pode definir o caractere de campo com no máximo 4.000 caracteres, de acordo com sua necessidade comercial. Consulte a [!DNL Salesforce Marketing Cloud] [Tipos de dados de extensões de dados](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_types.htm&amp;type=5) página de documentação para obter informações adicionais sobre tipos de atributos.

Consulte a [!DNL Salesforce Marketing Cloud] documentação para [criar atributos](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) se você precisar de orientação sobre como criar atributos.

Um exemplo da tela do designer de dados no [!DNL Salesforce Marketing Cloud], no qual você adicionará o atributo, é mostrado abaixo:
![Designer de dados da interface do usuário do Salesforce Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-data-designer.png)

Uma visão do [!DNL Salesforce Marketing Cloud] [!DNL Email Demographics] conjunto de atributos é mostrado abaixo:
![Conjunto de atributos demográficos de email da interface do usuário do Marketing Cloud do Salesforce.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-email-demograhics-fields.png)

A variável [!DNL (API) Salesforce Marketing Cloud] o destino usa o [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) para recuperar dinamicamente os atributos e seus Conjuntos de atributos definidos no [!DNL Salesforce Marketing Cloud].

Elas são exibidas na guia **[!UICONTROL Campo de destino]** janela de seleção ao configurar a variável [mapeamento](#mapping-considerations-example) no fluxo de trabalho para [ativar públicos-alvo para o destino](#activate).

>[!IMPORTANT]
>
>Dentro de [!DNL Salesforce Marketing Cloud], você deve criar atributos com um **[!UICONTROL NOME DO CAMPO]** que corresponde exatamente ao valor especificado em **[!UICONTROL ID do mapeamento]** para cada segmento ativado da Platform. Por exemplo, a captura de tela abaixo mostra um atributo chamado `salesforce_mc_segment_1`. Ao ativar um público-alvo para esse destino, adicione `salesforce_mc_segment_1` as **[!UICONTROL ID do mapeamento]** para preencher públicos-alvo do Experience Platform nesse atributo.

Um exemplo de criação de atributo em [!DNL Salesforce Marketing Cloud], é mostrado abaixo:
![Captura de tela da interface do usuário do Salesforce Marketing Cloud mostrando um atributo.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

>[!TIP]
>
>* Ao criar o atributo, não inclua caracteres de espaço em branco no nome do campo. Em vez disso, use sublinhado `(_)` como separador.
>* Para distinguir entre atributos usados para públicos da Platform e outros atributos em [!DNL Salesforce Marketing Cloud], você pode incluir um prefixo ou sufixo reconhecível para os atributos usados para os segmentos de Adobe. Por exemplo, em vez de `test_segment`, use `Adobe_test_segment` ou `test_segment_Adobe`.
>* Se você já tiver outros atributos criados no [!DNL Salesforce Marketing Cloud], você pode usar o mesmo nome do segmento da Platform para identificar facilmente o público-alvo no [!DNL Salesforce Marketing Cloud].

#### Atribuir funções e permissões de usuário no [!DNL Salesforce Marketing Cloud] {#prerequisites-roles-permissions}

Como [!DNL Salesforce Marketing Cloud] O suporta funções personalizadas dependendo do seu caso de uso, seu usuário deve receber as funções relevantes para atualizar seus atributos no [!DNL Salesforce Marketing Cloud] conjuntos de atributos. Um exemplo de funções atribuídas a um usuário é mostrado abaixo:
![Interface do usuário do Salesforce Marketing Cloud para um usuário selecionado que mostra suas funções atribuídas.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-edit-roles.png)

Dependendo de quais funções o seu [!DNL Salesforce Marketing Cloud] usuário tiver sido atribuído, também será necessário atribuir permissões ao [!DNL Salesforce Marketing Cloud] conjuntos de atributos que contêm os campos que você deseja atualizar.

Como esse destino requer acesso à `[!DNL attribute-set]`, você precisa permitir. Por exemplo, para a variável `Email` [!DNL attribute-set] você precisa permitir, conforme mostrado abaixo:

![Interface do usuário do Salesforce Marketing Cloud mostrando o conjunto de atributos de email com permissões permitidas.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-permisions-list.png)

Para restringir o nível de acesso, você também pode substituir acessos individuais usando privilégios granulares.
![Interface do usuário do Salesforce Marketing Cloud mostrando o conjunto de atributos de email com permissões granulares.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/sales-email-attribute-set-permission.png)

Consulte a [[!DNL Marketing Cloud Roles]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_marketing_cloud_roles.htm&amp;type=5) e [[!DNL Marketing Cloud Roles and Permissions]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_roles.htm&amp;type=5) para obter orientação detalhada.

#### Coletar [!DNL Salesforce Marketing Cloud] credenciais {#gather-credentials}

Anote os itens abaixo antes de autenticar na [!DNL (API) Salesforce Marketing Cloud] destino.

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| Subdomain | Consulte [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html) para saber como obter esse valor do [!DNL Salesforce Marketing Cloud] interface. | Se o seu [!DNL Salesforce Marketing Cloud] o domínio é<br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br>você precisa fornecer `mcq4jrssqdlyc4lph19nnqgzzs84` como o valor. |
| ID do cliente | Consulte a [!DNL Salesforce Marketing Cloud] [documentação](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) para saber como obter esse valor do [!DNL Salesforce Marketing Cloud] interface. | r23kxxxxxxxx0z05xxxxxx |
| Segredo do cliente | Consulte a [!DNL Salesforce Marketing Cloud] [documentação](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) para saber como obter esse valor do [!DNL Salesforce Marketing Cloud] interface. | ipxxxxxxxxxxT4xxxxxxxxxx |

{style="table-layout:auto"}

### Medidas de proteção {#guardrails}

* A Salesforce impõe certas [limites de taxa](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
   * Consulte a [!DNL Salesforce Marketing Cloud] [documentação](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) para resolver quaisquer limites prováveis que você possa encontrar e reduzir erros durante a execução.
   * Consulte a [[!DNL Salesforce Marketing Cloud] Preços do compromisso](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) página para *Baixe o gráfico de comparação da edição completa* como um pdf que detalha os limites impostos pelo seu plano.
   * A variável [Visão geral da API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) a página detalha limites adicionais.
   * Consultar [aqui](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) para uma página que reúne esses detalhes.
* A contagem de *campos personalizados permitidos por objeto* varia de acordo com sua edição do Salesforce.
   * Consulte a [!DNL Salesforce] [documentação](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) para obter orientação adicional.
   * Se tiver atingido o limite definido para *campos personalizados permitidos por objeto* no prazo de [!DNL Salesforce Marketing Cloud] será necessário
      * Remova atributos mais antigos antes de adicionar novos atributos no [!DNL Salesforce Marketing Cloud].
      * Atualize ou remova qualquer público ativado nos destinos da Platform que usam esses nomes de atributo mais antigos como o valor fornecido para **[!UICONTROL ID do mapeamento]** durante o [agendamento de público](#schedule-segment-export-example) etapa.

## Identidades suportadas {#supported-identities}

[!DNL (API) Salesforce Marketing Cloud] O oferece suporte à ativação das identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade de destino | Descrição | Considerações |
|---|---|---|
| contactKey | [!DNL Salesforce Marketing Cloud] Chave do contato. Consulte a [!DNL Salesforce Marketing Cloud] [documentação](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) se precisar de orientação adicional. | Obrigatório |

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | <ul><li>Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados *(por exemplo: endereço de email, número de telefone, sobrenome)*, de acordo com o mapeamento de campo.</li><li> Cada status de segmento em [!DNL Salesforce Marketing Cloud] é atualizado com o status de público-alvo correspondente na Platform, com base no **[!UICONTROL ID do mapeamento]** valor fornecido durante o [agendamento de público](#schedule-segment-export-example) etapa.</li></ul> |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do público-alvo, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

Dentro de **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, pesquisar [!DNL (API) Salesforce Marketing Cloud]. Como alternativa, você pode localizá-lo na **[!UICONTROL Marketing por email]** categoria.

### Autenticar para destino {#authenticate}

Para autenticar no destino, preencha os campos obrigatórios abaixo e selecione **[!UICONTROL Conectar ao destino]**. Consulte a [Coletar [!DNL Salesforce Marketing Cloud] credenciais](#gather-credentials) para obter orientação.

| [!DNL (API) Salesforce Marketing Cloud] destino | [!DNL Salesforce Marketing Cloud] |
| --- | --- |
| **[!UICONTROL Subdomain]** | Seu [!DNL Salesforce Marketing Cloud] prefixo do domínio. <br>Por exemplo, se o domínio for <br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br> você precisa fornecer `mcq4jrssqdlyc4lph19nnqgzzs84` como o valor. |
| **[!UICONTROL ID do cliente]** | Seu [!DNL Salesforce Marketing Cloud] `Client ID`. |
| **[!UICONTROL Segredo do cliente]** | Seu [!DNL Salesforce Marketing Cloud] `Client Secret`. |

![Captura de tela da interface do usuário da Platform mostrando como autenticar no Salesforce Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

Se os detalhes fornecidos forem válidos, a interface exibirá uma **[!UICONTROL Conectado]** com uma marca de seleção verde, você pode prosseguir para a próxima etapa.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.
![Captura de tela da interface do usuário da plataforma mostrando os detalhes do destino.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar públicos para este destino {#activate}

>[!IMPORTANT]
>
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e públicos para destinos de exportação de público de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Considerações e exemplo de mapeamento {#mapping-considerations-example}

Para enviar corretamente os dados do público-alvo do Adobe Experience Platform para a [!DNL (API) Salesforce Marketing Cloud] destino, é necessário passar pela etapa de mapeamento de campos. O mapeamento consiste em criar um link entre os campos do esquema do Experience Data Model (XDM) na sua conta da Platform e seus equivalentes correspondentes no destino.

Para mapear corretamente os campos XDM para o [!DNL (API) Salesforce Marketing Cloud] campos de destino, siga as etapas abaixo.

>[!IMPORTANT]
>
>* Embora seus nomes de atributo sejam os mesmos de acordo com [!DNL Salesforce Marketing Cloud] conta, os mapeamentos para ambos `contactKey` e `personalEmail.address` são obrigatórios.
>
>* A integração com o [!DNL Salesforce Marketing Cloud] A API está sujeita a um limite de paginação de quantos atributos o Experience Platform pode recuperar do Salesforce. Isso significa que, durante o **[!UICONTROL Mapeamento]** etapa, o esquema de campo de destino pode exibir no máximo 2000 atributos da sua conta do Salesforce.

1. No **[!UICONTROL Mapeamento]** etapa, selecione **[!UICONTROL Adicionar novo mapeamento]**. Você verá uma nova linha de mapeamento na tela.
   ![Exemplo de captura de tela da interface do Platform para Adicionar novo mapeamento.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)
1. No **[!UICONTROL Selecionar campo de origem]** escolha a **[!UICONTROL Selecionar atributos]** e selecione o atributo XDM ou escolha o atributo **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade.
1. No **[!UICONTROL Selecionar campo de destino]** escolha a **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade ou escolha **[!UICONTROL Selecionar atributos]** e selecione um atributo dos conjuntos de atributos exibidos conforme necessário. A variável [!DNL (API) Salesforce Marketing Cloud] o destino usa o [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) para recuperar dinamicamente os atributos e seus conjuntos de atributos definidos no [!DNL Salesforce Marketing Cloud]. Elas são exibidas na guia **[!UICONTROL Campo de destino]** pop-up ao configurar o [mapeamento](#mapping-considerations-example) no [ativar fluxo de trabalho de públicos](#activate).

   * Repita essas etapas para adicionar os seguintes mapeamentos entre o esquema de perfil XDM e [!DNL (API) Salesforce Marketing Cloud]:

     | Campo de origem | Campo de destino | Obrigatório |
     |---|---|---|
     | `IdentityMap: contactKey` | `Identity: salesforceContactKey` | `Mandatory` |
     | `xdm: person.name.firstName` | `Attribute: First Name` do conjunto de atributos desejado. | - |
     | `xdm: personalEmail.address` | `Attribute: Email Address` do conjunto de atributos desejado. | - |

   * Um exemplo usando esses mapeamentos é mostrado abaixo:
     ![Exemplo de captura de tela da interface do Platform mostrando os mapeamentos do Target.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

Quando terminar de fornecer os mapeamentos para sua conexão de destino, selecione **[!UICONTROL Próxima]**.

### Agendar exportação de público e exemplo {#schedule-segment-export-example}

Ao executar a [Agendar exportação de público](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) etapa, você deve mapear manualmente os públicos-alvo da Platform para a [atributos](#prerequisites-attribute) in [!DNL Salesforce Marketing Cloud].

Para fazer isso, selecione cada segmento e digite o nome do atributo em [!DNL Salesforce Marketing Cloud] no [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID do mapeamento]** campo. Consulte a [Criar atributo em [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) seção para obter orientação e práticas recomendadas sobre como criar atributos no [!DNL Salesforce Marketing Cloud].

Por exemplo, se o [!DNL Salesforce Marketing Cloud] atributo é `salesforce_mc_segment_1`, especifique esse valor no campo [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID do mapeamento]** para preencher públicos-alvo do Experience Platform nesse atributo.

Um exemplo de atributo de [!DNL Salesforce Marketing Cloud] é mostrado abaixo:
![Captura de tela da interface do usuário do Salesforce Marketing Cloud mostrando um atributo.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

Um exemplo indicando a localização do [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID do mapeamento]** é mostrado abaixo:
![Exemplo de captura de tela da interface do Platform mostrando Programar exportação de público-alvo.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

Como mostrado na [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID do mapeamento]** deve corresponder exatamente ao valor especificado [!DNL Salesforce Marketing Cloud] **[!UICONTROL NOME DO CAMPO]**.

Repita esta seção para cada segmento da Platform ativado.

Dependendo do caso de uso, todos os públicos ativados podem ser mapeados para o mesmo [!DNL Salesforce Marketing Cloud] **[!UICONTROL NOME DO CAMPO]** ou para diferentes **[!UICONTROL NOME DO CAMPO]** in [!DNL (API) Salesforce Marketing Cloud]. Um exemplo típico com base na imagem mostrada acima pode ser.
| [!DNL (API) Salesforce Marketing Cloud] nome do segmento | [!DNL Salesforce Marketing Cloud] **[!UICONTROL NOME DO CAMPO]** | [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID do mapeamento]** | | — | — | — | | público-alvo do salesforce mc 1 | `salesforce_mc_segment_1` | `salesforce_mc_segment_1` | | público-alvo da salesforce mc 2 | `salesforce_mc_segment_2` | `salesforce_mc_segment_2` |

## Validar exportação de dados {#exported-data}

Para validar se você configurou o destino corretamente, siga as etapas abaixo:

1. Selecionar **[!UICONTROL Destinos]** > **[!UICONTROL Procurar]** para navegar até a lista de destinos.
   ![Captura de tela da interface do usuário da plataforma mostrando os destinos de navegação.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. Selecionar o destino e validar se o status é **[!UICONTROL habilitado]**.
   ![Captura de tela da interface do usuário da plataforma mostrando a execução do fluxo de dados de destinos.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. Alterne para a **[!DNL Activation data]** e selecione um nome de público-alvo.
   ![Exemplo de captura de tela da interface do Platform mostrando Dados de ativação de destinos.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. Monitore o resumo do público-alvo e verifique se a contagem de perfis corresponde à contagem criada no segmento.
   ![Exemplo de captura de tela da interface do Platform mostrando o segmento.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. Faça logon no [[!DNL Salesforce Marketing Cloud]](https://mc.exacttarget.com/) site. Em seguida, navegue até o **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** e verifique se os perfis do público-alvo foram adicionados.
   ![Captura de tela da interface do usuário do Marketing Cloud do Salesforce que mostra a página Contatos com perfis usados no segmento.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. Para verificar se algum perfil foi atualizado, navegue até o **[!UICONTROL E-mail]** e verifique se os valores de atributo do perfil do público-alvo foram atualizados. Se tiver sucesso, você poderá ver que cada status de público-alvo em [!DNL Salesforce Marketing Cloud] foi atualizado com o status de público-alvo correspondente na Platform, com base na **[!UICONTROL ID do mapeamento]** valor fornecido na variável [agendamento de público](#schedule-segment-export-example) etapa.
   ![Captura de tela da interface do usuário do Marketing Cloud do Salesforce mostrando a página de email Contatos selecionada com status de público atualizado.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte o [Visão geral da governança de dados](/help/data-governance/home.md).

## Erros e solução de problemas {#errors-and-troubleshooting}

### Erros desconhecidos encontrados ao enviar eventos por push para o Marketing Cloud do Salesforce {#unknown-errors}

* Ao verificar uma execução de fluxo de dados, você pode encontrar a seguinte mensagem de erro: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  ![Captura de tela da interface do usuário da plataforma mostrando erro.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

   * Para corrigir esse erro, verifique se **[!UICONTROL ID do mapeamento]** que você forneceu no fluxo de trabalho de ativação para a [!DNL (API) Salesforce Marketing Cloud] destino corresponde exatamente ao nome do atributo criado no [!DNL Salesforce Marketing Cloud]. Consulte a [Criar atributo em [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) para obter orientação.

* Ao ativar um segmento, você pode obter uma mensagem de erro: `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Para corrigir esse erro, entre em contato com o [!DNL Salesforce Marketing Cloud] administrador da conta a adicionar [Endereços IP do Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) ao seu [!DNL Salesforce Marketing Cloud] intervalos de IP confiáveis das contas. Consulte a [!DNL Salesforce Marketing Cloud] [Endereços IP para inclusão nas Listas de permissões no Marketing Cloud](https://help.salesforce.com/s/articleView?id=sf.mc_es_ip_addresses_for_inclusion.htm&amp;type=5) se precisar de orientação adicional.

## Recursos adicionais {#additional-resources}

* [!DNL Salesforce Marketing Cloud] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
* [!DNL Salesforce Marketing Cloud] [documentação](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) explicando como os contatos são atualizados com as informações especificadas nos grupos de atributos especificados.

### Changelog {#changelog}

Esta seção captura a funcionalidade e as atualizações de documentação significativas feitas neste conector de destino.

+++ Exibir changelog

| Mês de lançamento | Tipo de atualização | Descrição |
|---|---|---|
| Abril de 2023 | Atualização da documentação | <ul><li>Corrigimos uma declaração e um link de referência na [Pré-requisitos no (API) Salesforce Marketing Cloud](#prerequisites-destination) seção para chamar isso [!DNL Salesforce Marketing Cloud Engagement] é uma assinatura obrigatória para usar esse destino. A seção anteriormente informava incorretamente que os usuários precisavam de uma assinatura do Marketing Cloud **Conta** Compromisso para continuar.</li> <li>Adicionamos uma seção em [pré-requisitos](#prerequisites) para [funções e permissões](#prerequisites-roles-permissions) a ser atribuído à [!DNL Salesforce] usuário para este destino funcionar. (PLATIR-26299)</li></ul> |
| Fevereiro de 2023 | Atualização da documentação | Atualizamos o [Pré-requisitos no (API) Salesforce Marketing Cloud](#prerequisites-destination) seção para incluir um link de referência chamando isso de [!DNL Salesforce Marketing Cloud Engagement] é uma assinatura obrigatória para usar esse destino. |
| Fevereiro de 2023 | Atualização de funcionalidade | Corrigimos um problema em que uma configuração incorreta no destino estava causando o envio de um JSON malformado para o Salesforce. Isso resultou em alguns usuários vendo altos números de identidades que falharam na ativação. (PLATIR-26299) |
| Janeiro de 2023 | Atualização da documentação | <ul><li>Atualizamos o [Pré-requisitos no [!DNL Salesforce]](#prerequisites-destination) seção para informar que os atributos precisam ser criados na [!DNL Salesforce] lado. Esta seção agora inclui instruções detalhadas sobre como fazer isso e práticas recomendadas para nomear os atributos em [!DNL Salesforce]. (PLATIR-25602)</li><li>Adicionamos instruções claras sobre como usar a ID de mapeamento para cada público ativado na [agendamento de público](#schedule-segment-export-example) etapa. (PLATIR-25602)</li></ul> |
| Outubro de 2022 | Versão inicial | Versão inicial de destino e publicação da documentação. |

{style="table-layout:auto"}

+++
