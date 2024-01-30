---
title: Criar um fluxo de dados para dados brasileiros na interface
description: Saiba como criar um fluxo de dados para sua conta do Brasil usando a interface do usuário do Adobe Experience Platform.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
source-git-commit: 632cff3ee4ca82d391e9a1df0cb38d903e8a5428
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 1%

---

# Criar um [!DNL Braze] conexão de origem na interface

>[!NOTE]
>
>A variável [!DNL Braze] a fonte está na versão beta. Leia as [visão geral das origens](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

[!DNL Braze] O capacita interações centradas no cliente entre consumidores e marcas em tempo real. [!DNL Braze Currents] é um fluxo de dados em tempo real de eventos de engajamento da plataforma Braze que é a exportação mais robusta, mas granular, do [!DNL Braze] plataforma.

Leia o tutorial a seguir para saber como trazer dados de eventos de engajamento do [!DNL Braze] para o Adobe Experience Platform na interface do usuário.

## Pré-requisitos

Para concluir as etapas deste guia, será necessário:

* Um logon para [Adobe Experience Platform](https://platform.adobe.com) e permissão para criar uma nova conexão de origem de streaming.
* Um logon no [[!DNL Braze] painel](https://dashboard.braze.com/sign_in), um não utilizado [Licença do Conector atual](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)e permissões para criar um conector. Para obter mais informações, leia a [requisitos para configurar [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Este tutorial também requer um entendimento prático de [[!DNL Braze] Correntes](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents).

Se você já tiver uma [!DNL Braze] conexão, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/marketing-automation.md).

## Conecte seu [!DNL Braze] conta para Experience Platform

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No *Automação de marketing* categoria, selecione **[!UICONTROL Braze]** e selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de origens na interface do usuário do Experience Platform com a origem de Correntes brasileiras selecionada.](../../../../images/tutorials/create/braze/catalog.png)

Em seguida, carregue o [Arquivo de amostra do Braze Currents](https://github.com/Appboy/currents-examples/blob/master/sample-data/Adobe/adobe_examples.json). Esse arquivo contém todos os campos possíveis que o Braze pode enviar como parte de um evento.

![A tela &quot;Add Data&quot; (Adicionar dados).](../../../../images/tutorials/create/braze/select-data.png)

Depois que o arquivo for carregado, você deverá fornecer os detalhes do fluxo de dados, incluindo informações sobre o conjunto de dados e o esquema para o qual está mapeando.
![A tela &quot;Detalhes do fluxo de dados&quot; destacando &quot;Detalhes do conjunto de dados&quot;.](../../../../images/tutorials/create/braze/dataflow-detail.png)

Em seguida, configure o mapeamento para os dados usando a interface de mapeamento.

![A tela &quot;Mapping&quot;.](../../../../images/tutorials/create/braze/mapping.png)

>[!IMPORTANT]
>
>Os carimbos de data e hora brasileiros não são expressos em milissegundos, mas em segundos. Para que os carimbos de data e hora no Experience Platform sejam refletidos com precisão, é necessário criar campos calculados em milissegundos. Um cálculo de &quot;time * 1000&quot; converterá corretamente em milissegundos, adequado para mapear para um campo de carimbo de data e hora dentro do Experience Platform.
>
>![Criação de um campo calculado para carimbo de data e hora ](../../../../images/tutorials/create/braze/create-calculated-field.png)

### Coletar credenciais necessárias

Depois que a conexão for criada, é necessário coletar os seguintes valores de credencial, que você fornecerá no Painel Brasileiro para enviar dados ao [!DNL Platform]. Para obter mais informações, leia a [!DNL Braze] [guia sobre como navegar até Correntes](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

| Campo | Descrição |
| ---------- | ----------- |
| `Client ID` | A ID do cliente associada à [!DNL Platform] origem. |
| `Client Secret` | O segredo do cliente associado à [!DNL Platform] origem. |
| `Tenant ID` | A ID do locatário associada à [!DNL Platform] origem. |
| `Sandbox Name` | A sandbox associada ao seu [!DNL Platform] origem. |
| `Dataflow ID` | A ID do fluxo de dados associado à [!DNL Platform] origem. |
| `Streaming Endpoint` | O terminal de transmissão associado à [!DNL Platform] origem. Observe que o Braze converterá automaticamente isso no endpoint de transmissão em lote. |

### Configurar [!DNL Braze Currents] para transmitir dados para sua fonte de dados

No prazo de [!DNL Braze Dashboard], navegue até Integrações de parceiros **->** Exportação de dados, selecione **[!DNL Create New Current]**. Você será solicitado a fornecer um nome para o conector, informações de contato para notificações sobre o conector e as credenciais listadas acima. Selecione os eventos que deseja receber, configure opcionalmente quaisquer exclusões/transformações de campo desejadas e selecione **[!DNL Launch Current]**.

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL Braze] conta. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados do sistema de automação de marketing para o [!DNL Platform]](../../dataflow/marketing-automation.md).