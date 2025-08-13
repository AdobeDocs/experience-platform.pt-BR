---
title: Perguntas frequentes do Audiences
description: Descubra respostas para perguntas frequentes sobre públicos-alvo e outros conceitos relacionados à segmentação.
exl-id: 79d54105-a37d-43f7-adcb-97f2b8e4249c
source-git-commit: 56bf7ae20c33b013a1710fba8c04d9edc23baf89
workflow-type: tm+mt
source-wordcount: '4849'
ht-degree: 2%

---

# Perguntas frequentes

O Adobe Experience Platform [!DNL Segmentation Service] fornece uma interface de usuário e uma API RESTful que permite criar públicos-alvo por meio de definições de segmento ou outras fontes a partir dos dados do [!DNL Real-Time Customer Profile]. Esses públicos-alvo são configurados e mantidos de forma centralizada no Experience Platform e prontamente acessíveis por qualquer solução da Adobe. Veja a seguir uma lista das perguntas frequentes sobre públicos-alvo e segmentação.

## Portal de público-alvo

A seção a seguir lista perguntas relacionadas ao Audience Portal.

### Tenho acesso ao Audience Portal e à Composição de público-alvo?

O Audience Portal e a Composição de público-alvo estão disponíveis para todos os clientes do Real-Time CDP Prime e do Ultimate (edições B2C, B2B e B2P) e clientes do Journey Optimizer Select, Prime, Ultimate Starter e Ultimate.

Nesse momento, somente os públicos-alvo baseados em perfil são compatíveis. O suporte para públicos-alvo baseados em conta será adicionado em uma versão posterior.

### Os públicos-alvo pré-criados gerados externamente são compatíveis com o Audience Portal?

Sim, públicos-alvo pré-criados gerados externamente são compatíveis com o Audience Portal. Nesse momento, é possível importar um público gerado externamente por meio de um arquivo CSV. No futuro, você poderá adicionar públicos-alvo por meio de conectores de origem em lote ou baseados em fluxo.

### Quais permissões são necessárias para fazer upload de públicos-alvo gerados externamente?

Para carregar públicos gerados externamente, você precisa ter as permissões &quot;Exibir segmentos&quot;, &quot;Gerenciar segmentos&quot; e &quot;Importar públicos&quot;. Não há controles de função específicos necessários para fazer upload de públicos-alvo gerados externamente.

### O que acontece quando carrego um público-alvo gerado externamente?

Ao fazer upload de um público gerado externamente, um conjunto de dados será criado e ficará visível no inventário do conjunto de dados. O nome do conjunto de dados será **o mesmo** do nome do público-alvo gerado externamente que você carregou.

### O que é composto por um público-alvo gerado externamente e o que acontece com esses dados quando são importados para o Experience Platform?

Durante o fluxo de trabalho de importação de público externo, você deve especificar qual coluna no arquivo CSV corresponde à **Identidade principal**. Um exemplo de identidade primária inclui endereço de email, ECID ou um namespace de identidade personalizado específico de uma organização.

Os dados associados a esta coluna de identidade primária são os dados **only** anexados ao perfil. Se não houver perfis que correspondam aos dados na coluna de identidade principal, um novo perfil será criado. No entanto, este perfil é essencialmente um perfil órfão, pois **não** atributos ou eventos de experiência estão associados a este perfil.

Todos os outros dados dentro do público gerado externamente são considerados **atributos de carga**. Estes atributos só podem **ser** usados para personalização e enriquecimento durante a ativação e estão **não** anexados a um perfil. No entanto, esses atributos são armazenados no data lake.

Embora seja possível fazer referência ao público-alvo gerado externamente ao criar públicos-alvo usando o Construtor de segmentos, os atributos de perfil individuais **não podem** ser usados.

### É possível reconciliar dados de público-alvo gerados externamente com um perfil existente no Experience Platform?

Sim, o público-alvo gerado externamente será mesclado com o perfil existente no Experience Platform se os identificadores primários corresponderem. Esses dados podem levar até 24 horas para serem reconciliados. Se os dados do perfil ainda não existirem, um novo perfil será criado à medida que os dados forem assimilados.

### Como as preferências de consentimento do cliente são respeitadas para públicos-alvo gerados externamente que são importados para o Audience Portal?{#consent}

Como os dados do cliente são captados em vários canais, as políticas de mesclagem e de compilação de identidades permitem que esses dados sejam consolidados em um mesmo perfil do cliente em tempo real. As informações sobre as preferências de consentimento dos clientes são armazenadas e avaliadas na camada do perfil.

Os destinos downstream verificam cada perfil em busca de informações de consentimento antes da ativação. As informações de consentimento de cada perfil são comparadas com os requisitos de consentimento de um determinado destino. Se o perfil não satisfizer os requisitos, ele não será enviado a um destino.

Quando um público externo é assimilado no Portal de público-alvo, ele é unido a perfis existentes usando uma ID primária, como email ou ECID. Como resultado, as políticas de consentimento existentes permanecerão em vigor durante a ativação.

Observe que você deve **não** incluir informações de consentimento com públicos gerados externamente, pois as variáveis de carga são **não** armazenadas no repositório de perfis, mas no data lake. Em vez disso, você **deve** usar um canal de assimilação da Adobe Experience Platform no qual os dados de perfil são importados.

### Posso usar um público gerado externamente para criar outros públicos?

Sim, qualquer público gerado externamente aparecerá no inventário de público e poderá ser usado ao construir públicos dentro do [Construtor de segmentos](./ui/segment-builder.md).

### Com que frequência os públicos-alvo gerados externamente são avaliados?

Públicos gerados externamente são **somente** avaliados durante o tempo de importação. Como os atributos associados a esses públicos de importação são não duráveis e **não** fazem parte do armazenamento Perfil, a única vez que um público gerado externamente será atualizado é se o público existente for atualizado manualmente.

### Posso usar atributos carregados externamente como parte da segmentação?

Não pode. Os atributos de perfil devem ser atributos de longa duração, enquanto os dados de público-alvo gerados externamente que são carregados contêm apenas dados contextuais associados a esse público-alvo gerado externamente.

Os dados contextuais do público-alvo gerados externamente, ou atributos de enriquecimento, têm **não** durabilidade longa, pois seu ciclo de vida está vinculado ao público-alvo carregado. Como resultado, devido à sua natureza transitória, esses atributos de enriquecimento **não** estão disponíveis para uso na segmentação.

No entanto, ao mapear os públicos-alvo para destinos em lote ou baseados em arquivo, é possível usar esses atributos de enriquecimento gerados externamente para aumentar os públicos-alvo e outras ativações downstream.

Para saber mais sobre esse recurso, leia o manual em [ativando dados de público-alvo para destinos de exportação de perfil em lote](../destinations/ui/activate-batch-profile-destinations.md#mapping).

### Há uma política de mesclagem específica para públicos-alvo gerados externamente?

A política de mesclagem padrão específica da organização é aplicada automaticamente ao carregar públicos gerados externamente. No entanto, é possível alterar a política de mesclagem aplicada ao público gerado externamente durante o fluxo de trabalho de importação de público.

### Onde posso ativar públicos gerados externamente para o?

Um público gerado externamente pode ser mapeado para qualquer destino e usado em campanhas e jornadas do Adobe Journey Optimizer.

### Posso excluir um público-alvo gerado externamente?

Sim! Públicos gerados externamente podem ser excluídos no Portal de público-alvo.

### O que devo fazer se fiz upload acidentalmente de um público-alvo gerado externamente?

Se você tiver carregado acidentalmente um público-alvo gerado externamente e quiser remover os dados, é possível limpar os perfis associados ao público-alvo carregando um arquivo CSV com uma linha e nenhum dado.

### Por quanto tempo os públicos-alvo gerados externamente duram?

A expiração de dados atuais para públicos gerados externamente é de **30 dias**. Essa expiração de dados foi escolhida para reduzir a quantidade de dados em excesso armazenados em sua organização.

Depois que o período de expiração dos dados passar, o conjunto de dados associado ainda estará visível no inventário do conjunto de dados, mas você **não** poderá ativar o público-alvo e a contagem de perfis será exibida como zero.

### Há um número máximo de públicos-alvo gerados externamente que eu possa importar?

Não há limite para o número de públicos-alvo gerados externamente que você pode importar. No entanto, observe que os públicos-alvo importados **do** contam com o limite geral de públicos-alvo.

### Como o Audience Portal e a Composição de público-alvo interagem com o lançamento dos dados de parceiros da Real-Time CDP?

O Portal de público-alvo e a Composição de público-alvo interagirão com os Dados do parceiro de duas maneiras:

1. Se você assimilar uma lista de clientes potenciais fornecida pelo parceiro usando a classe e o fluxo de trabalho Perfil de Cliente Potencial, os clientes potenciais serão mantidos **separadamente** da mesclagem de perfis de cliente no Serviço de Perfil. Como resultado, as listas de clientes potenciais **não** serão exibidas no Portal de público-alvo ou na Composição de público para uso.
2. Se você estiver usando atributos fornecidos pelo parceiro para enriquecer perfis primários **existentes**, esses públicos enriquecidos com dados do parceiro **serão** exibidos no Portal de público-alvo e na Composição de público para uso.

### Como posso usar atributos adicionais com meus públicos-alvo?

Com os públicos-alvo, há **dois** tipos diferentes de atributos adicionais que você pode adicionar: atributos de carga (contextuais) e atributos de enriquecimento.

Os atributos de carga são atributos assimilados como parte do upload de CSV de um público gerado externamente. Estes atributos são **não** assimilados no Perfil de cliente em tempo real, mas podem ser usados como parte de um destino downstream.

Os atributos de enriquecimento são atributos que vêm de um conjunto de dados e são unidos a um público na Composição do público-alvo. Esses atributos só podem ser usados atualmente em campanhas do Adobe Journey Optimizer. O suporte para Adobe Journey Optimizer jornada será lançado em breve, com suporte para destinos downstream aguardando lançamento futuro.

| Canal de ativação | Públicos-alvo de upload personalizado para CSV | Públicos da composição de público-alvo |
| --- | --- | --- |
| Destinos do Real-Time CDP | Os atributos de carga e os públicos-alvo podem ser ativados. | Somente o público-alvo pode ser ativado. Os atributos de enriquecimento **não podem** ser ativados. |
| Campanhas do Adobe Journey Optimizer | Nem o público-alvo nem os atributos de carga podem ser ativados. | É possível ativar o público-alvo e os atributos de enriquecimento. |

## Estados do ciclo de vida {#lifecycle-states}

A seção a seguir lista perguntas relacionadas aos estados do ciclo de vida e ao gerenciamento do estado do ciclo de vida no Portal de público-alvo.

### O que representam os diferentes estados do ciclo de vida?

O gráfico a seguir explica os diferentes status do ciclo de vida, o que eles representam, onde os públicos-alvo com esse status podem ser usados, bem como o impacto nas medidas de proteção de segmentação.

| Estado | Definição | Visível no Audience Portal? | Visível nos destinos? | Afeta os limites de segmentação? | Impacto nos públicos-alvo baseados em arquivos | Impacto na avaliação do público-alvo | Pode ser usado em outros públicos-alvo? | Editável |
| --- | --- | --- | --- | --- | --- | --- | --- | -- |
| Rascunho | Um público no estado **Rascunho** é um público que ainda está em desenvolvimento e não está pronto para ser usado em outros serviços. | Sim, mas pode ser oculto. | Não | Sim | Podem ser importadas ou atualizadas durante o processo de refinamento. | Avaliado para obter contagens de publicação precisas. | Sim, mas não é recomendável usar. | Sim |
| Publicado | Um público no estado **Publicado** é um público pronto para uso em todos os serviços downstream. | Sim | Sim | Sim | Pode ser importado ou atualizado. | Avaliado usando segmentação em lote, de fluxo ou de borda. | Sim | Sim |
| Inativo | Um público no estado **Inativo** é um público que não está sendo usado no momento. Ela ainda existe no Experience Platform, mas **não** poderá ser usada até que seja marcada como rascunho ou publicada. | Não, mas pode ser exibido. | Não | Não | Não é mais atualizado. | Não é mais avaliado ou atualizado pelo Experience Platform. | Não | Sim |
| Excluído | Um público no estado **Excluído** é um público que foi excluído. A exclusão real dos dados pode levar alguns minutos para ser executada. | Não | Não | Não | Os dados subjacentes são excluídos. | Não ocorre avaliação ou execução de dados após a conclusão da exclusão. | Não | Não |

### Em quais estados posso editar meus públicos-alvo?

Os públicos-alvo podem ser editados nos seguintes estados do ciclo de vida:

- **Rascunho**: se um público-alvo for editado no estado de rascunho, ele permanecerá no estado de rascunho, a menos que seja publicado explicitamente.
- **Publicado**: se um público-alvo for editado no estado publicado, ele permanecerá publicado, e o público será atualizado automaticamente.
- **Inativo**: se um público-alvo for editado no estado inativo, ele permanecerá inativo. Isso significa que ele não será avaliado ou atualizado. Se precisar atualizar o público-alvo, você precisará publicá-lo.

Depois que um público é excluído, ele **não pode** ser editado.

### Para quais estados do ciclo de vida posso mover um público-alvo?

Os possíveis estados do ciclo de vida para os quais um público-alvo pode ser movido dependem do estado atual do público-alvo.

![Um diagrama descrevendo as possíveis transições de estado do ciclo de vida disponíveis para os públicos-alvo.](./images/faq/lifecycle-state-transition.png)

Se o público-alvo estiver no estado de rascunho, você poderá publicá-lo ou excluí-lo se o público-alvo não tiver dependentes.

Se o público-alvo estiver no estado publicado, você poderá desativá-lo ou excluí-lo se o público-alvo não tiver dependentes.

Se o público-alvo estiver no estado inativo, você poderá republicá-lo ou excluí-lo se o público-alvo não tiver dependentes.

### Existem limitações para públicos-alvo em determinados estados do ciclo de vida?

Públicos-alvo no estado publicado só poderão ser movidos para outro estado se o público-alvo **não** tiver dependentes. Isso significa que, se o público-alvo for usado em um serviço downstream, ele não poderá ser desativado ou excluído.

Se um público avaliado usando a segmentação em lotes for republicado, isto é, quando um público passa de inativo para publicado, o público será atualizado **após** o trabalho diário em lotes. Ao ser republicado pela primeira vez, os perfis e os dados serão os **mesmos** de quando o público-alvo se tornou inativo.

### Como colocar um público-alvo no estado de rascunho?

O método para colocar um público no estado de rascunho depende da origem do público.

Para públicos-alvo criados com o Construtor de segmentos, é possível definir o público-alvo para o estado de rascunho ao selecionar &quot;[!UICONTROL Salvar como rascunho]&quot; no Construtor de segmentos.

Para públicos-alvo criados na Composição de público-alvo, os públicos-alvo são salvos automaticamente como rascunho até serem publicados.

Para públicos criados externamente, os públicos são publicados automaticamente.

Quando um público-alvo está no estado publicado, você **não pode** alterar o público-alvo original novamente para o estado de rascunho. No entanto, se você copiar o público-alvo, ele estará no estado de rascunho.

### Como colocar um público-alvo no estado publicado?

Para públicos-alvo criados com o Construtor de segmentos ou a Composição de público-alvo, é possível definir o público-alvo para o estado publicado ao selecionar &quot;[!UICONTROL Publicar]&quot; nas respectivas interfaces do usuário.

Os públicos-alvo criados externamente são definidos como publicados automaticamente.

### Como colocar um público-alvo no estado inativo?

Para colocar um público publicado no estado inativo, abra o menu de ações rápidas no Portal de público-alvo e selecione &quot;[!UICONTROL Desativar]&quot;.

### Como faço para republicar um público-alvo?

>[!NOTE]
>
>O estado &quot;republicado&quot; é igual ao estado publicado para o comportamento do público-alvo.

Você pode republicar um público selecionando um público que esteja no estado inativo, abrindo o menu de ações rápidas no Portal de público e selecionando [!UICONTROL Publicar].

### Como colocar um público-alvo no estado excluído?

>[!IMPORTANT]
>
>Você só pode excluir públicos-alvo que **não** sejam usados em ativações downstream. Além disso, não é possível excluir um público referenciado em outro público. Se você não pode excluir seu público-alvo, certifique-se de que você **não** está usando-o em qualquer serviço downstream ou como um bloco de construção de outro público-alvo.

Para colocar um público-alvo no estado de exclusão, abra o menu de ações rápidas no Portal de público-alvo e selecione [!UICONTROL Excluir].

### Existem limitações para as transições de estado do ciclo de vida?

Sim, há alguns avisos a serem observados quando você estiver usando públicos-alvo em serviços downstream, como o Adobe Journey Optimizer, ou públicos-alvo não baseados em clientes, como públicos-alvo baseados em conta.

No momento, você **deve** verificar manualmente se o público-alvo é usado downstream no Adobe Journey Optimizer, pois esse status não é verificado automaticamente no momento.

Além disso, você **deve** verificar manualmente se o público-alvo é usado como um componente de um público-alvo baseado em conta, pois esse status também não é verificado automaticamente no momento.

### O que acontece quando copio um público-alvo? {#copy}

Ao copiar um público-alvo, ele estará no estado de rascunho e manterá as mesmas pastas, tags e rótulos que foram aplicados ao público-alvo original.

### O uso de um público-alvo como público-alvo secundário afeta as transições de estado do ciclo de vida?

>[!NOTE]
>
>Um público-alvo pai é um público que **usa** outro público-alvo como uma dependência para o público-alvo.
>
>Um público-alvo filho é um público-alvo que é **usado como** uma dependência para o público-alvo.

Sim, usar um público-alvo como público-alvo filho afeta os estados de ciclo de vida que o público-alvo filho e pai pode realizar.

Para que um público-alvo filho seja movido para o estado publicado, todo o público-alvo pai **deve** estar no estado publicado. Os públicos-alvo principais podem ser publicados antes da publicação do público-alvo secundário ou, se o usuário confirmar, podem ser publicados automaticamente quando o público-alvo secundário é publicado.

Para que o público-alvo pai seja movido para o estado inativo ou excluído, todos os públicos-alvo filho **devem** ser desativados ou excluídos.

### Posso me referir a um público que esteja em um estado de ciclo de vida diferente?

Sim! Se o público-alvo estiver no estado de rascunho, você poderá fazer referência a públicos-alvo no estado de rascunho ou publicado. No entanto, para publicar este público-alvo, você **deve** publicar os outros públicos-alvo pai.

## Inventário de público

A seção a seguir lista perguntas relacionadas ao inventário de público-alvo no Portal de público-alvo.

### Preciso de permissões adicionais para usar os recursos de inventário de público-alvo?

Não, você não. Desde que você tenha permissões de edição para públicos-alvo, será possível criar, atualizar e gerenciar suas pastas e tags no Portal de público-alvo. Para obter mais informações sobre o gerenciamento de permissões, leia o [guia de gerenciamento de permissões](../access-control/ui/permissions.md).

### Há um limite para o número de pastas que posso criar?

Não, não há limite para o número de pastas que você pode criar. Para obter mais informações sobre pastas, leia a [seção de inventário de público-alvo](./ui/audience-portal.md#folders) da visão geral da interface do usuário do Serviço de segmentação.

### Há um limite para o número de tags que podem ser adicionadas a um público-alvo?

Não, não há limite para o número de tags que podem ser adicionadas a um público-alvo. Para obter mais informações sobre tags, leia a [seção de inventário de público-alvo](./ui/audience-portal.md#tags) da visão geral da interface do usuário do Serviço de segmentação.

### Há um limite para o número de tags que posso criar?

Não, não há limite para o número de tags que podem ser criadas. No entanto, você pode criar um máximo de **100** categorias para aplicar às tags. Para obter mais informações sobre o gerenciamento de tags, leia o [Guia de Gerenciamento de Tags](../administrative-tags/ui/managing-tags.md).

### Quando procuro um público-alvo por nome ou tag em uma pasta principal, também posso pesquisar pelas pastas secundárias relacionadas?

Não, esse comportamento não é compatível. No entanto, você pode alterar a exibição do inventário de público-alvo para analisar **Todos os públicos-alvo** e pesquisar em todas as pastas. Para obter mais informações sobre como usar a pesquisa no inventário de público-alvo, leia a [seção de pesquisa](./ui/audience-portal.md#search) da visão geral da interface do usuário do Serviço de segmentação.

### Posso atribuir automaticamente um público-alvo a uma pasta no momento da criação?

Nesse momento, não. No entanto, esse recurso pode estar disponível no futuro.

### Posso mover vários públicos-alvo para uma pasta ao mesmo tempo?

Nesse momento, não. No entanto, esse recurso pode estar disponível no futuro.

## Composição de público-alvo

A seção a seguir lista perguntas relacionadas à Composição do público-alvo.

### Quando devo usar a Composição de público-alvo em vez de usar o Construtor de segmentos?

A composição do público-alvo e o Construtor de segmentos têm funções importantes na criação de públicos-alvo no Experience Platform.

O Construtor de segmentos é mais adequado para o público-alvo **criação** (para construir um público do zero), enquanto a Composição de público-alvo é mais adequada para o público-alvo **curadoria e personalização** (para criar novos públicos com base em um público-alvo existente).

A tabela a seguir ilustra a diferença entre os dois serviços:

| Construtor de segmentos | Composição de público-alvo |
| --------------- | -------------------- |
| <ul><li>Geração de público-alvo de estágio único</li><li>Cria os blocos básicos de públicos-alvo a partir de dados de perfil, série temporal e várias entidades</li><li>Usado para criar **um** público-alvo</li></ul> | <ul><li>Geração de público-alvo em vários estágios, usando operações baseadas em conjuntos</li><li>Usa os públicos-alvo criados pelo Construtor de segmentos e aplica opções de enriquecimento de dados, como classificação de atributos de perfil e divisão em subpúblicos-alvo</li><li>Usado para criar **vários** públicos-alvo de uma só vez</li></ul> |

Para saber mais sobre o Construtor de segmentos, leia o [Guia do Construtor de segmentos](./ui/segment-builder.md). Para saber mais sobre a Composição de público-alvo, leia o [Guia de Composição de público-alvo](./ui/audience-composition.md).

### Posso usar públicos gerados externamente na Composição de público-alvo?

Nesse momento, não. No entanto, esse recurso deve estar disponível em breve.

### Posso enviar públicos-alvo da Composição de público-alvo para todos os destinos e canais de downstream?

Sim! Você pode usar públicos-alvo da Composição de público-alvo em Campanhas do Adobe Journey Optimizer, destinos do Real-Time CDP e Jornadas da Adobe Journey Optimizer.

### Existem medidas de proteção para o número de composições?

>[!IMPORTANT]
>
>Esta garantia se aplica somente a composições criadas com a Composição de público-alvo e **não** se aplica a composições criadas com a Composição de público federado.

Neste momento, você só pode ter **10** composições publicadas por sandbox. Esta garantia será aumentada em uma versão futura.

### Quais são as medidas de proteção do fluxo de trabalho para a Composição de público-alvo?

O componente de composição &quot;colocação&quot; segue uma estrutura rígida, como se segue:

1. Você **sempre** começa com o bloco [!UICONTROL Público-alvo] para selecionar sua atividade inicial. Você pode ter no máximo **um** [!UICONTROL público-alvo] bloco.
2. Opcionalmente, é possível adicionar um bloco [!UICONTROL Excluir] que segue o bloco [!UICONTROL Público-alvo].
3. Opcionalmente, é possível adicionar um bloco [!UICONTROL Enriquecer] após o bloco [!UICONTROL Excluir]. Você só pode usar **um** [!UICONTROL Enriquecer] bloco por composição.
4. Opcionalmente, é possível adicionar um bloco [!UICONTROL Classificação] ou [!UICONTROL Divisão]. Você pode **ter somente** um desses blocos por composição.
5. Você **sempre** termina com um bloco [!UICONTROL Salvar] para salvar seu público-alvo.

Além disso, as seguintes restrições se aplicam ao usar esses blocos:

- Dividir bloco
   - Este bloco só dá suporte a tipos de dados **Cadeia**. O bloco Split **não** oferece suporte ao tipo de dados date ou boolean.
   - Além disso, este bloco **não** oferece suporte a atributos de enriquecimento.
- Excluir bloco
   - Este bloco **não** oferece suporte ao tipo de dados data ou booleano.
- Classificar bloco
   - Este bloco **não** dá suporte a atributos de enriquecimento.

Para obter mais detalhes sobre como usar a Composição de público-alvo, leia o [Guia da interface do usuário de Composição de público-alvo](./ui/audience-composition.md).

### Quando os públicos-alvo criados usando a Composição de público-alvo são salvos e avaliados?

Os públicos-alvo são salvos automaticamente ao criá-los na Composição de público-alvo. O horário de criação do público será a primeira vez que esse salvamento automático ocorrerá.

Após a criação da composição de público-alvo, pode levar até 48 horas para que ela seja avaliada e ativada para uso em serviços downstream, como um destino do Real-Time CDP ou canal do Adobe Journey Optimizer.

### Quando posso usar o público-alvo que criei?

O público-alvo criado na Composição do público-alvo **imediatamente** será exibido no Portal de público-alvo. No entanto, para usá-lo em serviços downstream, como o Adobe Journey Optimizer, você deve aguardar pelo menos 24 horas após a avaliação.

### Os trabalhos de avaliação estão visíveis na seção de monitoramento?

No momento, os trabalhos de avaliação **não** são exibidos na interface de monitoramento.

### Posso usar uma composição de público-alvo em outra composição?

Não, os públicos-alvo criados com a Composição de Público-alvo **não podem** ser usados como entrada em outra composição de público-alvo.

### Como a divisão funciona na Composição do público-alvo?

A divisão de público-alvo permite ainda subdefinir o público-alvo em grupos menores.

Ao dividir por atributo, há exclusividade mútua entre os grupos. Isso significa que se um registro atender aos critérios de vários caminhos de divisão, ele será atribuído ao caminho **primeiro** à esquerda e **não** será atribuído a qualquer um dos outros caminhos.

Ao dividir por porcentagem, as divisões são **aleatoriamente** concluídas. Isso significa que os perfis serão atribuídos aleatoriamente a cada caminho.

Para obter mais informações sobre o bloco Split, leia o [guia da interface do usuário da composição de público-alvo](./ui/audience-composition.md#split).

### Posso usar todos os tipos de segmentação no fluxo de trabalho de Composição de público-alvo?

Sim, todos os tipos de segmentação ([segmentação em lote, segmentação de transmissão e segmentação de borda](./home.md#evaluate-segments)) são compatíveis com o fluxo de trabalho Composição de público-alvo. No entanto, como as composições atualmente são executadas apenas uma vez por dia, mesmo se os públicos avaliados por transmissão ou borda forem incluídos, o resultado será baseado na associação do público no momento em que a composição foi executada.

## Associação de público-alvo

A seção a seguir lista perguntas relacionadas à associação de público-alvo.

### Como posso confirmar a associação de um perfil em um público-alvo?

Para confirmar a associação de público-alvo de um perfil, visite a página de detalhes do perfil do perfil que deseja confirmar. Selecione **[!UICONTROL Atributos]**, seguido por **[!UICONTROL Exibir JSON]**, e você poderá confirmar se o objeto `segmentMembership` contém a ID do público-alvo.

### A associação de público pode variar entre a associação ideal e real?

Sim, a associação de público-alvo pode variar entre associação ideal e real se um público-alvo for avaliado usando a segmentação por transmissão **e**, esse público-alvo será baseado em um público-alvo avaliado usando a segmentação em lote.

Por exemplo, se o Público-alvo A se basear no Público-alvo B e o Público-alvo B for avaliado usando a segmentação em lote, já que o Público-alvo B é atualizado somente a cada 24 horas, o Público-alvo A se afastará dos dados reais até ressincronizar com as atualizações do Público-alvo B.

## Segmentação em lote {#batch-segmentation}

A seção a seguir lista perguntas relacionadas à segmentação em lote.

### Como a segmentação em lote resolve a associação de perfis?

Os públicos avaliados usando a segmentação em lote são resolvidos diariamente, com os resultados da associação de público sendo registrados no atributo `segmentMembership` do perfil. As pesquisas de perfil geram uma nova versão do perfil no momento da pesquisa, mas **não** atualiza os resultados da segmentação em lote.

Como resultado, quando são feitas alterações no perfil, como a mesclagem de dois perfis, essas alterações **irão** aparecer no perfil quando pesquisadas, mas **não** serão refletidas no atributo `segmentMembership` até que o trabalho de avaliação de segmento seja executado novamente.

Por exemplo, digamos que você tenha criado dois públicos mutuamente exclusivos: o Público-alvo A é para pessoas que vivem em Washington e o Público-alvo B é para pessoas que vivem **não** em Washington. Há dois perfis - perfil 1 para uma pessoa que mora em Washington e perfil 2 para uma pessoa que mora em Oregon.

Quando o trabalho de avaliação de segmentação em lote é executado, o perfil 1 vai para o Público-alvo A, enquanto o perfil 2 vai para o Público-alvo B. Posteriormente, mas antes da execução do trabalho de avaliação de segmentação em lote do próximo dia, um evento que reconcilia os dois perfis entra no Experience Platform. Como resultado, um único perfil mesclado que contém os perfis 1 e 2 é criado.

Até que o próximo trabalho de avaliação de segmento em lote seja executado, o novo perfil mesclado terá uma associação de público-alvo em **ambos** perfil 1 e perfil 2. Como resultado, ele se tornará um membro de **ambos** o Público-alvo A e o Público-alvo B, apesar do fato de que esses públicos-alvo têm definições contraditórias. Para o usuário final, esta é a **mesma situação** de antes da conexão dos perfis, pois sempre havia apenas uma pessoa envolvida, e o Experience Platform **não** tinha informações suficientes para conectar os dois perfis.

Se você usar a pesquisa de perfil para recuperar o perfil recém-criado e examinar sua associação de público-alvo, ela mostrará que é um membro de **ambos** o Público-alvo A e o Público B, apesar do fato de que esses dois públicos-alvo têm definições contraditórias. Quando o trabalho diário de avaliação da segmentação em lote for executado, a associação de público-alvo será atualizada para refletir esse estado atualizado dos dados do perfil.

Se você precisar de mais resolução de público em tempo real, use a transmissão ou a segmentação de borda.

### Quanto tempo leva para que os dados de transmissão estejam disponíveis em workflows de segmentação em lote?

Pode levar até três horas para que os dados de transmissão estejam disponíveis em workflows de segmentação em lote.

Por exemplo, se um trabalho de segmentação em lote for executado às 21 horas, será garantido que ele conterá transmissão de dados assimilados **até** 18 horas. Os dados assimilados por transmissão que foram assimilados após as 18h, mas antes das 21h de **maio** serão incluídos.

## Segmentação de borda {#edge-segmentation}

A seção a seguir lista perguntas relacionadas à segmentação de borda.

### Quanto tempo leva para uma definição de segmento ficar disponível no Edge Network?

Demora até uma hora para uma definição de segmento estar disponível no Edge Network.

## Segmentação de transmissão {#streaming-segmentation}

A seção a seguir lista perguntas relacionadas à segmentação de transmissão.

### A &quot;desqualificação&quot; da segmentação por transmissão também ocorre em tempo real?

Para a maioria das instâncias, a desqualificação da segmentação por transmissão ocorre em tempo real. No entanto, os segmentos de transmissão que usam segmentos de segmentos **não** não se qualificam em tempo real, em vez disso, se desqualificam após 24 horas.

### Em quais dados a segmentação por transmissão funciona?

A segmentação de streaming funciona em todos os dados que foram assimilados usando uma fonte de streaming. Os dados assimilados usando uma fonte baseada em lote serão avaliados à noite, mesmo que se qualifiquem para segmentação por transmissão. Os eventos transmitidos para o sistema com um carimbo de data e hora com mais de 24 horas serão processados na tarefa em lote subsequente.

### Como os segmentos são definidos como segmentação em lote ou por transmissão?

Uma definição de segmento é definida como segmentação de lote, fluxo ou borda com base em uma combinação de tipo de consulta e duração do histórico de eventos. Uma lista de quais segmentos serão avaliados como uma definição de segmento de streaming pode ser encontrada na [seção de tipos de consulta de segmentação de streaming](#query-types).

Observe que se uma definição de segmento contiver **ambos** uma expressão `inSegment` e uma cadeia direta de evento único, ela não poderá se qualificar para segmentação de transmissão. Se você quiser que essa definição de segmento se qualifique para a segmentação por transmissão, transforme a cadeia direta de evento único em seu próprio segmento.

### Por que o número de segmentos &quot;total qualificado&quot; continua aumentando, enquanto o número em &quot;Últimos X dias&quot; permanece em zero na seção de detalhes de definição do segmento?

O número total de segmentos qualificados é retirado do trabalho diário de segmentação, que inclui públicos qualificados para segmentos em lote e de fluxo. Esse valor é mostrado para segmentos em lote e de transmissão.

O número nos &quot;Últimos X dias&quot; **somente** inclui públicos qualificados na segmentação por transmissão e **somente** aumenta se você tiver transmitido dados para o sistema e se contar para essa definição de transmissão. Este valor é **somente** exibido para segmentos de streaming. Como resultado, o valor **maio** é exibido como 0 para segmentos em lote.

Como resultado, se você vir que o número em &quot;Últimos X dias&quot; é zero e o gráfico de linha também está relatando zero, você **não** transmitiu qualquer perfil no sistema que se qualificaria para esse segmento.

### Quanto tempo leva para uma definição de segmento ficar disponível?

Leva até uma hora para uma definição de segmento estar disponível.

### Existem limitações para os dados que estão sendo transmitidos?

Ao usar a segmentação de borda ou transmissão, verifique se os eventos de cada perfil estão espaçados. Se muitos eventos forem transmitidos no mesmo segundo, o Experience Platform tratará esses eventos como dados gerados por bot e eles serão descartados. Como prática recomendada, você deve ter **pelo menos** cinco segundos entre os dados do evento para garantir que os dados sejam usados corretamente.
