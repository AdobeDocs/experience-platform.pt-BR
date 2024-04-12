---
keywords: RTCDP;CDP;Real-time Customer Data Platform;real time customer data platform;real time cdp;cdp;rtcdp
title: Exemplo de caso de uso para o Real-time Customer Data Platform B2B Edition
description: Este modelo de cenário fornece um exemplo para a configuração da sua implementação da Adobe Real-time Customer Data Platform B2B Edition.
feature: Get Started, Use Cases, B2B
badgeB2B: label="Edição B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 15505980-ac33-44b2-8989-c08cbabd212b
source-git-commit: 2704184446f7945c744e7e2d2a8c3cda3fc12527
workflow-type: tm+mt
source-wordcount: '1151'
ht-degree: 2%

---

# Exemplo de caso de uso para o Real-time Customer Data Platform B2B Edition

O Real-time Customer Data Platform B2B Edition expande as ofertas existentes do Real-Time CDP e do Adobe Experience Platform para oferecer suporte a dados e workflows B2B. Este documento fornece um exemplo de caso de uso que demonstra os benefícios adicionais fornecidos pela B2B Edition. Eles incluem:

- Combine dados de pessoas e contas de diferentes fontes de dados em silos para produzir uma exibição abrangente que permita uma melhor compreensão dos clientes e uma segmentação mais precisa. Consulte a documentação em [criação de relacionamentos de esquema XDM](./schemas/b2b.md) para uso com fontes B2B variadas para obter mais informações.
- Segmentar um público com base em atributos de entidades relacionadas. Isso inclui Contas, Oportunidades, Campanhas e Listas de marketing. Os públicos-alvo não estão mais limitados apenas a Atributos de pessoa e Eventos de experiência. Consulte a [Documentação de segmentação B2B](./segmentation/b2b.md) para obter mais exemplos de criação de públicos-alvo específicos B2B.
- Suporte nativo ao caso de uso de uma pessoa relacionada a várias contas.

## Caso de uso

A Bodea, uma empresa de tecnologia, tem um novo produto e deseja direcionar os clientes simultaneamente a uma campanha de anúncios de e-mail e LinkedIn. Para maximizar a eficiência de sua campanha de marketing, a Bodea também deseja direcionar as pessoas associadas a essa conta existente que gastaram mais de um milhão de dólares em seus produtos anteriormente E que visitaram a nova página de produtos no mês passado.

No entanto, a Bodea tem duas linhas de negócios diferentes. A primeira linha de negócios da Bodea, a &quot;Linha 1&quot;, cria software para a indústria automotiva. Sua segunda linha de negócios &quot;Linha 2&quot; vende impressoras 3D que criam peças de automóveis. Como resultado das duas linhas de negócios da Bodea, os dados de receita gerados pelas contas de clientes da Bodea não são unificados em uma única visualização.

Cada linha de negócios tem seu próprio sistema de vendas: &quot;CRM 1&quot; e &quot;CRM 2&quot;. Ambos os sistemas de vendas de CRM estão conectados a sua própria plataforma de automação de marketing &quot;Marketo 1&quot; e &quot;Marketo 2&quot;. Os dados do CRM 1 são sincronizados somente no Marketo 1 e os dados do CRM2 são sincronizados somente no Marketo 2. Por fim, seus dados são mantidos em diferentes silos de informações corporativas.

## Situação dos dados atuais

Como ambas as linhas de negócios da Bodea vendem para a empresa Townsend, os dados de negócios Townsend são registrados como duas contas separadas em cada sistema de vendas.

No Marketo 1, Townsend é registrado como Account 1. Ela tem duas pessoas relacionadas (p1@townsend.com e p2@townsend.com) e uma oportunidade fechada de US$ 200 mil (&quot;Oportunidade 1&quot;) no CRM 1. Esses dados são sincronizados do CRM 1 com o Marketo 1.

No Marketo 2, Townsend é registrado como Account 2. A Conta 2 também tem duas pessoas relacionadas (p2@townsend.com e p3@townsend.com) e uma oportunidade fechada de US$ 900 mil (&quot;Oportunidade 2&quot;) no CRM 2. Esses dados são sincronizados do CRM 2 para o Marketo 2.

Para fins de integração e controle corporativo adicional, a Bodea também tem um sistema Master Data Management (MDM), onde mantém um registro indicando que a Conta 1 no Marketo 1 (e CRM 1) e a Conta 2 no Marketo 2 (e CRM 2) são a mesma empresa.

No último mês, `p2@townsend.com` visitou a nova página do produto e a visita à web foi registrada pelo Marketo 1.

![diagrama de informações da conta](./assets/account-info.png)

## O problema

A Linha 1 acaba de lançar um novo produto de software e gostaria de fazer uma venda adicional para a base de clientes de nível superior da Bodea. A Bodea lança uma campanha de marketing com esse público-alvo específico em mente.

Como as informações relevantes do Townsend são registradas como Account 1 no Marketo 1 e Account 2 no Marketo 2, a equipe de marketing da Bodea não pode utilizar as informações em silos de maneira eficiente.

Isso proíbe que a equipe de marketing da Bodea direcione contatos comerciais específicos com eficiência nessas empresas com essa nova oportunidade.

Até o momento, Townsend gastou mais de um milhão de dólares cumulativamente em produtos Bodea em todas as suas contas. No entanto, um público-alvo criado usando seu sistema antigo não incluiria ninguém da Townsend, a menos que o total gasto em um único sistema de vendas totalizasse mais de 1 milhão de dólares. Isso ocorre porque os dados da receita são colocados em silos nas contas em diferentes sistemas de vendas.

Como os gastos do Townsend são divididos em diferentes sistemas de vendas e não totalizam individualmente mais de um milhão, a definição do segmento não encontraria ninguém qualificado no Marketo 1 ou no Marketo 2.

### Como o Real-Time CDP B2B Edition resolve o problema

Com o Real-Time CDP B2B Edition, a equipe de marketing da Bodea pode:

- Combine os dados de todas as fontes diferentes (várias instâncias do Marketo e do CRM, e o Master Data Management) no Real-Time CDP B2B Edition.

Com o RT-CDP B2B Edition, o Bodea pode usar o Conector de origem do Marketo Engage para trazer dados B2B do Marketo 1 e Marketo 2 para o Experience Platform e manter esses dados atualizados usando aplicativos conectados à plataforma. Consulte a [Conector de origem do Marketo](../sources/connectors/adobe-applications/marketo/marketo.md) para obter mais informações.

Os dados B2B (Pessoas, Contas, Oportunidades e atividade ) do CRM1 são sincronizados no Marketo 1. Da mesma forma, todos os dados B2B do CRM 2 são sincronizados no Marketo 2. Eles são sincronizados com o Adobe Experience Platform por meio do conector de origem do Marketo. No entanto, se a Bodea quiser trazer dados adicionais de um CRM para o Experience Platform, ela poderá usar Conectores CRM existentes.

Para simplificar e para o propósito deste exemplo, as pessoas estão sendo identificadas por seus emails. Os dados da conta combinados para este exemplo são da seguinte forma:

| People |
|---|
| p1@townsend.com |
| p2@townsend.com (que visitou a nova página do produto no mês passado) |
| p3@townsend.com |

| Oportunidades (próprias) |
|---|
| Oportunidade 1, US$ 200 mil |
| Oportunidade 2, US$ 900 mil |

- Crie públicos-alvo exclusivos usando esses dados agregados para iniciativas de marketing variadas. Neste exemplo, a definição do segmento encontra todas as pessoas que:

   - Têm oportunidades associadas (em TODAS as contas) que excedem US$ 1 milhão em valor
   - AND
   - Visitaram a página do produto no mês passado

- Crie um público-alvo que seja o mais eficiente destinatário da nova campanha de marketing do Bodea. Neste exemplo, a RT-CDP, B2B Edition ajudará o profissional de marketing a identificar `p2@townsend.com` como o público-alvo correto para essa campanha de marketing.

Ao usar os destinos Marketo Engage e LinkedIn, a Bodea tem uma solução completa de gerenciamento de experiência do cliente (CXM) para sua equipe de marketing. O público-alvo criado no Experience Platform é enviado para o destino do Marketo, onde aparece como uma lista estática. Em seguida, esse público é adicionado automaticamente a uma campanha de marketing do Marketo. Simultaneamente, o público-alvo também pode ser enviado para uma campanha de marketing do LinkedIn pela RT-CDP B2B Edition.

## Próximas etapas

Ao ler este documento, você foi apresentado aos tipos de objetivos e problemas que podem ser resolvidos usando o Real-Time CDP B2B Edition.

A documentação a seguir é recomendada para melhorar a sua compreensão dos recursos específicos B2B:

- [Tutorial completo do Real-time Customer Data Platform B2B Edition](./b2b-tutorial.md)
- [Fontes na edição B2B do Real-time Customer Data Platform](./sources/b2b.md)
- [Esquemas no Real-time Customer Data Platform B2B Edition](./schemas/b2b.md)
- [Exemplos de segmentação B2B](./segmentation/b2b.md)
- [Visão geral dos perfis de conta](./accounts/account-profile-overview.md)
- [Destinos na edição B2B do Real-time Customer Data Platform](./destinations/b2b.md)
- [Configurar um destino de Públicos-alvo correspondidos do LinkedIn](../destinations/catalog/social/linkedin.md)
