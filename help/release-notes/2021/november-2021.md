---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão de novembro de 2021 para o Adobe Experience Platform.
exl-id: f649b516-8ef8-49af-bb3e-0392337d0d86
source-git-commit: 2c4b0d6dd0884fe81565356c31b18c0555bf973f
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 12%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 17 de novembro de 2021**

## Novos recursos

Novos recursos no Adobe Experience Platform:

- [Real-time Customer Data Platform Edição B2B](#B2B)
- [(Beta) Ativar segmentos de público-alvo para destinos em lote por meio da API de ativação ad-hoc](#ad-hoc-activation)

## Atualizações dos recursos existentes

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Attribution AI](#attribution-ai)
- [Customer AI](#customer-ai)

### Real-time Customer Data Platform Edição B2B {#B2B}

**Data de lançamento: 12 de novembro de 2021**

Baseada na Real-time Customer Data Platform (CDP em tempo real), a CDP B2B Edition em tempo real é projetada especificamente para profissionais de marketing que operam em um modelo de serviço de negócios para empresas. Ele reúne dados de várias fontes e os combina em uma única visualização de pessoas e perfis de conta. Esses dados unificados permitem que os profissionais de marketing direcionem com precisão públicos-alvo específicos e os envolvam em todos os canais disponíveis.

Há melhorias em uma variedade de recursos do Adobe Experience Platform que distinguem a CDP B2B Edition em tempo real da sua contraparte B2C. Eles incluem aprimoramentos no Experience Data Model (XDM) para casos de uso B2B, atualizações na resolução de identidade e na segmentação de perfil, bem como um conector e destino personalizado para o Marketo Engage. O conector Marketo permite que marcas B2B conectem seus dados de envolvimento B2B líderes do setor com informações comportamentais para alimentar leads e aprimorar operações de marketing baseadas em conta.

-[Novas edições B2B e B2P](#editions)
-[Novas fontes de dados e conectores de destino do Marketo](#marketo)
-[XDM B2B padrão](#XDM)

### Novas edições B2B e B2P {#editions}

Novas edições B2B e B2P que trazem dados e funcionalidades B2B para os produtos CDP em tempo real e Ativação de plataforma estão disponíveis para compra.

Para saber mais sobre a Real-time CDP B2B Edition, consulte o [visão geral](../../rtcdp/overview.md).

### Novas fontes de dados e conectores de destino do Marketo {#marketo}

Os novos conectores de origem de dados e de destino da Marketo fazem o stream de dados da Marketo para públicos-alvo da plataforma e da plataforma de volta para a Marketo. Disponível para todos os usuários da plataforma.

| Recurso | Descrição |
|-----------|--------------|
| Conector de fonte Marketo Engage | O [Conector de fonte Marketo Engage](../../sources/connectors/adobe-applications/marketo/marketo.md) O permite que os profissionais de marketing assimilem dados de uma ou mais instâncias do Marketo em suas instâncias do Adobe Experience Platform e fornece uma solução completa para o gerenciamento de clientes potenciais e para os profissionais de marketing B2B. |
| Destino de Marketo Engage | O [Destino do Marketo](../../destinations/catalog/adobe/marketo-engage.md) permite que os profissionais de marketing enviem segmentos criados no Adobe Experience Platform para o Marketo, onde serão exibidos como listas estáticas. |

### XDM B2B padrão {#XDM}

As classes padrão B2B XDM, os grupos de campos e os tipos de dados estão disponíveis para todos os usuários da plataforma.

| Recurso | Descrição |
|----------|-------------|
| Classes padrão B2B XDM | O Real-time Customer Data Platform B2B Edition fornece vários XDM padrão que capturam detalhes sobre entidades essenciais de dados B2B, como contas, oportunidades, campanhas e muito mais. |

Consulte a [Esquemas no Real-time Customer Data Platform B2B Edition](../../rtcdp/schemas/b2b.md) documentação para saber mais sobre como capturar entidades de dados B2B.

### (Beta) Ativar segmentos de público-alvo para destinos em lote por meio da API de ativação ad-hoc {#ad-hoc-activation}

A API de ativação ad-hoc permite que os profissionais de marketing ativem programaticamente segmentos de público-alvo para destinos, de maneira rápida e eficiente, para situações em que a ativação imediata é necessária. A ativação ad-hoc de público-alvo é compatível somente com [destinos com base em arquivo em lote](../../destinations/destination-types.md#file-based) e está atualmente em beta. Para obter mais informações, consulte o [documentação da API de ativação ad-hoc](../../destinations/api/ad-hoc-activation-api.md).

### Attribution AI {#attribution-ai}

O Attribution AI é usado para atribuir créditos a pontos de contato que levam a eventos de conversão. Ele pode ser usado pelos comerciantes para ajudar a quantificar o impacto de marketing de cada ponto de contato de marketing individual em várias jornadas de clientes.

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para vários conjuntos de dados | Agora, o Attribution AI pode assimilar vários conjuntos de dados facilmente diretamente na interface do usuário, sem a necessidade de mapear e compilar cada conjunto de dados. Esse novo recurso de economia de tempo fornece pontuações mais potentes e precisas com dados mais ricos de vários conjuntos de dados. |
| Mapeamento de canal de mídia e campo de campanha | O Attribution AI agora é compatível com o mapeamento de canais de mídia e campos de campanha. O mapeamento do canal de mídia entre conjuntos de dados melhora os insights derivados do Attribution AI e ajuda a fornecer resultados mais claros e fáceis de interpretar. |

Para obter mais informações sobre o Attribution AI, consulte o [Documentação do Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### Customer AI {#customer-ai}

O Customer AI disponível no Real-time Customer Data Platform é usado para gerar pontuações de propensão personalizadas, como churn e conversão para perfis individuais em escala. Isso é feito sem precisar transformar as necessidades de negócios em um problema de aprendizado de máquina, escolher um algoritmo, treinar ou implantar.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte para vários conjuntos de dados | O Customer AI agora pode assimilar facilmente vários conjuntos de dados diretamente na interface do usuário, sem a necessidade de mapear e compilar cada conjunto de dados. Esse novo recurso de economia de tempo fornece pontuações mais potentes e precisas com dados mais ricos de vários conjuntos de dados. |
| Atributos de perfil personalizados | O Customer AI agora é compatível com a definição de campos do conjunto de dados de perfil personalizado (com carimbos de data e hora) em seus dados, além de campos de evento padrão. Usar essa opção permite adicionar atributos de perfil adicionais que você considera influentes, o que pode melhorar a qualidade do modelo e fornecer resultados mais precisos. |

Para obter mais informações sobre a API do cliente, consulte o [Documentação do Customer AI](../../intelligent-services/customer-ai/overview.md).
