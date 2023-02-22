---
keywords: email, Email, email, destinos de email, salesforce, api salesforce marketing cloud destination
title: (API) Conexão do Salesforce Marketing Cloud
description: O destino do Marketing Cloud Salesforce (conhecido anteriormente como ExactTarget) permite exportar os dados da conta e ativá-los no Marketing Cloud Salesforce para as necessidades de sua empresa.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: 5a9b7af3b009f8529f2e473b17f77c54de35003e
workflow-type: tm+mt
source-wordcount: '2464'
ht-degree: 1%

---

# [!DNL (API) Salesforce Marketing Cloud] conexão

## Visão geral {#overview}

[[!DNL (API) Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/overview/) (anteriormente conhecido como [!DNL ExactTarget]) é um conjunto de marketing digital que permite criar e personalizar jornadas para visitantes e clientes para personalizar sua experiência.

>[!IMPORTANT]
>
>Observe a diferença entre essa conexão e a outra [[!DNL Salesforce Marketing Cloud] conexão](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) que existe na seção Catálogo de marketing de email . A outra conexão do Salesforce Marketing Cloud permite exportar arquivos para um local de armazenamento especificado, enquanto essa é uma conexão de transmissão baseada em API.

Essa [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) utiliza o [!DNL Salesforce Marketing Cloud] [atualizar contatos](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) API, que permite adicionar contatos/atualizar dados de contato para as necessidades de sua empresa depois de ativá-los em um novo [!DNL Salesforce Marketing Cloud] segmento.

[!DNL Salesforce Marketing Cloud] O usa o OAuth 2 com credenciais do cliente como o mecanismo de autenticação para se comunicar com o [!DNL Salesforce Marketing Cloud] API. Instruções para autenticação em seu [!DNL Salesforce Marketing Cloud] são mais abaixo, na variável [Autenticar para destino](#authenticate) seção.

## Casos de uso {#use-cases}

Para ajudá-lo a entender melhor como e quando você deve usar a variável [!DNL (API) Salesforce Marketing Cloud] destino, aqui está um exemplo de caso de uso que os clientes do Adobe Experience Platform podem resolver usando esse destino.

### Enviar emails para contatos para campanhas de marketing {#use-case-send-emails}

O departamento de vendas de uma plataforma de aluguel da casa deseja transmitir um email de marketing para um público-alvo de cliente. A equipe de marketing da plataforma pode adicionar novos contatos/atualizar contatos existentes *(e seus endereços de email)* por meio do Adobe Experience Platform, crie segmentos a partir de seus próprios dados offline e envie esses segmentos para [!DNL Salesforce Marketing Cloud], que pode ser usada para enviar o email da campanha de marketing.

## Pré-requisitos {#prerequisites}

### Pré-requisitos no Experience Platform {#prerequisites-in-experience-platform}

Antes de ativar os dados para o [!DNL (API) Salesforce Marketing Cloud] destino, você deve ter um [schema](/help/xdm/schema/composition.md), a [conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)e [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) criado em [!DNL Experience Platform].

### Pré-requisitos em [!DNL (API) Salesforce Marketing Cloud] {#prerequisites-destination}

Observe os seguintes pré-requisitos para exportar dados do Platform para seu [!DNL Salesforce Marketing Cloud] conta:

#### Você precisa ter um [!DNL Salesforce Marketing Cloud] account {#prerequisites-account}

A [!DNL Salesforce Marketing Cloud] com uma assinatura para a [Envolvimento da conta do Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) produto é obrigatório para prosseguir.

Entre em contato com o [[!DNL Salesforce] Suporte](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) se você não tiver um [!DNL Salesforce Marketing Cloud] ou sua conta estiver sem a [!DNL Marketing Cloud Account Engagement] assinatura do produto.

#### Criar atributos dentro de [!DNL Salesforce Marketing Cloud] {#prerequisites-attribute}

Ao ativar segmentos para a [!DNL (API) Salesforce Marketing Cloud] , você deve inserir um valor na variável **[!UICONTROL ID de mapeamento]** para cada segmento ativado, no campo **[Agendamento do segmento](#schedule-segment-export-example)** etapa.

[!DNL Salesforce] exige que esse valor leia e interprete corretamente os segmentos provenientes do Experience Platform e atualize seu status de segmento dentro de [!DNL Salesforce Marketing Cloud]. Consulte a documentação do Experience Platform para [Grupo de campos Detalhes da associação ao segmento](/help/xdm/field-groups/profile/segmentation.md) se você precisar de orientação sobre os status do segmento.

Para cada segmento que você ativa da plataforma para o [!DNL Salesforce Marketing Cloud], é necessário criar um atributo do tipo `Text` within [!DNL Salesforce]. Use o [!DNL Salesforce Marketing Cloud] [!DNL Contact Builder] para criar atributos. Os nomes dos campos de atributo são usados para a variável [!DNL (API) Salesforce Marketing Cloud] campo de destino e deve ser criado na variável `[!DNL Email Demographics system attribute-set]`. Você pode definir o caractere de campo com no máximo 4000 caracteres, de acordo com seu requisito comercial. Consulte a [!DNL Salesforce Marketing Cloud] [Tipos de dados das extensões de dados](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_types.htm&amp;type=5) página de documentação para obter informações adicionais sobre tipos de atributos.

Consulte a [!DNL Salesforce Marketing Cloud] documentação para [criar atributos](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) se você precisar de orientação sobre como criar atributos.

Um exemplo da tela do designer de dados em [!DNL Salesforce Marketing Cloud], no qual você adicionará o atributo é mostrado abaixo:
![Designer de dados da interface do usuário do Salesforce Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-data-designer.png)

Uma visão da [!DNL Salesforce Marketing Cloud] [!DNL Email Demographics] o conjunto de atributos é mostrado abaixo:
![Conjuntos de atributos demográficos de email da interface do usuário do Salesforce Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-email-demograhics-fields.png)

O [!DNL (API) Salesforce Marketing Cloud] O destino usa o [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) para recuperar dinamicamente os atributos e seus Conjuntos de atributos definidos em [!DNL Salesforce Marketing Cloud].

Eles são exibidos na variável **[!UICONTROL Campo de destino]** janela de seleção ao configurar [mapeamento](#mapping-considerations-example) no fluxo de trabalho para [ativar segmentos para o destino](#activate). Observe que somente os mapeamentos para os atributos definidos na variável [!DNL Salesforce Marketing Cloud] `[!DNL Email Demographics]` conjunto de atributos são suportados.

>[!IMPORTANT]
>
>Within [!DNL Salesforce Marketing Cloud], você deve criar atributos com um **[!UICONTROL NOME DO CAMPO]** que corresponde exatamente ao valor especificado em **[!UICONTROL ID de mapeamento]** para cada segmento da plataforma ativada. Por exemplo, a captura de tela abaixo mostra um atributo chamado `salesforce_mc_segment_1`. Ao ativar um segmento para esse destino, adicione `salesforce_mc_segment_1` as **[!UICONTROL ID de mapeamento]** para preencher públicos-alvo de segmento do Experience Platform para este atributo.

Um exemplo da criação de atributo em [!DNL Salesforce Marketing Cloud], é mostrado abaixo:
![Captura de tela da interface do usuário do Salesforce Marketing Cloud mostrando um atributo.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

>[!TIP]
>
>* Ao criar o atributo, não inclua caracteres de espaço em branco no nome do campo. Em vez disso, use o sublinhado `(_)` como separador.
>* Para distinguir entre atributos usados para segmentos da Platform e outros atributos de [!DNL Salesforce Marketing Cloud], é possível incluir um prefixo ou sufixo reconhecível para os atributos usados para segmentos de Adobe. Por exemplo, em vez de `test_segment`, use `Adobe_test_segment` ou `test_segment_Adobe`.
>* Se você já tiver outros atributos criados em [!DNL Salesforce Marketing Cloud], você pode usar o mesmo nome do segmento da Plataforma para identificar facilmente o segmento em [!DNL Salesforce Marketing Cloud].


#### Colete [!DNL Salesforce Marketing Cloud] credenciais {#gather-credentials}

Anote os itens abaixo antes de autenticar para o [!DNL (API) Salesforce Marketing Cloud] destino.

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| Subdomain | Consulte [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html) para saber como obter esse valor do [!DNL Salesforce Marketing Cloud] interface. | Se o seu [!DNL Salesforce Marketing Cloud] domínio é<br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br>é necessário fornecer `mcq4jrssqdlyc4lph19nnqgzzs84` como o valor. |
| ID do cliente | Consulte a [!DNL Salesforce Marketing Cloud] [documentação](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) para saber como obter esse valor do [!DNL Salesforce Marketing Cloud] interface. | r23kxxxxxxxx0z05xxxxxx |
| Segredo do cliente | Consulte a [!DNL Salesforce Marketing Cloud] [documentação](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) para saber como obter esse valor do [!DNL Salesforce Marketing Cloud] interface. | ipxxxxxxxxxxT4xxxxxxxxxx |

{style=&quot;table-layout:auto&quot;}

### Medidas de proteção {#guardrails}

* Salesforce impõe certas [limites de taxa](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
   * Consulte a [!DNL Salesforce Marketing Cloud] [documentação](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) para endereçar quaisquer limites prováveis que você possa encontrar e reduzir erros durante a execução.
   * Consulte a [[!DNL Salesforce Marketing Cloud] Preços do contrato](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) página para *Baixe o Gráfico de Comparação da Edição Completa* como um pdf que detalha os limites impostos pelo seu plano.
   * O [Visão geral da API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) a página detalha os limites adicionais.
   * Consulte [here](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) para uma página que colige esses detalhes.
* A contagem de *campos personalizados permitidos por objeto* varia de acordo com seu Salesforce Edition.
   * Consulte a [!DNL Salesforce] [documentação](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) para obter orientações adicionais.
   * Se você atingiu o limite definido para *campos personalizados permitidos por objeto* within [!DNL Salesforce Marketing Cloud] você precisará
      * Remova os atributos mais antigos antes de adicionar novos atributos em [!DNL Salesforce Marketing Cloud].
      * Atualize ou remova quaisquer segmentos ativados nos destinos da plataforma que usam esses nomes de atributos mais antigos como o valor fornecido para **[!UICONTROL ID de mapeamento]** durante a [agendamento de segmento](#schedule-segment-export-example) etapa.

## Identidades suportadas {#supported-identities}

[!DNL (API) Salesforce Marketing Cloud] O suporta a ativação de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| contactKey | [!DNL Salesforce Marketing Cloud] Chave de contato. Consulte a [!DNL Salesforce Marketing Cloud] [documentação](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) se precisar de orientação adicional. | Obrigatório |

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | <ul><li>Você está exportando todos os membros de um segmento, junto com os campos de esquema desejados *(por exemplo: endereço de email, número de telefone, sobrenome)*, de acordo com o mapeamento de campo.</li><li> Cada status de segmento em [!DNL Salesforce Marketing Cloud] é atualizado com o status de segmento correspondente da Platform, com base no **[!UICONTROL ID de mapeamento]** valor fornecido durante a [agendamento de segmento](#schedule-segment-export-example) etapa.</li></ul> |
| Frequência de exportação | **[!UICONTROL Streaming]** | Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow para configurar destino , preencha os campos listados nas duas seções abaixo.

Within **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]**, pesquisar por [!DNL (API) Salesforce Marketing Cloud]. Como alternativa, você pode localizá-lo sob a variável **[!UICONTROL Marketing por email]** categoria .

### Autenticar para destino {#authenticate}

Para autenticar para o destino, preencha os campos obrigatórios abaixo e selecione **[!UICONTROL Ligar ao destino]**. Consulte a [Colete [!DNL Salesforce Marketing Cloud] credenciais](#gather-credentials) para quaisquer orientações.

| [!DNL (API) Salesforce Marketing Cloud] destino | [!DNL Salesforce Marketing Cloud] |
| --- | --- |
| **[!UICONTROL Subdomain]** | Seu [!DNL Salesforce Marketing Cloud] prefixo do domínio. <br>Por exemplo, se o domínio for <br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br> é necessário fornecer `mcq4jrssqdlyc4lph19nnqgzzs84` como o valor. |
| **[!UICONTROL ID do cliente]** | Seu [!DNL Salesforce Marketing Cloud] `Client ID`. |
| **[!UICONTROL Segredo do cliente]** | Seu [!DNL Salesforce Marketing Cloud] `Client Secret`. |

![Captura de tela da interface do usuário da plataforma que mostra como autenticar no Salesforce Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

Se os detalhes fornecidos forem válidos, a interface do usuário exibirá uma **[!UICONTROL Conectado]** com uma marca de seleção verde, você pode prosseguir para a próxima etapa.

### Preencha os detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.
![Captura de tela da interface do usuário da plataforma que mostra os detalhes do destino.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
>
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmentos de fluxo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Considerações e exemplo de mapeamento {#mapping-considerations-example}

Para enviar corretamente os dados de público-alvo do Adobe Experience Platform para a [!DNL (API) Salesforce Marketing Cloud] , é necessário percorrer a etapa de mapeamento de campo . O mapeamento consiste em criar um link entre os campos do esquema do Modelo de dados de experiência (XDM) na conta da plataforma e os equivalentes correspondentes do destino.

Para mapear corretamente os campos XDM para a variável [!DNL (API) Salesforce Marketing Cloud] campos de destino, siga as etapas abaixo.

>[!IMPORTANT]
>
>Embora seus nomes de atributo sejam de acordo com seu [!DNL Salesforce Marketing Cloud] , os mapeamentos para ambos `contactKey` e `personalEmail.address` são obrigatórias. Ao mapear atributos, somente atributos do Experience Platform `Email Demographics` conjunto de atributos deve ser usado nos campos de destino.

1. No **[!UICONTROL Mapeamento]** etapa , selecione **[!UICONTROL Adicionar novo mapeamento]**. Você verá uma nova linha de mapeamento na tela.
   ![Exemplo de captura de tela da interface do usuário da plataforma para Adicionar novo mapeamento.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)
1. No **[!UICONTROL Selecionar campo de origem]** escolha a **[!UICONTROL Selecionar atributos]** e selecione o atributo XDM ou escolha a **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade.
1. No **[!UICONTROL Selecionar campo de destino]** escolha a **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade ou escolha **[!UICONTROL Selecionar atributos personalizados]** e selecione um atributo do `Email Demographics` atributos exibidos conforme necessário. O [!DNL (API) Salesforce Marketing Cloud] O destino usa o [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) para recuperar dinamicamente os atributos e seus conjuntos de atributos definidos em [!DNL Salesforce Marketing Cloud]. Eles são exibidos na variável **[!UICONTROL Campo de destino]** pop-up ao configurar o [mapeamento](#mapping-considerations-example) no [ativar segmentos para fluxo de trabalho](#activate). Observação: somente mapeamentos para os atributos definidos na variável [!DNL Salesforce Marketing Cloud] `[!DNL Email Demographics]` conjunto de atributos são suportados.

   * Repita essas etapas para adicionar os seguintes mapeamentos entre o esquema de perfil XDM e [!DNL (API) Salesforce Marketing Cloud]: |Campo de Origem|Campo de Destino| Obrigatório| |—|—| |`IdentityMap: contactKey`|`Identity: salesforceContactKey`| `Mandatory` |\
      |`xdm: person.name.firstName`|`Attribute: Email Demographics.First Name`| - | |`xdm: personalEmail.address`|`Attribute: Email Addresses.Email Address`| - |

   * Um exemplo de uso desses mapeamentos é mostrado abaixo:
      ![Exemplo de captura de tela da interface do usuário da plataforma que mostra os mapeamentos do Target.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

Quando terminar de fornecer os mapeamentos para a conexão de destino, selecione **[!UICONTROL Próximo]**.

### Programar exportação de segmento e exemplo {#schedule-segment-export-example}

Ao executar o [Agendar exportação de segmentos](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) , é necessário mapear manualmente os segmentos da Platform para a [atributos](#prerequisites-attribute) em [!DNL Salesforce Marketing Cloud].

Para fazer isso, selecione cada segmento e insira o nome do atributo de [!DNL Salesforce Marketing Cloud] no [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de mapeamento]** campo. Consulte a [Criar atributo dentro de [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) seção para orientação e práticas recomendadas na criação de atributos em [!DNL Salesforce Marketing Cloud].

Por exemplo, se a variável [!DNL Salesforce Marketing Cloud] atributo é `salesforce_mc_segment_1`, especifique esse valor no [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de mapeamento]** para preencher públicos-alvo de segmento do Experience Platform para este atributo.

Um exemplo de atributo de [!DNL Salesforce Marketing Cloud] é mostrado abaixo:
![Captura de tela da interface do usuário do Salesforce Marketing Cloud mostrando um atributo.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

Um exemplo indicando a localização da variável [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de mapeamento]** é mostrado abaixo:
![Exemplo de captura de tela da interface do usuário da plataforma que mostra a exportação do segmento de Programação.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

Como mostrado na [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de mapeamento]** deve corresponder exatamente ao valor especificado em [!DNL Salesforce Marketing Cloud] **[!UICONTROL NOME DO CAMPO]**.

Repita esta seção para cada segmento da Plataforma ativada.

Dependendo do caso de uso, todos os segmentos ativados podem ser mapeados para o mesmo [!DNL Salesforce Marketing Cloud] **[!UICONTROL NOME DO CAMPO]** ou a **[!UICONTROL NOME DO CAMPO]** em [!DNL (API) Salesforce Marketing Cloud]. Um exemplo típico baseado na imagem mostrada acima pode ser.
| [!DNL (API) Salesforce Marketing Cloud] nome do segmento | [!DNL Salesforce Marketing Cloud] **[!UICONTROL NOME DO CAMPO]** | [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL ID de mapeamento]** | | — | — | — | | salesforce mc segment 1 | `salesforce_mc_segment_1` | `salesforce_mc_segment_1` | | salesforce mc Segment 2 | `salesforce_mc_segment_2` | `salesforce_mc_segment_2` |

## Validar exportação de dados {#exported-data}

Para validar se você configurou o destino corretamente, siga as etapas abaixo:

1. Selecionar **[!UICONTROL Destinos]** > **[!UICONTROL Procurar]** para navegar até a lista de destinos.
   ![Captura de tela da interface do usuário da plataforma que mostra os Destinos de navegação.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. Selecione o destino e valide se o status é **[!UICONTROL ativado]**.
   ![Captura de tela da interface do usuário da plataforma que mostra a Execução do fluxo de dados de destinos.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. Alterne para **[!DNL Activation data]** e selecione um nome de segmento.
   ![Exemplo de captura de tela da interface do usuário da plataforma que mostra os Dados de ativação de destinos.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. Monitore o resumo do segmento e garanta que a contagem de perfis corresponda à contagem criada no segmento.
   ![Exemplo de captura de tela da interface do usuário da plataforma que mostra o Segmento.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. Faça logon no [[!DNL Salesforce Marketing Cloud]](https://mc.exacttarget.com/) site. Em seguida, navegue até o **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** e verificar se os perfis do segmento foram adicionados.
   ![Captura de tela da interface do usuário do Salesforce Marketing Cloud mostrando a página Contatos com perfis usados no segmento.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. Para verificar se algum perfil foi atualizado, navegue até o **[!UICONTROL Email]** e verifique se os valores do atributo do perfil do segmento foram atualizados. Se bem-sucedido, você pode ver que cada status de segmento em [!DNL Salesforce Marketing Cloud] foi atualizado com o status de segmento correspondente da Platform, com base no **[!UICONTROL ID de mapeamento]** do [agendamento de segmento](#schedule-segment-export-example) etapa.
   ![Captura de tela da interface do usuário do Salesforce Marketing Cloud mostrando a página de email de contatos selecionada com status de segmento atualizados.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](/help/data-governance/home.md).

## Erros e solução de problemas {#errors-and-troubleshooting}

### Erros desconhecidos encontrados ao enviar eventos para o Marketing Cloud Salesforce {#unknown-errors}

* Ao verificar uma execução de fluxo de dados, você pode encontrar a seguinte mensagem de erro: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

   ![Captura de tela da interface do usuário da plataforma que mostra o erro.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

   * Para corrigir esse erro, verifique se a variável **[!UICONTROL ID de mapeamento]** que você forneceu no workflow de ativação para o [!DNL (API) Salesforce Marketing Cloud] o destino corresponde exatamente ao nome do atributo que você criou em [!DNL Salesforce Marketing Cloud]. Consulte a [Criar atributo dentro de [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) seção para orientação.

* Ao ativar um segmento, você pode obter uma mensagem de erro: `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Para corrigir este erro, entre em contato com seu [!DNL Salesforce Marketing Cloud] administrador da conta para adicionar [Endereços IP de Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) para [!DNL Salesforce Marketing Cloud] intervalos IP confiáveis das contas. Consulte a [!DNL Salesforce Marketing Cloud] [Endereços IP para inclusão em Lista de permissões no Marketing Cloud](https://help.salesforce.com/s/articleView?id=sf.mc_es_ip_addresses_for_inclusion.htm&amp;type=5) documentação se precisar de orientação adicional.

## Recursos adicionais {#additional-resources}

* [!DNL Salesforce Marketing Cloud] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
* [!DNL Salesforce Marketing Cloud] [documentação](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) explicando como os contatos são atualizados com as informações especificadas nos grupos de atributos especificados.