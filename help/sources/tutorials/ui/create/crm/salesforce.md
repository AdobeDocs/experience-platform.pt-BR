---
title: Conectar sua conta da Salesforce usando a interface do usuário da Experience Platform
description: Saiba como conectar sua conta do Salesforce e trazer seus dados do CRM para o Experience Platform usando a interface do usuário.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: 11e9e1a25a45f4011f15b1e28753a98d4158012c
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 3%

---

# Conectar sua conta do [!DNL Salesforce] à Experience Platform usando a interface

Leia este guia para saber como conectar sua conta do [!DNL Salesforce] e trazer seus dados do CRM para a Adobe Experience Platform usando a interface do usuário do Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conta autenticada do [!DNL Salesforce], ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados para dados do CRM](../../dataflow/crm.md).

### Coletar credenciais necessárias {#gather-required-credentials}

A origem [!DNL Salesforce] dá suporte à autenticação por meio da Credencial do Cliente OAuth2.

| Credencial | Descrição |
| --- | --- |
| URL do ambiente | A URL da instância de origem [!DNL Salesforce]. O formato da URL do ambiente é `https://[domain].my.salesforce.com`. |
| ID de cliente | A ID do cliente é usada em conjunto com o segredo do cliente como parte da autenticação OAuth2. Juntos, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo no [!DNL Salesforce]. |
| Segredo do cliente | O segredo do cliente é usado em conjunto com a ID do cliente como parte da autenticação OAuth2. Juntos, a ID do cliente e o segredo do cliente permitem que o aplicativo opere em nome da sua conta, identificando o aplicativo no [!DNL Salesforce]. |
| Versão da API | A versão da API REST da instância [!DNL Salesforce] que você está usando. O valor da versão da API deve ser formatado com um decimal. Por exemplo, se você estiver usando a versão da API `52`, será necessário inserir o valor como `52.0`. Se esse campo ficar em branco, o Experience Platform usará automaticamente a versão mais recente disponível. |
| Incluir objetos excluídos | Um valor booleano usado para determinar se os registros excluídos por software devem ser incluídos. Se definido como verdadeiro, os registros excluídos por software podem ser incluídos na consulta do [!DNL Salesforce] e assimilados de sua conta na Experience Platform. Se você não especificar sua configuração, esse valor assumirá como padrão `false`. |

Para obter mais informações sobre como usar o OAuth para [!DNL Salesforce], leia o [[!DNL Salesforce] guia sobre Fluxos de Autorização do OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5).

## Conectar sua conta do [!DNL Salesforce]

Na interface do Experience Platform, navegue até **[!UICONTROL Sources]** no menu esquerdo para abrir o espaço de trabalho [!UICONTROL Sources]. Use o catálogo à esquerda para procurar categorias ou use a barra de pesquisa para localizar rapidamente a origem que deseja conectar.

Selecione **[!DNL Salesforce]** na categoria *[!UICONTROL CRM]* e selecione **[!UICONTROL Add data]**.

>[!TIP]
>
>No catálogo de fontes, você verá **[!UICONTROL Set up]** se nenhuma conta estiver conectada ou **[!UICONTROL Add data]** se uma conta já estiver autenticada.

![O catálogo de origens na interface do usuário do Experience Platform com o cartão de origem do Salesforce selecionado.](../../../../images/tutorials/create/salesforce/catalog.png)

A página **[!UICONTROL Connect to Salesforce]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Usar uma conta existente

Para usar uma conta existente, selecione **[!UICONTROL Existing account]** e, em seguida, selecione a conta que deseja usar na lista exibida. Quando terminar, selecione **[!UICONTROL Next]** para continuar.

![Uma lista de contas autenticadas do Salesforce que já existem em sua organização.](../../../../images/tutorials/create/salesforce/existing.png)

### Criar uma nova conta

Para criar uma nova conta, selecione **[!UICONTROL New account]** e forneça um nome e uma descrição para sua nova conta [!DNL Salesforce].

Para a Credencial do cliente OAuth 2, selecione **[!UICONTROL OAuth2 Client Credential]** e forneça valores para as seguintes credenciais:

* URL do ambiente
* ID de cliente
* Segredo do cliente
* Versão da API
* Incluir objetos de exclusão

Quando terminar, selecione **[!UICONTROL Connect to source]**.


![A interface na qual você pode criar uma nova conta do Salesforce fornecendo as credenciais de autenticação apropriadas.](../../../../images/tutorials/create/salesforce/new.png)

### Ignorar pré-visualização de dados de amostra {#skip-preview-of-sample-data}

Durante a etapa de seleção de dados, você pode encontrar um tempo limite ao assimilar tabelas ou arquivos de dados grandes. Você pode ignorar a visualização de dados para contornar o tempo limite e ainda visualizar o esquema, embora sem dados de amostra. Para ignorar a visualização de dados, habilite o botão **[!UICONTROL Skip previewing sample data]**.

O restante do workflow permanecerá o mesmo. O único problema é que ignorar a pré-visualização de dados pode impedir que campos calculados e obrigatórios sejam validados automaticamente durante a etapa de mapeamento e, em seguida, será necessário validar manualmente esses campos durante o mapeamento.

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL Salesforce]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para o  [!DNL Experience Platform]](../../dataflow/crm.md).
