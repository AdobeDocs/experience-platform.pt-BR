---
description: O Adobe Experience Platform Destination SDK é um conjunto de APIs de configuração que permitem configurar padrões de integração de destino para o Experience Platform para fornecer dados de público-alvo e de perfil ao seu terminal ou local de armazenamento, com base em dados e formatos de autenticação de sua escolha. As configurações são armazenadas no Experience Platform e podem ser recuperadas por meio da API para obter atualizações adicionais.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 2%

---

# Adobe Experience Platform Destination SDK

## Visão geral {#destinations-sdk}

O Adobe Experience Platform Destination SDK é um conjunto de APIs de configuração que permitem configurar padrões de integração de destino para o Experience Platform para fornecer dados de público-alvo e de perfil ao seu terminal ou local de armazenamento, com base em dados e formatos de autenticação de sua escolha. As configurações são armazenadas no Experience Platform e podem ser recuperadas por meio da API para obter atualizações adicionais.

A documentação do Destination SDK fornece instruções para que você use o Adobe Experience Platform Destination SDK para configurar, testar e lançar uma integração de destino produzida com o Adobe Experience Platform, e fazer com que seu destino faça parte do catálogo de destinos em crescimento. Ao usar o Destination SDK, você também pode criar seu próprio destino privado personalizado para exportar dados adaptados às suas necessidades.

![Captura de tela da interface do usuário do Experience Platform, mostrando o catálogo de destinos](./assets/destinations-catalog-overview.png)

## Integrações produzidas e personalizadas {#productized-custom-integrations}

>[!IMPORTANT]
>
> Essa funcionalidade para criar destinos personalizados privados está disponível somente para [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) clientes.

Como parceiro de Destination SDK, você pode se beneficiar com a adição do destino produzido ao [Catálogo de Experience Platform](/help/destinations/catalog/overview.md):
1. Padronize as configurações de integração entre clientes com parâmetros pré-configurados e simplifique a experiência de configuração para clientes.
2. Introduza uma placa de destino com marca no catálogo de destinos do Experience Platform para obter uma configuração e um conhecimento mais simplificados do cliente.
3. Ser apresentado como uma integração de destino produzida com o Adobe Experience Platform &amp; Adobe Real-time Customer Data Platform.

Como cliente do Experience Platform, você também pode criar um destino personalizado privado, o que pode se adequar melhor às suas necessidades de ativação.

![Um diagrama de visão geral que mostra como os desenvolvedores de destino interagem com o Destination SDK e como os clientes do Real-Time CDP se beneficiam de destinos produtivos e privados.](./assets/destination-sdk-visual.png)

## Tipos de integrações compatíveis {#supported-integration-types}

Por meio do Destination SDK, o Adobe Experience Platform oferece suporte a integrações em tempo real com destinos que têm um ponto de extremidade de API REST. A integração em tempo real com o Experience Platform suporta recursos como:
* Transformação e agregação de mensagens
* Preenchimento retroativo de perfil
* Integração configurável de metadados para inicializar a configuração do público-alvo e a transferência de dados
* Autenticação configurável
* Um conjunto de APIs de teste e validação para que você teste e itere suas configurações de destino

Por meio do Destination SDK, você também pode configurar integrações para exportar periodicamente arquivos para o local de armazenamento de sua escolha. A integração em tempo real com o Experience Platform suporta recursos como:
* Exportação de arquivo em vários formatos compatíveis (CSV, Parquet, JSON)
* Opções configuráveis de formatação de arquivos, que permitem estruturar o formato dos arquivos exportados para atender aos seus requisitos de downstream.

Leia sobre os requisitos técnicos nos destinos no [pré-requisitos de integração](./integration-prerequisites.md) artigo 10. o

## Obter acesso ao Destination SDK {#get-access}

O acesso ao Destination SDK varia com base no seu status de parceiro ou Experience Platform, cliente da Real-Time CDP. Consulte a tabela abaixo para obter mais informações.


| Tipo de parceiro ou cliente | Como acessar o Destination SDK |
---------|----------|
| Fornecedor independente de software (ISV) | Associe-se à [Programa Adobe Exchange](https://partners.adobe.com/exchangeprogram/experiencecloud.html) e para obter uma sandbox Experience Platform para acessar o Destination SDK. |
| Integrador de sistema (SI) | Você precisa estar no nível Gold ou Platinum na [Programa Adobe Solution Partner](https://solutionpartners.adobe.com/home.html)e você terá uma sandbox de Experience Platform e acesso ao Destination SDK. |
| cliente Experience Platform no [Pacote do Real-Time CDP Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | Por padrão, você obtém acesso às sandboxes e ao Destination SDK do Experience Platform, permitindo criar destinos privados para sua organização. |

{style=&quot;table-layout:auto&quot;}

## Processo de alto nível {#process}

O processo para configurar seu destino no Experience Platform é descrito abaixo:

1. Se você for um ISV ou SI, consulte as informações de acesso na seção acima. [Adobe Experience Platform Ativation](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) Os clientes do podem ignorar esta etapa.
2. [Solicitação para provisionar uma sandbox de Experience Platform](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) e ative a permissão de criação de destino.
3. Crie sua integração. Siga as instruções na documentação do produto para configurar [destinos de transmissão](./configure-destination-instructions.md) ou [destinos com base em arquivo](./configure-file-based-destination-instructions.md).
4. Teste sua integração. Siga as instruções na documentação do produto para testar [destinos de transmissão](./test-destination.md) ou [destinos com base em arquivo](./file-based-destination-testing-overview.md).
5. Se você for um ISV ou SI, crie uma [integração produzida](./overview.md#productized-custom-integrations), [enviar sua integração](./submit-destination.md) para Adobe: tempo de resposta padrão é de cinco dias úteis.
6. Se você for um ISV ou SI criando uma integração produzida, use o [processo de documentação de autoatendimento](./docs-framework/documentation-instructions.md) para criar uma página de documentação do produto no Experience League para o seu destino.
7. Para integrações produzidas, uma vez aprovadas pelo Adobe, sua integração será exibida no [Catálogo de Experience Platform](/help/destinations/catalog/overview.md).
8. Se quiser atualizar sua integração, siga o mesmo processo.

## Referência {#reference}

O Adobe recomenda que você leia e entenda a seguinte documentação do Experience Platform:

* [Visão geral dos destinos Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [Base da composição do esquema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=pt-BR)
* [Visão geral do namespace de identidade](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=pt-BR)
