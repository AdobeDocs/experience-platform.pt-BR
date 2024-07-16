---
title: Visão geral do Braze Current Source
description: Saiba como transmitir dados de Correntes brasileiras para o Experience Platform.
badge: Beta
exl-id: dd304e10-26e5-4586-ab39-8fe3294b19c9
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 3%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>A origem [!DNL Braze Currents] está na versão beta. Leia a [visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

O Adobe Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, bancos de dados e muitas outras.

O Experience Platform fornece suporte para assimilação de dados de aplicativos de transmissão. O suporte para provedores de streaming inclui [!DNL Braze Currents].

O [!DNL Braze] possibilita interações centradas no cliente entre consumidores e marcas em tempo real. [!DNL Braze Currents] é um fluxo de dados em tempo real de eventos de envolvimento da plataforma Braze que é a exportação mais robusta, mas granular, da plataforma [!DNL Braze].

## Pré-requisitos

Para concluir as etapas deste guia, será necessário:

* Um logon no [Adobe Experience Platform](https://platform.adobe.com) e permissão para criar uma nova conexão de origem de streaming.
* Um logon no [[!DNL Braze] painel](https://dashboard.braze.com/sign_in), uma [licença do Conector atual](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents) não usada e permissões para criar um conector. Para obter mais informações, leia os [requisitos para configurar [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

### Coletar credenciais necessárias

Para enviar com êxito seus dados do [!DNL Braze Currents] para o Experience Platform, você precisa inserir as seguintes credenciais de Experience Platform no painel da interface do usuário do [!DNL Braze].

| Campo | Descrição |
| --- | --- |
| ID de cliente | A ID do cliente associada à origem do Experience Platform. |
| Segredo do cliente | O segredo do cliente associado à sua origem de Experience Platform. |
| ID do inquilino | A ID do locatário associada à origem do Experience Platform. |
| Nome da sandbox | A sandbox associada à origem do Experience Platform. |
| ID do fluxo de dados | A ID de fluxo de dados associada à origem do Experience Platform. |
| Endpoint de transmissão | O ponto final de transmissão associado à fonte do Experience Platform. **Observação**: [!DNL Braze] converte automaticamente isso no ponto de extremidade de streaming em lote. |

Para obter informações sobre como recuperar esses valores, leia o guia em [introdução às APIs da plataforma](../../../landing/api-authentication.md). Para obter informações sobre como usar o painel [!DNL Braze], leia o guia [!DNL Braze] sobre como [Navegar até as Atualizações](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

## Próximas etapas

Ao ler este documento, você concluiu a configuração de pré-requisito necessária para transmitir dados da sua conta do [!DNL Braze Currents] para o Experience Platform. Agora você pode prosseguir para o guia em [conectando [!DNL Braze Currents] ao Experience Platform usando a interface de usuário](../../tutorials/ui/create/marketing-automation/braze.md).
