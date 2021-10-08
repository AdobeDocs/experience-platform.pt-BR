---
keywords: RTCDP; CDP; Real-time Customer Data Platform; plataforma de dados do cliente em tempo real; cdp em tempo real; cdp; rtcdp
title: Exemplo de caso de uso para Real-time Customer Data Platform B2B Edition
description: Este cenário de exemplo fornece um exemplo para a configuração de sua implementação do Real-time Customer Data Platform B2B Edition.
exl-id: 15505980-ac33-44b2-8989-c08cbabd212b
source-git-commit: 4ebc3ef813c3c44aa2b8a7aab5ccabbcc3c332b2
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 1%

---

# Exemplo de caso de uso para Real-time Customer Data Platform B2B Edition

>[!IMPORTANT]
>
>A CDP Business-to-Business Edition em tempo real está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

O Real-time Customer Data Platform B2B Edition expande as ofertas de CDP em tempo real e Adobe Experience Platform existentes para oferecer suporte a dados e fluxos de trabalho B2B. Este documento fornece um exemplo de caso de uso que demonstra os benefícios adicionais fornecidos pela B2B Edition. Eles incluem:

- Combine dados de pessoas e contas de diferentes fontes de dados em silos para produzir uma exibição abrangente que permita uma melhor compreensão dos clientes e uma segmentação mais precisa. Consulte a documentação sobre [criação de relações de esquema XDM](./schemas/b2b.md) para uso com fontes B2B variadas para obter mais informações.
- Segmente um público-alvo com base em atributos de entidades relacionadas. Isso inclui contas, oportunidades, campanhas e listas de marketing. Os segmentos não estão mais limitados a atributos de Pessoa e Eventos de Experiência. Consulte a [documentação de segmentação B2B](./segmentation/b2b.md) para obter mais exemplos de criação de públicos-alvo específicos de B2B.
- Oferece suporte nativo ao caso de uso de uma pessoa relacionada a várias contas.

## Caso de uso

A Bodea, uma empresa de tecnologia, tem um novo produto e deseja direcionar simultaneamente os clientes com um e-mail e uma campanha publicitária da LinkedIn. Para maximizar a eficiência de sua campanha de marketing, a Bodea também quer direcionar as pessoas associadas a essa conta existente que gastaram mais de um milhão de dólares em seus produtos anteriormente, E já visitaram a nova página de produtos no último mês.

No entanto, a Bodea tem duas linhas de negócio diferentes. A primeira linha de negócios da Bodea, a &quot;Linha 1&quot;, cria softwares para a indústria automobilística. Sua segunda linha de negócios, a &quot;Linha 2&quot;, vende impressoras 3D que criam peças de automóveis. Como resultado das duas linhas de negócios do Bodea, os dados de receita gerados nas contas de clientes do Bodea não são unificados em uma única visualização.

Cada linha de negócios tem seu próprio sistema de vendas: &quot;CRM 1&quot; e &quot;CRM 2&quot;. Ambos os sistemas de vendas CRM estão conectados à sua própria plataforma de automação de marketing &quot;Marketo 1&quot; e &quot;Marketo 2&quot;. Os dados do CRM 1 são sincronizados apenas no Marketo 1 e os dados do CRM2 são sincronizados apenas no Marketo 2. Em última análise, seus dados são mantidos em diferentes silos de informações corporativas.

<!-- ![lines of business diagram](./assets/lines-of-business.png) -->

## Situação atual dos dados

Como as duas linhas de negócios da Bodea vendem para a Townsend, os dados comerciais da Townsend são registrados como duas contas separadas em cada sistema de vendas.

No Marketo 1, Townsend é registrado como Conta 1. Ela tem duas pessoas relacionadas (p1@townsend.com e p2@townsend.com) e uma oportunidade vencida de $200k (&quot;Oportunidade 1&quot;) no CRM 1. Esses dados são sincronizados do CRM 1 para o Marketo 1.

No Marketo 2, Townsend é registrado como Conta 2. A Conta 2 também tem duas pessoas relacionadas (p2@townsend.com e p3@townsend.com) e uma oportunidade vencida de US$ 900k (&quot;Oportunidade 2&quot;) no CRM 2. Esses dados são sincronizados do CRM 2 para o Marketo 2.

Para fins de integração e de controle corporativo adicional, o Bodea também tem um sistema Principal de Gestão de Dados (MDM), onde mantém um registro indicando que a Conta 1 no Marketo 1 (e o CRM 1) e a Conta 2 no Marketo 2 (e o CRM 2) são a mesma empresa.

No último mês, `p2@townsend.com` visitou a nova página de produto e a visita da Web foi registrada pelo Marketo 1.

![diagrama de informações da conta](./assets/account-info.png)

## O problema

A linha 1 acabou de lançar um novo produto de software e gostaria de fazer uma venda adicional para a base de clientes de nível superior da Bodea. O Bodea inicia uma campanha de marketing tendo em mente esse público-alvo específico.

Como as informações relevantes do Townsend são registradas como Conta 1 no Marketo 1 e Conta 2 no Marketo 2, a equipe de marketing do Bodea não consegue utilizar com eficiência as informações em silos.

Isso proíbe que a equipe de marketing da Bodea tenha como alvo de maneira eficiente contatos comerciais específicos nessas empresas com essa nova oportunidade.

Até agora, Townsend gastou mais de um milhão de dólares cumulativamente em produtos da Bodea em todas as suas contas. No entanto, um segmento criado usando seu sistema antigo não incluiria ninguém do Townsend, a menos que o total gasto em um único sistema de vendas totalizasse mais de 1 milhão de dólares. Isso ocorre porque os dados de receita são colocados em contas em diferentes sistemas de vendas.

Como as despesas da Townsend são repartidas por diferentes sistemas de vendas e não totalizam individualmente mais de um milhão, o segmento não encontraria ninguém qualificado no Marketo 1 ou no Marketo 2.

### Como a CDP B2B Edition em tempo real resolve o problema

Com a CDP B2B Edition em tempo real, a equipe de marketing da Bodea pode:

- Combine os dados de todas as fontes diferentes (várias instâncias do Marketo e do CRM e o gerenciamento de dados Principal) na CDP B2B Edition em tempo real.

Com RT-CDP B2B Edition, o Bodea pode usar o Conector de fonte Marketo Engage para trazer dados B2B do Marketo 1 e Marketo 2 para o Experience Platform e manter esses dados atualizados usando aplicativos conectados à plataforma. Consulte a documentação do [Marketo source connector](../sources/connectors/adobe-applications/marketo/marketo.md) para obter mais informações.

Os dados B2B (Pessoas, Contas, Oportunidades e Atividade ) do CRM1 são sincronizados no Marketo 1. Da mesma forma, todos os dados B2B do CRM 2 são sincronizados no Marketo 2. Eles são sincronizados no Adobe Experience Platform por meio do conector de origem do Marketo. No entanto, se a Bodea quiser trazer dados adicionais de um CRM para o Experience Platform, poderá usar os Conectores CRM existentes.

Por uma questão de simplicidade e com a finalidade deste exemplo, as pessoas estão sendo identificadas por seus emails. Os dados combinados da conta para este exemplo têm a seguinte aparência:

| People |
|---|
| p1@townsend.com |
| p2@townsend.com (quem visitou a nova página do produto no mês passado) |
| p3@townsend.com |

| Oportunidades (fechadas) |
|---|
| Oportunidade 1, US$ 200 mil |
| Oportunidade 2, US$ 900 mil |

- Crie segmentos exclusivos usando esses dados agregados para iniciativas de marketing variadas. Neste exemplo, o segmento encontra todas as pessoas que:

   - Ter oportunidades associadas (em todas as contas) acima de US$ 1 milhão em valor
   - E
   - Visitaram a página do produto no último mês

- Crie um público-alvo que seja o recipient mais eficiente da nova campanha de marketing do Bodea. Neste exemplo, RT-CDP, B2B Edition ajudará o profissional de marketing a identificar `p2@townsend.com` como o alvo correto para essa campanha de marketing.

Ao usar os destinos Marketo Engage e LinkedIn, o Bodea tem uma solução completa de gerenciamento de experiência do cliente (CXM) para sua equipe de marketing. O público-alvo criado no Experience Platform é enviado para o destino do Marketo, onde é exibido como uma lista estática. Esse público-alvo é adicionado automaticamente a uma campanha de marketing do Marketo. Simultaneamente, o público-alvo também pode ser enviado para uma campanha de marketing do LinkedIn pela RT-CDP B2B Edition.

## Próximas etapas

Ao ler este documento, você foi introduzido nos tipos de objetivos e problemas que podem ser resolvidos usando a CDP B2B Edition em tempo real.

A documentação a seguir é recomendada para melhorar sua compreensão dos recursos específicos de B2B:

<!-- PLACEHOLDER Link to B2B tutorial required  -->
- [Fontes no Real-time Customer Data Platform B2B Edition](./sources/b2b.md)
- [Esquemas no Real-time Customer Data Platform B2B Edition](./schemas/b2b.md)
- [Exemplos de segmentação B2B](./segmentation/b2b.md)
- [Visão geral dos perfis da conta](./accounts/account-profile-overview.md)
- [Destinos no Real-time Customer Data Platform B2B Edition](./destinations/b2b.md)
- [Configurar um destino de públicos-alvo correspondentes ao LinkedIn](../destinations/catalog/social/linkedin.md)
