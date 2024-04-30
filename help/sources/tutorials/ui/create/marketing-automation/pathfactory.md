---
title: Conectar sua conta PathFactory ao Experience Platform por meio da interface
description: Saiba como conectar sua conta PathFactory ao Experience Platform por meio da interface do usuário do.
badge: Beta
exl-id: 859dd0c1-8c4b-43e3-a87b-84c879460bc0
source-git-commit: ca17854830edabaf2bd74265258d6f0096f2888e
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 1%

---

# Conecte seu [!DNL PathFactory] conta para o Experience Platform por meio da interface

Este tutorial fornece etapas sobre como conectar seus [!DNL PathFactory] Dados de Visitantes, Sessões e Exibições de página do Adobe Experience Platform por meio da interface do.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma [!DNL PathFactory] conta, você pode ignorar o restante deste documento e prosseguir para o tutorial em [como trazer dados de automação de marketing para o Experience Platform usando a interface do](../../dataflow/marketing-automation.md).

### Colete as credenciais necessárias {#gather-credentials}

Para acessar a conta PathFactory na Platform, você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| Nome de usuário | Seu nome de usuário da conta PathFactory. Isso é essencial para identificar sua conta no sistema. |
| Senha | A senha associada à sua conta PathFactory. Verifique se isso está protegido para impedir o acesso não autorizado. |
| Domínio | O domínio associado à sua conta PathFactory. Normalmente, refere-se ao identificador exclusivo no URL do PathFactory. |
| Token de acesso | Um token exclusivo usado para autenticação de API para garantir a comunicação segura entre seus sistemas e o PathFactory. |
| Endpoints de API | Endpoints de API específicos para acessar dados: Visitantes, Sessões e Exibições de página. Cada endpoint corresponde a diferentes conjuntos de dados que você pode recuperar. **Nota:** Eles são predefinidos por [!DNL PathFactory] e são específicos aos dados que você pretende acessar: <ul><li>**Endpoint de visitantes**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Endpoint de sessões**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Ponto de extremidade de exibições de página**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Para obter orientação detalhada sobre como proteger e usar suas credenciais, e para obter informações sobre como obter e atualizar seu token de acesso, visite o [Centro de suporte PathFactory](https://support.pathfactory.com/categories/adobe/). Esse recurso oferece guias abrangentes sobre como gerenciar suas credenciais e garantir uma integração de API eficaz e segura.


## Conecte seu [!DNL PathFactory] account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes suportadas pelo Experience Platform.

Você pode selecionar a categoria apropriada na lista de categorias. Você também pode usar a barra de pesquisa para filtrar por uma fonte específica.

No [!UICONTROL Automação de marketing] categoria, selecione **[!UICONTROL PathFactory]** e selecione **[!UICONTROL Configurar]**.

![O catálogo de origens com a origem PathFactory selecionada.](../../../../images/tutorials/create/pathfactory/catalog.png)

A variável **[!UICONTROL Conectar ao PathFactory]** é exibida. Nesta página, você pode criar uma nova conta ou usar uma conta existente.

### Nova conta

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome para sua conta, uma descrição opcional e as credenciais de autenticação que correspondem à [!DNL PathFactory] conta.

Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

![A nova interface de conta onde você pode autenticar uma nova conta para PathFactory.](../../../../images/tutorials/create/pathfactory/new.png)

### Conta existente

Se você já tiver uma conta existente, selecione **[!UICONTROL Conta existente]** e, em seguida, selecione a conta que deseja usar na lista exibida.

![A interface de conta existente onde você pode selecionar em uma lista de contas PathFactory existentes.](../../../../images/tutorials/create/pathfactory/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão entre suas [!DNL PathFactory] conta e Experience Platform. Agora você pode seguir para o próximo tutorial e [crie um fluxo de dados para trazer seus dados de automação de marketing para o Experience Platform](../../dataflow/marketing-automation.md).
