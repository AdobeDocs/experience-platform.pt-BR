---
title: Perguntas frequentes do Audiences
description: Descubra respostas para perguntas frequentes sobre públicos-alvo.
source-git-commit: 4dbd20dd3ac596052a3390eb6d3731fac7095c0d
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---


# Perguntas frequentes

Adobe Experience Platform [!DNL Segmentation Service] O fornece uma interface de usuário e uma API RESTful que permite criar públicos-alvo por meio de definições de segmento ou outras fontes da [!DNL Real-Time Customer Profile] dados. Esses públicos-alvo são configurados e mantidos centralmente na Platform e estão prontamente acessíveis por qualquer solução da Adobe. Veja a seguir uma lista das perguntas frequentes sobre públicos-alvo e segmentação.

## Tenho acesso ao Audience Portal e à Composição de público-alvo?

O Audience Portal e a Composição de público-alvo estão disponíveis para todos os clientes do Real-Time CDP Prime e Ultimate (edições B2C, B2B e B2P) e para clientes do Journey Optimizer Select, Prime, Ultimate Starter e Ultimate.

Nesse momento, somente os públicos-alvo baseados em perfil são compatíveis. O suporte para públicos-alvo baseados em conta será adicionado em uma versão posterior.

## Os públicos-alvo pré-criados gerados externamente são compatíveis com o Audience Portal?

Sim, públicos-alvo pré-criados gerados externamente são compatíveis com o Audience Portal. Nesse momento, é possível importar um público gerado externamente por meio de um arquivo CSV. No futuro, você poderá adicionar públicos-alvo por meio de conectores de origem em lote ou baseados em fluxo.

## Posso reconciliar dados de público-alvo gerados externamente com um perfil existente na Platform?

Sim, o público-alvo gerado externamente será mesclado com o perfil existente na Platform se os identificadores principais corresponderem. Esses dados podem levar até 24 horas para serem reconciliados. Se os dados do perfil ainda não existirem, um novo perfil será criado à medida que os dados forem assimilados.

## Posso usar um público gerado externamente para criar outros públicos?

Sim, qualquer público gerado externamente aparecerá no inventário de público e poderá ser usado ao criar públicos dentro da [Construtor de segmentos](./ui/segment-builder.md).

## Posso usar atributos carregados externamente como parte da segmentação?

Não pode. Os atributos de perfil devem ser atributos de longa duração, enquanto os dados de público-alvo gerados externamente que são carregados contêm apenas dados contextuais associados a esse público-alvo gerado externamente.

Os dados contextuais do público gerados externamente, ou atributos de enriquecimento, são **não** duravelmente longo, pois seu ciclo de vida está vinculado ao público-alvo carregado. Como resultado, devido à sua natureza transitória, esses atributos de enriquecimento **não** disponível para uso na segmentação.

No entanto, ao mapear os públicos-alvo para destinos em lote ou baseados em arquivo, é possível usar esses atributos de enriquecimento gerados externamente para aumentar os públicos-alvo e outras ativações downstream.

Para saber mais sobre esse recurso, leia o guia na [ativação de dados do público-alvo para destinos de exportação de perfis em lote](../destinations/ui/activate-batch-profile-destinations.md#mapping).

## Posso ativar públicos gerados externamente para o Adobe Journey Optimizer?

Nesse momento, não. No entanto, esse recurso estará disponível em breve.

## Posso excluir um público-alvo gerado externamente?

Nesse momento, não. Em vez disso, você pode desativar ou arquivar esse público-alvo. Nesse estado, os perfis **irá** permanecem ativos para uso em aplicativos downstream. O suporte para excluir públicos-alvo gerados externamente será adicionado em uma versão subsequente.

## Como o Audience Portal e a Composição de público-alvo interagem com o lançamento dos dados de parceiros da Real-Time CDP?

O Portal de público-alvo e a Composição de público-alvo interagirão com os Dados do parceiro de duas maneiras:

1. Se você assimilar uma lista de clientes potenciais fornecida pelo parceiro usando a classe e o fluxo de trabalho Perfil do cliente potencial, os clientes potenciais serão mantidos **separadamente** dos perfis de cliente de mesclagem no Serviço de perfil. Como resultado, isso significa que as listas de clientes potenciais serão **não** aparecem no Portal de público-alvo ou na Composição de público-alvo para uso.
2. Se você estiver utilizando atributos fornecidos pelo parceiro para enriquecer **existente** perfis primários, esses públicos-alvo enriquecidos com dados de parceiros **irá** aparecem no Portal de público-alvo e na Composição de público-alvo para uso.

## Posso usar públicos gerados externamente na Composição de público-alvo?

Nesse momento, não. No entanto, esse recurso deve estar disponível em breve.

## Posso enviar públicos-alvo da Composição de público-alvo para todos os destinos e canais de downstream?

Nesse momento, não. Atualmente, você pode usar públicos-alvo da Composição de público-alvo nas Campanhas do Adobe Journey Optimizer e destinos da CDP em tempo real. O Adobe Journey Optimizer Jornada será compatível em uma versão futura.

## Existem medidas de proteção para o número de composições?

Nesse momento, você só pode ter **10** composições publicadas por sandbox. Esta garantia será aumentada em uma versão futura.

## Quais são as medidas de proteção do fluxo de trabalho para a Composição de público-alvo?

O componente de composição &quot;colocação&quot; segue uma estrutura rígida, como se segue:

1. Você **sempre** comece com o [!UICONTROL Público] para selecionar sua atividade inicial. Você pode ter no máximo **um** [!UICONTROL Público] bloco.
2. Opcionalmente, é possível adicionar um [!UICONTROL Excluir] bloco que segue o [!UICONTROL Público] bloco.
3. Opcionalmente, é possível adicionar um [!UICONTROL Enriquecer] bloco que segue o [!UICONTROL Excluir] bloco.
4. Opcionalmente, é possível adicionar um [!UICONTROL Classificação] ou [!UICONTROL Split] bloco. Você pode **somente** têm um desses blocos por composição.
5. Você **sempre** terminar com um [!UICONTROL Salvar] bloco para salvar o público-alvo.

Para obter mais detalhes sobre como usar a Composição de público-alvo, leia a [Guia da interface do usuário da Composição de público-alvo](./ui/audience-composition.md).

## Posso usar uma composição de público-alvo em outra composição?

Não, públicos-alvo criados usando a Composição de público-alvo **não é possível** ser usado como entrada em outra composição de público-alvo.

## Como a divisão funciona na Composição do público-alvo?

A divisão de público-alvo permite ainda subdefinir o público-alvo em grupos menores. Essa divisão força a exclusividade mútua entre os grupos. Isso significa que se um registro atender aos critérios de vários caminhos divididos, ele receberá a **primeiro** caminho a partir da esquerda e **não** atribuído a qualquer outro caminho.

Para obter mais informações sobre o bloco Split, leia o [Guia da interface do usuário da Composição de público-alvo](./ui/audience-composition.md#split).

## Posso usar todos os tipos de segmentação no fluxo de trabalho de Composição de público-alvo?

Sim, todos os tipos de segmentação ([segmentação em lote, segmentação por transmissão e segmentação de borda](./home.md#evaluate-segments)) são compatíveis com o fluxo de trabalho Composição de público-alvo. No entanto, como as composições atualmente são executadas apenas uma vez por dia, mesmo se os públicos avaliados por transmissão ou borda forem incluídos, o resultado será baseado na associação do público no momento em que a composição foi executada.

## Como posso confirmar a associação de um perfil em um público-alvo?

Para confirmar a associação de público-alvo de um perfil, visite a página de detalhes do perfil do perfil que deseja confirmar. Selecionar **[!UICONTROL Atributos]**, seguido por **[!UICONTROL Exibir JSON]** e você poderá confirmar que a variável `segmentMembership` O objeto contém a ID do público-alvo.
