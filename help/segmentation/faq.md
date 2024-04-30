---
title: Perguntas frequentes do Audiences
description: Descubra respostas para perguntas frequentes sobre públicos-alvo e outros conceitos relacionados à segmentação.
exl-id: 79d54105-a37d-43f7-adcb-97f2b8e4249c
source-git-commit: 27571f3ed57399eb588865e1a52e7569957ffbff
workflow-type: tm+mt
source-wordcount: '3976'
ht-degree: 0%

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

Sim! Públicos gerados externamente podem ser excluídos no Portal de público-alvo.

### O que devo fazer se fiz upload acidentalmente de um público-alvo gerado externamente?

Se você tiver carregado acidentalmente um público-alvo gerado externamente e quiser remover os dados, é possível limpar os perfis associados ao público-alvo carregando um arquivo CSV com uma linha e nenhum dado.

### Por quanto tempo os públicos-alvo gerados externamente duram?

A expiração dos dados atuais de públicos gerados externamente é **30 dias**. Essa expiração de dados foi escolhida para reduzir a quantidade de dados em excesso armazenados em sua organização.

Depois que o período de expiração dos dados passar, o conjunto de dados associado ainda estará visível no inventário do conjunto de dados, mas você **não** ser capaz de ativar o público-alvo e a contagem de perfis será exibida como zero.

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

## Estados do ciclo de vida {#lifecycle-states}

A seção a seguir lista perguntas relacionadas aos estados do ciclo de vida e ao gerenciamento do estado do ciclo de vida no Portal de público-alvo.

### O que representam os diferentes estados do ciclo de vida?

O gráfico a seguir explica os diferentes status do ciclo de vida, o que eles representam, onde os públicos-alvo com esse status podem ser usados, bem como o impacto nas medidas de proteção de segmentação.

| Estado | Definição | Visível no Audience Portal? | Visível nos destinos? | Afeta os limites de segmentação? | Impacto nos públicos-alvo baseados em arquivos | Impacto na avaliação do público-alvo | Pode ser usado em outros públicos-alvo? | Editável |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Rascunho | Um público-alvo na **Rascunho** state é um público que ainda está em desenvolvimento e não está pronto para ser usado em outros serviços. | Sim, mas pode ser oculto. | Não | Sim | Podem ser importadas ou atualizadas durante o processo de refinamento. | Podem ser avaliadas para obter contagens precisas de publicações. | Sim, mas não é recomendável usar. | Sim |
| Publicado | Um público-alvo na **Publicado** O estado do é um público-alvo pronto para uso em todos os serviços downstream. | Sim | Sim | Sim | Pode ser importado ou atualizado. | Avaliado usando segmentação em lote, de fluxo ou de borda. | Sim | Sim |
| Inativo | Um público-alvo na **Inativo** estado é um público que não está em uso no momento. Ele ainda existe na Platform, mas continuará **não** ser utilizável até que seja marcado como rascunho ou publicado. | Não, mas pode ser exibido. | Não | Não | Não é mais atualizado. | Não é mais avaliado ou atualizado pela Platform. | Sim | Sim |
| Excluído | Um público-alvo na **Excluído** estado é um público-alvo que foi excluído. A exclusão real dos dados pode levar alguns minutos para ser executada. | Não | Não | Não | Os dados subjacentes são excluídos. | Não ocorre avaliação ou execução de dados após a conclusão da exclusão. | Não | Não |

### Em quais estados posso editar meus públicos-alvo?

Os públicos-alvo podem ser editados nos seguintes estados do ciclo de vida:

- **Rascunho**: se um público-alvo for editado no estado de rascunho, ele permanecerá no estado de rascunho, a menos que seja publicado explicitamente.
- **Publicado**: se um público-alvo for editado no estado publicado, ele permanecerá publicado e o público-alvo será atualizado automaticamente.
- **Inativo**: se um público-alvo for editado no estado inativo, ele permanecerá inativo. Isso significa que ele não será avaliado ou atualizado. Se precisar atualizar o público-alvo, você precisará publicá-lo.

Depois que um público-alvo é excluído, ele **não é possível** ser editado.

### Para quais estados do ciclo de vida posso mover um público-alvo?

Os possíveis estados do ciclo de vida para os quais um público-alvo pode ser movido dependem do estado atual do público-alvo.

![Um diagrama descrevendo as possíveis transições de estado do ciclo de vida disponíveis para os públicos-alvo.](./images/faq/lifecycle-state-transition.png)

Se o público-alvo estiver no estado de rascunho, você poderá publicá-lo ou excluí-lo se o público-alvo não tiver dependentes.

Se o público-alvo estiver no estado publicado, você poderá desativá-lo ou excluí-lo se o público-alvo não tiver dependentes.

Se o público-alvo estiver no estado inativo, você poderá republicá-lo ou excluí-lo se o público-alvo não tiver dependentes.

### Existem limitações para públicos-alvo em determinados estados do ciclo de vida?

Os públicos-alvo no estado publicado só poderão ser movidos para outro estado se o público-alvo **não** têm dependentes. Isso significa que, se o público-alvo for usado em um serviço downstream, ele não poderá ser desativado ou excluído.

Se um público avaliado usando a segmentação em lote for republicado, isto é, quando um público passa de inativo para publicado, o público será atualizado **após** o trabalho em lotes diário. Quando for republicado pela primeira vez, os perfis e os dados serão os **igual** como quando o público-alvo foi inativado.

### Como colocar um público-alvo no estado de rascunho?

O método para colocar um público no estado de rascunho depende da origem do público.

Para públicos-alvo criados usando o Construtor de segmentos, é possível definir o público-alvo para o estado de rascunho ao selecionar &quot;[!UICONTROL Salvar como rascunho]&quot; no Construtor de segmentos.

Para públicos-alvo criados na Composição de público-alvo, os públicos-alvo são salvos automaticamente como rascunho até serem publicados.

Para públicos criados externamente, os públicos são publicados automaticamente.

Quando o público-alvo está no estado publicado, você **não é possível** alterar o público original de volta para o estado de rascunho. No entanto, se você copiar o público-alvo, ele estará no estado de rascunho.

### Como colocar um público-alvo no estado publicado?

Para públicos-alvo criados usando o Construtor de segmentos ou a Composição de público-alvo, é possível definir o público-alvo para o estado publicado ao selecionar &quot;[!UICONTROL Publish]&quot; em suas respectivas interfaces do usuário.

Os públicos-alvo criados externamente são definidos como publicados automaticamente.

### Como colocar um público-alvo no estado inativo?

Você pode colocar um público publicado no estado inativo abrindo o menu de ações rápidas no Portal de público-alvo e selecionando &quot;[!UICONTROL Desativar]&quot;.

### Como faço para republicar um público-alvo?

>[!NOTE]
>
>O estado &quot;republicado&quot; é igual ao estado publicado para o comportamento do público-alvo.

Você pode republicar um público selecionando um público que esteja no estado inativo, abrindo o menu de ações rápidas no Portal de público e selecionando [!UICONTROL Publish].

### Como colocar um público-alvo no estado excluído?

>[!IMPORTANT]
>
>Você só pode excluir públicos-alvo que estejam **não** usado em qualquer ativação downstream. Além disso, não é possível excluir um público referenciado em outro público. Se não for possível excluir o público-alvo, verifique se você está **não** usá-lo em qualquer serviço downstream ou como um bloco de construção de outro público-alvo.

Para colocar um público-alvo no estado de exclusão, abra o menu de ações rápidas no Portal de público-alvo e selecione [!UICONTROL Excluir].

### O uso de um público-alvo como público-alvo secundário afeta as transições de estado do ciclo de vida?

>[!NOTE]
>
>Um público-alvo principal é um público-alvo que **usos** outro público-alvo como uma dependência do público-alvo.
>
>Um público-alvo filho é um público-alvo que é **usado como** uma dependência para o público-alvo.

Sim, usar um público-alvo como público-alvo filho afeta os estados de ciclo de vida que o público-alvo filho e pai pode realizar.

Para que um público-alvo filho seja movido para o estado publicado, todo o público-alvo pai **deve** estar no estado publicado. Os públicos-alvo principais podem ser publicados antes da publicação do público-alvo secundário ou, se o usuário confirmar, podem ser publicados automaticamente quando o público-alvo secundário é publicado.

Para que o público-alvo principal seja movido para o estado inativo ou excluído, todos os públicos-alvo secundários **deve** ser desativados ou excluídos.

### Posso me referir a um público que esteja em um estado de ciclo de vida diferente?

Sim! Se o público-alvo estiver no estado de rascunho, você poderá fazer referência a públicos-alvo no estado publicado ou inativo. No entanto, para publicar esse público-alvo, você **deve** publicar os outros públicos-alvo principais.

## Inventário de público

A seção a seguir lista perguntas relacionadas ao inventário de público-alvo no Portal de público-alvo.

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

## associação de público

A seção a seguir lista perguntas relacionadas à associação de público-alvo.

### Como posso confirmar a associação de um perfil em um público-alvo?

Para confirmar a associação de público-alvo de um perfil, visite a página de detalhes do perfil do perfil que deseja confirmar. Selecionar **[!UICONTROL Atributos]**, seguido por **[!UICONTROL Exibir JSON]** e você poderá confirmar que a variável `segmentMembership` O objeto contém a ID do público-alvo.

### Como a segmentação em lote resolve a associação de perfis?

Os públicos avaliados usando a segmentação em lote são resolvidos diariamente, com os resultados da associação de público sendo registrados no do perfil `segmentMembership` atributo. As pesquisas de perfil geram uma versão nova do perfil no momento da pesquisa, mas isso acontece **não** atualize os resultados da segmentação em lote.

Como resultado, quando alterações são feitas no perfil, como mesclar dois perfis, essas alterações **irá** aparecem no perfil quando pesquisados, mas **não** devem refletir-se na `segmentMembership` até que o trabalho de avaliação de segmento tenha sido executado novamente.

Por exemplo, digamos que você tenha criado dois públicos mutuamente exclusivos: o público-alvo A é para pessoas que vivem em Washington e o B é para pessoas que vivem **não** viver em Washington. Há dois perfis - perfil 1 para uma pessoa que mora em Washington e perfil 2 para uma pessoa que mora em Oregon.

Quando o trabalho de avaliação de segmentação em lote é executado, o perfil 1 vai para o Público-alvo A, enquanto o perfil 2 vai para o Público-alvo B. Posteriormente, mas antes da execução do trabalho de avaliação de segmentação em lote do próximo dia, um evento que reconcilia os dois perfis entra na Platform. Como resultado, um único perfil mesclado que contém os perfis 1 e 2 é criado.

Até que o próximo trabalho de avaliação de segmento em lote seja executado, o novo perfil mesclado terá a associação de público-alvo no **ambos** perfil 1 e perfil 2. Como resultado, isso significa que será um membro de **ambos** Público-alvo A e público-alvo B, apesar de terem definições contraditórias. Para o usuário final, essa é a variável **mesma situação exata** como antes, os perfis estavam conectados, já que sempre havia apenas uma pessoa envolvida, e a Platform apenas **não** Ter informações suficientes para conectar os dois perfis.

Se você usar a pesquisa de perfil para recuperar o perfil recém-criado e observar sua associação de público-alvo, ela mostrará que é um membro de **ambos** Público-alvo A e público-alvo B, apesar de ambos terem definições contraditórias. Quando o trabalho diário de avaliação da segmentação em lote for executado, a associação de público-alvo será atualizada para refletir esse estado atualizado dos dados do perfil.

Se você precisar de mais resolução de público em tempo real, use a transmissão ou a segmentação de borda.

### Quanto tempo leva para que os dados de transmissão estejam disponíveis em workflows de segmentação em lote?

Pode levar até três horas para que os dados de transmissão estejam disponíveis em workflows de segmentação em lote.

Por exemplo, se um trabalho de segmentação em lote for executado às 21h, haverá garantia de que ele conterá a transmissão de dados assimilados **até** 18H. Transmissão de dados assimilados que foram assimilados após 18h, mas antes das 9h **maio** ser incluídos.

