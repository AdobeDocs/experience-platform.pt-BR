---
keywords: Experience Platform;Zendesk;fontes;conectores;conectores de origem;fontes sdk;sdk;SDK;zendesk;Zendesk
title: Criar uma conexão de origem do Zendesk na interface
description: Saiba como criar uma conexão de origem do Zendesk usando a interface do Adobe Experience Platform.
exl-id: 75d303b0-2dcd-4202-987c-fe3400398d90
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 6%

---

# (Beta) Criar um [!DNL Zendesk] conexão de origem na interface

>[!NOTE]
>
>A variável [!DNL Zendesk] a fonte está na versão beta. Consulte a [visão geral das origens](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

Este tutorial fornece etapas para a criação de um [!DNL Zendesk] conexão de origem usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

### Coletar credenciais necessárias

Para acessar seu [!DNL Zendesk] na Platform, você deve fornecer valores para as seguintes credenciais:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| Subdomain | O domínio exclusivo específico da sua conta criado durante o processo de registro. | `yoursubdomain` |
| Token de acesso | Token da API do Zendesk. | `0lZnClEvkJSTQ7olGLl7PMhVq99gu26GTbJtf` |

Para obter mais informações sobre a autenticação do [!DNL Zendesk] fonte, consulte o [[!DNL Zendesk] visão geral da origem](../../../../connectors/customer-success/zendesk.md).

![Token de API do Zendesk](../../../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

### Criar um esquema da Platform para [!DNL Zendesk]

Antes de criar uma [!DNL Zendesk] conexão de origem, você também deve garantir que primeiro crie um esquema da Platform para usar em sua origem. Veja o tutorial sobre [criação de um schema do Platform](../../../../../xdm/schema/composition.md) para obter etapas abrangentes sobre como criar um schema.

Para obter orientação adicional sobre o [!DNL Zendesk] esquema necessário para o [!DNL Zendesk Search API], consulte o [limites](#limits) abaixo.

![Criar esquema](../../../../images/tutorials/create/zendesk/schema.png)

## Conecte seu [!DNL Zendesk] account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No *Sucesso do cliente* categoria, selecione **[!UICONTROL Zendesk]** e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/zendesk/catalog.png)

A variável **[!UICONTROL Conectar a conta do Zendesk]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a variável *Zendesk* conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próxima]** para continuar.

![existente](../../../../images/tutorials/create/zendesk/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas credenciais. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

![novo](../../../../images/tutorials/create/zendesk/new.png)

### Selecionar dados

Depois que a fonte é autenticada, a página é atualizada em uma árvore de esquema interativa que permite explorar e inspecionar a hierarquia dos dados. Selecionar **[!UICONTROL Próxima]** para continuar.

![select-data](../../../../images/tutorials/create/zendesk/select-data.png)

## Próximas etapas

Ao seguir este tutorial, você autenticou e criou uma conexão de origem entre [!DNL Zendesk] conta e plataforma. Agora você pode seguir para o próximo tutorial e [criar um fluxo de dados para trazer os dados de sucesso do cliente para a Platform](../../dataflow/customer-success.md).

## Recursos adicionais

As seções abaixo fornecem recursos adicionais que você pode consultar ao usar o [!DNL Zendesk] origem.

### Validação {#validation}

As etapas a seguir descrevem as etapas que você pode seguir para validar se conectou com êxito o [!DNL Zendesk] fonte e que [!DNL Zendesk] perfis estão sendo assimilados na Platform.

Na interface do usuário da Platform, selecione **[!UICONTROL Conjuntos de dados]** na navegação à esquerda, para acessar a [!UICONTROL Conjuntos de dados] espaço de trabalho. A variável [!UICONTROL Atividade do conjunto de dados] exibe os detalhes das execuções.

![Página Atividade](../../../../images/tutorials/create/zendesk/dataset-activity.png)

Em seguida, selecione a ID de execução do fluxo de dados que deseja exibir para ver detalhes específicos sobre essa execução do fluxo de dados.

![Página de fluxo de dados](../../../../images/tutorials/create/zendesk/dataflow-monitoring.png)

Finalmente, selecione **[!UICONTROL Visualizar conjunto de dados]** para exibir os dados assimilados.

![Conjunto de dados do Zendesk](../../../../images/tutorials/create/zendesk/preview-dataset.png)

Você também pode verificar seus dados da Platform em relação aos dados em sua [!DNL Zendesk] > [!DNL Customers] página.

![zendesk-customers](../../../../images/tutorials/create/zendesk/zendesk-customers.png)

### Esquema do Zendesk

A tabela abaixo lista os mapeamentos suportados que devem ser configurados para o Zendesk.

>[!TIP]
>
>Consulte [API do Zendesk Search > Exportar resultados da pesquisa](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) para obter mais informações sobre a API.

| Fonte | Tipo |
|---|---|
| `results.active` | Booleano |
| `results.alias` | String |
| `results.created_at` | String |
| `results.custom_role_id` | Número inteiro |
| `results.default_group_id` | Número inteiro |
| `results.details` | String |
| `results.email` | String |
| `results.external_id` | Número inteiro |
| `results.iana_time_zone` | String |
| `results.id` | Número inteiro |
| `results.last_login_at` | String |
| `results.locale` | String |
| `results.locale_id` | Número inteiro |
| `results.moderator` | Booleano |
| `results.name` | String |
| `results.notes` | String |
| `results.only_private_comments` | Booleano |
| `results.organization_id` | Número inteiro |
| `results.phone` | String |
| `results.photo` | String |
| `results.report_csv` | Booleano |
| `results.restricted_agent` | Booleano |
| `results.result_type` | String |
| `results.role` | String |
| `results.role_type` | Número inteiro |
| `results.shared` | Booleano |
| `results.shared_agent` | Booleano |
| `results.shared_phone_number` | Booleano |
| `results.signature` | String |
| `results.suspended` | Booleano |
| `results.ticket_restriction` | String |
| `results.time_zone` | String |
| `results.two_factor_auth_enabled` | Booleano |
| `results.updated_at` | String |
| `results.url` | String |
| `results.verified` | Booleano |

{style="table-layout:auto"}

### Limites {#limits}

* A variável [API do Zendesk Search > Exportar resultados da pesquisa](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) retorna no máximo 1000 registros por página.
   * O valor para a variável ``filter[type]`` está definido como ``user`` e, portanto, a conexão do Zendesk só retorna usuários.
   * O número de resultados por página é gerenciado pelo ``page[size]`` parâmetro. O valor está definido como ``100``. Isso é feito para reduzir o impacto das restrições de redução de velocidade definidas pelo Zendesk.
   * Consulte [Limites](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#limits) e [Paginação](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#pagination-1).
   * Também é possível consultar [Paginação em listas usando a paginação de cursor](https://developer.zendesk.com/documentation/developer-tools/pagination/paginating-through-lists-using-cursor-pagination/).
