---
title: Visão geral da origem das correntes brasileiras
description: Saiba como transmitir dados de Correntes brasileiras para o Experience Platform.
badge: Beta
source-git-commit: 64975ccb6a44730489427cef745f3dbce5bcedf1
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 2%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>A variável [!DNL Braze Currents] a fonte está na versão beta. Leia as [visão geral das origens](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de aplicativos de transmissão. O suporte para provedores de transmissão inclui [!DNL Braze Currents].

[!DNL Braze] O capacita interações centradas no cliente entre consumidores e marcas em tempo real. [!DNL Braze Currents] é um fluxo de dados em tempo real de eventos de engajamento da plataforma Braze que é a exportação mais robusta, mas granular, do [!DNL Braze] plataforma.

## Pré-requisitos

Para concluir as etapas deste guia, será necessário:

* Um logon para [Adobe Experience Platform](https://platform.adobe.com) e permissão para criar uma nova conexão de origem de streaming.
* Um logon no [[!DNL Braze] painel](https://dashboard.braze.com/sign_in), um não utilizado [Licença do Conector atual](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)e permissões para criar um conector. Para obter mais informações, leia a [requisitos para configurar [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

### Coletar credenciais necessárias

Para enviar com sucesso seu [!DNL Braze Currents] dados para Experience Platform, você precisa inserir as seguintes credenciais de Experience Platform no [!DNL Braze] Painel da interface do usuário.

| Campo | Descrição |
| --- | --- |
| ID do cliente | A ID do cliente associada à origem do Experience Platform. |
| Segredo do cliente | O segredo do cliente associado à sua origem de Experience Platform. |
| ID do inquilino | A ID do locatário associada à origem do Experience Platform. |
| Nome da sandbox | A sandbox associada à origem do Experience Platform. |
| ID do fluxo de dados | A ID de fluxo de dados associada à origem do Experience Platform. |
| Endpoint de transmissão | O ponto final de transmissão associado à fonte do Experience Platform. **Nota**: [!DNL Braze] O converte automaticamente isso no endpoint de transmissão em lote. |

Para obter informações sobre como recuperar esses valores, leia o manual sobre [introdução às APIs da Platform](../../../landing/api-authentication.md). Para obter informações sobre como usar o [!DNL Braze] painel, leia o [!DNL Braze] guia sobre como [Navegar até Atuais](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

## Próximas etapas

Ao ler este documento, você concluiu a configuração de pré-requisito necessária para transmitir dados de seu [!DNL Braze Currents] conta para Experience Platform. Agora você pode prosseguir para o guia em [conectando [!DNL Braze Currents] para Experience Platform usando a interface do usuário](../../tutorials/ui/create/marketing-automation/braze.md).