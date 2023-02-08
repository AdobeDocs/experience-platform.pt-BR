---
keywords: crm; CRM; destinos crm; salesforce crm; destino do salesforce crm
title: Conexão Salesforce CRM
description: O destino Salesforce CRM permite exportar seus dados de conta e ativá-los no Salesforce CRM para suas necessidades comerciais.
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: edf49d8a52eeddea65a18c1dad0035ec7e5d2c12
workflow-type: tm+mt
source-wordcount: '3089'
ht-degree: 0%

---

# [!DNL Salesforce CRM] conexão

## Visão geral {#overview}

[[!DNL Salesforce CRM]](https://www.salesforce.com/crm/) O é uma plataforma popular de CRM (relacionamento com o cliente) e oferece suporte ao seguinte:

* [Clientes potenciais](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) - Um cliente potencial é o nome de uma pessoa ou empresa que pode (ou não) estar interessada nos produtos ou serviços que vende.
* [Contatos](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) - Um contato é um indivíduo com o qual um dos seus representantes estabeleceu uma relação e foi qualificado como cliente potencial.

Essa [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) utiliza o [[!DNL Salesforce composite API]](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm), que suporta ambos os tipos de perfis descritos acima.

When [ativação de segmentos](#activate), você pode selecionar entre leads ou contatos e atualizar os atributos e os dados do segmento no [!DNL Salesforce CRM].

[!DNL Salesforce CRM] O usa o OAuth 2 com concessão de senha como um mecanismo de autenticação para se comunicar com a API REST do Salesforce. Instruções para autenticação em seu [!DNL Salesforce CRM] são mais abaixo, na variável [Autenticar para destino](#authenticate) seção.

## Casos de uso {#use-cases}

Como profissional de marketing, você pode fornecer experiências personalizadas para seus usuários, com base em atributos de seus perfis do Adobe Experience Platform. Você pode criar segmentos a partir de seus dados offline e enviar esses segmentos para o Salesforce CRM, para exibir nos feeds dos usuários assim que os segmentos e os perfis forem atualizados no Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

### Pré-requisitos no Experience Platform {#prerequisites-in-experience-platform}

Antes de ativar os dados no destino do Salesforce CRM, você deve ter uma [schema](/help/xdm/schema/composition.md), a [conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)e [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) criado em [!DNL Experience Platform].

### Pré-requisitos em [!DNL Salesforce CRM] {#prerequisites-destination}

Observe os seguintes pré-requisitos em [!DNL Salesforce CRM], para exportar dados do Platform para sua conta do Salesforce:

#### Você precisa ter um [!DNL Salesforce] account {#prerequisites-account}

Vá para o [!DNL Salesforce] [avaliação](https://www.salesforce.com/in/form/signup/freetrial-sales/) página para registrar e criar uma [!DNL Salesforce] , se você ainda não tiver uma.

#### Configure um aplicativo conectado no [!DNL Salesforce] {#prerequisites-connected-app}

Primeiro, você precisa configurar um [[!DNL Salesforce] aplicativo conectado](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&amp;language=en_US&amp;r=https%3A%2F%2Fhelp.salesforce.com%2F&amp;type=5) em seu [!DNL Salesforce] , se você ainda não tiver uma. [!DNL Salesforce CRM] aproveitará o aplicativo conectado ao qual [!DNL Salesforce].

Em seguida, habilite [!DNL OAuth Settings for API Integration] para [!DNL Salesforce connected app]. Consulte a [[!DNL Salesforce]](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) documentação para orientação.

Além disso, verifique se a variável [escopos](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) mencionados abaixo são selecionados para a variável [!DNL Salesforce connected app].

* ``chatter_api``
* ``lightning``
* ``visualforce``
* ``content``
* ``openid``
* ``full``
* ``api``
* ``web``
* ``refresh_token``
* ``offline_access``

Por último, assegure que o `password` a concessão é ativada em seu [!DNL Salesforce] conta. Consulte a [!DNL Salesforce] [Fluxo de Senha do Nome de Usuário do OAuth 2.0 para Cenários Especiais](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_username_password_flow.htm&amp;type=5) documentação se precisar de orientação.

>[!IMPORTANT]
>
>Se o seu [!DNL Salesforce] o administrador da conta restringiu o acesso a intervalos IP confiáveis, é necessário contatá-los para obter [Experience Platform IP&#39;s](/help/destinations/catalog/streaming/ip-address-allow-list.md) incluir na lista de permissões. Consulte a [!DNL Salesforce] [Restringir o acesso a intervalos IP confiáveis para um aplicativo conectado](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) documentação se precisar de orientação adicional.

#### Criar campos personalizados em [!DNL Salesforce] {#prerequisites-custom-field}

Ao ativar segmentos para a [!DNL Salesforce CRM] , você deve inserir um valor na variável **[!UICONTROL ID de mapeamento]** para cada segmento ativado, no campo **[Agendamento do segmento](#schedule-segment-export-example)** etapa.

[!DNL Salesforce CRM] exige que esse valor leia e interprete corretamente os segmentos provenientes do Experience Platform e atualize seu status de segmento dentro de [!DNL Salesforce]. Consulte a documentação do Experience Platform para [Grupo de campos Detalhes da associação ao segmento](/help/xdm/field-groups/profile/segmentation.md) se você precisar de orientação sobre os status do segmento.

Para cada segmento que você ativa da plataforma para o [!DNL Salesforce CRM], é necessário criar um campo personalizado do tipo `Text Area (Long)` within [!DNL Salesforce]. Você pode definir o comprimento de caracteres de campo de qualquer tamanho entre 256 - 131.072 caracteres de acordo com sua necessidade comercial. Consulte a [!DNL Salesforce] [Tipos de campo personalizado](https://help.salesforce.com/s/articleView?id=sf.custom_field_types.htm&amp;type=5) página de documentação para obter informações adicionais sobre tipos de campos personalizados. Consulte também a [!DNL Salesforce] documentação para [criar campos personalizados](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) se precisar de assistência na criação de campos.

>[!IMPORTANT]
>
>Não inclua caracteres de espaço em branco no nome do campo. Em vez disso, use o sublinhado `(_)` como separador.
>Within [!DNL Salesforce] você deve criar campos personalizados com um **[!UICONTROL Nome do campo]** que corresponde exatamente ao valor especificado em **[!UICONTROL ID de mapeamento]** para cada segmento da plataforma ativada. Por exemplo, a captura de tela abaixo mostra um campo personalizado chamado `crm_2_seg`. Ao ativar um segmento para esse destino, adicione `crm_2_seg` as **[!UICONTROL ID de mapeamento]** para preencher públicos de segmento do Experience Platform para este campo personalizado.

Um exemplo da criação de campo personalizado em [!DNL Salesforce], *Etapa 1 - Selecionar o tipo de dados*, é mostrado abaixo:
![Captura de tela da interface do usuário do Salesforce que mostra a criação de campo personalizado, Etapa 1 - Selecione o tipo de dados.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-1.png)

Um exemplo da criação de campo personalizado em [!DNL Salesforce], *Etapa 2 - Inserir os detalhes do campo personalizado*, é mostrado abaixo:
![Captura de tela da interface do usuário do Salesforce que mostra a criação de campo personalizado, Etapa 2 - Insira os detalhes do campo personalizado.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-2.png)

>[!TIP]
>
>* Para distinguir entre campos personalizados usados para segmentos da Platform e outros campos personalizados em [!DNL Salesforce] é possível incluir um prefixo ou sufixo reconhecível ao criar o campo personalizado. Por exemplo, em vez de `test_segment`, use `Adobe_test_segment` ou `test_segment_Adobe`
>* Se você já tiver outros campos personalizados criados em [!DNL Salesforce], você pode usar o mesmo nome do segmento da Plataforma para identificar facilmente o segmento em [!DNL Salesforce].


>[!NOTE]
>
>* Objetos no Salesforce estão restritos a 25 campos externos, consulte [Atributos de campo personalizados](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
>* Essa restrição implica que você só pode ter no máximo 25 associações de Experience Platform a qualquer momento.
>* Se você atingiu esse limite no Salesforce, é necessário remover os atributos personalizados do Salesforce que foram usados para armazenar o status do segmento em relação aos segmentos mais antigos no Experience Platform antes de um novo **[!UICONTROL ID de mapeamento]** pode ser usada.


#### Colete [!DNL Salesforce CRM] credenciais {#gather-credentials}

Anote os itens abaixo antes de autenticar para o [!DNL Salesforce CRM] destino:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| `Username` | Seu [!DNL Salesforce] nome de usuário da conta. |  |
| `Password` | Seu [!DNL Salesforce] senha da conta. |  |
| `Security Token` | Seu [!DNL Salesforce] token de segurança que será anexado posteriormente ao final de seu [!DNL Salesforce] Senha para criar uma cadeia de caracteres concatenada a ser usada como **[!UICONTROL Senha]** when [autenticação no destino](#authenticate).<br> Consulte a [!DNL Salesforce] documentação para [redefinir o token de segurança](https://help.salesforce.com/s/articleView?id=sf.user_security_token.htm&amp;type=5) para aprender como regenerá-la a partir do [!DNL Salesforce] se você não tiver o Token de segurança. |  |
| `Custom Domain` | Seu [!DNL Salesforce] prefixo do domínio. <br> Consulte a [[!DNL Salesforce] documentação](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) para saber como obter esse valor do [!DNL Salesforce] interface. | Se o seu [!DNL Salesforce] domínio é<br> *`d5i000000isb4eak-dev-ed`.my.salesforce.com*,<br> você precisará `d5i000000isb4eak-dev-ed` como o valor. |
| `Client ID` | Seu Salesforce `Consumer Key`. <br> Consulte a [[!DNL Salesforce] documentação](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) para saber como obter esse valor do [!DNL Salesforce] interface. |  |
| `Client Secret` | Seu Salesforce `Consumer Secret`. <br> Consulte a [[!DNL Salesforce] documentação](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) para saber como obter esse valor do [!DNL Salesforce] interface. |  |

### Medidas de proteção {#guardrails}

[!DNL Salesforce] equilibra as cargas de transação impondo limites de solicitação, taxa e tempo limite. Consulte a [Limites e alocações de solicitação de API](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) para obter detalhes.

Se o seu [!DNL Salesforce] o administrador da conta aplicou restrições de IP, será necessário adicionar [Endereços IP de Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) para [!DNL Salesforce] intervalos IP confiáveis das contas. Consulte a [!DNL Salesforce] [Restringir o acesso a intervalos IP confiáveis para um aplicativo conectado](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) documentação se precisar de orientação adicional.

>[!IMPORTANT]
>
>When [ativação de segmentos](#activate) você deve selecionar entre *Contato* ou *Líder* tipos. É necessário garantir que seus segmentos tenham o mapeamento de dados apropriado de acordo com o tipo selecionado.

## Identidades suportadas {#supported-identities}

[!DNL Salesforce CRM] O suporta a atualização de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| `SalesforceId` | O [!DNL Salesforce CRM] identificador do contato ou identidade de cliente potencial que você exporta ou atualiza por meio de seu segmento. | Obrigatório |

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | <ul><li>Você está exportando todos os membros de um segmento, junto com os campos de esquema desejados *(por exemplo: endereço de email, número de telefone, sobrenome)*, de acordo com o mapeamento de campo.</li><li> Cada status de segmento em [!DNL Salesforce CRM] é atualizado com o status de segmento correspondente da Platform, com base no **[!UICONTROL ID de mapeamento]** valor fornecido durante a [agendamento de segmento](#schedule-segment-export-example) etapa.</li></ul> |
| Frequência de exportação | **[!UICONTROL Streaming]** | <ul><li>Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow para configurar destino , preencha os campos listados nas duas seções abaixo.

Within **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** pesquisar por [!DNL Salesforce CRM]. Como alternativa, você pode localizá-lo sob a variável **[!UICONTROL CRM]** categoria .

### Autenticar para destino {#authenticate}

Para autenticar para o destino, preencha os campos obrigatórios abaixo e selecione **[!UICONTROL Ligar ao destino]**. Consulte a [Colete [!DNL Salesforce CRM] credenciais](#gather-credentials) para quaisquer orientações.
| Credencial | Descrição | | — | — | | **[!UICONTROL Nome do usuário]** | Seu [!DNL Salesforce] nome de usuário da conta. | | **[!UICONTROL Senha]** | Uma string concatenada composta por [!DNL Salesforce] senha da conta anexada com seu [!DNL Salesforce] Token de segurança.<br>O valor concatenado assume a forma de `{PASSWORD}{TOKEN}`.<br> Observação: não use chaves ou espaços.<br>Por exemplo, se sua [!DNL Salesforce] A senha é `MyPa$$w0rd123` e [!DNL Salesforce] O token de segurança é `TOKEN12345....0000`, o valor concatenado que será usado na variável **[!UICONTROL Senha]** é `MyPa$$w0rd123TOKEN12345....0000`. | | **[!UICONTROL Domínio personalizado]** | Seu [!DNL Salesforce] prefixo do domínio. <br>Por exemplo, se o domínio for *`d5i000000isb4eak-dev-ed`.my.salesforce.com*, é necessário fornecer `d5i000000isb4eak-dev-ed` como o valor. | | **[!UICONTROL ID do cliente]** | Seu [!DNL Salesforce] aplicativo conectado `Consumer Key`. | | **[!UICONTROL Segredo do cliente]** | Seu [!DNL Salesforce] aplicativo conectado `Consumer Secret`. |

![Captura de tela da interface do usuário da plataforma que mostra como autenticar.](../../assets/catalog/crm/salesforce/authenticate-destination.png)

Se os detalhes fornecidos forem válidos, a interface do usuário exibirá uma **[!UICONTROL Conectado]** com uma marca de seleção verde, você pode prosseguir para a próxima etapa.

### Preencha os detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.
* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL Tipo de ID do Salesforce]**:
   * Selecionar **[!UICONTROL Contato]** se as identidades que você deseja exportar ou atualizar forem do tipo *Contato*.
   * Selecionar **[!UICONTROL Líder]** se as identidades que você deseja exportar ou atualizar forem do tipo *Líder*.

![Captura de tela da interface do usuário da plataforma que mostra os detalhes do destino.](../../assets/catalog/crm/salesforce/destination-details.png)

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
>
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmentos de fluxo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Considerações e exemplo de mapeamento {#mapping-considerations-example}

Para enviar corretamente os dados de público-alvo do Adobe Experience Platform para a [!DNL Salesforce CRM] , é necessário percorrer a etapa de mapeamento de campo . O mapeamento consiste em criar um link entre os campos do esquema do Modelo de dados de experiência (XDM) na conta da plataforma e os equivalentes correspondentes do destino.

Atributos especificados na **[!UICONTROL Campo de destino]** O deve ser nomeado exatamente como descrito na tabela de mapeamentos de atributo, pois esses atributos formarão o corpo da solicitação.

Atributos especificados na **[!UICONTROL Campo de origem]** não seguir tal restrição. Você pode mapeá-lo com base na sua necessidade, no entanto, verifique se o formato dos dados de entrada é válido de acordo com a variável [[!DNL Salesforce] documentação](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5). Se os dados de entrada não forem válidos, a chamada de atualização para [!DNL Salesforce] falhará e seus contatos/leads não serão atualizados.

Para mapear corretamente os campos XDM para a variável [!DNL (API) Salesforce CRM] campos de destino, siga estas etapas:

1. No **[!UICONTROL Mapeamento]** etapa , selecione **[!UICONTROL Adicionar novo mapeamento]**, você verá uma nova linha de mapeamento na tela.
   ![Exemplo de captura de tela da interface do usuário da plataforma para Adicionar novo mapeamento.](../../assets/catalog/crm/salesforce/add-new-mapping.png)
1. No **[!UICONTROL Selecionar campo de origem]** escolha a **[!UICONTROL Selecionar atributos]** e selecione o atributo XDM ou escolha a **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade.
1. No **[!UICONTROL Selecionar campo de destino]** escolha a **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade ou escolha **[!UICONTROL Selecionar atributos personalizados]** e selecione um atributo ou defina um usando o **[!UICONTROL Nome do atributo]** conforme necessário. Consulte a [[!DNL Salesforce CRM] documentação](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5) para obter orientação sobre atributos compatíveis.
   * Repita essas etapas para adicionar os seguintes mapeamentos entre o esquema de perfil XDM e [!DNL (API) Salesforce CRM]:

   **Trabalhar com contatos**

   * Se você estiver trabalhando com *Contatos* no seu segmento, consulte a Referência de objeto no Salesforce para [Contato](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) para definir mapeamentos para os campos a serem atualizados.
   * Você pode identificar campos obrigatórios pesquisando a palavra *Obrigatório*, que é mencionado nas descrições de campo no link acima.
   * Dependendo dos campos que você deseja exportar ou atualizar, adicione mapeamentos entre o esquema de perfil XDM e [!DNL (API) Salesforce CRM]: |Campo de origem|Campo de destino| Notas | | — | — | — | |`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`| |`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`. Sobrenome do contato com até 80 caracteres. |\
      |`xdm: person.name.firstName`|`Attribute: FirstName`| O nome do contato com até 40 caracteres. | |`xdm: personalEmail.address`|`Attribute: Email`| O endereço de email do contato. |

   * Um exemplo de uso desses mapeamentos é mostrado abaixo:
      ![Exemplo de captura de tela da interface do usuário da plataforma que mostra os mapeamentos do Target.](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   **Trabalhar com leads**

   * Se você estiver trabalhando com *Clientes potenciais* no seu segmento, consulte a Referência de objeto no Salesforce para [Líder](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) para definir mapeamentos para os campos a serem atualizados.
   * Você pode identificar campos obrigatórios pesquisando a palavra *Obrigatório*, que é mencionado nas descrições de campo no link acima.
   * Dependendo dos campos que você deseja exportar ou atualizar, adicione mapeamentos entre o esquema de perfil XDM e [!DNL (API) Salesforce CRM]: |Campo de origem|Campo de destino| Notas | | — | — | — | |`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`| |`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`. Sobrenome do lead até 80 caracteres. |\
      |`xdm: b2b.companyName`|`Attribute: Company`| `Mandatory`. A companhia do líder. | |`xdm: personalEmail.address`|`Attribute: Email`| O endereço de email do cliente potencial. |

   * Um exemplo de uso desses mapeamentos é mostrado abaixo:
      ![Exemplo de captura de tela da interface do usuário da plataforma que mostra os mapeamentos do Target.](../../assets/catalog/crm/salesforce/mappings-leads.png)



Quando terminar de fornecer os mapeamentos para a conexão de destino, selecione **[!UICONTROL Próximo]**.

### Programar exportação de segmento e exemplo {#schedule-segment-export-example}

Ao executar o [Agendar exportação de segmentos](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) etapa você deve mapear manualmente os segmentos ativados da Platform para seu campo personalizado correspondente em [!DNL Salesforce].

Para fazer isso, selecione cada segmento e insira o nome do campo personalizado de [!DNL Salesforce] no [!DNL Salesforce CRM] **[!UICONTROL ID de mapeamento]** campo. Consulte a [Criar campos personalizados em [!DNL Salesforce]](#prerequisites-custom-field) para obter orientação e práticas recomendadas sobre como criar campos personalizados em [!DNL Salesforce].

Por exemplo, se a variável [!DNL Salesforce] o campo personalizado é `crm_2_seg`, especifique esse valor no [!DNL Salesforce CRM] **[!UICONTROL ID de mapeamento]** para preencher públicos de segmento do Experience Platform para este campo personalizado.

Um exemplo de campo personalizado de [!DNL Salesforce] é mostrado abaixo:
![[!DNL Salesforce] Captura de tela da interface do usuário que mostra o campo personalizado.](../../assets/catalog/crm/salesforce/salesforce-custom-field.png)

Um exemplo indicando a localização da variável [!DNL Salesforce CRM] **[!UICONTROL ID de mapeamento]** é mostrado abaixo:
![Exemplo de captura de tela da interface do usuário da plataforma que mostra a exportação do segmento de Programação.](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

Como mostrado acima, [!DNL Salesforce] **[!UICONTROL Nome do campo]** corresponde exatamente ao valor especificado em [!DNL Salesforce CRM] **[!UICONTROL ID de mapeamento]**.

Dependendo do caso de uso, todos os segmentos ativados podem ser mapeados para o mesmo [!DNL Salesforce] campo personalizado ou diferente **[!UICONTROL Nome do campo]** em [!DNL Salesforce CRM]. Um exemplo típico baseado na imagem mostrada acima pode ser.
| [!DNL Salesforce CRM] nome do segmento | [!DNL Salesforce] **[!UICONTROL Nome do campo]** | [!DNL Salesforce CRM] **[!UICONTROL ID de mapeamento]** | | — | — | — | | crm_1_seg | `crm_1_seg` | `crm_1_seg` | | crm_2_seg | `crm_2_seg` | `crm_2_seg` |

Repita esta seção para cada segmento da Plataforma ativada.

## Validar exportação de dados {#exported-data}

Para validar se você configurou o destino corretamente, siga as etapas abaixo:

1. Selecionar **[!UICONTROL Destinos]** > **[!UICONTROL Procurar]** para navegar até a lista de destinos.
   ![Captura de tela da interface do usuário da plataforma que mostra os Destinos de navegação.](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. Selecione o destino e valide se o status é **[!UICONTROL ativado]**.
   ![Captura de tela da interface do usuário da plataforma que mostra a Execução do fluxo de dados de destinos.](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. Alterne para **[!UICONTROL Dados de ativação]** e selecione um nome de segmento.
   ![Exemplo de captura de tela da interface do usuário da plataforma que mostra os Dados de ativação de destinos.](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. Monitore o resumo do segmento e garanta que a contagem de perfis corresponda à contagem criada no segmento.
   ![Exemplo de captura de tela da interface do usuário da plataforma que mostra o Segmento.](../../assets/catalog/crm/salesforce/segment.png)

1. Por fim, faça logon no site do Salesforce e valide se os perfis do segmento foram adicionados ou atualizados.

   **Trabalhar com contatos**

   * Se você selecionou *Contatos* no segmento Plataforma , navegue até o **[!DNL Apps]** > **[!DNL Contacts]** página.
      ![Captura de tela do Salesforce CRM mostrando a página Contatos com os perfis do segmento.](../../assets/catalog/crm/salesforce/contacts.png)

   * Selecione um *Contato* e verifique se os campos foram atualizados. Você pode ver que cada status de segmento em [!DNL Salesforce CRM] foi atualizado com o status de segmento correspondente da Platform, com base no **[!UICONTROL ID de mapeamento]** valor fornecido durante a [agendamento de segmento](#schedule-segment-export-example).
      ![Captura de tela do Salesforce CRM mostrando a página Detalhes do contato com status de segmento atualizados.](../../assets/catalog/crm/salesforce/contact-info.png)

   **Trabalhar com leads**

   * Se você selecionou *Clientes potenciais* no segmento Plataforma , navegue até a **[!DNL Apps]** > **[!DNL Leads]** página.
      ![Captura de tela do Salesforce CRM mostrando a página Leads com os perfis do segmento.](../../assets/catalog/crm/salesforce/leads.png)

   * Selecione um *Líder* e verifique se os campos foram atualizados. Você pode ver que cada status de segmento em [!DNL Salesforce CRM] foi atualizado com o status de segmento correspondente da Platform, com base no **[!UICONTROL ID de mapeamento]** valor fornecido durante a [agendamento de segmento](#schedule-segment-export-example).
      ![Captura de tela do Salesforce CRM mostrando a página Detalhes do cliente potencial com status de segmento atualizados.](../../assets/catalog/crm/salesforce/lead-info.png)


## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](/help/data-governance/home.md).

## Erros e solução de problemas {#errors-and-troubleshooting}

### Erros desconhecidos encontrados ao enviar eventos para o destino {#unknown-errors}

* Ao verificar uma execução de fluxo de dados, você pode encontrar a seguinte mensagem de erro: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

   ![Captura de tela da interface do usuário da plataforma que mostra o erro.](../../assets/catalog/crm/salesforce/error.png)

   * Para corrigir esse erro, verifique se a variável **[!UICONTROL ID de mapeamento]** que você forneceu no workflow de ativação para o [!DNL Salesforce CRM] o destino corresponde exatamente ao valor do tipo de campo personalizado criado em [!DNL Salesforce]. Consulte a [Criar campos personalizados em [!DNL Salesforce]](#prerequisites-custom-field) seção para orientação.

* Ao ativar um segmento, você pode obter uma mensagem de erro: `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Para corrigir este erro, entre em contato com seu [!DNL Salesforce] administrador da conta para adicionar [Endereços IP de Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) para [!DNL Salesforce] intervalos IP confiáveis das contas. Consulte a [!DNL Salesforce] [Restringir o acesso a intervalos IP confiáveis para um aplicativo conectado](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) documentação se precisar de orientação adicional.

## Recursos adicionais {#additional-resources}

Informações úteis adicionais da [Portal do desenvolvedor do Salesforce](https://developer.salesforce.com/) está abaixo:
* [Início rápido](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [Criar um registro](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [Públicos-alvo de recomendação personalizados](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [Uso de recursos compostos](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* Esse destino aproveita o [Atualizar vários registros](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) API em vez de [Upsert Single Record](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) Chamada de API.