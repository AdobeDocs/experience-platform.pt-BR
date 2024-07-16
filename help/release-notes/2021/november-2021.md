---
title: Notas de versão da Adobe Experience Platform de novembro de 2021
description: As notas de versão de novembro de 2021 para o Adobe Experience Platform.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 20%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 17 de novembro de 2021**

## Novos recursos

Novos recursos na Adobe Experience Platform:

- [Real-Time Customer Data Platform B2B Edition](#B2B)
- [(Beta) Ative segmentos de público-alvo para destinos em lote por meio da API de ativação ad-hoc](#ad-hoc-activation)

## Atualizações dos recursos existentes

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [IA de atribuição](#attribution-ai)
- [IA do cliente](#customer-ai)

### Real-Time Customer Data Platform B2B Edition {#B2B}

**Data de lançamento: 12 de novembro de 2021**

Criada com base na Real-time Customer Data Platform (Real-Time CDP), a Real-Time CDP B2B Edition foi desenvolvida especificamente para profissionais de marketing que operam em um modelo de serviço B2B. A plataforma reúne dados de várias origens e os combina numa única exibição de perfis de pessoas e contas. Esses dados unificados permitem que profissionais de marketing direcionem públicos-alvo específicos com precisão e gerem engajamento em todos os canais disponíveis.

Há melhorias em uma variedade de recursos do Adobe Experience Platform que distinguem o Real-Time CDP B2B Edition de seu equivalente B2C. Eles incluem melhorias no Experience Data Model (XDM) para casos de uso de B2B, atualizações na resolução de identidade e segmentação de perfil, bem como um conector e destino personalizados para Marketo Engage. O conector do Marketo permite que as marcas B2B conectem seus dados de engajamento B2B líderes do setor com informações comportamentais, a fim de nutrir clientes potenciais e aprimorar as operações de marketing baseadas em conta.

-[Novas edições B2B e B2P](#editions)
-[Novos conectores de origem e destino de dados do Marketo](#marketo)
-[XDM B2B padrão](#XDM)

### Novas edições B2B e B2P {#editions}

Novas edições B2B e B2P que trazem dados e funcionalidades B2B para os produtos Real-Time CDP e Platform Ativation estão disponíveis para compra.

Para saber mais sobre o Real-Time CDP B2B Edition, consulte a [visão geral](../../rtcdp/overview.md).

### Novos conectores de origem e destino de dados do Marketo {#marketo}

Novos conectores de origem e destino de dados do Marketo transmitem dados do Marketo para os públicos da Platform e do de volta para a Marketo. Disponível para todos os usuários da Platform.

| Recurso | Descrição |
|----------|-------------|
| conector de origem do Marketo Engage | O [conector de origem do Marketo Engage](../../sources/connectors/adobe-applications/marketo/marketo.md) permite que os profissionais de marketing assimilem dados de uma ou mais instâncias do Marketo na instância do Adobe Experience Platform e fornece uma solução completa para o gerenciamento de clientes potenciais e para os profissionais de marketing B2B. |
| Destino do Marketo Engage | O [destino do Marketo](../../destinations/catalog/adobe/marketo-engage.md) permite que os profissionais de marketing enviem segmentos criados no Adobe Experience Platform para o Marketo, onde eles aparecerão como listas estáticas. |

### XDM B2B padrão {#XDM}

Classes B2B XDM padrão, grupos de campos e tipos de dados estão disponíveis para todos os usuários da Platform.

| Recurso | Descrição |
|-----------|--------------|
| Classes B2B XDM padrão | O Real-time Customer Data Platform B2B Edition fornece vários XDM padrão que capturam detalhes sobre entidades de dados B2B essenciais, como contas, oportunidades, campanhas e muito mais. |

Consulte a documentação [Esquemas no Real-time Customer Data Platform B2B Edition](../../rtcdp/schemas/b2b.md) para saber mais sobre como capturar entidades de dados B2B.

### (Beta) Ative segmentos de público-alvo para destinos em lote por meio da API de ativação ad-hoc {#ad-hoc-activation}

A API de ativação ad-hoc permite que os profissionais de marketing ativem programaticamente segmentos de público-alvo para destinos, de forma rápida e eficiente, para situações em que a ativação imediata é necessária. A ativação de público-alvo ad-hoc é suportada apenas pelos [destinos baseados em arquivo em lote](../../destinations/destination-types.md#file-based) e está atualmente na versão beta. Para obter mais informações, consulte a [documentação da API de ativação ad hoc](../../destinations/api/ad-hoc-activation-api.md).

### IA de atribuição {#attribution-ai}

O Attribution AI é usado para atribuir créditos a pontos de contato que levam a eventos de conversão. Ela pode ser usada por comerciantes para ajudar a quantificar o impacto de marketing de cada ponto de contato de marketing individual em várias jornadas de clientes.

| Recurso | Descrição |
|-----------|---------------|
| Suporte para vários conjuntos de dados | O Attribution AI agora pode assimilar facilmente vários conjuntos de dados diretamente na interface do usuário, sem a necessidade de mapear e compilar cada conjunto de dados. Esse novo recurso que economiza tempo fornece pontuações mais poderosas e precisas com dados mais avançados de vários conjuntos de dados. |
| Canal de mídia e mapeamento de campo de campanha | O Attribution AI agora oferece suporte ao mapeamento de canais de mídia e campos de campanha. O mapeamento de canal de mídia entre conjuntos de dados melhora os insights derivados do Attribution AI e ajuda a fornecer resultados mais claros e fáceis de interpretar. |

Para obter mais informações sobre o Attribution AI, consulte a [documentação do Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### IA do cliente {#customer-ai}

A IA do cliente, disponível no Real-time Customer Data Platform, é usada para gerar pontuações de propensão personalizadas, como churn e conversão para perfis individuais em escala. Isso é feito sem precisar transformar as necessidades de negócios em um problema de aprendizado de máquina, escolher um algoritmo, treinar ou implantar.

**Recursos atualizados**

| Recurso | Descrição |
|-----------|-------------|
| Suporte para vários conjuntos de dados | A IA do cliente agora pode assimilar facilmente vários conjuntos de dados diretamente na interface do usuário, sem a necessidade de mapear e compilar cada conjunto de dados. Esse novo recurso que economiza tempo fornece pontuações mais poderosas e precisas com dados mais avançados de vários conjuntos de dados. |
| Atributos de perfil personalizados | A IA do cliente agora é compatível com a definição de campos de conjunto de dados de perfil personalizado (com carimbos de data e hora) em seus dados, além de campos de evento padrão. Usar essa opção permite adicionar outros atributos de perfil que você considera influentes, o que pode melhorar a qualidade do seu modelo e fornecer resultados mais precisos. |

Para obter mais informações sobre o Customer AI, consulte a [documentação do Customer AI](../../intelligent-services/customer-ai/overview.md).
