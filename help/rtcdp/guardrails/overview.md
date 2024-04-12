---
title: Medidas de proteção do Real-Time CDP
description: Saiba mais sobre as medidas de proteção de dados em vários serviços e áreas do Real-Time CDP.
feature: Guardrails, Data Management, Data Ingestion, Data Export
exl-id: 377499b4-5707-4d50-94e3-02f88ad5bf2c
source-git-commit: 2704184446f7945c744e7e2d2a8c3cda3fc12527
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 1%

---

# Medidas de proteção do Real-Time CDP

As garantias são limites que fornecem orientação para o uso de dados e do sistema, otimização do desempenho e prevenção de erros ou resultados inesperados no Real-Time CDP. As garantias podem se referir ao uso ou consumo de dados e processamento em relação aos seus direitos de licenciamento.

Comece aqui e siga os links abaixo para entender todas as medidas de proteção nos vários serviços e áreas do Real-Time CDP:

* [Medidas de proteção para assimilação de dados](/help/ingestion/guardrails.md)
* [Medidas de proteção para [!DNL Edge Network Server API]](/help/server-api/guardrails.md)
* [Medidas de proteção para [!DNL Real-Time Customer Profile] dados e segmentação](/help/profile/guardrails.md)
* [Medidas de proteção para [!DNL Identity Service] dados](/help/identity-service/guardrails.md)
* [Medidas de proteção para [!DNL Query Service]](/help/query-service/guardrails.md)
* [Medidas de proteção para ativação de dados por meio de destinos](/help/destinations/guardrails.md)
* [Medidas de proteção para o Real-Time CDP B2B](/help/rtcdp/b2b-guardrails.md)

>[!TIP]
>
>Além disso, visite [os blueprints de experiência digital](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html) para obter mais informações, como [diagramas de latência de ponta a ponta](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) para vários serviços de Experience Platform.

## Tipos de grade de proteção {#guardrail-types}

Observe que os dois tipos de proteção em todas as áreas e serviços da Real-Time CDP são:

| Tipo de grade de proteção | Descrição |
|----------|---------|
| **Proteção de desempenho (limite flexível)** | As medidas de proteção de desempenho são limites de uso relacionados ao escopo dos seus casos de uso. Ao exceder as medidas de proteção de desempenho, você pode enfrentar degradação e latência do desempenho. O Adobe não é responsável por essa degradação de desempenho. Os clientes que excederem consistentemente uma garantia de desempenho podem optar por licenciar capacidade adicional para evitar a degradação do desempenho. |
| **Medidas de proteção aplicadas pelo sistema (limite rígido)** | As medidas de proteção aplicadas pelo sistema são aplicadas pela interface do usuário ou API do Real-Time CDP. Esses são limites que você não pode exceder, pois a interface do usuário e a API o bloquearão de fazer isso ou retornarão um erro. |

{style="table-layout:auto"}

## Informações sobre licenciamento e direitos do Real-Time CDP {#product-descriptions}

Além disso, consulte os links de descrição do produto abaixo para obter informações sobre licenciamento e direitos com base na edição e no nível da Real-Time CDP que você adquiriu:

* [Todas as descrições de produto do Adobe](https://helpx.adobe.com/legal/product-descriptions.html?lang=pt-BR)
* [Real-time Customer Data Platform (B2C Edition - Pacotes Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (Edição B2P - Pacotes Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (Edição B2B - Pacotes Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

## Medidas de proteção para outros aplicativos Experience Platform  {#guardrails-other-aep-apps}

Existem medidas de proteção semelhantes para outras aplicações de Experience Platform. Acesse os links abaixo para obter mais informações:

* [Medidas de proteção do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=en)
* [Grades de proteção de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html)

## Próximas etapas

Depois de entender as medidas de proteção que se aplicam a várias áreas e serviços do Real-Time CDP, você pode seguir com uma [exemplo de uso de uma implementação do Real-Time CDP](/help/rtcdp/get-started.md).
