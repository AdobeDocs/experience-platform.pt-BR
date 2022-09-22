---
keywords: crm; CRM; destinos crm; salesforce crm; destino do salesforce crm
title: Conexão Salesforce CRM
description: O destino Salesforce CRM permite exportar seus dados de conta e ativá-los no Salesforce CRM para suas necessidades comerciais.
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: b243a5f88cadc238ac3edd3bf45a54564598bbf0
workflow-type: tm+mt
source-wordcount: '2256'
ht-degree: 1%

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

#### Você precisa ter uma conta do Salesforce {#prerequisites-account}

Ir para o Salesforce [avaliação](https://www.salesforce.com/in/form/signup/freetrial-sales/) para registrar e criar uma conta do Salesforce, se você ainda não tiver uma.

#### Configurar um aplicativo conectado {#prerequisites-connected-app}

Em seguida, é necessário configurar um [aplicativo conectado](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&amp;language=en_US&amp;r=https%3A%2F%2Fhelp.salesforce.com%2F&amp;type=5) na conta do Salesforce, se você ainda não tiver uma.

No aplicativo conectado, verifique se [Configurações de OAuth](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) estiver ativado.

Certifique-se também de que [escopos](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) são selecionados os mencionados abaixo.

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

#### Criar campo personalizado no Salesforce {#prerequisites-custom-field}

Criar o campo personalizado do tipo `Text Area Long`, que Experience Platform usará para atualizar o status do segmento em [!DNL Salesforce CRM].
Consulte a documentação do Salesforce para [criar campos personalizados](https://help.salesforce.com/s/articleView?id=sf.adding_fields.htm&amp;type=5) se precisar de orientação adicional.

>[!IMPORTANT]
>
>Verifique se não há caracteres de espaço em branco no nome do campo. Em vez disso, use o sublinhado `(_)` como separador.

>[!NOTE]
>
>* Objetos no Salesforce estão restritos a 25 campos externos, consulte [Atributos de campo personalizados](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
>* Essa restrição implica que você só pode ter no máximo 25 associações de Experience Platform a qualquer momento.
>* Se você atingiu esse limite no Salesforce, é necessário remover o atributo personalizado do Salesforce que foi usado para armazenar o status do segmento em relação aos segmentos mais antigos no Experience Platform antes de um novo **[!UICONTROL ID de mapeamento]** pode ser usada.


Consulte a documentação da Adobe Experience Platform para [Grupo de campos Detalhes da associação ao segmento](/help/xdm/field-groups/profile/segmentation.md) se você precisar de orientação sobre os status do segmento.

#### Obter credenciais do Salesforce {#gather-credentials}

Anote os itens abaixo antes de autenticar para o [!DNL Salesforce CRM] destino:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| <ul><li>Prefixo de domínio do Salesforce</li></ul> | Consulte [Prefixo de domínio do Salesforce](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) para obter orientações adicionais. | <ul><li>Se o seu domínio for como abaixo, você precisará do valor destacado.<br> <i>`d5i000000isb4eak-dev-ed`.my.salesforce.com</i></li></ul> |
| <ul><li>Chave do consumidor</li><li>Segredo do consumidor</li></ul> | Consulte a [Documentação do Salesforce](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) se precisar de orientação adicional. | <ul><li>r23kxxxxxxxx0z05xxxxxx</code></li><li>ipxxxxxxxxxxxT4xxxxxxxxxxx</code></li></ul> |

### Medidas de proteção {#guardrails}

O Salesforce equilibra as cargas de transação impondo limites de solicitação, taxa e tempo limite. Consulte a [Limites e alocações de solicitação de API](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) para obter detalhes.

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

Para autenticar para o destino, preencha os campos obrigatórios e selecione **[!UICONTROL Ligar ao destino]**.

![Captura de tela da interface do usuário da plataforma que mostra como autenticar.](../../assets/catalog/crm/salesforce/authenticate-destination.png)

* **[!UICONTROL Senha]**: Sua senha da conta do Salesforce.
* **[!UICONTROL Domínio personalizado]**: Seu domínio do Salesforce.
* **[!UICONTROL ID do cliente]**: Sua Chave de consumidor do aplicativo conectado do Salesforce.
* **[!UICONTROL Segredo do cliente]**: Seu Segredo do Consumidor do aplicativo conectado do Salesforce.
* **[!UICONTROL Nome do usuário]**: Seu nome de usuário da conta do Salesforce.

Se os detalhes fornecidos forem válidos, a interface do usuário exibirá uma **[!UICONTROL Conectado]** com uma marca de seleção verde, você pode prosseguir para a próxima etapa.

### Preencha os detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.
![Captura de tela da interface do usuário da plataforma que mostra os detalhes do destino.](../../assets/catalog/crm/salesforce/destination-details.png)

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.
* **[!UICONTROL Tipo de ID do Salesforce]**: Selecionar **[!UICONTROL Contato]** se as identidades que você deseja exportar ou atualizar forem do tipo *Contato*. Selecionar **[!UICONTROL Líder]** se as identidades que você deseja exportar ou atualizar forem do tipo *Líder*.

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
>
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmentos de fluxo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Considerações e exemplo de mapeamento {#mapping-considerations-example}

Para enviar corretamente os dados de público-alvo do Adobe Experience Platform para a [!DNL Salesforce CRM] , é necessário percorrer a etapa de mapeamento de campo . O mapeamento consiste em criar um link entre os campos do esquema do Modelo de dados de experiência (XDM) na conta da plataforma e os equivalentes correspondentes do destino. Para mapear corretamente os campos XDM para a variável [!DNL Salesforce CRM] campos de destino, siga estas etapas:

1. No **[!UICONTROL Mapeamento]** etapa , selecione **[!UICONTROL Adicionar novo mapeamento]**, você verá uma nova linha de mapeamento na tela.
   ![Exemplo de captura de tela da interface do usuário da plataforma para Adicionar novo mapeamento.](../../assets/catalog/crm/salesforce/add-new-mapping.png)

1. No **[!UICONTROL Selecionar campo de origem]** escolha a **[!UICONTROL Selecionar namespace de identidade]** ou **[!UICONTROL Selecionar atributos]** categoria e selecione `crmID`.
   ![Exemplo de captura de tela da interface do usuário da plataforma para o mapeamento da fonte.](../../assets/catalog/crm/salesforce/source-mapping.png)

1. No **[!UICONTROL Selecionar campo de destino]** escolha a **[!UICONTROL Selecionar namespace de identidade]** categoria e selecione `SalesforceId`.
   ![Captura de tela da interface do usuário da plataforma que mostra o mapeamento do Target para SalesforceId.](../../assets/catalog/crm/salesforce/target-mapping-salesforceid.png)

   * Adicione o seguinte mapeamento entre o esquema de perfil XDM e o [!DNL Salesforce CRM] instância:
   | Esquema de perfil do XDM | [!DNL Salesforce CRM] Instância | Obrigatório |
   |---|---|---|
   | `crmID` | `SalesforceId` | Sim |

   * **[!UICONTROL Selecionar atributos personalizados]**: selecione essa opção para mapear o campo de origem para um atributo personalizado definido na variável **[!UICONTROL Nome do atributo]** campo. Consulte a [[!DNL Salesforce CRM] documentação](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5) para obter orientação sobre atributos compatíveis.
      ![Captura de tela da interface do usuário da plataforma que mostra o mapeamento do Target para LastName.](../../assets/catalog/crm/salesforce/target-mapping-lastname.png)

   * Se você estiver trabalhando com *Contatos* no seu segmento, consulte a Referência de objeto no Salesforce para [Contato](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) para definir mapeamentos para os campos a serem atualizados.
   * Você pode identificar campos obrigatórios pesquisando a palavra *Obrigatório*, que é mencionado nas descrições de campo no link acima.
   * Dependendo dos campos que você deseja exportar ou atualizar, adicione mapeamentos entre o esquema de perfil XDM e o [!DNL Salesforce CRM] instância:

   | Esquema de perfil do XDM | [!DNL Salesforce CRM] Instância | Notas |
   | --- | --- | --- |
   | `person.name.lastName` | `LastName` | `Required`. Sobrenome do contato com até 80 caracteres. |
   | `person.name.firstName` | `FirstName` | O nome do contato com até 40 caracteres. |
   | `personalEmail.address` | `Email` | O endereço de email do contato. |

   * Um exemplo de uso desses mapeamentos é mostrado abaixo:
      ![Exemplo de captura de tela da interface do usuário da plataforma que mostra os mapeamentos do Target.](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   * Se você estiver trabalhando com *Clientes potenciais* no seu segmento, consulte a Referência de objeto no Salesforce para [Líder](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) para definir mapeamentos para os campos a serem atualizados.
   * Você pode identificar campos obrigatórios pesquisando a palavra *Obrigatório*, que é mencionado nas descrições de campo no link acima.
   * Dependendo dos campos que você deseja exportar ou atualizar, adicione mapeamentos entre o esquema de perfil XDM e o [!DNL Salesforce CRM] instância:

   | Esquema de perfil do XDM | [!DNL Salesforce CRM] Instância | Notas |
   | --- | --- | --- |
   | `person.name.lastName` | `LastName` | `Required`. Sobrenome do contato com até 80 caracteres. |
   | `b2b.companyName` | `Company` | `Required`. A companhia do líder. |
   | `personalEmail.address` | `Email` | O endereço de email do contato. |

   * Um exemplo de uso desses mapeamentos é mostrado abaixo:
      ![Exemplo de captura de tela da interface do usuário da plataforma que mostra os mapeamentos do Target.](../../assets/catalog/crm/salesforce/mappings-leads.png)




### Programar exportação de segmento e exemplo {#schedule-segment-export-example}

Ao executar o [Agendar exportação de segmentos](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) etapa você deve mapear manualmente os segmentos da Platform para o atributo de campo personalizado no Salesforce.

Para fazer isso, selecione cada segmento e insira o atributo de campo personalizado correspondente do Salesforce no **[!UICONTROL ID de mapeamento]** campo.

>[!IMPORTANT]
>
>* O valor usado para a variável **[!UICONTROL ID de mapeamento]** deve corresponder exatamente ao nome do atributo de campo personalizado criado no Salesforce.
>* Certifique-se de que o nome do atributo de campo personalizado que você criou no Salesforce não use o caractere de espaço em branco.


Um exemplo é mostrado abaixo:
![Exemplo de captura de tela da interface do usuário da plataforma que mostra a exportação do segmento de Programação.](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

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
   * Se tiver tido *Contatos* no segmento Plataforma , navegue até o **[!DNL Apps]** > **[!DNL Contacts]** página.
      ![Captura de tela do Salesforce CRM mostrando a página Contatos com os perfis do segmento.](../../assets/catalog/crm/salesforce/contacts.png)

   * Selecione um *Contato* e verifique se os campos foram atualizados. Você pode ver que cada status de segmento em [!DNL Salesforce CRM] foi atualizado com o status de segmento correspondente da Platform, com base no **[!UICONTROL ID de mapeamento]** valor fornecido durante a [agendamento de segmento](#schedule-segment-export-example).
      ![Captura de tela do Salesforce CRM mostrando a página Detalhes do contato com status de segmento atualizados.](../../assets/catalog/crm/salesforce/contact-info.png)

   * Se tiver tido *Clientes potenciais* no segmento Plataforma , navegue até a **[!DNL Apps]** > **[!DNL Leads]** página.
      ![Captura de tela do Salesforce CRM mostrando a página Leads com os perfis do segmento.](../../assets/catalog/crm/salesforce/leads.png)

   * Selecione um *Líder* e verifique se os campos foram atualizados. Você pode ver que cada status de segmento em [!DNL Salesforce CRM] foi atualizado com o status de segmento correspondente da Platform, com base no **[!UICONTROL ID de mapeamento]** valor fornecido durante a [agendamento de segmento](#schedule-segment-export-example).
      ![Captura de tela do Salesforce CRM mostrando a página Detalhes do cliente potencial com status de segmento atualizados.](../../assets/catalog/crm/salesforce/lead-info.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](/help/data-governance/home.md).

## Erros e solução de problemas {#errors-and-troubleshooting}

### Erros desconhecidos encontrados ao enviar eventos para o destino {#unknown-errors}

Ao verificar uma execução de fluxo de dados, se você obter a seguinte mensagem de erro: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

![Captura de tela da interface do usuário da plataforma que mostra o erro.](../../assets/catalog/crm/salesforce/error.png)

Para corrigir esse erro, verifique se a variável **[!UICONTROL ID de mapeamento]** você forneceu [!DNL Salesforce CRM] para seu segmento da Platform é válido e existe em [!DNL Salesforce CRM].

## Recursos adicionais {#additional-resources}

Informações úteis adicionais da [Portal do desenvolvedor do Salesforce](https://developer.salesforce.com/) está abaixo:
* [Início rápido](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [Criar um registro](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [Públicos-alvo de recomendação personalizados](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [Uso de recursos compostos](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* Esse destino aproveita o [Atualizar vários registros](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) API em vez de [Upsert Single Record](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) Chamada de API.