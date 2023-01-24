---
title: Criar uma conexão de origem de Eventos do SugarCRM na interface do usuário
description: Saiba como criar uma conexão de origem de Eventos do SugarCRM usando a interface do usuário do Adobe Experience Platform.
source-git-commit: 17d8a6517686ee2459955f766d75980b41851320
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 1%

---

# (Beta) Criar um [!DNL SugarCRM Events] conexão de origem na interface do usuário

>[!NOTE]
>
>O [!DNL SugarCRM Events] A fonte está em beta. Consulte a [visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

Este tutorial fornece etapas para criar um [!DNL SugarCRM Events] conexão de origem usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL SugarCRM] , você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/crm.md).

### Obter credenciais necessárias

Para se conectar [!DNL SugarCRM Events] para Plataforma, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| `Host` | O endpoint da API SugarCRM ao qual a origem se conecta. | `developer.salesfusion.com` |
| `Username` | Seu nome de usuário da conta de desenvolvedor do SugarCRM. | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | Sua senha da conta de desenvolvedor do SugarCRM. | `123456789` |

### Criar um esquema da Platform para [!DNL SugarCRM]

Antes de criar um [!DNL SugarCRM] na conexão de origem, você também deve garantir que primeiro crie um esquema da plataforma para usar na origem. Veja o tutorial em [criação de um schema da plataforma](../../../../../xdm/schema/composition.md) para obter etapas abrangentes sobre como criar um schema.

![Captura de tela da interface do usuário da plataforma mostrando um esquema de exemplo para Eventos do SugarCRM](../../../../images/tutorials/create/sugarcrm-events/sugarcrm-schema-events.png)

>[!WARNING]
>
>Ao mapear o esquema, certifique-se também de mapear a variável `event_id` e `timestamp` campos exigidos pela Platform.

## Conecte seu [!DNL SugarCRM Events] account

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em *CRM* categoria , selecione **[!UICONTROL Eventos SugarCRM]** e selecione **[!UICONTROL Adicionar dados]**.

![Captura de tela da interface do usuário da plataforma para o catálogo com a placa de eventos SugarCRM](../../../../images/tutorials/create/sugarcrm-events/catalog-sugarcrm-events.png)

O **[!UICONTROL Conta de Eventos do Connect SugarCRM]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Conta existente

Para usar uma conta existente, selecione a [!DNL SugarCRM Events] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próximo]** para continuar.

![Captura de tela da interface do usuário da plataforma para a conta de Eventos do Connect SugarCRM com uma conta existente](../../../../images/tutorials/create/sugarcrm-events/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e, em seguida, forneça um nome, uma descrição opcional e suas credenciais. Quando terminar, selecione **[!UICONTROL Conectar-se à origem]** e, em seguida, permitir que a nova conexão seja estabelecida.

![Captura de tela da interface do usuário da plataforma para a conta de Eventos do Connect SugarCRM com uma nova conta](../../../../images/tutorials/create/sugarcrm-events/new.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com seu [!DNL SugarCRM Events] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a plataforma](../../dataflow/crm.md).

## Recursos adicionais

As seções abaixo fornecem recursos adicionais que você pode consultar ao usar o [!DNL SugarCRM] fonte.

### Medidas de proteção {#guardrails}

O [!DNL SugarCRM] As taxas de controle da API são 90 chamadas por minuto ou 2000 chamadas por dia, o que ocorrer primeiro. No entanto, essa restrição foi contornada ao adicionar um parâmetro à especificação da conexão que atrasará o tempo de solicitação para que o limite de taxa nunca seja atingido.

### Validação {#validation}

Para validar se você configurou a origem corretamente e [!DNL SugarCRM Events] Os dados estão sendo assimilados, siga as etapas abaixo:

* Na interface do usuário da plataforma, selecione **[!UICONTROL Exibir Fluxos de Dados]** ao lado do [!DNL SugarCRM Events] menu cartão no catálogo de fontes. Em seguida, selecione **[!UICONTROL Visualizar conjunto de dados]** para verificar os dados assimilados.

* Dependendo do tipo de objeto com o qual você está trabalhando, é possível verificar os dados agregados em relação às contagens visíveis na [!DNL SugarMarket] Página Eventos abaixo:

![Captura de tela da página Contas de Mercado do Açúcar exibindo a lista de contas](../../../../images/tutorials/create/sugarcrm-events/sugarmarket-events.png)

>[!NOTE]
>
>O [!DNL SugarMarket] as páginas não incluem a contagem de objetos excluídos. No entanto, os dados recuperados por meio dessa fonte também incluirão a contagem excluída, que será marcada com um sinalizador excluído.