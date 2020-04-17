---
keywords: Experience Platform;home;intelligent services;popular topics
solution: Experience Platform
title: Preparar dados para uso no Intelligent Services
topic: Intelligent Services
translation-type: tm+mt
source-git-commit: 1d827d1637da05d3d2afc338f48911bb23039949

---


# Preparar dados para uso no Intelligent Services

Para que os Serviços inteligentes detectem insights de seus dados de eventos de marketing, os dados devem ser semanticamente enriquecidos e mantidos em uma estrutura padrão. Os Serviços inteligentes aproveitam os schemas do Experience Data Model (XDM) para conseguir isso. Especificamente, todos os conjuntos de dados que são usados no Intelligent Services devem estar em conformidade com o schema XDM ( **Consumer Experience Eventos)** .

Este documento fornece orientação geral sobre como mapear os dados de seus eventos de marketing de vários canais para esse schema, descrevendo informações sobre campos importantes dentro do schema para ajudá-lo a determinar como mapear efetivamente seus dados para sua estrutura.

## Como entender o schema CEE

O schema ExperienceEvent do consumidor descreve o comportamento de um indivíduo, pois ele se relaciona aos eventos de marketing digital (Web ou móveis), bem como à atividade de comércio online ou offline. O uso desse schema é necessário para os Serviços inteligentes devido aos campos semânticos bem definidos (colunas), evitando nomes desconhecidos que deixariam os dados menos claros.

Como todos os schemas XDM, a mistura CEE é extensível. Em outras palavras, campos adicionais podem ser adicionados à mistura CEE e variações diferentes podem ser incluídas em vários schemas, se necessário.

Um exemplo completo da mistura pode ser encontrado no repositório [XDM](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)público e deve ser usado como referência para os campos principais descritos na seção abaixo.

### Campos principais

A tabela abaixo destaca os principais campos da mistura CEE que devem ser utilizados para que os Serviços inteligentes gerem insights úteis, incluindo descrições e links para a documentação de referência para obter mais exemplos.

| Campo XDM | Descrição | Referência |
| --- | --- | --- |
| `xdm:channel` | O canal de marketing relacionado ao ExperienceEvent. O campo inclui informações sobre o tipo de canal, o tipo de mídia e o tipo de local. **Este campo _deve_ser fornecido para que a Atribuição AI funcione com seus dados**. Consulte a [tabela abaixo](#example-channels) para ver alguns exemplos de mapeamentos. | [schema Experience canal](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) |
| `xdm:productListItems` | Uma matriz de itens que representam os produtos selecionados por um cliente, incluindo o SKU do produto, o nome, o preço e a quantidade. | [schema de detalhes comerciais](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) |
| `xdm:commerce` | Contém informações específicas de comércio sobre o ExperienceEvent, incluindo o número do pedido de compra e as informações de pagamento. | [schema de detalhes comerciais](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) |
| `xdm:web` | Representa detalhes da Web relacionados ao ExperienceEvent, como interação, detalhes da página e quem indicou. | [schema de detalhes da Web do ExperienceEvent](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) |

### canais de exemplo {#example-channels}

O `xdm:channel` campo representa o canal de marketing relacionado ao ExperienceEvent. A tabela a seguir fornece alguns exemplos de canais de marketing mapeados para XDM:

| Canal | `channel.mediaType` | `channel._type` | `channel.mediaAction` |
| --- | --- | --- | --- |
| Pesquisa paga | PAGO | PESQUISA | CLIQUE EM |
| Social - Marketing | GANHADO | SOCIAL | CLIQUE EM |
| Exibir | PAGO | EXIBIÇÃO | CLIQUE EM |
| Email | PAGO | EMAIL | CLIQUE EM |
| Quem indicou interna | PROPRIEDADE | DIRETO | CLIQUE EM |
| Exibir ViewThrough | PAGO | EXIBIÇÃO | IMPRESSÃO |
| Redirecionamento de código QR | PROPRIEDADE | DIRETO | CLIQUE EM |
| Mensagem SMS | PROPRIEDADE | SMS | CLIQUE EM |
| Dispositivo móvel | PROPRIEDADE | MÓVEL | CLIQUE EM |

## Dados de mapeamento e assimilação

Depois de determinar se seus dados da série de tempo podem ser mapeados para o schema CEE, você pode start o processo de inserir seus dados nos Serviços inteligentes. Entre em contato com os Serviços de consultoria da Adobe para ajudar a mapear seus dados para o schema e assimilá-los ao serviço.

Se você tiver uma subscrição da plataforma Adobe Experience e quiser mapear e assimilar os dados, siga as etapas descritas na seção abaixo.

### Uso da plataforma Adobe Experience

>[!NOTE] As etapas abaixo exigem uma subscrição para a plataforma Experience. Se você não tiver acesso à Plataforma, pule para a seção de [próximas etapas](#next-steps) .

Esta seção descreve o fluxo de trabalho para mapear e assimilar dados na Experience Platform para uso em Serviços inteligentes, incluindo links para tutoriais para etapas detalhadas.

#### Criar um schema CEE e um conjunto de dados

Quando estiver pronto para o start preparando seus dados para ingestão, a primeira etapa é criar um novo schema XDM que emprega a combinação CEE. Os seguintes tutoriais acompanham o processo de criação de um novo schema na interface do usuário ou na API:

* [Criar um schema na interface do usuário](../xdm/tutorials/create-schema-ui.md)
* [Criar um schema na API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT] Os tutoriais acima seguem um fluxo de trabalho genérico para criar um schema. Ao escolher uma classe para o schema, você deve usar a classe **** XDM ExperienceEvent. Depois que essa classe for escolhida, você poderá adicionar a mistura CEE ao schema.

Depois de adicionar o mixin CEE ao schema, você pode adicionar outras combinações, conforme necessário, para campos adicionais em seus dados.

Depois de criar e salvar o schema, você pode criar um novo conjunto de dados com base nesse schema. Os seguintes tutoriais acompanham o processo de criação de um novo conjunto de dados na interface do usuário ou na API:

* [Criar um conjunto de dados na interface do usuário](../catalog/datasets/user-guide.md#create) (Siga o fluxo de trabalho para usar um schema existente)
* [Criar um conjunto de dados na API](../catalog/datasets/create.md)

#### Mapear e assimilar dados

Depois de criar um schema CEE e um conjunto de dados, você pode fazer um start mapeando suas tabelas de dados para o schema e ingerir esses dados na Plataforma. Consulte o tutorial sobre como [mapear um arquivo CSV para um schema](../ingestion/tutorials/map-a-csv-file.md) XDM para obter etapas sobre como executar isso na interface do usuário. Depois que um conjunto de dados é preenchido, o mesmo conjunto de dados pode ser usado para assimilar arquivos de dados adicionais.

## Próximas etapas {#next-steps}

Este documento fornece orientação geral sobre como preparar seus dados para uso nos Serviços inteligentes. Se precisar de consultoria adicional com base no caso de uso, entre em contato com o Suporte de consultoria da Adobe.

Depois de preencher com êxito um conjunto de dados com os dados de experiência do cliente, você pode usar os Serviços inteligentes para gerar insights. Consulte os seguintes documentos para começar:

* [Visão geral do AI de atribuição](./attribution-ai/overview.md)
* [Visão geral da IA do cliente](./customer-ai/overview.md)
