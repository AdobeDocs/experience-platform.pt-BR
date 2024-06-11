---
title: Simulação de gráfico
description: Saiba como usar a Simulação de gráfico na interface do usuário do serviço de identidade.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 2afdfd54b420bcf59423ea64048d928422ea61c9
workflow-type: tm+mt
source-wordcount: '1590'
ht-degree: 5%

---

# Simulação de gráfico

A Simulação de gráfico é uma ferramenta na interface do serviço de identidade que pode ser usada para simular como um gráfico de identidade se comporta, considerando uma combinação específica de identidades e como você configura a [algoritmo de otimização de identidade](./identity-optimization-algorithm.md).

Leia este documento para saber como você pode usar a Simulação de gráfico para entender melhor o comportamento do gráfico de identidade e como o algoritmo de gráfico funciona.

## Conheça a interface de Simulação de gráfico

É possível acessar a Simulação de gráfico na interface do usuário do Adobe Experience Platform. Selecionar **[!UICONTROL Identidades]** na navegação à esquerda e selecione **[!UICONTROL Simulação de gráfico]** no cabeçalho superior.

![A interface de Simulação de gráfico na interface do Adobe Experience Platform.](../images/graph-simulation/graph-simulation.png)

A interface de Simulação de gráfico pode ser dividida em três seções:

* Eventos: use o **[!UICONTROL Eventos]** painel para adicionar identidades e simular um gráfico. Uma identidade totalmente qualificada deve ter um namespace de identidade e seu valor de identidade correspondente. Você deve adicionar pelo menos duas identidades para simular um gráfico. Também é possível selecionar **[!UICONTROL Carregar exemplo]** para inserir uma configuração pré-configurada de evento e algoritmo.

![O painel Eventos da ferramenta Simulação de gráfico.](../images/graph-simulation/events.png)

* Configuração do algoritmo: use o **[!UICONTROL Configuração do algoritmo]** para adicionar e configurar o algoritmo de otimização para seus namespaces. Você pode arrastar e soltar um namespace para modificar sua respectiva classificação de prioridade. Também é possível selecionar **[!UICONTROL Exclusivo por gráfico]** para determinar se um namespace é exclusivo.

![A configuração de algoritmo da ferramenta de Simulação de gráfico.](../images/graph-simulation/algorithm-configuration.png)

* Visualizador de gráficos simulado: o visualizador de gráficos simulado exibe o gráfico resultante com base nos eventos adicionados e no algoritmo configurado. Uma linha reta entre dois nós significa que um link é estabelecido. Uma linha pontilhada indica que um link foi removido.


![O painel visualizador de gráficos simulado, com um exemplo de gráfico simulado.](../images/graph-simulation/simulated-graph.png)

## Adicionar eventos

Para começar, selecione **[!UICONTROL Adicionar eventos]**.

![O botão Adicionar eventos selecionado.](../images/graph-simulation/add-events.png)

Uma janela pop-up é exibida para [!UICONTROL Evento #1]. Aqui, insira sua combinação de namespace de identidade e valor de identidade. Você pode usar o menu suspenso para selecionar um namespace de identidade. Como alternativa, você pode digitar as primeiras letras de um namespace e selecionar as opções fornecidas no menu suspenso. Depois de selecionar o namespace, forneça um valor de identidade que corresponda a ele.

![](../images/graph-simulation/event-one.png)

>[!TIP]
>
>O valor de identidade inserido durante os exercícios de Simulação de gráfico não precisa ser valores de identidade reais e pode ser espaços reservados simples.

Quando a primeira identidade for concluída, selecione o ícone adicionar (**`+`**) para adicionar uma segunda identidade.

![A primeira identidade totalmente qualificada de {Email: tom@acme.com} é inserida no painel Eventos da Simulação de gráfico.](../images/graph-simulation/event-one-added.png)

Em seguida, repita as mesmas etapas e adicione uma segunda identidade. Duas identidades totalmente qualificadas são necessárias para gerar um gráfico de identidade. No exemplo abaixo, uma ECID é adicionada como namespace e recebe um valor de `111`. Quando terminar, selecione **[!UICONTROL Salvar]**.

![Uma segunda identidade de {ECID: 111} é adicionado ao Evento #1.](../images/graph-simulation/first-event.png)

A variável [!UICONTROL Eventos] As atualizações de interface do para exibir seu primeiro evento, que neste caso é: `{Email: tom@acme.com, ECID: 111}`.

![A interface de eventos atualizada com {Email: tom@acme.com, ECID: 111}.](../images/graph-simulation/add-second-event.png)

Em seguida, repita as mesmas etapas para adicionar um segundo evento. Para Evento #2, adicione `{Email: summer@acme.com}` como sua primeira identidade e, em seguida, adicionar a mesma `{ECID: 111}` como a segunda identidade, criando assim um segundo evento de: `{Email: summer@acme.com}, {ECID: 111}`. Quando terminar, você deverá ter dois eventos, um para `{Email: tom@acme.com, ECID: 111}` e um para `{Email: summer@acme.com}, {ECID: 111}`.

![A interface de eventos atualizada com dois eventos.](../images/graph-simulation/two-events.png)

### Carregar exemplo

+++Selecione para exibir etapas sobre como usar exemplos de gráfico pré-carregado

Para configurar um gráfico de exemplo com um algoritmo pré-configurado, selecione **[!UICONTROL Carregar exemplo]**. Uma janela pop-up é exibida, fornecendo os cenários de gráfico disponíveis entre os quais você pode escolher:

| Exemplo de gráfico | Descrição | Exemplo |
| --- | --- | --- |
| Dispositivo compartilhado | Dispositivo compartilhado refere-se a cenários em que dois usuários diferentes fazem logon no mesmo dispositivo único. | Marido e esposa compartilham uma iPad para navegação na Internet e comércio eletrônico. |
| Telefone inválido (não é único) | Telefone inválido ou não exclusivo refere-se a cenários em que dois usuários diferentes usam o mesmo número de telefone para criar uma conta. | Uma mãe e sua filha usam o número de telefone residencial compartilhado para se inscreverem em qualquer conta de comércio eletrônico. |
| Valores de identidade “incorretos” | Os valores de identidade &quot;inválidos&quot; referem-se a cenários em que o Serviço de identidade gera IDFAs não exclusivos devido à implementação incorreta. | O WebSDK envia incorretamente um `user_null` para cada evento devido a problemas de implementação de código. |

Selecione qualquer uma das opções para carregar a Simulação de gráfico com eventos e algoritmo pré-configurados. Você ainda pode fazer mais configurações em qualquer exemplo de cenário de gráfico pré-carregado.

Quando terminar, selecione **[!UICONTROL Simular]**.

+++

### Usar versão de texto

+++Selecione para exibir etapas sobre como usar a versão de texto

Você também pode usar o modo texto para configurar eventos. Para usar o modo de texto, selecione a engrenagem (?) e selecione **[!UICONTROL Texto (usuários avançados)]**.

Você pode inserir suas identidades manualmente com o modo de texto. Use dois pontos (`:`) para distinguir o valor de identidade que corresponde ao namespace inserido e usar uma vírgula (`,`) para separar suas identidades. Para distinguir eventos diferentes uns dos outros, use uma nova linha para cada evento.

+++

### Editar evento

Para editar um evento, selecione as reticências (`...`) ao lado de um determinado evento e selecione **[!UICONTROL Editar]**.

### Excluir evento

Para excluir um evento, selecione as reticências (`...`) ao lado de um determinado evento e selecione **[!UICONTROL Excluir]**.

## Configurar algoritmo

O algoritmo que você configurar ditará como o Serviço de identidade trata os namespaces inseridos em seus eventos. Todas as configurações agrupadas na interface de simulação de gráfico não são salvas nas configurações de identidade.

Para começar, selecione adicionar (`+`) no canto inferior do painel de configuração de algoritmo.



Uma linha de configuração vazia é exibida. Primeiro, insira o mesmo namespace que você usou para os eventos. Nesse caso, comece inserindo a ID do CRM. Depois de inserir o namespace, as colunas para [!UICONTROL Símbolo de identidade] e [!UICONTROL Tipo de identidade] é preenchido automaticamente.



Em seguida, repita as mesmas etapas e adicione seu segundo namespace, que neste caso é a ECID. Depois que todos os namespaces forem inseridos, você poderá começar a configurar suas prioridades e exclusividade.

* **Prioridade de namespace**: a prioridade de um namespace determina sua importância relativa em comparação com os outros namespaces em um determinado gráfico de identidade. Por exemplo, se o seu gráfico de identidade tiver quatro namespaces diferentes: CRM ID, ECID, Email e Apple IDFA, você poderá configurar prioridades para determinar uma ordem de importância para os quatro namespaces. (ADICIONE O MOTIVO)
* **Namespace exclusivo**: se um namespace for designado como exclusivo, o Serviço de identidade gerará gráficos com a ressalva de que apenas uma identidade com determinado namespace exclusivo pode existir. Por exemplo, se a ID do CRM for designada como um namespace exclusivo, um gráfico só poderá ter uma identidade com a ID do CRM. Se houver mais de uma identidade com o namespace da ID do CRM, o link mais antigo será removido.

Para configurar a prioridade do namespace, selecione e arraste as linhas do namespace até a ordem de prioridade desejada, com a linha superior representando a prioridade mais alta e a linha inferior representando a prioridade mais baixa. Para designar um namespace como exclusivo, selecione o **[!UICONTROL Exclusivo por gráfico]** caixa de seleção



Quando terminar, selecione **[!UICONTROL Simular]**.

## Exibir gráfico simulado

A variável [!UICONTROL Gráfico simulado] exibe os gráficos de identidade gerados com base nos eventos adicionados e no algoritmo configurado.

| Ícones de gráfico | Descrição |
| --- | --- |
| Linha sólida | Uma linha sólida representa um vínculo estabelecido entre duas identidades. |
| Linha pontilhada | Uma linha pontilhada representa um link removido entre duas identidades. |
| Número na linha | Um número em uma linha representa o carimbo de data e hora de quando determinado link foi gerado. O número mais baixo (1) representa o link estabelecido mais antigo. |

No gráfico de exemplo abaixo, existe uma linha pontilhada entre `{CRM ID: Tom}` e `{ECID: 111}` pelos seguintes motivos:

* A ID do CRM foi designada como exclusiva durante a etapa de configuração do algoritmo. Portanto, somente uma identidade com um namespace de ID do CRM pode existir em um gráfico.
* O vínculo entre `{CRM ID: Tom}` e `{ECID: 111}` foi a primeira identidade estabelecida (Evento #1). É o link mais antigo e, portanto, é removido.

## Exemplo de cenários de gráfico

>[!NOTE]
>
>&quot;ID do CRM&quot; é um namespace personalizado. Portanto, os exemplos abaixo exigem que você crie um namespace personalizado com um nome para exibição e um símbolo de identidade de &quot;ID do CRM&quot;.

Os seguintes exemplos de seção de cenários de gráficos que você pode encontrar com a Simulação de gráfico.

### Somente ID do CRM

Eventos:

* ID do CRM: Tom, ECID: 111

Configuração do algoritmo:

| Prioridade | Nome de exibição | Símbolo de identidade | Tipo de identidade | Único por gráfico |
| ---| --- | --- | --- | --- |
| 1 | ID do CRM | ID do CRM | CROSS_DEVICE | Sim |
| 2 | ECID | ECID | COOKIE | NÃO |

+++Selecione para exibir o gráfico simulado

+++

### ID do CRM com email com hash

Nesse cenário, uma ID do CRM é assimilada e representa os dados online (evento de experiência) e offline (registro de perfil). Esse cenário também envolve a assimilação de um email com hash, que representa outro namespace enviado no conjunto de dados do registro do CRM junto com a ID do CRM.

Eventos:

* ID do CRM: Tom, Email_LC_SHA256: tom<span>@acme.com
* ID do CRM: Tom, ECID: 111
* ID do CRM: Summer, Email_LC_SHA256: summer<span>@acme.com
* ID do CRM: Verão, ECID: 222

Configuração do algoritmo:

| Prioridade | Nome de exibição | Símbolo de identidade | Tipo de identidade | Único por gráfico |
| ---| --- | --- | --- | --- |
| 1 | ID do CRM | ID do CRM | CROSS_DEVICE | Sim |
| 2 | Emails (SHA256, em letras minúsculas) | Email_LC_SHA256 | Email | NÃO |
| 3 | ECID | ECID | COOKIE | NÃO |

+++Selecione para exibir o gráfico simulado

+++

### ID do CRM com email com hash, telefone com hash, GAID e IDFA

Eventos:

* ID do CRM: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* ID do CRM: Tom, ECID: 111
* ID do CRM: Tom, ECID: 222, IDFA: A-A-A
* ID do CRM: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* ID do CRM: Summer, ECID: 333
* ID do CRM: Verão, ECID: 444, GAID:B-B-B

Configuração do algoritmo:

| Prioridade | Nome de exibição | Símbolo de identidade | Tipo de identidade | Único por gráfico |
| ---| --- | --- | --- | --- |
| 1 | ID do CRM | ID do CRM | CROSS_DEVICE | Sim |
| 2 | Emails (SHA256, em letras minúsculas) | Email_LC_SHA256 | Email | NÃO |
| 3 | Telefone (SHA256) | Phone_SHA256 | Telefone  | NÃO |
| 4 | ID de anúncio do Google (GAID) | GAID | DISPOSITIVO | NÃO |
| 5 | Apple IDFA (ID para Apple) | IDFA | DISPOSITIVO | NÃO |
| 6 | ECID | ECID | COOKIE | NÃO |

+++Selecione para exibir o gráfico simulado

+++