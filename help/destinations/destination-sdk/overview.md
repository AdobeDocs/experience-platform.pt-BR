---
description: O Adobe Experience Platform Destination SDK é um conjunto de APIs de configuração que permitem configurar padrões de integração de destino para o Experience Platform para fornecer dados de público-alvo e de perfil ao seu ponto de extremidade, com base em dados e formatos de autenticação de sua escolha. As configurações são armazenadas no Experience Platform e podem ser recuperadas por meio da API para obter atualizações adicionais.
title: SDK de destino do Adobe Experience Platform
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: bd65cfa557fb42d23022578b98bc5482e8bd50b1
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 2%

---

# SDK de destino do Adobe Experience Platform

## Visão geral {#destinations-sdk}

O Adobe Experience Platform Destination SDK é um conjunto de APIs de configuração que permitem configurar padrões de integração de destino para o Experience Platform para fornecer dados de público-alvo e perfil ao seu terminal, com base em dados e formatos de autenticação de sua escolha. As configurações são armazenadas no Experience Platform e podem ser recuperadas por meio da API para obter atualizações adicionais.

A documentação do SDK de destino fornece instruções para que você use o SDK de destino do Adobe Experience Platform para configurar, testar e lançar uma integração de destino produzida com o Adobe Experience Platform, e fazer com que seu destino faça parte do catálogo de destinos em crescimento.

![Visão geral do catálogo de destinos](./assets/destinations-catalog-overview.png)

## Integrações produzidas e personalizadas {#productized-custom-integrations}

Como parceiro do SDK de destino, você pode se beneficiar de adicionar seu destino produzido ao [catálogo de Experience Platform](/help/destinations/catalog/overview.md):
1. Padronize as configurações de integração entre clientes com parâmetros pré-configurados e simplifique a experiência de configuração para clientes.
2. Introduza uma placa de destino com marca no catálogo de destinos do Experience Platform para obter uma configuração e um conhecimento mais simplificados do cliente.
3. Ser apresentado como uma integração de destino produzida com a Adobe Experience Platform e a Plataforma de dados do cliente em tempo real.

Como cliente do Experience Platform, você pode criar um destino personalizado privado, o que pode se adequar melhor às suas necessidades de ativação.

![Diagrama visual do SDK de destino](./assets/destination-sdk-visual.png)

<!--

## Types of destinations in Adobe Experience Platform {#types-of-destinations}

In Adobe Experience Platform, we distinguish between two destination types - *connections* and *extensions*. In the user interface, customers can choose between two types of connection destinations, Profile Export destinations and Segment Export destinations. For more details around the difference between the different destination types, read [Destination Types and Categories](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en).

![Destination types](./assets/types-of-destinations.png)

This documentation set provides you with all the necessary information to add your destination to Adobe Experience Platform, as a *connection*, either Profile Export or Segment Export. To set up an extension, visit the [Experience Platform Launch developer portal](https://developer.adobelaunch.com/extensions/).

-->

## Tipos de integrações compatíveis {#supported-integration-types}

Por meio do SDK de destino, o Adobe Experience Platform oferece suporte a integrações em tempo real com destinos com um endpoint da API REST. A integração em tempo real com o Experience Platform suporta recursos como:
* Transformação e agregação de mensagens
* Preenchimento retroativo de perfil
* Integração configurável de metadados para inicializar a configuração do público-alvo e a transferência de dados
* Autenticação configurável
* Um conjunto de APIs de teste e validação para que você teste e itere suas configurações de destino

Leia sobre os requisitos técnicos nos destinos no artigo [pré-requisitos de integração](./integration-prerequisites.md).


## Obter acesso ao SDK de destino {#get-access}

O acesso ao SDK de destino varia com base no seu status de parceiro ou cliente Experience Platform. Consulte a tabela abaixo para obter mais informações.


| Tipo de parceiro ou cliente | Como acessar o SDK de destino |
---------|----------|
| Fornecedor independente de software (ISV) | Associe-se ao [Adobe Exchange program](https://partners.adobe.com/exchangeprogram/experiencecloud.html) e solicite uma sandbox Experience Platform provisionada para acessar o SDK de destino. |
| Integrador de sistema (SI) | Você precisa estar no nível Gold ou Platinum no [Adobe Solution Partner Program](https://solutionpartners.adobe.com/home.html), e você terá uma sandbox Experience Platform e acesso ao SDK de destino. |
| Experience Platform customer no [pacote de ativação](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) | Por padrão, você obtém acesso às sandboxes do Experience Platform e ao SDK de destino. |
| Cliente Experience Platform no [pacote CDP em tempo real](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | Você não tem acesso ao SDK de destino, mas tem acesso a todos os destinos produzidos configurados por outras empresas usando o SDK de destino e publicados em organizações de Experience Platform. |

{style=&quot;table-layout:auto&quot;}

## Processo de alto nível {#process}

O processo para configurar seu destino no Experience Platform é descrito abaixo:

1. Se você for um ISV ou SI, consulte as informações de acesso na seção acima. [Os clientes ](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) da Adobe Experience Platform Ativation podem ignorar esta etapa.
2. [Solicitação para provisionar uma ](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) sandbox de Experience Platform e habilitar a permissão de criação de destino.
3. [Crie sua ](./configure-destination-instructions.md) integração seguindo a documentação do produto.
4. [Teste sua ](./test-destination.md) integração seguindo a documentação do produto.
5. [Envie sua ](./destination-publish-api.md) integração para análise do Adobe (o tempo de resposta padrão é de 5 dias úteis).
6. Se você for um ISV ou SI criando um [productized integration](./overview.md#productized-custom-integrations), use o [self-service documentation process](./docs-framework/documentation-instructions.md) para criar uma página de documentação de produto no Experience League para seu destino.
7. Depois de aprovada pelo Adobe, sua integração será exibida no [Experience Platform catalog](/help/destinations/catalog/overview.md).
8. Se quiser atualizar sua integração, siga o mesmo processo.

## Referência {#reference}

O Adobe recomenda que você leia e entenda a seguinte documentação do Experience Platform:

* [Visão geral dos destinos Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [Base da composição do esquema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en)
* [Visão geral do namespace de identidade](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=pt-BR)
