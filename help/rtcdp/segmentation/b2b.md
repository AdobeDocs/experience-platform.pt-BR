---
title: Visão geral de casos de uso de segmentação para a CDP B2B Edition em tempo real.
description: Uma visão geral dos vários casos de uso da CDP B2B em tempo real disponíveis.
exl-id: 2a99b85e-71b3-4781-baf7-a4d5436339d3
source-git-commit: cc4bd6f3b70a90b53aaaf6a4c31d23fddd8a3f44
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 1%

---

# Visão geral de casos de uso de segmentação para Real-time Customer Data Platform B2B Edition (Beta)

<!-- This document relates to this [ticket](https://jira.corp.adobe.com/browse/PLAT-100468) -->

>[!IMPORTANT]
>
>A CDP B2B Edition em tempo real está atualmente em beta. A documentação e a funcionalidade estão sujeitas a alterações.

Este documento fornece exemplos sobre a segmentação disponível para a CDP B2B Edition em tempo real e como os diferentes tipos de atributos podem ser combinados para casos de uso comuns B2B.

>[!NOTE]
>
>Os atributos necessários para esses casos de uso de segmentação estão disponíveis somente para clientes do Real-time Customer Data Platform B2B Edition. Para saber mais sobre a CDP em tempo real, incluindo os recursos e funcionalidades disponíveis para cada tipo de licença, comece lendo a [Visão geral da CDP em tempo real](../overview.md).

## Pré-requisitos

Antes de usar os atributos de segmentação para classes B2B, você deve concluir as seguintes etapas:

1. Crie esquemas que usam classes B2B. As classes B2B Edition incluem Conta, Campanha, Oportunidade, Lista de marketing e muito mais. Para obter informações sobre [como configurar schemas para uso com classes B2B](../schemas/b2b.md), consulte a documentação do schema.
1. Crie relações entre seus esquemas B2B do Experience Data Model (XDM). Segmentos baseados nos atributos B2B Edition exigem relacionamentos entre as classes para usar totalmente a funcionalidade estendida de Segmentação B2B. Consulte a documentação sobre [como definir uma relação entre dois esquemas B2B](../../xdm/tutorials/relationship-b2b.md) para obter mais informações.
1. Assimilar dados usando conjuntos de dados com base em seus esquemas B2B. Consulte a documentação das fontes para obter [informações sobre como assimilar dados](../../sources/connectors/adobe-applications/marketo/marketo.md).
1. Leia o [Guia do usuário do Construtor de segmentos](../../segmentation/ui/segment-builder.md) para obter uma orientação mais detalhada sobre como criar segmentos.

Depois que esses requisitos forem atendidos, você poderá combinar esses atributos para casos de uso comuns do B2B.

## Introdução

Depois que os esquemas de união para as classes B2B tiverem relações estabelecidas e tiverem sido usados para assimilar dados, seus atributos serão disponibilizados no painel esquerdo do Construtor de segmentos.

As classes B2B e seus atributos são anexados com um rótulo `B2B` no espaço de trabalho de Segmentação para diferenciá-los dos disponíveis como padrão no Real-time Customer Data Platform.

Para criar segmentos de maneira eficaz para casos de uso B2B, é importante ter um conhecimento profundo do schema e entender a aparência do modelo de dados. Também é útil estar ciente do caminho que os dados levam de um objeto de dados para outro.

A imagem abaixo ilustra as relações entre as classes B2B disponíveis na CDP B2B Edition em tempo real.

![ERD de classe B2B](../assets/segmentation/b2b-classes.png)

Como seu modelo de dados pode ser complicado, você pode usar a interface do usuário da plataforma para exibir uma representação visual mais detalhada do modelo de dados para ajudar a encontrar os atributos relevantes para o caso de uso. Para iniciar, vá para a interface do usuário da plataforma e selecione Schemas no painel de navegação esquerdo.

Selecione o schema apropriado na lista disponível e selecione o relacionamento apropriado no painel lateral [!UICONTROL Composition]. No exemplo abaixo, selecionar a relação &quot;Pessoa&quot; revela qual atributo no schema atual faz referência ao schema &quot;Pessoa&quot; relacionado (se for o schema de origem no relacionamento), ou é referenciado pelo schema &quot;Pessoa&quot; (se for o schema de destino no relacionamento).

![exemplo de chave de origem usando o relacionamento de pessoas no espaço de trabalho do schema](../assets/segmentation/source-key-schema-relationship-example.png)

Essa relação é refletida no Construtor de segmentos por meio do uso de pastas `Key` , conforme mostrado na imagem abaixo.

![exemplo da chave de origem usando o construtor de segmentos no espaço de trabalho de segmentação](../assets/segmentation/source-key-segmentation-example.png)

Consulte os [schemas na documentação do Real-time Customer Data Platform B2B Edition](../schemas/b2b.md) para obter mais informações sobre as classes B2B disponíveis.

Os casos de uso abaixo fornecem informações sobre quais classes são usadas para estabelecer relações entre os diferentes esquemas para alcançar esses resultados. Esses exemplos podem ser usados para ajudar você a criar seus próprios segmentos.

## Exemplos de casos de uso diferentes

Os seguintes casos de uso estão disponíveis para segmentação com a B2B Edition. Cada exemplo fornece uma descrição do que o segmento faz e uma descrição das classes usadas para criá-las. As imagens fornecidas destacam o caminho do arquivo no painel lateral [!UICONTROL Attributes] que reflete a estrutura do schema. A seção [!UICONTROL Segment properties] à direita da exibição contém um detalhamento escrito dos atributos do segmento.

### Exemplo 1

Encontre todas as pessoas que são o &quot;Decisor&quot; de qualquer oportunidade. Este segmento requer um link entre a classe [!UICONTROL Perfil individual XDM] e a classe [!UICONTROL Relação de pessoa de oportunidade de negócios XDM].

![Interface do usuário exibindo configurações do exemplo 1](../assets/segmentation/example-1.png)

### Exemplo 2

Encontre todas as pessoas que são diretamente atribuídas a quaisquer oportunidades das quais a quantia de oportunidade é superior à quantia especificada (US$1 milhão). Este segmento requer um link entre a classe [!UICONTROL Perfil individual XDM], [!UICONTROL Relação de pessoa de oportunidade de negócios XDM] e a classe [!UICONTROL Oportunidade de negócios XDM].

![Interface do usuário exibindo configurações do exemplo 2](../assets/segmentation/example-2.png)

### Exemplo 3

Encontre todas as pessoas que são atribuídas diretamente a qualquer oportunidade em que a conta esteja localizada em um determinado local (Canadá). Este segmento requer um link entre a classe [!UICONTROL Perfil individual XDM], [!UICONTROL Relação de pessoa de oportunidade de negócios XDM], classe [!UICONTROL Oportunidade de negócios XDM] e classe [!UICONTROL Conta de negócios XDM].

![Interface do usuário exibindo configurações do exemplo 3](../assets/segmentation/example-3.png)

### Exemplo 4

Encontre todas as pessoas que são &quot;Decisores&quot; de qualquer oportunidade, onde a conta esteja no setor &quot;Finanças&quot;, e visite a página de preços nos últimos três dias. Este segmento requer um link entre a classe [!UICONTROL Perfil individual XDM], [!UICONTROL Relação de pessoa de oportunidade de negócios XDM], classe [!UICONTROL Oportunidade de negócios XDM] e classe [!UICONTROL Conta de negócios XDM] e classe [!UICONTROL ExperiênciaXDM].

![Interface do usuário exibindo configurações de exemplo 4](../assets/segmentation/example-4.png)

### Exemplo 5

Encontre todas as pessoas que trabalham em um departamento de Recursos Humanos (HR) e estão relacionadas a qualquer conta que tenha pelo menos uma oportunidade aberta no valor de um determinado valor (US$ 1 milhão) ou mais. Este segmento requer um link entre a classe [!UICONTROL Perfil individual XDM], [!UICONTROL Conta de negócios XDM] e a classe [!UICONTROL Oportunidade de negócios XDM].

![Interface do usuário exibindo configurações de exemplo 5](../assets/segmentation/example-5.png)

### Exemplo 6

Encontre todas as pessoas cujo cargo é Vice-presidente e estejam relacionadas a qualquer conta com receita anual do valor especificado (US$ 100 milhões) ou mais, e tenha visitado a página de preços pelo menos três vezes no último mês. Este segmento requer um link entre a classe [!UICONTROL Perfil individual XDM], [!UICONTROL Conta empresarial XDM] e a classe [!UICONTROL XDM ExperienceEvent].

![Interface do usuário exibindo configurações de exemplo 6](../assets/segmentation/example-6.png)

### Exemplo 7

Encontre todas as pessoas que são &quot;Decisores&quot; de qualquer oportunidade perdida e visite a página de preços na última semana. Este segmento requer um link entre a classe [!UICONTROL Perfil individual XDM], [!UICONTROL Relação de pessoa da oportunidade de negócios XDM], classe [!UICONTROL Oportunidade de negócios XDM] e classe [!UICONTROL ExperienceEvent] XDM.

![Interface do usuário exibindo configurações do exemplo 7](../assets/segmentation/example-7.png)

## Próximas etapas

Depois de ler essa visão geral, você agora tem uma compreensão das possibilidades de segmentação que estão disponíveis usando a CDP em tempo real, a B2B Edition. Para obter mais informações sobre o Serviço de segmentação, leia a [Documentação de segmentação](../../segmentation/home.md).
