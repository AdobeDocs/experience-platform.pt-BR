---
solution: Experience Platform
title: Guia da interface do usuário dos manuais
description: Saiba como usar a interface do usuário do Experience Platform para exibir e ativar manuais de reprodução.
badgeBeta: label="Beta" type="Informative"
source-git-commit: 63ea852ca9f9a45d1c071fd1033cbd44cbb427c6
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 2%

---


# (Beta) Como ativar e reutilizar um manual

>[!AVAILABILITY]
>
>No momento, essa funcionalidade está na versão beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Para usar um manual, navegue até **[!UICONTROL Playbooks de caso de uso] > [!UICONTROL Playbooks]**. Navegue e use as várias opções de pesquisa e filtragem na página para selecionar e começar a usar um manual específico.

## Pesquisar e filtrar {#search-and-filter}

Use a janela de pesquisa e os filtros disponíveis na página para encontrar o manual correto para seu caso de uso.

Por exemplo, você pode filtrar manuais de reprodução que podem ser usados com base no estágio no funil de marketing que deseja direcionar - conversão, engajamento ou retenção. Você também pode filtrar os manuais exibidos pelo setor em que você está ou pelo direito do produto ao qual você tem acesso - Adobe Journey Optimizer ou Real-time CDP.

![Filtrar manuais por funil de marketing, setor ou produto](/help/use-case-playbooks/assets/playbooks/ui-guide/filter-by-funnel-industry-product.gif)

Você também pode usar a funcionalidade de pesquisa para encontrar o manual certo para você. Veja abaixo um exemplo de como encontrar um manual que ajuda você a se envolver com usuários que podem ter abandonado o carrinho de compras.

![Interaja com usuários que podem ter abandonado o carrinho.](/help/use-case-playbooks/assets/playbooks/ui-guide/engage-abandoned-cart.gif)

Ou você pode filtrar os manuais disponíveis pelos canais que planeja usar para alcançar seus clientes, como pode ver abaixo:

![Filtrar por canal](/help/use-case-playbooks/assets/playbooks/ui-guide/channel-select-filter.gif)

Experimente com as opções de filtros e pesquisa e encontre o manual certo para você.

## Exibir manual e gerar ativos {#view-playbook-generate-assets}

Antes de definir um manual e criar ocorrências dele, você deve inspecioná-lo para verificar se ele atende às suas necessidades. Para ajudá-lo a entender melhor os casos de uso abordados, todos os manuais contêm as seções listadas abaixo. Quando estiver pronto para continuar e gerar ativos, selecione **[!UICONTROL Criar instância]**.

### Mindmap {#mindmap}

Use a seção de mapa mental em um manual para entender as etapas do fluxo de trabalho que o manual pode ajudar a resolver. Visualizar o fluxo de como todos os objetos gerados podem ajudar a obter o caso de uso, da perspectiva da persona direcionada no caso de uso.

O mapa mental começa com uma definição de quem é atingido na jornada do usuário e descreve em cada etapa se algo é entregue pelo Adobe, como uma nova mensagem ou um lembrete, ou se é algo que a persona direcionada fez que aciona a próxima mensagem ou evento.

![Mapa mental do manual destacado.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-mindmap.png)


### Resumo {#summary}

Inspect na seção de resumo para entender quais ativos são gerados depois que você cria instâncias do manual. Os ativos gerados para cada manual são adaptados ao caso de uso que o manual permite. Obtenha mais informações abaixo sobre todos os itens na seção de resumo.

| Item | Descrição |
---------|----------|
| **[!UICONTROL Público alvo]** | Descreve as personalidades que você deseja acessar por meio deste manual de casos de uso. |
| **[!UICONTROL Canais de marketing]** | Descreve os canais usados para acessar as personalidades direcionadas no manual. |
| **[!UICONTROL Ativos técnicos]** | Uma lista dos ativos técnicos que são gerados após a criação de instâncias do manual. Os ativos gerados diferem por manual, dependendo do caso de uso. Alguns manuais podem gerar esquemas, segmentos e jornadas. Outros podem gerar destinos. Consulte a [Entender os ativos gerados](#understand-assets) mais abaixo para obter mais informações sobre como usar e reutilizar os ativos gerados. |

{style="table-layout:auto"}

![Resumo do manual destacado](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-summary.png)

### Instâncias {#instances}

Role para baixo até a seção instâncias para obter uma visão geral das instâncias deste manual que você ou os membros de sua equipe já criaram. Você pode usar vários controles para classificar e filtrar as instâncias exibidas, por exemplo, para ver apenas as criadas por você. Você também pode ver várias informações sobre cada instância, conforme listado abaixo.

| Item | Descrição |
|---------|----------|
| **[!UICONTROL Nome]** | O nome da instância com base no manual. Você pode personalizar o nome e a descrição de uma instância. Leia a seção abaixo em [como editar metadados da instância](#edit-instance-metadata) para obter mais informações. |
| **[!UICONTROL Status]** | Indica o status da instância. A **[!UICONTROL enviado]** está pronta para uso. |
| **[!UICONTROL Criado]** | Indica quando a instância foi criada. |
| **[!UICONTROL Criado por]** | Indica quem criou a instância. |
| **[!UICONTROL Última modificação]** | Indica quando a instância foi modificada pela última vez. |

{style="table-layout:auto"}

![Instância do manual realçada.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-instances.png)

## Ativar o manual {#enable-playbook}

Quando estiver pronto para continuar com um manual e criar uma instância, selecione **[!UICONTROL Criar instância]** para continuar com o manual e gerar ativos técnicos.

![Criar uma instância de um manual.](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

Essa ação gera vários ativos para você usar a fim de obter o caso de uso descrito no manual.

![Visualização de manual dos ativos gerados após a ativação.](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### Usar os controles de configuração para editar nomes e descrições de instâncias {#edit-instance-metadata}

Depois de criar uma instância com base em um manual, você pode personalizá-lo para diferenciá-lo de outras instâncias criadas no mesmo manual. Selecione o controle de configuração conforme mostrado abaixo. Edite o nome, a descrição e as notas e selecione **[!UICONTROL Salvar]** quando terminar.

![Editar o nome e a descrição de uma instância.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### Entender os ativos gerados {#understand-assets}

>[!IMPORTANT]
>
>Não precisa se preocupar! Este é um espaço seguro para experimentar e você não pode quebrar nada. Ainda não há dados associados a nenhum dos ativos que você cria. Primeiro, você deve assimilar dados para obter os casos de uso.

É importante entender que os ativos gerados diferem com base no caso de uso que você está ativando:

* Ativos diferentes são gerados para diferentes tipos de manuais. Esses ativos são criados especificamente para o caso de uso obtido por meio do manual. Por exemplo, um manual gera um esquema, um segmento, uma jornada e mensagens. Outro manual gera um esquema, um segmento e um destino para ativar os dados.
* Os ativos em si diferem entre os manuais. Por exemplo, para o **[!UICONTROL Enviar Uma Mensagem De Aniversário Aos Convidados]** playbook, o público-alvo criado tem a regra `birthday=today AND year=any`.

Para ilustrar um exemplo, para o **[!UICONTROL Carrinho abandonado: Mercadorias]** playbook, você pode ver que uma jornada específica é criada e inclui as mensagens criadas para esse caso de uso.

![Jornada criada a partir do manual de casos de uso.](/help/use-case-playbooks/assets/playbooks/ui-guide/journey-preview.png)

### Usar e editar os ativos gerados {#use-and-edit-assets}

Ao explorar os ativos gerados após a criação de uma instância de um manual, é possível editar qualquer um dos ativos criados.

Se você ou alguém da sua equipe criar outra instância do manual, os ativos editados serão mantidos e novos ativos serão criados para a nova instância do manual.

O comportamento descrito acima é verdadeiro para todos os ativos criados, exceto para esquemas. No caso de esquemas, novos esquemas não são criados quando uma nova instância de um manual é criada, portanto, você estará usando o esquema editado de outra instância do manual na instância recém-criada.

>[!TIP]
>
>Teste na sandbox de desenvolvimento e mude para produção quando estiver pronto.
>
>Depois que os objetos forem gerados, você poderá continuar o teste nas sandboxes de desenvolvimento adicionando dados. Você pode testar os ativos conforme desejar na sandbox de desenvolvimento e pode replicar a lógica do ativo (definições de segmento, jornadas, esquemas e assim por diante) na sandbox de produção quando estiver pronto.

### Reutilizar manuais {#reuse-playbooks}

Ao criar várias instâncias do mesmo manual, é possível implementar o mesmo caso de uso posteriormente, sem modificar os detalhes da implementação anterior do caso de uso.

### Compartilhar o manual e os ativos gerados com outros membros da equipe {#share-playbook}

Você pode compartilhar a instância gerada e os ativos com outros membros da equipe. Para fazer isso, copie o link do URL do navegador e compartilhe-o com sua equipe para fornecer uma visão geral dos ativos gerados.

![URL destacado em uma visualização do manual de caso de uso.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## Próximas etapas {#next-steps}

Ao ler este guia de interface do usuário, agora você sabe como interpretar as várias seções de um manual e como usar os ativos que são gerados após criar uma instância de um manual. Em seguida, você pode navegar no catálogo de manuais para encontrar o manual correto para o seu caso de uso e ler o guia de solução de problemas se encontrar erros.