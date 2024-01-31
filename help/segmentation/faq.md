---
title: Perguntas frequentes do Audiences
description: Descubra respostas para perguntas frequentes sobre públicos-alvo e outros conceitos relacionados à segmentação.
exl-id: 79d54105-a37d-43f7-adcb-97f2b8e4249c
source-git-commit: dbc14c639ef02b8504cc9895c6aacb6e205549b2
workflow-type: tm+mt
source-wordcount: '2746'
ht-degree: 1%

---

# Perguntas frequentes

Adobe Experience Platform [!DNL Segmentation Service] O fornece uma interface de usuário e uma API RESTful que permite criar públicos-alvo por meio de definições de segmento ou outras fontes da [!DNL Real-Time Customer Profile] dados. Esses públicos-alvo são configurados e mantidos centralmente na Platform e estão prontamente acessíveis por qualquer solução da Adobe. Veja a seguir uma lista das perguntas frequentes sobre públicos-alvo e segmentação.

## Portal de público-alvo

A seção a seguir lista perguntas relacionadas ao Audience Portal.

### Tenho acesso ao Audience Portal e à Composição de público-alvo?

O Audience Portal e a Composição de público-alvo estão disponíveis para todos os clientes do Real-Time CDP Prime e Ultimate (edições B2C, B2B e B2P) e para clientes do Journey Optimizer Select, Prime, Ultimate Starter e Ultimate.

Nesse momento, somente os públicos-alvo baseados em perfil são compatíveis. O suporte para públicos-alvo baseados em conta será adicionado em uma versão posterior.

### Os públicos-alvo pré-criados gerados externamente são compatíveis com o Audience Portal?

Sim, públicos-alvo pré-criados gerados externamente são compatíveis com o Audience Portal. Nesse momento, é possível importar um público gerado externamente por meio de um arquivo CSV. No futuro, você poderá adicionar públicos-alvo por meio de conectores de origem em lote ou baseados em fluxo.

### Quais permissões são necessárias para fazer upload de públicos-alvo gerados externamente?

Para carregar públicos gerados externamente, você precisa ter as permissões &quot;Exibir públicos-alvo/segmentos&quot;, &quot;Gerenciar públicos-alvo/segmentos&quot;, &quot;Exibir conjuntos de dados&quot;, &quot;Gerenciar conjuntos de dados&quot;, &quot;Exibir fontes&quot; e &quot;Gerenciar fontes&quot;. Não há controles de função específicos necessários para fazer upload de públicos-alvo gerados externamente.

### O que acontece quando carrego um público-alvo gerado externamente?

Ao fazer upload de um público-alvo gerado externamente, os seguintes itens são criados:

- Conjunto de dados
   - O conjunto de dados estará visível no inventário do conjunto de dados, e o nome do conjunto de dados será o **igual** como o nome do público-alvo gerado externamente que você carregou.
- Trabalho em lotes
   - Um processo em lote **automaticamente** execute quando você fizer upload de um público gerado externamente. Isso significa que você **não** É necessário aguardar a execução do trabalho de segmentação diária para ativar o público-alvo gerado externamente.
- Esquema ad hoc
   - A **novo** O esquema XDM será criado para uso com o público-alvo gerado externamente. Os campos neste esquema XDM têm namespace para uso com o conjunto de dados que também foi criado.

### O que é composto por um público-alvo gerado externamente e o que acontece com esses dados quando são importados para a Platform?

Durante o fluxo de trabalho de importação de público externo, você deve especificar qual coluna no arquivo CSV corresponde à variável **Identidade principal**. Um exemplo de identidade primária inclui endereço de email, ECID ou um namespace de identidade personalizado específico de uma organização.

Os dados associados a esta coluna de identidade primária são **somente** dados anexados ao perfil. Se não houver perfis que correspondam aos dados na coluna de identidade principal, um novo perfil será criado. No entanto, esse perfil é essencialmente um perfil órfão, pois **não** atributos ou eventos de experiência estão associados a este perfil.

Todos os outros dados dentro do público gerado externamente são considerados **atributos de carga**. Esses atributos podem **somente** para personalização e enriquecimento durante a ativação, e são **não** anexado a um perfil. No entanto, esses atributos são armazenados no data lake.

Embora o público-alvo gerado externamente possa ser referenciado ao criar públicos-alvo usando o Construtor de segmentos, os atributos de perfil individuais **não é possível** ser utilizado.

### Posso reconciliar dados de público-alvo gerados externamente com um perfil existente na Platform?

Sim, o público-alvo gerado externamente será mesclado com o perfil existente na Platform se os identificadores principais corresponderem. Esses dados podem levar até 24 horas para serem reconciliados. Se os dados do perfil ainda não existirem, um novo perfil será criado à medida que os dados forem assimilados.

### Posso usar um público gerado externamente para criar outros públicos?

Sim, qualquer público gerado externamente aparecerá no inventário de público e poderá ser usado ao criar públicos dentro da [Construtor de segmentos](./ui/segment-builder.md).

### Posso usar atributos carregados externamente como parte da segmentação?

Não pode. Os atributos de perfil devem ser atributos de longa duração, enquanto os dados de público-alvo gerados externamente que são carregados contêm apenas dados contextuais associados a esse público-alvo gerado externamente.

Os dados contextuais do público gerados externamente, ou atributos de enriquecimento, são **não** duravelmente longo, pois seu ciclo de vida está vinculado ao público-alvo carregado. Como resultado, devido à sua natureza transitória, esses atributos de enriquecimento **não** disponível para uso na segmentação.

No entanto, ao mapear os públicos-alvo para destinos em lote ou baseados em arquivo, é possível usar esses atributos de enriquecimento gerados externamente para aumentar os públicos-alvo e outras ativações downstream.

Para saber mais sobre esse recurso, leia o guia na [ativação de dados do público-alvo para destinos de exportação de perfis em lote](../destinations/ui/activate-batch-profile-destinations.md#mapping).

### Há uma política de mesclagem específica para públicos-alvo gerados externamente?

A política de mesclagem padrão específica da organização é aplicada automaticamente ao carregar públicos gerados externamente. No entanto, é possível alterar a política de mesclagem aplicada ao público gerado externamente durante o fluxo de trabalho de importação de público.

### Onde posso ativar públicos gerados externamente para o?

Um público gerado externamente pode ser mapeado para qualquer destino RTCDP e pode ser usado em campanhas do Adobe Journey Optimizer.

### Quando os públicos-alvo gerados externamente estão prontos para ativação?

Se ativados para um destino de transmissão, os dados do público-alvo gerado externamente estarão disponíveis em duas horas.

Se ativados para um destino em lote, os dados do público-alvo gerado externamente serão sincronizados com o próximo trabalho de segmentação de 24 horas.

### Posso excluir um público-alvo gerado externamente?

Nesse momento, só é possível desativar um público gerado externamente. Nesse estado, os perfis **irá** permanecem ativos para uso em aplicativos downstream. O suporte para excluir públicos-alvo gerados externamente será adicionado em uma versão subsequente.

### O que devo fazer se fiz upload acidentalmente de um público-alvo gerado externamente?

Se você tiver carregado acidentalmente um público-alvo gerado externamente e quiser remover os dados, é possível limpar os perfis associados ao público-alvo carregando um arquivo CSV com uma linha e nenhum dado.

### Por quanto tempo os públicos-alvo gerados externamente duram?

A expiração dos dados atuais de públicos gerados externamente é **30 dias**. Essa expiração de dados foi escolhida para reduzir a quantidade de dados em excesso armazenados em sua organização.

Depois que o período de expiração dos dados passar, o conjunto de dados associado ainda estará visível no inventário do conjunto de dados, mas você **não** ser capaz de ativar o público-alvo e a contagem de perfis será exibida como zero.

### O que representam os diferentes estados do ciclo de vida?

O gráfico a seguir explica os diferentes status do ciclo de vida, o que eles representam, onde os públicos-alvo com esse status podem ser usados, bem como o impacto nas medidas de proteção de segmentação.

| Estado | Definição | Visível no Audience Portal? | Visível nos destinos? | Afeta os limites de segmentação? | Impacto nos públicos-alvo baseados em arquivos | Impacto na avaliação do público-alvo | Pode ser usado em outros públicos-alvo? |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Rascunho | Um público-alvo na **Rascunho** state é um público que ainda está em desenvolvimento e não está pronto para ser usado em outros serviços. | Sim, mas pode ser oculto. | Não | Sim | Podem ser importadas ou atualizadas durante o processo de refinamento. | Podem ser avaliadas para obter contagens precisas de publicações. | Sim, mas não é recomendável usar. |
| Publicado | Um público-alvo na **Publicado** O estado do é um público-alvo pronto para uso em todos os serviços downstream. | Sim | Sim | Sim | Pode ser importado ou atualizado. | Avaliado usando segmentação em lote, de fluxo ou de borda. | Sim |
| Inativo | Um público-alvo na **Inativo** estado é um público que não está em uso no momento. Ele ainda existe na Platform, mas continuará **não** ser utilizável até que seja marcado como rascunho ou publicado. | Não, mas pode ser exibido. | Não | Não | Não é mais atualizado. | Não é mais avaliado ou atualizado pela Platform. | Sim |
| Excluído | Um público-alvo na **Excluído** estado é um público-alvo que foi excluído. A exclusão real dos dados pode levar alguns minutos para ser executada. | Não | Não | Não | Os dados subjacentes são excluídos. | Não ocorre avaliação ou execução de dados após a conclusão da exclusão. | Não |
| Ativo | Este status foi **obsoleto** e é substituída pela **Publicado** status. | N/D | N/D | N/D | N/D | N/D | N/D |

### Como o Audience Portal e a Composição de público-alvo interagem com o lançamento dos dados de parceiros da Real-Time CDP?

O Portal de público-alvo e a Composição de público-alvo interagirão com os Dados do parceiro de duas maneiras:

1. Se você assimilar uma lista de clientes potenciais fornecida pelo parceiro usando a classe e o fluxo de trabalho Perfil do cliente potencial, os clientes potenciais serão mantidos **separadamente** dos perfis de cliente de mesclagem no Serviço de perfil. Como resultado, isso significa que as listas de clientes potenciais serão **não** aparecem no Portal de público-alvo ou na Composição de público-alvo para uso.
2. Se você estiver utilizando atributos fornecidos pelo parceiro para enriquecer **existente** perfis primários, esses públicos-alvo enriquecidos com dados de parceiros **irá** aparecem no Portal de público-alvo e na Composição de público-alvo para uso.

### Como posso usar atributos adicionais com meus públicos-alvo?

Com os públicos-alvo, **dois** diferentes tipos de atributos adicionais que você pode adicionar — atributos de carga (contextuais) e atributos de enriquecimento.

Os atributos de carga são atributos assimilados como parte do upload de CSV de um público gerado externamente. Esses atributos são **não** assimilado no Perfil do cliente em tempo real, mas pode ser usado como parte de um destino downstream.

Os atributos de enriquecimento são atributos que vêm de um conjunto de dados e são unidos a um público na Composição do público-alvo. Esses atributos só podem ser usados atualmente em campanhas do Adobe Journey Optimizer. O suporte para Adobe Journey Optimizer jornada será lançado em breve, com suporte para destinos downstream aguardando lançamento futuro.

| Canal de ativação | Públicos-alvo de upload personalizado para CSV | Públicos da composição de público-alvo |
| --- | --- | --- |
| Destinos do Real-Time CDP | Os atributos de carga e os públicos-alvo podem ser ativados. | Somente o público-alvo pode ser ativado. Atributos de enriquecimento **não é possível** ser ativados. |
| Campanhas do Adobe Journey Optimizer | Nem o público-alvo nem os atributos de carga podem ser ativados. | É possível ativar o público-alvo e os atributos de enriquecimento. |

## Inventário de público

As seções a seguir listam as perguntas relacionadas ao inventário de público-alvo no Portal de público-alvo.

### Preciso de permissões adicionais para usar os recursos de inventário de público-alvo?

Não, você não. Desde que você tenha permissões de edição para públicos-alvo, será possível criar, atualizar e gerenciar suas pastas e tags no Portal de público-alvo. Para obter mais informações sobre o gerenciamento de permissões, leia a [guia gerenciar permissões](../access-control/ui/permissions.md).

### Há um limite para o número de pastas que posso criar?

Não, não há limite para o número de pastas que você pode criar. Para obter mais informações sobre pastas, leia a [seção inventário de público](./ui/overview.md#folders) da visão geral da interface do usuário do serviço de segmentação.

### Há um limite para o número de tags que podem ser adicionadas a um público-alvo?

Não, não há limite para o número de tags que podem ser adicionadas a um público-alvo. Para obter mais informações sobre tags, leia a [seção inventário de público](./ui/overview.md#tags) da visão geral da interface do usuário do serviço de segmentação.

### Há um limite para o número de tags que posso criar?

Não, não há limite para o número de tags que podem ser criadas. No entanto, é possível criar um máximo de **100** categorias a serem aplicadas às tags. Para obter mais informações sobre o gerenciamento de tags, leia a [Guia de gerenciamento de tags](../administrative-tags/ui/managing-tags.md).

### Quando procuro um público-alvo por nome ou tag em uma pasta principal, também posso pesquisar pelas pastas secundárias relacionadas?

Não, esse comportamento não é compatível. No entanto, é possível alterar a exibição do inventário de público-alvo para analisar **Todos os públicos-alvo**, em seguida, pesquise em todas as pastas. Para obter mais informações sobre como usar a pesquisa no inventário de público-alvo, leia a [seção de pesquisa](./ui/overview.md#search) da visão geral da interface do usuário do serviço de segmentação.

### Posso atribuir automaticamente um público-alvo a uma pasta no momento da criação?

Nesse momento, não. No entanto, esse recurso pode estar disponível no futuro.

### Posso mover vários públicos-alvo para uma pasta ao mesmo tempo?

Nesse momento, não. No entanto, esse recurso pode estar disponível no futuro.

## Composição de público-alvo

A seção a seguir lista perguntas relacionadas à Composição do público-alvo.

### Quando devo usar a Composição de público-alvo em vez de usar o Construtor de segmentos?

A composição do público-alvo e o Construtor de segmentos têm funções importantes na criação de públicos-alvo de construção na Platform.

O Construtor de segmentos é mais adequado para o público-alvo **criação** (para criar um público do zero), enquanto a Composição de público-alvo é mais adequada para o público **curadoria e personalização** (para criar novos públicos-alvo com base em um público-alvo existente).

A tabela a seguir ilustra a diferença entre os dois serviços:

| Construtor de segmentos | Composição de público-alvo |
| --------------- | -------------------- |
| <ul><li>Geração de público-alvo de estágio único</li><li>Cria os blocos básicos de públicos-alvo a partir de dados de perfil, série temporal e várias entidades</li><li>Usado para criar **um** público</li></ul> | <ul><li>Geração de público-alvo em vários estágios, usando operações baseadas em conjuntos</li><li>Usa os públicos-alvo criados pelo Construtor de segmentos e aplica opções de enriquecimento de dados, como classificação de atributos de perfil e divisão em subpúblicos-alvo</li><li>Usado para criar **múltiplo** públicos de uma só vez</li></ul> |

Para saber mais sobre o Construtor de segmentos, leia o [Guia do Construtor de segmentos](./ui/segment-builder.md). Para saber mais sobre a Composição de público-alvo, leia o [Guia de composição de público-alvo](./ui/audience-composition.md).

### Posso usar públicos gerados externamente na Composição de público-alvo?

Nesse momento, não. No entanto, esse recurso deve estar disponível em breve.

### Posso enviar públicos-alvo da Composição de público-alvo para todos os destinos e canais de downstream?

Nesse momento, não. Atualmente, você pode usar públicos-alvo da Composição de público-alvo em campanhas do Adobe Journey Optimizer e destinos do Real-Time CDP. O Adobe Journey Optimizer Jornada será compatível em uma versão futura.

### Existem medidas de proteção para o número de composições?

Nesse momento, você só pode ter **10** composições publicadas por sandbox. Esta garantia será aumentada em uma versão futura.

### Quais são as medidas de proteção do fluxo de trabalho para a Composição de público-alvo?

O componente de composição &quot;colocação&quot; segue uma estrutura rígida, como se segue:

1. Você **sempre** comece com o [!UICONTROL Público] para selecionar sua atividade inicial. Você pode ter no máximo **um** [!UICONTROL Público] bloco.
2. Opcionalmente, é possível adicionar um [!UICONTROL Excluir] bloco que segue o [!UICONTROL Público] bloco.
3. Opcionalmente, é possível adicionar um [!UICONTROL Enriquecer] bloco que segue o [!UICONTROL Excluir] bloco. Você só pode usar **um** [!UICONTROL Enriquecer] bloco por composição.
4. Opcionalmente, é possível adicionar um [!UICONTROL Classificação] ou [!UICONTROL Split] bloco. Você pode **somente** têm um desses blocos por composição.
5. Você **sempre** terminar com um [!UICONTROL Salvar] bloco para salvar o público-alvo.

Além disso, as seguintes restrições (?) aplicar ao usar estes blocos:

- Dividir bloco
   - Este bloco só suporta **String** tipos de dados. O bloco Split não **não** oferecem suporte ao tipo de dados date ou boolean.
   - Além disso, esse bloco não **não** suportar atributos de enriquecimento.
- Excluir bloco
   - Este bloco não **não** oferecem suporte ao tipo de dados date ou boolean.
- Bloco de classificação
   - Este bloco não **não** suportar atributos de enriquecimento.

Para obter mais detalhes sobre como usar a Composição de público-alvo, leia a [Guia da interface do usuário da Composição de público-alvo](./ui/audience-composition.md).

### Quando os públicos-alvo criados usando a Composição de público-alvo são salvos e avaliados?

Os públicos-alvo são salvos automaticamente ao criá-los na Composição de público-alvo. O horário de criação do público será a primeira vez que esse salvamento automático ocorrerá.

Depois que o público-alvo é criado, pode levar até 24 horas para ser avaliado.

### Quando posso usar o público-alvo que criei?

O público-alvo criado na Composição de público-alvo será **imediatamente** apareça no Audience Portal. No entanto, para usá-lo no Adobe Journey Optimizer, você deve aguardar pelo menos 24 horas após a avaliação.

### Os trabalhos de avaliação estão visíveis na seção de monitoramento?

No momento, os trabalhos de avaliação são **não** exibido na interface do usuário de monitoramento.

### Posso usar uma composição de público-alvo em outra composição?

Não, públicos-alvo criados usando a Composição de público-alvo **não é possível** ser usado como entrada em outra composição de público-alvo.

### Como a divisão funciona na Composição do público-alvo?

A divisão de público-alvo permite ainda subdefinir o público-alvo em grupos menores.

Ao dividir por atributo, há exclusividade mútua entre os grupos. Isso significa que se um registro atender aos critérios de vários caminhos divididos, ele receberá a **primeiro** caminho a partir da esquerda e **não** atribuído a qualquer outro caminho.

Ao dividir por porcentagem, as divisões são **aleatoriamente** concluído. Isso significa que os perfis serão atribuídos aleatoriamente a cada caminho. A divisão é **não** persistente, para que o perfil possa estar em um subpúblico-alvo diferente em cada avaliação.

Para obter mais informações sobre o bloco Split, leia o [Guia da interface do usuário da Composição de público-alvo](./ui/audience-composition.md#split).

### Posso usar todos os tipos de segmentação no fluxo de trabalho de Composição de público-alvo?

Sim, todos os tipos de segmentação ([segmentação em lote, segmentação por transmissão e segmentação de borda](./home.md#evaluate-segments)) são compatíveis com o fluxo de trabalho Composição de público-alvo. No entanto, como as composições atualmente são executadas apenas uma vez por dia, mesmo se os públicos avaliados por transmissão ou borda forem incluídos, o resultado será baseado na associação do público no momento em que a composição foi executada.

## Como posso confirmar a associação de um perfil em um público-alvo?

Para confirmar a associação de público-alvo de um perfil, visite a página de detalhes do perfil do perfil que deseja confirmar. Selecionar **[!UICONTROL Atributos]**, seguido por **[!UICONTROL Exibir JSON]** e você poderá confirmar que a variável `segmentMembership` O objeto contém a ID do público-alvo.
