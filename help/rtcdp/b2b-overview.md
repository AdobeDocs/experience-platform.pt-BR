---
keywords: RTCDP; CDP; B2B Edition; Real-time Customer Data Platform; plataforma de dados do cliente em tempo real; cdp em tempo real; b2b; cdp; Customer AI
title: Visão geral da CDP B2B Edition em tempo real
description: Visão geral da conta do Real-time Customer Data Platform B2B Edition
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 1%

---

# Visão geral do Real-time Customer Data Platform B2B Edition

Baseada na Real-time Customer Data Platform (CDP em tempo real), a CDP B2B Edition em tempo real é projetada especificamente para profissionais de marketing que operam em um modelo de serviço de negócios para empresas. Ele reúne dados de várias fontes e os combina em uma única visualização de pessoas e perfis de conta. Esses dados unificados permitem que os profissionais de marketing direcionem com precisão públicos-alvo específicos e os envolvam em todos os canais disponíveis.

Há melhorias em uma variedade de recursos do Adobe Experience Platform que distinguem a CDP B2B Edition em tempo real da sua contraparte B2C. Eles incluem aprimoramentos no Experience Data Model (XDM) para casos de uso B2B, atualizações para resolução de identidade e segmentação de perfil, bem como um conector e destino personalizado para [!DNL Marketo Engage]. O [!DNL Marketo] O conector permite que marcas B2B conectem seus dados de envolvimento B2B líderes do setor com informações comportamentais para alimentar leads e aprimorar operações de marketing baseadas em conta.

Com a CDP B2B Edition em tempo real, você pode:

* Combine dados coletados de várias fontes em uma única visualização para criar pessoas holísticas e perfis de conta.
* Enriqueça, segmente e exporte todos os seus dados entre origens de um armazenamento centralizado de perfis de conta unificados.
* Gerencie seus dados usando ferramentas de controle de dados disponíveis em cada etapa do processo de centralização para garantir que seus dados estejam em conformidade com os regulamentos legais e as políticas de negócios.

Detalhes mais abrangentes sobre as melhorias feitas para a CDP B2B Edition em tempo real são divididos nas seções abaixo.

## XDM

A CDP B2B Edition em tempo real oferece várias novas classes de esquema XDM, grupos de campos e tipos de relacionamento para capturar e estruturar seus dados especificamente para fins B2B. Consulte a visão geral em [XDM na CDP B2B em tempo real](./schemas/b2b.md) para obter um detalhamento de cada uma dessas melhorias.

Ao usar esquemas B2B pré-configurados, é possível trazer dados para uma estrutura padronizada e acionável. Muitas das novas classes de esquema mapeiam quase diretamente para as encontradas em CRMs principais, como [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo]e outras fontes de dados B2B. Com a CDP B2B Edition em tempo real, você pode trazer dados de fontes B2B para a plataforma de maneira simples e com resultados fáceis de auditar.

Essas melhorias no XDM permitem assimilar e ativar melhor os dados por fontes e destinos centrados em B2B, melhorando a unificação e a apresentação de dados para casos de uso mais diversos e flexíveis.

## Resolução de identidade

Depois que os esquemas são definidos e os dados são assimilados de acordo com esses esquemas, a CDP B2B Edition em tempo real identifica registros de origem que representam pessoas e negócios do mundo real por meio de um poderoso sistema de resolução de identidade em tempo real.

O sistema de resolução de identidade fornece os seguintes recursos:

* Registros de pessoas B2B e B2C combinados
* Uma hierarquia de conta de vários níveis
* Conexões de muitos para muitos e de pessoas para conta
* As identidades de pessoas e de conta são resolvidas em tempo real

O sistema de resolução de identidade foi expandido para oferecer suporte a uma classificação mais multifacetada de pessoas. O sistema permite identificar pessoas como líderes em oportunidades de negócios e clientes.

Os registros da conta sincronizados pelo CRM de origem e conectados por vários caminhos no sistema são mesclados pela Platform. O sistema reúne as pessoas associadas às oportunidades de negócio e as registradas como clientes, mas também pode preservar a distinção entre elas como um atributo, se forem identificáveis.

Identificadores correspondentes são usados para vincular e mesclar registros de conta de vários sistemas. As hierarquias da conta são preservadas ao longo deste processo. Diferenciadores são usados para examinar se uma pessoa está associada a uma conta ou não e fornecer a capacidade de separá-la da conta, se necessário.

## Perfis e segmentação

Quando a CDP B2B Edition em tempo real tiver assimilado dados e identidades resolvidas relacionadas a pessoas, empresas, atributos e comportamentos, esses dados serão usados para construir perfis. Esses perfis podem então ser segmentados em públicos-alvo navegáveis que podem ser ativados para vários destinos.

Quando implementado corretamente, o sistema rastreia pessoas usando identificadores primários exclusivos em vez de atributos que podem ser alterados, como endereços de email. Isso significa que, quando alguém muda de função, o sistema ainda os segue. A pessoa ainda é a mesma entidade, mas em vez disso está vinculada a uma nova conta. Essa funcionalidade nativa oferece um grande vetor de expansão em novas contas, à medida que o sistema segue essas pessoas como indivíduos, incluindo todos os atributos e comportamentos.

## Fontes B2B

A Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma. O [!DNL Marketo] A fonte permite que você faça stream de dados B2B para a Plataforma e mantenha esses dados atualizados usando aplicativos conectados à Plataforma. É compatível com qualquer número de instâncias de [!DNL Marketo] (o que é benéfico para grandes empresas com várias instâncias) e puxa para uma única Organização IMS, onde os dados são mesclados.

>[!NOTE]
>
>O [!DNL Marketo] source is **not** necessário para usar a CDP B2B Edition em tempo real.

Consulte a [Fontes na Real-time CDP B2B Edition](./sources/b2b.md) documentação para obter mais informações sobre o Marketo e trazer dados B2B para a plataforma.

## Destinos B2B

Destinos de Experience Platform como Google Customer Match, Facebook, LinkedIn, Marketo Engage, Amazon S3, Google Display &amp; Video 360, Google Ads e Google Ad Manager estão disponíveis e são totalmente compatíveis com a CDP B2B Edition em tempo real. O destino Marketo Engage também envia dados de associação de segmentos para fora da plataforma e os disponibiliza como listas no Marketo.

Consulte a visão geral no [Destino de Marketo Engage](../destinations/catalog/adobe/marketo-engage.md) para obter mais informações.

Para empresas com mais de um CRM, a CDP B2B Edition em tempo real oferece a opção de configurar conectores de destino para instâncias separadas de Marketo ou CRM. Se necessário, você pode configurar conectores de destino para cada instância e enviar públicos-alvo para cada uma das instâncias do CRM independentemente.

## Próximas etapas

Agora que você entende melhor os benefícios para os profissionais de marketing oferecidos pela CDP B2B Edition em tempo real, e as diferenças entre ela e a CDP em tempo real, você pode aprender a aplicar esses recursos à sua própria organização IMS.

Para entender como a CDP B2B Edition em tempo real pode beneficiar seu modelo de serviço empresa a empresa, consulte a seguinte documentação para ajudar você a começar:

* [Um exemplo de caso de uso da CDP B2B em tempo real](./b2b-use-case.md)
* [Um tutorial completo do Real-time Customer Data Platform B2B Edition](./b2b-tutorial.md)
* [Como assimilar dados](./sources/b2b.md)
* [Como acessar perfis](./profile/profile-overview.md)
* [Esquemas no Real-time Customer Data Platform B2B Edition](./schemas/b2b.md)
* [Como criar segmentos](./segmentation/b2b.md)
* [Como ativar segmentos para destinos](./destinations/b2b.md)
* [Como definir e aplicar políticas de controle de dados](./privacy/data-governance-overview.md)
