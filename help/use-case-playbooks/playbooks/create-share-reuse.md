---
solution: Experience Platform
title: Criar, compartilhar e reutilizar instâncias do manual
description: Saiba como criar, compartilhar e reutilizar instâncias do manual para concluir seu caso de uso de marketing.
badgeBeta: label="Beta" type="Informative"
source-git-commit: 51e4a77472ccb560dbfa5f56011ce50932d87b64
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 1%

---


# (Beta) Criar, compartilhar e reutilizar instâncias do manual

>[!AVAILABILITY]
>
>No momento, essa funcionalidade está na versão beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Para usar um manual, navegue até **[!UICONTROL Playbooks de caso de uso] > [!UICONTROL Playbooks]**. Navegue e use as várias opções de pesquisa e filtragem na página para selecionar e começar a usar um manual específico.

## Criar uma instância do manual {#create-playbook-instance}

Antes de criar uma instância de manual, explore os manuais disponíveis para [descubra o manual certo para você](/help/use-case-playbooks/playbooks/discover.md). Quando estiver pronto para continuar com um manual e criar uma instância, selecione **[!UICONTROL Criar instância]** para continuar com o manual e gerar ativos técnicos.

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

Ao ler este guia e o sobre como descobrir o manual certo para você, agora você sabe como interpretar as várias seções de um manual e como usar os ativos que são gerados após criar uma instância de um manual.

Em seguida, você pode navegar pelo catálogo de manuais para encontrar o manual correto para o seu caso de uso e ler o [guia de solução de problemas](/help/use-case-playbooks/playbooks/troubleshooting.md) caso encontre algum problema.