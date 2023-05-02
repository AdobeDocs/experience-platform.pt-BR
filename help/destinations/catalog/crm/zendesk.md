---
title: Conexão com o Zendesk
description: O destino do Zendesk permite exportar seus dados de conta e ativá-los no Zendesk para atender às suas necessidades comerciais.
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 55f1eafa68124b044d20f8f909f6238766076a7a
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 1%

---

# [!DNL Zendesk] conexão

[[!DNL Zendesk]](https://www.zendesk.com) O é uma solução de atendimento ao cliente e uma ferramenta de vendas.

Essa [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) utiliza o [[!DNL Zendesk] API de contatos](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/)para **criar e atualizar identidades** em um segmento como contatos dentro de [!DNL Zendesk].

[!DNL Zendesk] O usa os tokens do portador como um mecanismo de autenticação para se comunicar com o [!DNL Zendesk] API de contatos. Instruções para autenticação em seu [!DNL Zendesk] são mais abaixo, na variável [Autenticar para destino](#authenticate) seção.

## Casos de uso {#use-cases}

O departamento de atendimento ao cliente de uma plataforma B2C multicanal deseja garantir uma experiência personalizada contínua para seus clientes. O departamento pode criar segmentos a partir de seus próprios dados offline para criar novos perfis de usuário ou atualizar informações de perfil existentes a partir de diferentes interações (por exemplo, compras, devoluções etc.) e enviar esses segmentos do Adobe Experience Platform para o [!DNL Zendesk]. Ter as informações atualizadas em [!DNL Zendesk] garante que o agente de atendimento ao cliente tenha as informações recentes do cliente imediatamente disponíveis, permitindo respostas e resolução mais rápidas.

## Pré-requisitos {#prerequisites}

### Pré-requisitos do Experience Platform {#prerequisites-in-experience-platform}

Antes de ativar os dados para o [!DNL Zendesk] destino, você deve ter um [schema](/help/xdm/schema/composition.md), a [conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)e [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) criado em [!DNL Experience Platform].

Consulte a documentação do Experience Platform para [Grupo de campos Detalhes da associação ao segmento](/help/xdm/field-groups/profile/segmentation.md) se você precisar de orientação sobre os status do segmento.

### [!DNL Zendesk] pré-requisitos {#prerequisites-destination}

Para exportar dados da Platform para seu [!DNL Zendesk] conta que você precisa ter uma [!DNL Zendesk] conta.

#### Colete [!DNL Zendesk] credenciais {#gather-credentials}

Anote os itens abaixo antes de autenticar para o [!DNL Zendesk] destino:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| `Bearer token` | O token de acesso gerado em seu [!DNL Zendesk] conta. <br> Siga a documentação para [gerar um [!DNL Zendesk] token de acesso](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) se não tiver um. | `a0b1c2d3e4...v20w21x22y23z` |

## Medidas de proteção {#guardrails}

O [Preços e limites de taxa](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) detalha a página [!DNL Zendesk] Limites de API associados à sua conta. Você precisa garantir que seus dados e carga estejam dentro dessas restrições.

## Identidades suportadas {#supported-identities}

[!DNL Zendesk] O suporta a atualização de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Exemplo | Descrição | Obrigatório |
|---|---|---|---|
| `email` | `test@test.com` | Endereço de email do contato. | Sim |

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | <ul><li>Você está exportando todos os membros de um segmento, junto com os campos de esquema desejados *(por exemplo: endereço de email, número de telefone, sobrenome)*, de acordo com o mapeamento de campo.</li><li> Cada status de segmento em [!DNL Zendesk] é atualizado com o status de segmento correspondente da Platform, com base no **[!UICONTROL ID de mapeamento]** valor fornecido durante a [agendamento de segmento](#schedule-segment-export-example) etapa.</li></ul> |
| Frequência de exportação | **[!UICONTROL Streaming]** | <ul><li>Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow para configurar destino , preencha os campos listados nas duas seções abaixo.

Within **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** pesquisar por [!DNL Zendesk]. Como alternativa, você pode localizá-lo sob a variável **[!UICONTROL CRM]** categoria .

### Autenticar para destino {#authenticate}

Preencha os campos obrigatórios abaixo. Consulte a [Colete [!DNL Zendesk] credenciais](#gather-credentials) para quaisquer orientações.
* **[!UICONTROL Token do portador]**: O Token de acesso gerado em seu [!DNL Zendesk] conta.

Para autenticar para o destino, selecione **[!UICONTROL Ligar ao destino]**.
![Captura de tela da interface do usuário da plataforma que mostra como autenticar.](../../assets/catalog/crm/zendesk/authenticate-destination.png)

Se os detalhes fornecidos forem válidos, a interface do usuário exibirá uma **[!UICONTROL Conectado]** status com uma marca de seleção verde. Você pode prosseguir para a próxima etapa.

### Preencha os detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.
![Captura de tela da interface do usuário da plataforma que mostra os detalhes do destino.](../../assets/catalog/crm/zendesk/destination-details.png)

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

Para enviar corretamente os dados de público-alvo do Adobe Experience Platform para a [!DNL Zendesk] , é necessário percorrer a etapa de mapeamento de campo . O mapeamento consiste em criar um link entre os campos do esquema do Modelo de dados de experiência (XDM) na conta da plataforma e os equivalentes correspondentes do destino.

Atributos especificados na **[!UICONTROL Campo de destino]** O deve ser nomeado exatamente como descrito na tabela de mapeamentos de atributo, pois esses atributos formarão o corpo da solicitação.

Atributos especificados na **[!UICONTROL Campo de origem]** não seguir tal restrição. Você pode mapeá-lo com base em sua necessidade, no entanto, se o formato de dados não estiver correto quando enviado para o [!DNL Zendesk] isso resultará em um erro.

Para mapear corretamente os campos XDM para a variável [!DNL Zendesk] campos de destino, siga estas etapas:

1. No **[!UICONTROL Mapeamento]** etapa , selecione **[!UICONTROL Adicionar novo mapeamento]**. Você verá uma nova linha de mapeamento na tela.
1. No **[!UICONTROL Selecionar campo de origem]** escolha a **[!UICONTROL Selecionar atributos]** e selecione o atributo XDM ou escolha a **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade.
1. No **[!UICONTROL Selecionar campo de destino]** escolha a **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade de destino ou escolha a **[!UICONTROL Selecionar atributos]** e selecione um dos atributos de esquema compatíveis.
   * Repita essas etapas para adicionar os seguintes mapeamentos obrigatórios, você também pode adicionar outros atributos que deseja atualizar entre o esquema de perfil XDM e o esquema [!DNL Zendesk] instância: |Campo de Origem|Campo de Destino| Obrigatório| |—|—| |`xdm: person.name.lastName`|`xdm: last_name`| Sim | |`IdentityMap: Email`|`Identity: email`| Sim | |`xdm: person.name.firstName`|`xdm: first_name`| |

   * Um exemplo de uso desses mapeamentos é mostrado abaixo:
      ![Exemplo de captura de tela da interface do usuário da plataforma com mapeamentos de atributo.](../../assets/catalog/crm/zendesk/mappings.png)

>[!IMPORTANT]
>
>O `Attribute: last_name` e `Identity: email` os target mappings são obrigatórios para este destino. Se esses mapeamentos estiverem ausentes, quaisquer outros mapeamentos serão ignorados e não serão enviados para [!DNL Zendesk].

Quando terminar de fornecer os mapeamentos para a conexão de destino, selecione **[!UICONTROL Próximo]**.

### Programar exportação de segmento e exemplo {#schedule-segment-export-example}

No [[!UICONTROL Agendar exportação de segmentos]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) etapa do fluxo de trabalho de ativação, você deve mapear manualmente os segmentos da Platform para o atributo de campo personalizado em [!DNL Zendesk].

Para fazer isso, selecione cada segmento e insira o atributo de campo personalizado correspondente de [!DNL Zendesk] no **[!UICONTROL ID de mapeamento]** campo.

Um exemplo é mostrado abaixo:
![Exemplo de captura de tela da interface do usuário da plataforma que mostra a exportação do segmento de Programação.](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## Validar exportação de dados {#exported-data}

Para validar se você configurou o destino corretamente, siga as etapas abaixo:

1. Selecionar **[!UICONTROL Destinos]** > **[!UICONTROL Procurar]** e navegue até a lista de destinos.
1. Em seguida, selecione o destino e alterne para a **[!UICONTROL Dados de ativação]** e selecione um nome de segmento.
   ![Exemplo de captura de tela da interface do usuário da plataforma que mostra os Dados de ativação de destinos.](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. Monitore o resumo do segmento e garanta que a contagem de perfis corresponda à contagem no segmento.
   ![Exemplo de captura de tela da interface do usuário da plataforma que mostra o Segmento.](../../assets/catalog/crm/zendesk/segment.png)

1. Faça logon no [!DNL Zendesk] e navegue até o **[!UICONTROL Contatos]** para verificar se os perfis do segmento foram adicionados. Essa lista pode ser configurada para exibir colunas para os campos adicionais criados com o segmento **[!UICONTROL ID de mapeamento]** e do segmento.
   ![Captura de tela da interface do usuário do Zendesk mostrando a página Contatos com os campos adicionais criados com o nome do segmento.](../../assets/catalog/crm/zendesk/contacts.png)

1. Como alternativa, você pode fazer drill-down em um **[!UICONTROL Pessoa]** e verifique a **[!UICONTROL Campos adicionais]** seção exibindo o nome do segmento e os status do segmento.
   ![Captura de tela da interface do usuário do Zendesk mostrando a página Pessoa com a seção de campos adicionais exibindo o nome do segmento e os status do segmento.](../../assets/catalog/crm/zendesk/contact.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

Informações úteis adicionais da [!DNL Zendesk] a documentação está abaixo:
* [Efetuar sua primeira chamada](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [Campos personalizados](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)

### Changelog

Esta seção captura a funcionalidade e atualizações significativas de documentação feitas neste conector de destino.

+++ Exibir log de alterações

| Mês de lançamento | Tipo de atualização | Descrição |
|---|---|---|
| Abril de 2023 | Atualização da documentação | <ul><li>Atualizamos o [casos de uso](#use-cases) com um exemplo mais claro de quando os clientes se beneficiariam com o uso desse destino.</li> <li>Atualizamos o [mapeamento](#mapping-considerations-example) para refletir os mapeamentos necessários corretos. O `Attribute: last_name` e `Identity: email` os target mappings são obrigatórios para este destino. Se esses mapeamentos estiverem ausentes, quaisquer outros mapeamentos serão ignorados e não serão enviados para [!DNL Zendesk].</li> <li>Atualizamos o [mapeamento](#mapping-considerations-example) com exemplos claros de mapeamentos obrigatórios e opcionais.</li></ul> |
| Março de 2023 | Versão inicial | Versão inicial de destino e publicação de documentação. |

{style="table-layout:auto"}

+++