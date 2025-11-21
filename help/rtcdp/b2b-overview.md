---
keywords: RTCDP;CDP;B2B edition;Real-Time Customer Data Platform;real time customer data platform;real time cdp;b2b;cdp;Customer AI
title: Visão geral do Real-Time CDP B2B edition
description: Visão geral da conta da Real-time Customer Data Platform B2B Edition
feature: Get Started, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 4%

---

# Visão geral do Real-Time Customer Data Platform B2B edition

Criada na Adobe Real-Time Customer Data Platform (Real-Time CDP), a Real-Time CDP B2B edition foi desenvolvida especificamente para profissionais de marketing que operam em um modelo de serviço business-to-business. A plataforma reúne dados de várias origens e os combina numa única exibição de perfis de pessoas e contas. Esses dados unificados permitem que profissionais de marketing direcionem públicos-alvo específicos com precisão e gerem engajamento em todos os canais disponíveis.

Há melhorias em uma variedade de recursos do Adobe Experience Platform que distinguem o Real-Time CDP B2B edition de seu equivalente B2C. Eles incluem melhorias no Experience Data Model (XDM) para casos de uso B2B, atualizações na resolução de identidade e segmentação de perfil, bem como um conector e destino personalizados para [!DNL Marketo Engage]. O conector [!DNL Marketo] permite que as marcas B2B conectem seus dados de envolvimento B2B líderes do setor com informações comportamentais para fomentar clientes potenciais e aprimorar as operações de marketing baseadas em conta.

Com o Real-Time CDP B2B edition, você pode:

* Combine dados coletados de várias fontes em uma única visualização para criar pessoas holísticas e perfis de conta.
* Enriqueça, segmente e exporte todos os seus dados entre origens a partir de um armazenamento centralizado de perfis de conta unificados.
* Gerencie seus dados usando as ferramentas de governança de dados disponíveis em cada etapa do processo de centralização para garantir que seus dados estejam em conformidade com as regulamentações legais e as políticas de negócios.

Detalhes mais abrangentes sobre as melhorias feitas no Real-Time CDP B2B edition estão divididos nas seções abaixo.

## XDM

O Real-Time CDP B2B edition fornece várias novas classes de esquema XDM, grupos de campos e tipos de relacionamento para capturar e estruturar seus dados especificamente para fins B2B. Consulte a visão geral no [XDM no Real-Time CDP B2B edition](./schemas/b2b.md) para obter um detalhamento de cada um desses aprimoramentos.

Ao usar esquemas B2B pré-configurados, você pode trazer dados em uma estrutura padronizada e acionável. Muitas das novas classes de esquema mapeiam quase diretamente para aquelas encontradas nos principais CRMs, como [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo] e outras fontes de dados B2B. Com o Real-Time CDP B2B edition, você pode trazer dados de fontes B2B para o Experience Platform de uma maneira simples e com resultados fáceis de auditar.

Esses aprimoramentos do XDM permitem assimilar e ativar melhor os dados por meio de fontes e destinos centrados em B2B, melhorando a unificação e a apresentação dos dados para casos de uso mais variados e flexíveis.

## Resolução de identidade

Depois que os esquemas são definidos e os dados são assimilados em conformidade com esses esquemas, o Real-Time CDP B2B edition identifica registros de origem que representam pessoas e empresas do mundo real por meio de um poderoso sistema de resolução de identidades em tempo real.

O sistema de resolução de identidades oferece os seguintes recursos:

* Registros de pessoas B2B e B2C combinados
* Uma hierarquia de conta de vários níveis
* Conexões muitos para muitos, pessoas para conta
* Pessoas e identidades de conta são resolvidas em tempo real

O sistema de resolução de identidades foi expandido para suportar uma classificação mais multifacetada das pessoas. O sistema permite que as pessoas sejam identificadas como líderes em oportunidades de negócios, bem como clientes.

Os registros de conta sincronizados pelo CRM de origem e conectados por vários caminhos no sistema são mesclados pela Experience Platform. O sistema reúne as pessoas associadas a oportunidades de negócios e as registradas como clientes, mas também é capaz de preservar a distinção entre elas como um atributo, se forem identificáveis.

Os identificadores correspondentes são usados para vincular e mesclar registros de conta de vários sistemas. As hierarquias de conta são preservadas em todo esse processo. Os diferenciais são usados para analisar se uma pessoa está associada a uma conta ou não e fornecer a capacidade de separá-la da conta, se necessário.

## Perfis e segmentação

Depois que o Real-Time CDP B2B edition assimilou dados e resolveu identidades relacionadas a pessoas, empresas, atributos e comportamentos, esses dados são usados para criar perfis. Esses perfis podem ser segmentados em públicos navegáveis que podem ser ativados para vários destinos.

Quando implementado corretamente, o sistema rastreia as pessoas usando identificadores primários exclusivos em vez de atributos que podem ser alterados, como endereços de email. Isso significa que quando alguém muda de trabalho o sistema ainda os segue. A pessoa ainda é a mesma entidade, mas em vez disso, está vinculada a uma nova conta. Essa funcionalidade nativa oferece um excelente vetor para expansão em novas contas, já que o sistema segue essas pessoas como indivíduos, incluindo todos os seus atributos e comportamentos.

## Fontes B2B

O Experience Platform permite que os dados sejam assimilados de fontes externas e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da Experience Platform. A fonte [!DNL Marketo] permite que você transmita dados B2B para o Experience Platform e mantenha esses dados atualizados usando aplicativos conectados à Experience Platform. Ele oferece suporte a qualquer número de instâncias de [!DNL Marketo] (o que é benéfico para grandes empresas com várias instâncias) e é extraído para uma única organização onde os dados são mesclados.

>[!NOTE]
>
>A origem [!DNL Marketo] é **não** necessária para usar o Real-Time CDP B2B edition.

Consulte as [fontes na documentação do Real-Time CDP B2B edition](./sources/b2b.md) para obter mais informações sobre o Marketo e trazer dados B2B para o Experience Platform.

## Destinos B2B

Destinos do Experience Platform, como Google Customer Match, Facebook, LinkedIn, Marketo Engage, Amazon S3, Google Display &amp; Video 360, Google Ads e Google Ad Manager estão disponíveis e têm suporte total do Real-Time CDP B2B edition. O destino do Marketo Engage também transmite dados de associação do segmento do Experience Platform e os disponibiliza como listas no Marketo.

Consulte a visão geral no [Destino do Marketo Engage](../destinations/catalog/adobe/marketo-engage.md) para obter mais informações.

Para empresas com mais de um CRM, o Real-Time CDP B2B edition fornece a opção de configurar conectores de destino para instâncias separadas do Marketo ou do CRM. Se necessário, você poderá configurar conectores de destino para cada instância e enviar públicos-alvo para cada uma das instâncias do CRM de maneira independente.

## Próximas etapas

Agora que você entende melhor os benefícios para profissionais de marketing oferecidos pelo Real-Time CDP B2B edition e as diferenças entre ele e o Real-Time CDP, você pode aprender a aplicar esses recursos à sua própria organização.

Para entender como o Real-Time CDP B2B edition pode beneficiar seu modelo de serviço business-to-business, consulte a seguinte documentação para ajudá-lo a começar:

* [Um exemplo de caso de uso para o Real-Time CDP B2B edition](./b2b-use-case.md)
* [Um tutorial completo do Real-Time Customer Data Platform B2B edition](./b2b-tutorial.md)
* [Como assimilar dados](./sources/b2b.md)
* [Como acessar perfis](./profile/profile-overview.md)
* [Esquemas no Real-Time Customer Data Platform B2B edition](./schemas/b2b.md)
* [Como criar públicos-alvo do](./segmentation/b2b.md)
* [Como ativar públicos para destinos](./destinations/b2b.md)
* [Como definir e aplicar políticas de governança de dados](./privacy/data-governance-overview.md)
