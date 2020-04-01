---
title: Visão geral do controle de dados
seo-title: Controle de dados na plataforma de dados do cliente em tempo real
description: 'O Data Governance permite gerenciar dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. '
seo-description: 'O Data Governance permite gerenciar dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. '
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# Controle de dados em CDP em tempo real

A Plataforma de dados do cliente em tempo real (CDP em tempo real) reúne dados de vários sistemas corporativos, permitindo que os profissionais de marketing identifiquem, entendam e envolvam melhor seus clientes. Esses dados podem estar sujeitos a restrições de uso definidas pela sua organização ou por regulamentos legais. Portanto, é importante garantir que a CDP em tempo real esteja em conformidade com as políticas de uso ao manipular seus dados.

O Adobe Experience Platform Data Governance permite gerenciar dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental na CDP em tempo real, permitindo que você defina políticas de uso, classifique seus dados com base nessas políticas e verifique violações de políticas ao executar determinadas ações de marketing.

A CDP em tempo real foi desenvolvida sobre a plataforma Adobe Experience e, portanto, a maioria dos recursos de controle de dados são abordados na documentação da plataforma Experience. Este documento é destinado a complementar a visão geral [do controle de](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_overview.md) dados da plataforma Experience e descreve os recursos de controle disponíveis na CDP em tempo real. Os seguintes tópicos são abordados:

* [Aplicar rótulos de uso aos seus dados](#labels)
* [Gerenciar políticas de uso de dados](#policies)
* [Impor conformidade de uso de dados](#enforcement)

## Aplicar rótulos de uso aos seus dados {#labels}

O controle de dados permite que você aplique rótulos de uso aos seus dados, no nível do conjunto de dados ou do campo do conjunto de dados. Os rótulos de uso de dados permitem que você categorize os dados de acordo com as políticas de uso que se aplicam a esses dados.

Para obter informações detalhadas sobre como trabalhar com rótulos de uso de dados, consulte o guia [do usuário de rótulos de uso de](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/tutorials/dule/dule_working_with_labels.md) dados da Adobe Experience Platform.

## Definir restrições para destinos

É possível definir restrições de uso de dados em um destino definindo casos de uso de marketing para esse destino. A definição de casos de uso para destinos permite verificar violações da política de uso e garantir que quaisquer perfis ou segmentos enviados para esse destino sejam compatíveis com as regras de controle de dados.

Casos de uso de marketing podem ser definidos durante a fase _de Configuração_ para o fluxo de trabalho _Editar destino_ . Consulte a documentação de destino para obter mais informações.


## Gerenciar políticas de uso de dados {#policies}

Para que os rótulos de uso de dados suportem de forma eficaz a conformidade dos dados, as políticas de uso de dados devem ser definidas e ativadas. As políticas de uso de dados são regras que descrevem os tipos de ações de marketing às quais você tem permissão ou é restrito para executar em dados dentro da CDP em tempo real. Consulte a seção &quot;Políticas de uso de dados&quot; na visão geral [do Experience Platform](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_overview.md) Data Governance para obter mais informações.

A plataforma Adobe Experience fornece várias políticas **** principais para casos comuns de uso da experiência do cliente. Essas políticas podem ser visualizadas fazendo uma solicitação para a API [do serviço de política](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)DULE, como mostra a seção &quot;Lista de todas as políticas&quot; no guia [do desenvolvedor do serviço de](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_policy_service_developer_guide.md)política. Você também pode criar suas próprias políticas **** personalizadas para modelar restrições de uso personalizadas, como mostrado na seção &quot;Criar uma política&quot; no guia do desenvolvedor.

## (Beta) Reforçar a conformidade de uso de dados {#enforce-data-usage-compliance}

>[!IMPORTANT]
>Este recurso está atualmente em beta e não está disponível para todos os usuários. Ele pode ser ativado mediante solicitação. A documentação e a funcionalidade estão sujeitas a alterações.

Depois que os dados forem rotulados e as políticas de uso forem definidas, você poderá aplicar a conformidade de uso de dados com as políticas. Ao ativar segmentos de audiência para destinos em CDP em tempo real, o Data Governance automaticamente aplica as políticas de uso caso ocorram violações.

O diagrama a seguir ilustra como a aplicação de políticas é integrada ao fluxo de dados da ativação de segmentos:

![](assets/enforcement-flow.png)

Quando um segmento é ativado pela primeira vez, o Serviço de Política DULE verifica se há violações de política com base nos seguintes fatores:

* Os rótulos de uso de dados aplicados a campos e conjuntos de dados dentro do segmento a ser ativado.
* A finalidade de comercialização do destino.

### Mensagens de violação de política {#enforcement}

Se ocorrer uma violação de política ao tentar ativar um segmento (ou [fazer edições em um segmento](#policy-enforcement-for-activated-segments)já ativado), a ação será impedida e um fornecedor será exibido indicando que uma ou mais políticas foram violadas. Selecione uma violação de política na coluna esquerda do provedor para exibir detalhes dessa violação.

![](assets/violation-popover.png)

A guia *Detalhes* do fornecedor indica a ação que acionou a violação o motivo da violação e fornece sugestões para como resolver o problema.

Clique em Linhagem **de** dados para rastrear os destinos, segmentos, políticas de mesclagem ou conjuntos de dados cujos rótulos de dados acionaram a violação.

![](assets/data-lineage.png)

Depois que uma violação é acionada, o botão **Salvar** é desativado para a ativação até que os componentes apropriados sejam atualizados para atender às políticas de uso de dados.

### Aplicação de política para segmentos ativados

A imposição de políticas ainda se aplica aos segmentos depois de ativados, restringindo quaisquer alterações a um segmento ou seu destino que resultariam em uma violação de política. Devido aos diversos componentes envolvidos na ativação de segmentos para destinos, qualquer uma das ações a seguir pode possivelmente acionar uma violação:

* Atualização de rótulos de uso de dados
* Alteração de conjuntos de dados para um segmento
* Alteração de predicados de segmento
* Alteração das configurações de destino

Se qualquer uma das ações acima acionar uma violação, essa ação será impedida de ser salva e uma mensagem de violação de política será exibida, garantindo que seus segmentos ativados continuem a seguir as políticas de uso de dados ao serem modificados.

## Próximas etapas

Agora que você foi apresentado aos principais recursos de controle de dados em CDP em tempo real e como a plataforma de experiência os habilita, continue com a [documentação de controle de dados na plataforma](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html)Adobe Experience. A documentação fornece visões gerais dos conceitos essenciais do Data Governance, bem como workflows passo a passo para gerenciar rótulos e políticas de uso de dados.