---
title: Configurar a detecção de bot para sequências de dados
description: Saiba como configurar a detecção de bot para sequências de dados, para diferenciar o tráfego humano e não humano.
exl-id: 6b221d97-0145-4d3e-a32d-746d72534add
source-git-commit: 5f599b8572c4cebcdfb9ab85027211da4d8a020c
workflow-type: tm+mt
source-wordcount: '1374'
ht-degree: 0%

---

# Configurar a detecção de bot para sequências de dados

O tráfego não humano de programas automatizados, raspadores da Web, aranhas e scanners com script pode dificultar a identificação de eventos de visitantes humanos. Esse tipo de tráfego pode afetar negativamente métricas comerciais importantes, resultando em relatórios de tráfego incorretos.

A detecção de bot permite identificar eventos gerados pelo [Web SDK](/help/collection/js/js-overview.md), [SDK Móvel](https://developer.adobe.com/client-sdks/home/) e [[!DNL Edge Network API]](https://developer.adobe.com/data-collection-apis/docs/api/) como sendo gerados pelos spiders e bots conhecidos.

Ao configurar a detecção de bot para seus fluxos de dados, você pode identificar endereços IP específicos, intervalos IP e cabeçalhos de solicitação para classificar como eventos de bot. Isso ajuda a fornecer uma medida mais precisa da atividade do usuário no seu site ou aplicativo móvel.

Quando uma solicitação para o Edge Network corresponde a qualquer uma das regras de detecção de bot, o esquema XDM é atualizado com uma pontuação de bot (sempre definida como 1), conforme mostrado abaixo:

```json
{
  "botDetection": {
    "score": 1
  }
}
```

Essa pontuação de bot ajuda as soluções que recebem a solicitação a identificar corretamente o tráfego de bot.

>[!IMPORTANT]
>
>A detecção de bot não elimina nenhuma solicitação de bot. Ela atualiza somente o esquema XDM com a pontuação de bot e encaminha o evento para o [serviço de sequência de dados](configure.md) que você configurou.
>
>As soluções da Adobe podem lidar com a pontuação de bots de maneiras diferentes. Por exemplo, o Adobe Analytics usa seu próprio [serviço de filtragem de bot](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/bot-removal/bot-rules.html) e não usa a pontuação definida pelo Edge Network. Os dois serviços usam a mesma [lista de bot IAB](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/), portanto, a pontuação do bot é idêntica.

## Considerações técnicas {#technical-considerations}

Antes de ativar a detecção de bot nos datastreams, lembre-se de alguns pontos principais para garantir resultados precisos e uma implementação sem problemas:

* A detecção de bot se aplica somente a solicitações não autenticadas enviadas para `edge.adobedc.net`.
* As solicitações autenticadas enviadas para `server.adobedc.net` não são avaliadas para tráfego de bot, pois o tráfego autenticado é considerado confiável.
* As regras de detecção de bot podem levar até 15 minutos para se propagarem pela Edge Network após serem criadas.

## Pré-requisitos {#prerequisites}

Para que a detecção de bot funcione na sequência de dados, é necessário adicionar o grupo de campos **[!UICONTROL Bot Detection Information]** ao esquema. Consulte a documentação do [esquema XDM](../xdm/ui/resources/schemas.md#add-field-groups) para saber como adicionar grupos de campos a um esquema.

## Configurar a detecção de bot para sequências de dados {#configure}

Você pode configurar a detecção de bot após criar uma configuração de sequência de dados. Consulte a documentação sobre como [criar e configurar uma sequência de dados](configure.md) e, em seguida, siga as instruções abaixo para adicionar recursos de detecção de bot à sua sequência de dados.

Vá para a lista de sequências de dados e selecione a sequência de dados à qual deseja adicionar a detecção de bot.

![Interface do usuário de sequências de dados mostrando a lista de sequências de dados.](assets/bot-detection/datastream-list.png)

Na página de detalhes da sequência de dados, selecione a opção **[!UICONTROL Bot Detection]** no painel direito.

![Opção de detecção de bot realçada na interface de usuário de fluxos de dados.](assets/bot-detection/bot-detection.png)

A página **[!UICONTROL Bot Detection Rules]** é exibida.

![Configurações de detecção de bot na página de configurações da sequência de dados.](assets/bot-detection/bot-detection-page.png)

Na página Regras de detecção de bot, você pode configurar a detecção de bot usando as seguintes funcionalidades:

* Usando o [!DNL [IAB/ABC International Spiders and Bots List]](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/).
* Criar suas próprias regras de detecção de bot.

### Usar a Lista Internacional de spiders e bots da IAB/ABC {#iab-list}

A [Lista Internacional de Aranhas e Bots do IAB/ABC](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/) é uma lista de spiders e bots da Internet padrão do setor de terceiros. Essa lista ajuda a identificar o tráfego automatizado, como rastreadores de mecanismo de pesquisa, ferramentas de monitoramento e outro tráfego não humano que talvez você não queira incluir nas contagens de análise.

Para configurar seu fluxo de dados para usar a Lista internacional de spiders e bots da IAB/ABC:

1. Alternar a opção **[!UICONTROL Use IAB/ABC International Spiders and Bots List for bot detection on this datastream]**.
2. Selecione **[!UICONTROL Save]** para aplicar as configurações de detecção de bot ao seu fluxo de dados.

![Aranhas IAB e lista de bot habilitadas.](assets/bot-detection/bot-detection-list.png)

### Criar regras de detecção de bot {#rules}

Além de usar a [Lista Internacional de spiders e bots do IAB/ABC](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/), você pode definir suas próprias regras de detecção de bot para cada sequência de dados.

Você pode criar regras de detecção de bot com base em **endereços IP** e **intervalos de endereço IP**.

Se você precisar de regras de detecção de bot mais granulares, poderá combinar as condições de IP com as condições do cabeçalho da solicitação. As regras de detecção de bot podem usar os seguintes cabeçalhos:

| Cabeçalho HTTP | Descrição |
| --- | --- |
| `user-agent` | Um cabeçalho que permite que servidores e colegas de rede identifiquem o aplicativo, o sistema operacional, o fornecedor e/ou a versão do agente do usuário solicitante. |
| `content-type` | Indica o tipo de mídia original do recurso (antes de qualquer codificação de conteúdo aplicada para envio). |
| `referer` | Identifica o endereço da página da Web da qual o recurso foi solicitado. |
| `sec-ch-ua` | Fornece a marca e a versão significativa de cada marca associada ao navegador em uma lista separada por vírgulas. |
| `sec-ch-ua-mobile` | Indica se o navegador está em um dispositivo móvel. Ele também pode ser usado por um navegador de desktop para indicar uma preferência por uma experiência do usuário móvel. |
| `sec-ch-ua-platform` | Fornece a plataforma ou o sistema operacional em que o agente do usuário está sendo executado. Por exemplo: &quot;Windows&quot; ou &quot;Android&quot;. |
| `sec-ch-ua-platform-version` | Fornece a versão do sistema operacional no qual o agente do usuário está sendo executado. |
| `sec-ch-ua-arch` | Fornece a arquitetura CPU subjacente do agente do usuário, como ARM ou x86. |
| `sec-ch-ua-model` | Indica o modelo do dispositivo no qual o navegador está sendo executado. |
| `sec-ch-ua-bitness` | Fornece o &quot;bit&quot; da arquitetura CPU subjacente do agente do usuário. Esse é o tamanho em bits de um número inteiro ou endereço de memória — normalmente 64 ou 32 bits. |
| `sec-ch-ua-wow64` | Indica se um binário do agente do usuário está sendo executado no modo de 32 bits no Windows de 64 bits. |

Para criar uma regra de detecção de bot, siga as etapas abaixo:

1. Selecione **[!UICONTROL Add New Rule]**.

   ![Tela de configurações de detecção de bot com o botão Adicionar nova regra realçado.](assets/bot-detection/bot-detection-new-rule.png)

2. Digite um nome para a regra no campo **[!UICONTROL Rule Name]**.

   ![Tela de regra de detecção de bot com o nome de regra realçado.](assets/bot-detection/rule-name.png)

3. Selecione **[!UICONTROL Add new IP condition]** para adicionar uma nova regra baseada em IP. Você pode definir a regra por endereço IP ou por intervalo de endereços IP.

   ![Tela de regra de detecção de bot com o campo de endereço IP realçado.](assets/bot-detection/ip-address-rule.png)

   ![Tela de regra de detecção de bot com o campo de intervalo IP realçado.](assets/bot-detection/ip-range-rule.png)

   >[!TIP]
   >
   >As condições de IP são baseadas em uma operação `OR` lógica. Uma solicitação é marcada como originária de um bot se corresponder a qualquer uma das condições de IP definidas.

4. Se quiser adicionar condições de cabeçalho à regra, selecione **[!UICONTROL Add header conditions group]** e, em seguida, selecione os cabeçalhos que deseja que a regra use.

   ![Tela de regra de detecção de bot com as condições de cabeçalho realçadas.](assets/bot-detection/header-conditions.png)

   Em seguida, adicione as condições a serem usadas para o cabeçalho selecionado.

   ![Tela de regra de detecção de bot com as condições de cabeçalho realçadas.](assets/bot-detection/header-condition-rule.png)

5. Depois de configurar as regras de detecção de bot desejadas, selecione **[!UICONTROL Save]** para aplicar as regras à sua sequência de dados.

   ![Tela de regra de detecção de bot com as condições de cabeçalho realçadas.](assets/bot-detection/bot-detection-save.png)


## Exemplos de regras de detecção de bot {#examples}

Para ajudar você a começar a usar a detecção de bot, use os exemplos detalhados abaixo para criar regras de detecção de bot.

### Detecção de bot com base em um endereço IP {#one-ip}

Para marcar todas as solicitações originadas de um endereço IP específico como tráfego de bot, crie uma nova regra de detecção de bot que avalia um único endereço IP, conforme mostrado na imagem abaixo.

![Regra de detecção de bot baseada em um endereço IP.](assets/bot-detection/bot-detection-one-ip.png)

### Detecção de bot com base em dois endereços IP {#two-ip}

Para marcar todas as solicitações originadas de um dos dois endereços IP específicos como tráfego de bot, crie uma nova regra de detecção de bot que avalia dois endereços IP, conforme mostrado na imagem abaixo.

![Regra de detecção de bot baseada em dois endereços IP.](assets/bot-detection/bot-detection-two-ips.png)

### Detecção de bot com base em um intervalo de endereços IP {#range}

Para marcar todas as solicitações originadas de qualquer endereço IP em um intervalo específico como tráfego de bot, crie uma nova regra de detecção de bot que avalia um intervalo de endereços IP inteiro, como mostrado na imagem abaixo.

![Regra de detecção de bot baseada no intervalo de IPs.](assets/bot-detection/bot-detection-range.png)

### Detecção de bot com base em um endereço IP e um cabeçalho de solicitação {#ip-header}

Para marcar todas as solicitações originadas de um endereço IP específico e que contenham um cabeçalho de solicitação específico como tráfego de bot, crie uma nova regra de detecção de bot, conforme mostrado na imagem abaixo.

Esta regra verifica se a solicitação se origina de um endereço IP específico e se o cabeçalho da solicitação `referer` começa com `www.adobe.com`.

![Regra de detecção de bot baseada no endereço IP e no cabeçalho da solicitação.](assets/bot-detection/bot-detection-header-ip.png)

### Detecção de bot com base em várias condições {#multiple-conditions}

Você pode criar regras de detecção de bot com base em:

* **Várias condições diferentes**: condições diferentes são avaliadas como uma operação `AND` lógica, o que significa que as condições precisam ser atendidas simultaneamente para que a solicitação seja identificada como originária de um bot.
* **Várias condições do mesmo tipo**: condições do mesmo tipo são avaliadas como uma operação `OR` lógica, o que significa que, se qualquer uma das condições for atendida, a solicitação será identificada como originária de um bot.

A regra mostrada na imagem abaixo identifica uma solicitação de origem de bot se as seguintes condições forem atendidas:

A solicitação se origina de um dos dois endereços IP, o cabeçalho `referer` começa com `www.adobe.com` e o cabeçalho `sec-ch-ua-mobile` identifica a solicitação como originada de um navegador de desktop.

![Regra de detecção de bot baseada em várias condições.](assets/bot-detection/bot-detection-multiple.png)
