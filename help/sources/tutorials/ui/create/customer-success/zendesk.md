---
title: Criar uma conexão do Zendesk Source na interface
description: Saiba como criar uma conexão de origem do Zendesk usando a interface do Adobe Experience Platform.
exl-id: 75d303b0-2dcd-4202-987c-fe3400398d90
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 7%

---

# Criar uma conexão de origem [!DNL Zendesk] na interface

Este tutorial fornece etapas para criar uma conexão de origem [!DNL Zendesk] usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

### Coletar credenciais necessárias

Para acessar sua conta do [!DNL Zendesk] no Experience Platform, você deve fornecer valores para as seguintes credenciais:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| Subdomínio | O domínio exclusivo específico da sua conta criado durante o processo de registro. | `yoursubdomain` |
| Token de acesso | Token da API do Zendesk. | `0lZnClEvkJSTQ7olGLl7PMhVq99gu26GTbJtf` |

Para obter mais informações sobre como autenticar sua origem [!DNL Zendesk], consulte a [[!DNL Zendesk] visão geral da origem](../../../../connectors/customer-success/zendesk.md).

![Token de API do Zendesk](../../../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

### Criar um esquema do Experience Platform para [!DNL Zendesk]

Antes de criar uma conexão de origem [!DNL Zendesk], você também deve garantir que primeiro crie um esquema do Experience Platform para usar na sua origem. Consulte o tutorial sobre [criação de um esquema do Experience Platform](../../../../../xdm/schema/composition.md) para obter etapas abrangentes sobre como criar um esquema.

Para obter orientação adicional sobre o esquema [!DNL Zendesk] necessário para o [!DNL Zendesk Search API], consulte a seção [limites](#limits) abaixo.

![Criar Esquema](../../../../images/tutorials/create/zendesk/schema.png)

## Conectar sua conta do [!DNL Zendesk]

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *Sucesso do cliente*, selecione **[!UICONTROL Zendesk]** e **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/zendesk/catalog.png)

A página **[!UICONTROL Conectar conta do Zendesk]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a conta do *Zendesk* com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/zendesk/existing.png)

### Nova conta

Se você estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas credenciais. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![novo](../../../../images/tutorials/create/zendesk/new.png)

### Selecionar dados

Depois que a fonte é autenticada, a página é atualizada em uma árvore de esquema interativa que permite explorar e inspecionar a hierarquia dos dados. Selecione **[!UICONTROL Avançar]** para continuar.

![selecionar-dados](../../../../images/tutorials/create/zendesk/select-data.png)

## Próximas etapas

Seguindo este tutorial, você autenticou e criou uma conexão de origem entre sua conta do [!DNL Zendesk] e a Experience Platform. Agora você pode seguir para o próximo tutorial e [criar um fluxo de dados para trazer os dados de sucesso do cliente para a Experience Platform](../../dataflow/customer-success.md).

## Recursos adicionais

As seções abaixo fornecem recursos adicionais que você pode consultar ao usar a origem [!DNL Zendesk].

### Validação {#validation}

As etapas a seguir descrevem as etapas que você pode seguir para validar se conectou com êxito a origem do [!DNL Zendesk] e se os perfis do [!DNL Zendesk] estão sendo assimilados para o Experience Platform.

Na interface do Experience Platform, selecione **[!UICONTROL Conjuntos de dados]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Conjuntos de dados]. A tela [!UICONTROL Atividade do Conjunto de Dados] exibe os detalhes das execuções.

![Página de atividade](../../../../images/tutorials/create/zendesk/dataset-activity.png)

Em seguida, selecione a ID de execução do fluxo de dados que deseja exibir para ver detalhes específicos sobre essa execução do fluxo de dados.

![Página de fluxo de dados](../../../../images/tutorials/create/zendesk/dataflow-monitoring.png)

Finalmente, selecione **[!UICONTROL Visualizar conjunto de dados]** para exibir os dados que foram assimilados.

![Conjunto de dados do Zendesk](../../../../images/tutorials/create/zendesk/preview-dataset.png)

Você também pode verificar seus dados do Experience Platform em relação aos dados na página [!DNL Zendesk] > [!DNL Customers].

![zendesk-customers](../../../../images/tutorials/create/zendesk/zendesk-customers.png)

### Esquema do Zendesk

A tabela abaixo lista os mapeamentos suportados que devem ser configurados para o Zendesk.

>[!TIP]
>
>Consulte [API de pesquisa do Zendesk > Exportar resultados da pesquisa](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) para obter mais informações sobre a API.

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

* A [API de Pesquisa do Zendesk > Exportar Resultados da Pesquisa](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) retorna um máximo de 1000 registros por página.
   * O valor do parâmetro ``filter[type]`` está definido como ``user`` e, portanto, a conexão do Zendesk retorna somente usuários.
   * O número de resultados por página é gerenciado pelo parâmetro ``page[size]``. O valor está definido como ``100``. Isso é feito para reduzir o impacto das restrições de redução de velocidade definidas pelo Zendesk.
   * Consulte [Limites](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#limits) e [Paginação](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#pagination-1).
   * Também é possível consultar [Paginação por meio de listas usando a paginação de cursor](https://developer.zendesk.com/documentation/developer-tools/pagination/paginating-through-lists-using-cursor-pagination/).
