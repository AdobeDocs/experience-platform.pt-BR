---
title: Criar uma conexão de origem de Eventos do SugarCRM na interface
description: Saiba como criar uma conexão de origem de Eventos do SugarCRM usando a interface do Adobe Experience Platform.
source-git-commit: 17d8a6517686ee2459955f766d75980b41851320
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 1%

---

# (Beta) Criar um [!DNL SugarCRM Events] conexão de origem na interface

>[!NOTE]
>
>A variável [!DNL SugarCRM Events] a fonte está na versão beta. Consulte a [visão geral das origens](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

Este tutorial fornece etapas para a criação de um [!DNL SugarCRM Events] conexão de origem usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL SugarCRM] conta, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/crm.md).

### Coletar credenciais necessárias

Para se conectar [!DNL SugarCRM Events] Para o Platform, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| `Host` | O ponto de extremidade da API do SugarCRM ao qual a origem se conecta. | `developer.salesfusion.com` |
| `Username` | Seu nome de usuário da conta de desenvolvedor do SugarCRM. | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | A senha da sua conta de desenvolvedor do SugarCRM. | `123456789` |

### Criar um esquema da Platform para [!DNL SugarCRM]

Antes de criar uma [!DNL SugarCRM] conexão de origem, você também deve garantir que primeiro crie um esquema da Platform para usar em sua origem. Veja o tutorial sobre [criação de um schema do Platform](../../../../../xdm/schema/composition.md) para obter etapas abrangentes sobre como criar um schema.

![Captura de tela da interface do usuário da plataforma mostrando um esquema de exemplo para eventos do SugarCRM](../../../../images/tutorials/create/sugarcrm-events/sugarcrm-schema-events.png)

>[!WARNING]
>
>Ao mapear o esquema, certifique-se de mapear também a variável `event_id` e `timestamp` campos exigidos pela Platform.

## Conecte seu [!DNL SugarCRM Events] account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No *CRM* categoria, selecione **[!UICONTROL Eventos do SugarCRM]** e selecione **[!UICONTROL Adicionar dados]**.

![Captura de tela da interface do usuário do Platform para catálogo com o cartão de eventos do SugarCRM](../../../../images/tutorials/create/sugarcrm-events/catalog-sugarcrm-events.png)

A variável **[!UICONTROL Conectar a conta de Eventos do SugarCRM]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a variável [!DNL SugarCRM Events] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próxima]** para continuar.

![Captura de tela da interface do usuário da plataforma para a conta Connect SugarCRM Events com uma conta existente](../../../../images/tutorials/create/sugarcrm-events/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas credenciais. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

![Captura de tela da interface do usuário da plataforma para a conta Connect SugarCRM Events com uma nova conta](../../../../images/tutorials/create/sugarcrm-events/new.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL SugarCRM Events] conta. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Platform](../../dataflow/crm.md).

## Recursos adicionais

As seções abaixo fornecem recursos adicionais que você pode consultar ao usar o [!DNL SugarCRM] origem.

### Medidas de proteção {#guardrails}

A variável [!DNL SugarCRM] As taxas de limitação da API são de 90 chamadas por minuto ou 2000 chamadas por dia, o que ocorrer primeiro. No entanto, essa restrição foi contornada adicionando um parâmetro na especificação da conexão que atrasará o tempo de solicitação para que o limite da taxa nunca seja atingido.

### Validação {#validation}

Para validar se você configurou corretamente a origem e [!DNL SugarCRM Events] Os dados do estão sendo assimilados, siga as etapas abaixo:

* Na interface do usuário da Platform, selecione **[!UICONTROL Exibir fluxos de dados]** ao lado da variável [!DNL SugarCRM Events] no catálogo de origens. Em seguida, selecione **[!UICONTROL Visualizar conjunto de dados]** para verificar os dados assimilados.

* Dependendo do tipo de objeto com o qual você está trabalhando, é possível verificar os dados agregados em relação às contagens visíveis na [!DNL SugarMarket] Página Eventos abaixo:

![Captura de tela da página SugarMarket Accounts exibindo a lista de contas](../../../../images/tutorials/create/sugarcrm-events/sugarmarket-events.png)

>[!NOTE]
>
>A variável [!DNL SugarMarket] As páginas não incluem as contagens de objetos excluídos. No entanto, os dados recuperados por meio dessa fonte também incluirão a contagem de excluídos, que seria marcada com um sinalizador excluído.