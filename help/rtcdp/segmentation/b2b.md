---
title: Casos de uso de segmentação para Real-time Customer Data Platform B2B Edition
description: Uma visão geral dos vários casos de uso disponíveis do Adobe Real-time Customer Data Platform B2B Edition.
exl-id: 2a99b85e-71b3-4781-baf7-a4d5436339d3
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '1283'
ht-degree: 0%

---

# Casos de uso de segmentação para Real-time Customer Data Platform B2B Edition

Este documento fornece exemplos de definições de segmento no Adobe Real-time Customer Data Platform B2B Edition e como diferentes tipos de atributos podem ser combinados para casos de uso comuns do B2B. Para entender como os destinos se encaixam no fluxo de trabalho B2B, consulte [tutorial completo](../b2b-tutorial.md#create-a-segment-to-evaluate-your-data).

>[!NOTE]
>
>Os atributos necessários para esses casos de uso de segmentação estão disponíveis somente para clientes do Real-time Customer Data Platform B2B Edition. Se você não estiver usando o Real-time Customer Data Platform B2B Edition, consulte [visão geral da segmentação](./segmentation-overview.md) em vez disso.

## Pré-requisitos {#prerequisites}

Antes de usar os atributos de segmentação para classes B2B, você deve concluir as seguintes etapas:

1. Crie esquemas que usam classes B2B. As classes B2B Edition incluem Conta, Campanha, Oportunidade, Lista de marketing e muito mais. Para obter informações sobre [como configurar esquemas para usar com classes B2B](../schemas/b2b.md) consulte a documentação do schema.
1. Crie relações entre seus esquemas B2B do Experience Data Model (XDM). Segmentos baseados nos atributos B2B Edition exigem relacionamentos entre as classes para usar totalmente a funcionalidade estendida de Segmentação B2B. Consulte a documentação em [como definir uma relação entre dois esquemas B2B](../../xdm/tutorials/relationship-b2b.md) para obter mais informações.
1. Assimilar dados usando conjuntos de dados com base em seus esquemas B2B. Consulte a documentação das fontes para [informações sobre como assimilar dados](../../sources/connectors/adobe-applications/marketo/marketo.md).
1. Leia o [Guia do usuário do Construtor de segmentos](../../segmentation/ui/segment-builder.md) para obter uma orientação mais detalhada sobre como criar segmentos.

Depois que esses requisitos forem atendidos, você poderá combinar esses atributos para casos de uso comuns do B2B.

## Introdução {#getting-started}

Depois que os esquemas de união para as classes B2B tiverem relações estabelecidas e tiverem sido usados para assimilar dados, seus atributos serão disponibilizados no painel esquerdo do Construtor de segmentos.

As classes B2B e seus atributos são anexados com um `B2B` no espaço de trabalho Segmentação para diferenciá-los dos disponíveis como padrão no Real-time Customer Data Platform.

Para criar segmentos de maneira eficaz para casos de uso B2B, é importante ter um conhecimento profundo do schema e entender a aparência do modelo de dados. Também é útil estar ciente do caminho que os dados levam de um objeto de dados para outro.

A imagem abaixo ilustra as relações entre as classes B2B disponíveis no Real-Time CDP B2B Edition.

![ERD de classe B2B](../assets/segmentation/b2b-classes.png)

Como seu modelo de dados pode ser complicado, você pode usar a interface do usuário da plataforma para exibir uma representação visual mais detalhada do modelo de dados para ajudar a encontrar os atributos relevantes para o caso de uso. Para iniciar, vá para a interface do usuário da plataforma e selecione Schemas no painel de navegação esquerdo.

Selecione o schema apropriado na lista disponível e selecione o relacionamento apropriado no [!UICONTROL Composição] painel lateral. No exemplo abaixo, selecionar a relação &quot;Pessoa&quot; revela qual atributo no schema atual faz referência ao schema &quot;Pessoa&quot; relacionado (se for o schema de origem no relacionamento), ou é referenciado pelo schema &quot;Pessoa&quot; (se for o schema de referência no relacionamento).

![exemplo de chave de origem usando o relacionamento de pessoas no espaço de trabalho do schema](../assets/segmentation/source-key-schema-relationship-example.png)

Essa relação é refletida no Construtor de segmentos por meio do uso de `Key` conforme mostrado na imagem abaixo.

![exemplo da chave de origem usando o construtor de segmentos no espaço de trabalho de segmentação](../assets/segmentation/source-key-segmentation-example.png)

Consulte a [esquemas na documentação do Real-time Customer Data Platform B2B Edition](../schemas/b2b.md) para obter mais informações sobre as classes B2B disponíveis.

Os casos de uso abaixo fornecem informações sobre quais classes são usadas para estabelecer relações entre os diferentes esquemas para alcançar esses resultados. Esses exemplos podem ser usados para ajudar você a criar seus próprios segmentos.

## Exemplos de casos de uso de segmentação diferente {#use-cases}

Os seguintes casos de uso estão disponíveis para segmentação com a B2B Edition. Cada exemplo fornece uma descrição do que o segmento faz e uma descrição das classes usadas para criá-las. As imagens fornecidas realçam o caminho do arquivo na [!UICONTROL Atributos] painel lateral que reflete a estrutura do schema . O [!UICONTROL Propriedades do segmento] A seção à direita da exibição contém um detalhamento escrito dos atributos do segmento.

### Exemplo 1: Encontre &quot;tomadores de decisão&quot; para oportunidades B2B {#find-decision-maker}

Encontre todas as pessoas que são o &quot;Decisor&quot; de qualquer oportunidade. Esse segmento requer um link entre as [!UICONTROL Perfil individual XDM] classe e [!UICONTROL Relação de Pessoa da Oportunidade de Negócios XDM] classe .

![Interface do usuário exibindo configurações do exemplo 1](../assets/segmentation/example-1.png)

### Exemplo 2: Localizar perfis B2B atribuídos a oportunidades em um determinado valor de dólar {#find-opportunities-amount}

Encontre todas as pessoas que são diretamente atribuídas a quaisquer oportunidades das quais a quantia de oportunidade é superior à quantia especificada (US$1 milhão). Esse segmento requer um link entre as [!UICONTROL Perfil individual XDM] classe, [!UICONTROL Relação de Pessoa da Oportunidade de Negócios XDM] classe e [!UICONTROL Oportunidade de negócios XDM] classe .

![Interface do usuário exibindo configurações do exemplo 2](../assets/segmentation/example-2.png)

### Exemplo 3: Localizar perfis B2B atribuídos a oportunidades por localização {#find-opportunities-location}

Encontre todas as pessoas que são atribuídas diretamente a qualquer oportunidade em que a conta esteja localizada em um determinado local (Canadá). Esse segmento requer um link entre as [!UICONTROL Perfil individual XDM] classe, [!UICONTROL Relação de Pessoa da Oportunidade de Negócios XDM] classe, [!UICONTROL Oportunidade de negócios XDM] classe e [!UICONTROL Conta Comercial XDM] classe .

![Interface do usuário exibindo configurações do exemplo 3](../assets/segmentation/example-3.png)

### Exemplo 4: Encontre &quot;tomadores de decisão&quot; para oportunidades por setor e comportamento de navegação {#find-industry-browsing-behavior}

Encontre todas as pessoas que são &quot;Decisores&quot; de qualquer oportunidade, onde a conta esteja no setor &quot;Finanças&quot;, e visite a página de preços nos últimos três dias. Esse segmento requer um link entre as [!UICONTROL Perfil individual XDM] classe, [!UICONTROL Relação de Pessoa da Oportunidade de Negócios XDM] classe, [!UICONTROL Oportunidade de negócios XDM] classe e [!UICONTROL Conta Comercial XDM] classe e [!UICONTROL ExperiênciaEvento XDM] classe .

![Interface do usuário exibindo configurações de exemplo 4](../assets/segmentation/example-4.png)

### Exemplo 5: Encontre perfis B2B para oportunidades por nome de departamento e quantia de oportunidade {#find-department-opportunity-amount}

Encontre todas as pessoas que trabalham em um departamento de Recursos Humanos (HR) e estão relacionadas a qualquer conta que tenha pelo menos uma oportunidade aberta no valor de um determinado valor (US$ 1 milhão) ou mais. Esse segmento requer um link entre as [!UICONTROL Perfil individual XDM] classe, [!UICONTROL Conta Comercial XDM] classe e [!UICONTROL Oportunidade de negócios XDM] classe .

![Interface do usuário exibindo configurações de exemplo 5](../assets/segmentation/example-5.png)

### Exemplo 6: Localizar perfis B2B por cargo e receita anual da conta {#find-by-job-title-and-revenue}

Encontre todas as pessoas cujo cargo é Vice-presidente e estejam relacionadas a qualquer conta com receita anual do valor especificado (US$ 100 milhões) ou mais, e tenha visitado a página de preços pelo menos três vezes no último mês. Esse segmento requer um link entre as [!UICONTROL Perfil individual XDM] classe, [!UICONTROL Conta Comercial XDM] classe e [!UICONTROL ExperiênciaEvento XDM] classe .

![Interface do usuário exibindo configurações de exemplo 6](../assets/segmentation/example-6.png)

### Exemplo 7: Encontre &quot;tomadores de decisão&quot; pelo status da oportunidade e comportamento de navegação {#find-by-opportunity-status-and-browsing-behavior}

Encontre todas as pessoas que são &quot;Decisores&quot; de qualquer oportunidade perdida e visite a página de preços na última semana. Esse segmento requer um link entre as [!UICONTROL Perfil individual XDM] classe, [!UICONTROL Relação de Pessoa da Oportunidade de Negócios XDM] classe, [!UICONTROL Oportunidade de negócios XDM] classe e [!UICONTROL ExperiênciaEvento XDM] classe .

![Interface do usuário exibindo configurações do exemplo 7](../assets/segmentation/example-7.png)

### Exemplo 8: Usar contas relacionadas para expandir o alcance de segmentação {#related-accounts}

Encontre todas as pessoas que trabalham em um departamento de Recursos Humanos (HR) e estão relacionadas a qualquer conta *ou qualquer uma das contas relacionadas da conta* que tenha pelo menos uma oportunidade aberta com valor igual ou superior a ($1 milhão). Esse segmento requer um link entre as [!UICONTROL Perfil individual XDM] classe, [!UICONTROL Conta Comercial XDM] classe e [!UICONTROL Oportunidade de negócios XDM] classe .

![Interface do usuário que exibe a segmentação para contas relacionadas](../assets/segmentation/segmentation-related-accounts.png)

### Exemplo 9: Usar pontuações de lead e/ou pontuações da conta para qualificar o perfil {#account-scoring}

Encontre todos os perfis com pontuação de lead acima de 80.

![Interface do usuário que exibe a segmentação para lead preditivo e pontuação de conta](../assets/segmentation/segmentation-predictive-lead-and-account-scoring.png)

## Próximas etapas {#next-steps}

Após a leitura dessa visão geral, agora você tem uma compreensão das possibilidades de segmentação disponíveis com o Real-Time CDP, B2B Edition. Para obter mais informações sobre o Serviço de segmentação, leia o [Documentação de segmentação](../../segmentation/home.md).
