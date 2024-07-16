---
title: Criar uma conexão de origem de Eventos do SugarCRM na interface
description: Saiba como criar uma conexão de origem de Eventos do SugarCRM usando a interface do Adobe Experience Platform.
exl-id: db346ec0-2c57-4b82-8a39-f15d4cd377d4
source-git-commit: 68c14d7b187075b4af6b019a8bd1ca2625beabde
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 2%

---

# Criar uma conexão de origem [!DNL SugarCRM Events] na interface

Este tutorial fornece etapas para criar uma conexão de origem [!DNL SugarCRM Events] usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conta válida do [!DNL SugarCRM], ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/crm.md).

### Coletar credenciais necessárias

Para conectar [!DNL SugarCRM Events] à Platform, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| `Host` | O ponto de extremidade da API do SugarCRM ao qual a origem se conecta. | `developer.salesfusion.com` |
| `Username` | Seu nome de usuário da conta de desenvolvedor do SugarCRM. | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | A senha da sua conta de desenvolvedor do SugarCRM. | `123456789` |

### Criar um esquema da plataforma para [!DNL SugarCRM]

Antes de criar uma conexão de origem do [!DNL SugarCRM], você também deve garantir que primeiro crie um esquema da Platform para usar em sua origem. Consulte o tutorial sobre [criação de um esquema da Platform](../../../../../xdm/schema/composition.md) para obter etapas abrangentes sobre como criar um esquema.

![Captura de tela da interface do usuário da plataforma mostrando um exemplo de esquema para eventos do SugarCRM](../../../../images/tutorials/create/sugarcrm-events/sugarcrm-schema-events.png)

>[!WARNING]
>
>Ao mapear o esquema, certifique-se de mapear também os campos obrigatórios `event_id` e `timestamp` exigidos pela Platform.

## Conectar sua conta do [!DNL SugarCRM Events]

Na interface da Platform, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *CRM*, selecione **[!UICONTROL Eventos do SugarCRM]** e **[!UICONTROL Adicionar dados]**.

![Captura de tela da interface do usuário da plataforma para catálogo com o cartão de Eventos do SugarCRM](../../../../images/tutorials/create/sugarcrm-events/catalog-sugarcrm-events.png)

A página **[!UICONTROL Conectar conta de Eventos do SugarCRM]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a conta [!DNL SugarCRM Events] com a qual deseja criar um novo fluxo de dados e clique em **[!UICONTROL Avançar]** para continuar.

![Captura de tela da interface de usuário da plataforma para a conta de eventos do Connect SugarCRM com uma conta existente](../../../../images/tutorials/create/sugarcrm-events/existing.png)

### Nova conta

Se você estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas credenciais. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![Captura de tela da interface do usuário da plataforma para a conta de eventos do Connect SugarCRM com uma nova conta](../../../../images/tutorials/create/sugarcrm-events/new.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL SugarCRM Events]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Platform](../../dataflow/crm.md).

## Recursos adicionais

As seções abaixo fornecem recursos adicionais que você pode consultar ao usar a origem [!DNL SugarCRM].

### Medidas de proteção {#guardrails}

As taxas de limitação da API [!DNL SugarCRM] são de 90 chamadas por minuto ou 2000 chamadas por dia, o que ocorrer primeiro. No entanto, essa restrição foi contornada adicionando um parâmetro na especificação da conexão que atrasará o tempo de solicitação para que o limite da taxa nunca seja atingido.

### Validação {#validation}

Para validar se você configurou corretamente a origem e se os dados de [!DNL SugarCRM Events] estão sendo assimilados, siga as etapas abaixo:

* Na interface da Platform, selecione **[!UICONTROL Exibir Fluxos de Dados]** ao lado do menu de cartão [!DNL SugarCRM Events] no catálogo de fontes. Em seguida, selecione **[!UICONTROL Visualizar conjunto de dados]** para verificar os dados que foram assimilados.

* Dependendo do tipo de objeto com o qual você está trabalhando, é possível verificar os dados agregados em relação às contagens visíveis na página [!DNL SugarMarket] Eventos abaixo:

![Captura de tela da página Contas do SugarMarket exibindo a lista de contas](../../../../images/tutorials/create/sugarcrm-events/sugarmarket-events.png)

>[!NOTE]
>
>As páginas [!DNL SugarMarket] não incluem as contagens de objetos excluídos. No entanto, os dados recuperados por meio dessa fonte também incluirão a contagem de excluídos, que seria marcada com um sinalizador excluído.
