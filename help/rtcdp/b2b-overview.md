---
keywords: RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;real time customer data platform;real time cdp;b2b;cdp;Customer AI
title: Visão geral da Real-Time CDP B2B Edition
description: Visão geral da conta da Real-time Customer Data Platform B2B Edition
feature: Get Started, B2B
badgeB2B: label="Edição B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 4%

---

# Visão geral da Real-time Customer Data Platform B2B Edition

Criado no Adobe Real-time Customer Data Platform (Real-Time CDP), o Real-Time CDP B2B Edition foi desenvolvido especificamente para profissionais de marketing que operam em um modelo de serviço business-to-business. A plataforma reúne dados de várias origens e os combina numa única exibição de perfis de pessoas e contas. Esses dados unificados permitem que profissionais de marketing direcionem públicos-alvo específicos com precisão e gerem engajamento em todos os canais disponíveis.

Há melhorias em uma variedade de recursos do Adobe Experience Platform que distinguem o Real-Time CDP B2B Edition de seu equivalente B2C. Eles incluem melhorias no Experience Data Model (XDM) para casos de uso de B2B, atualizações na resolução de identidade e segmentação de perfil, bem como um conector e destino personalizados para [!DNL Marketo Engage]. A variável [!DNL Marketo] O conector do permite que as marcas B2B conectem seus dados de envolvimento B2B líderes do setor com informações comportamentais, a fim de nutrir clientes potenciais e aprimorar as operações de marketing baseadas em conta.

Com o Real-Time CDP B2B Edition, você pode:

* Combine dados coletados de várias fontes em uma única visualização para criar pessoas holísticas e perfis de conta.
* Enriqueça, segmente e exporte todos os seus dados entre origens a partir de um armazenamento centralizado de perfis de conta unificados.
* Gerencie seus dados usando as ferramentas de governança de dados disponíveis em cada etapa do processo de centralização para garantir que seus dados estejam em conformidade com as regulamentações legais e as políticas de negócios.

Detalhes mais abrangentes sobre as melhorias feitas no Real-Time CDP B2B Edition estão divididos em seções abaixo.

## XDM

O Real-Time CDP B2B Edition fornece várias novas classes de esquema XDM, grupos de campos e tipos de relacionamento para capturar e estruturar seus dados especificamente para fins B2B. Consulte a visão geral em [XDM na edição B2B do Real-Time CDP](./schemas/b2b.md) para obter uma análise de cada um desses aprimoramentos.

Ao usar esquemas B2B pré-configurados, você pode trazer dados em uma estrutura padronizada e acionável. Muitas das novas classes de esquema mapeiam quase diretamente para aquelas encontradas nos principais CRMs, como [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo]e outras fontes de dados B2B. Com o Real-Time CDP B2B Edition, você pode trazer dados de fontes B2B para a Platform de uma maneira simples e com resultados fáceis de auditar.

Esses aprimoramentos do XDM permitem assimilar e ativar melhor os dados por meio de fontes e destinos centrados em B2B, melhorando a unificação e a apresentação dos dados para casos de uso mais variados e flexíveis.

## Resolução de identidade

Depois que os esquemas são definidos e os dados são assimilados em conformidade com esses esquemas, o Real-Time CDP B2B Edition identifica registros de origem que representam pessoas e empresas do mundo real por meio de um sistema poderoso de resolução de identidades em tempo real.

O sistema de resolução de identidades oferece os seguintes recursos:

* Registros de pessoas B2B e B2C combinados
* Uma hierarquia de conta de vários níveis
* Conexões muitos para muitos, pessoas para conta
* Pessoas e identidades de conta são resolvidas em tempo real

O sistema de resolução de identidades foi expandido para suportar uma classificação mais multifacetada das pessoas. O sistema permite que as pessoas sejam identificadas como líderes em oportunidades de negócios, bem como clientes.

Os registros de conta sincronizados pelo CRM de origem e conectados por vários caminhos no sistema são mesclados pela Platform. O sistema reúne as pessoas associadas a oportunidades de negócios e as registradas como clientes, mas também é capaz de preservar a distinção entre elas como um atributo, se forem identificáveis.

Os identificadores correspondentes são usados para vincular e mesclar registros de conta de vários sistemas. As hierarquias de conta são preservadas em todo esse processo. Os diferenciais são usados para analisar se uma pessoa está associada a uma conta ou não e fornecer a capacidade de separá-la da conta, se necessário.

## Perfis e segmentação

Depois que o Real-Time CDP B2B Edition tiver assimilado dados e resolvido identidades relacionadas a pessoas, empresas, atributos e comportamentos, esses dados serão usados para criar perfis. Esses perfis podem ser segmentados em públicos navegáveis que podem ser ativados para vários destinos.

Quando implementado corretamente, o sistema rastreia as pessoas usando identificadores primários exclusivos em vez de atributos que podem ser alterados, como endereços de email. Isso significa que quando alguém muda de trabalho o sistema ainda os segue. A pessoa ainda é a mesma entidade, mas em vez disso, está vinculada a uma nova conta. Essa funcionalidade nativa oferece um excelente vetor para expansão em novas contas, já que o sistema segue essas pessoas como indivíduos, incluindo todos os seus atributos e comportamentos.

## Fontes B2B

A Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da Platform. A variável [!DNL Marketo] A fonte de dados permite transmitir dados B2B para a Platform e manter esses dados atualizados usando aplicativos conectados à Platform. Ele oferece suporte a várias instâncias de [!DNL Marketo] (o que é benéfico para grandes empresas com várias instâncias) e obtém uma única organização onde os dados são mesclados.

>[!NOTE]
>
>A variável [!DNL Marketo] a origem é **não** necessário para usar o Real-Time CDP B2B Edition.

Consulte a [origens na Real-Time CDP B2B Edition](./sources/b2b.md) documentação para obter mais informações sobre o Marketo e trazer dados B2B para a Platform.

## Destinos B2B

Destinos de Experience Platform, como Google Customer Match, Facebook, LinkedIn, Marketo Engage, Amazon S3, Google Display &amp; Video 360, Google Ads e Google Ad Manager estão disponíveis e são totalmente compatíveis com o Real-Time CDP B2B Edition. O destino Marketo Engage também transmite dados de associação de segmento da Platform e os disponibiliza como listas no Marketo.

Consulte a visão geral no [Destino do Marketo Engage](../destinations/catalog/adobe/marketo-engage.md) para obter mais informações.

Para empresas com mais de um CRM, o Real-Time CDP B2B Edition fornece a opção de configurar conectores de destino para instâncias separadas do Marketo ou CRM. Se necessário, você poderá configurar conectores de destino para cada instância e enviar públicos-alvo para cada uma das instâncias do CRM de maneira independente.

## Próximas etapas

Agora que você entende melhor os benefícios para profissionais de marketing oferecidos pelo Real-Time CDP B2B Edition e as diferenças entre ele e o Real-Time CDP, você pode aprender como aplicar esses recursos à sua própria organização.

Para entender como o Real-Time CDP B2B Edition pode beneficiar seu modelo de serviço B2B, consulte a seguinte documentação para ajudá-lo a começar:

* [Um exemplo de caso de uso para o Real-Time CDP B2B Edition](./b2b-use-case.md)
* [Um tutorial completo do Real-time Customer Data Platform B2B Edition](./b2b-tutorial.md)
* [Como assimilar dados](./sources/b2b.md)
* [Como acessar perfis](./profile/profile-overview.md)
* [Esquemas no Real-time Customer Data Platform B2B Edition](./schemas/b2b.md)
* [Como criar segmentos](./segmentation/b2b.md)
* [Como ativar segmentos para destinos](./destinations/b2b.md)
* [Como definir e aplicar políticas de governança de dados](./privacy/data-governance-overview.md)
