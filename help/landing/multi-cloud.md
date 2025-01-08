---
solution: Experience Platform
title: Visão geral de várias nuvens do Adobe Experience Platform
description: Saiba quais são as diferenças entre executar o Experience Platform no Microsoft Azure e no Amazon Web Services.
source-git-commit: d3654573cec338f173d151fd5e62ef5c8b893c11
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 3%

---


# Visão geral de várias nuvens do Adobe Experience Platform

O Adobe Experience Platform é um produto de várias nuvens, que oferece a opção de execução em [[!DNL Microsoft Azure]](https://azure.microsoft.com/en-us) ou [[!DNL Amazon Web Services (AWS)]](https://aws.amazon.com/). Essa flexibilidade permite escolher a melhor opção para seus requisitos técnicos e de negócios.

>[!AVAILABILITY]
>
>O Adobe Experience Platform em execução no Amazon Web Services (AWS) está disponível atualmente para um número limitado de clientes. Para saber mais sobre o Experience Platform no AWS, entre em contato com a equipe de conta do Adobe.

Esta página fornece uma visão geral de alto nível das duas infraestruturas de nuvem disponíveis e inclui orientação sobre como escolher a mais adequada para sua empresa.

## Qual é a implementação de nuvem certa para mim? {#which-cloud-is-right}

Escolher entre o Experience Platform no Azure ou no AWS depende de vários fatores específicos da sua empresa:

* **Necessidades técnicas e comerciais**: avalie as necessidades da sua organização e a estratégia de nuvem a longo prazo.
* **Infraestrutura existente**: considere sua infraestrutura de nuvem atual e suas necessidades de integração.
* **Dependência de tecnologia de nuvem**: se sua empresa depende muito das tecnologias da Microsoft, o Azure pode ser a melhor opção. Se você depender mais dos serviços da Amazon, o AWS pode ser a melhor opção.
* **Considerações sobre residência de dados**: avalie os requisitos de residência de dados de sua organização e garanta que a plataforma de nuvem escolhida ofereça regiões que estejam em conformidade com esses regulamentos.

Considerando os fatores acima, use esta árvore decisória simplificada para ajudar a decidir sobre a implementação de nuvem correta para suas necessidades comerciais.

![Imagem que mostra a distribuição geográfica de locais de hospedagem.](assets/multi-cloud/diagram-cloud.png){align="center" zoomable="yes"}

## Localizações de hospedagem {#available-cloud-regions}

Escolher a região de nuvem certa é fundamental para atender aos requisitos de residência de dados e garantir o desempenho ideal.

![Imagem que mostra a distribuição geográfica de locais de hospedagem.](assets/multi-cloud/hosting-locations-map.png){align="center" zoomable="yes"}

O Experience Platform está disponível em seis locais de hospedagem do Microsoft Azure, um local de hospedagem do Amazon Web Services (AWS) e roteia dados para serviços da Adobe por meio de sete [nós Edge Network](../collection/home.md#edge) distribuídos ao redor do mundo.

### Regiões do Microsoft Azure {#azure-regions}

A tabela abaixo indica as regiões do Microsoft Azure em que o Experience Platform está hospedado.

| País | Código da região | Localização |
|---------|-------------|----------|
| Estados Unidos | VA7 | Virgínia |
| Reino Unido | GBR9 | Londres |
| Holanda | NDL2 | Amsterdam |
| Canadá | CAN2 | Toronto |
| Índia | IND2 | Maharashtra |
| Austrália | AUS5 | Nova Gales do Sul |

{style="table-layout:auto"}

### Regiões do Amazon Web Services (AWS) {#aws-regions}

A tabela abaixo indica as regiões da AWS onde o Experience Platform está hospedado. Volte regularmente para ver se locais adicionais foram adicionados.

| País | Código da região | Localização |
|---------|-------------|----------|
| Estados Unidos | VA6 | Virgínia |

{style="table-layout:auto"}

## Paridade de recursos {#feature-parity}

O Adobe tem o compromisso de oferecer paridade de recursos entre plataformas de nuvem para todos os aplicativos em execução no Experience Platform, como:

* [Real-Time Customer Data Platform](../rtcdp/home.md)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/ajo-home)
* [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-landing)

No entanto, algumas funcionalidades podem diferir entre as implementações do Azure e do AWS. Essas diferenças são descritas na seção abaixo e em outras partes da documentação do produto, quando aplicável.

### Diferenças entre a execução do Experience Platform no Microsoft Azure e no AWS {#azure-aws-differences}

A tabela abaixo destaca as principais diferenças entre a execução do Experience Platform no Microsoft Azure e no AWS.

| Recurso/funcionalidade | Microsoft Azure | Amazon Web Services |
| --- | --- | --- |
| [Conformidade com a HIPAA](https://www.adobe.com/trust/compliance/hipaa-ready.html) | Suportado | Não suportado |
| [Catálogo de conectores de origem](/help/sources/home.md) | Todos os conectores no catálogo de fontes são compatíveis | Um número limitado de conectores de origem está disponível. Todos os conectores de origem disponíveis para implementações do AWS são chamados em uma nota no topo da página em suas respectivas páginas de documentação. |

{style="table-layout:auto"}

<!-- To be determined if we need to add this part about the AI Assistant 

| [Experience Platform AI Assistant](/help/ai-assistant/home.md) | Supported | Not supported |

-->

## Conclusão {#conclusion}

O Experience Platform oferece flexibilidade e opções, oferecendo a opção de execução no Microsoft Azure ou Amazon Web Services. Avalie suas necessidades de negócios e a infraestrutura existente para tomar uma decisão informada sobre qual plataforma de nuvem usar.
