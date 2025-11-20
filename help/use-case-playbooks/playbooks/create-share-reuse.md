---
solution: Experience Platform
title: Criar, compartilhar e reutilizar instâncias do manual de estratégia
description: Saiba como criar, compartilhar e reutilizar instâncias do manual de estratégia para concluir seu caso de uso de marketing.
role: User, Developer
exl-id: b06d8186-c41f-4150-bac4-69c616151ef9
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 71%

---

# Criar, compartilhar e reutilizar instâncias do manual de estratégia

Para usar um manual, navegue até **[!UICONTROL Use Case Playbooks]>[!UICONTROL Playbooks]**. Explore e use as várias opções de pesquisa e filtragem na página para selecionar e começar a usar um manual de estratégia específico.

## Criar uma instância do manual de estratégia {#create-playbook-instance}

>[!CONTEXTUALHELP]
>id="platform_playbooks_create"
>title="Criar instância"
>abstract="Gere uma lista de ativos como jornadas, públicos-alvo, esquemas ou destinos para usar em cenários de jornada ou ativação."

Antes de criar uma instância de manual, explore os manuais disponíveis para [escolher o manual correto](/help/use-case-playbooks/playbooks/choose.md). Quando estiver pronto para continuar com um manual e criar uma instância, selecione **[!UICONTROL Create Instance]** para continuar com o manual e gerar ativos técnicos.

![Criar uma instância de um manual de estratégia.](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

Essa ação gera vários ativos para serem usados a fim de obter o caso de uso descrito no manual de estratégia.

![Visualização do manual de estratégia de habilitos gerados após a habilitação.](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### Use os controles de configuração para editar nomes e descrições de instâncias {#edit-instance-metadata}

Depois de criar uma instância com base em um manual de estratégia, é possível personalizá-la para diferenciá-la de outras instâncias criadas a partir do mesmo manual de estratégia. Selecione o controle de configuração conforme mostrado abaixo. Edite o nome, a descrição e as anotações e selecione **[!UICONTROL Save]** quando terminar.

![Editar o nome e a descrição de uma instância.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### Entender os ativos gerados {#understand-assets}

>[!IMPORTANT]
>
>Não se preocupe. Este é um espaço seguro para experimentar, e nada pode ser desconfigurado. Ainda não há dados associados a nenhum dos ativos que você criou. Primeiro é necessário assimilar os dados para atingir os casos de uso.

É importante entender que os ativos gerados diferem com base no caso de uso sendo habilitado:

* Ativos diferentes são gerados para diferentes tipos de manuais de estratégia. Esses ativos são criados especificamente para o caso de uso atingido através do manual de estratégia. Por exemplo, um manual gera um esquema, um público-alvo, uma jornada e mensagens. Outro manual gera um esquema, um público-alvo e um destino para ativar os dados.
* Os ativos em si diferem entre os manuais de estratégia. Por exemplo, para o manual **[!UICONTROL Send A Birthday Message To Guests]**, o público-alvo criado tem a regra `birthday=today AND year=any`.

Para ilustrar um exemplo, para o manual **[!UICONTROL Abandoned Cart: Merchandise]**, você pode ver que uma jornada específica é criada e inclui as mensagens criadas para este caso de uso.

![Jornada criada a partir do manual de estratégia de caso de uso.](/help/use-case-playbooks/assets/playbooks/ui-guide/journey-preview.png)

### Usar e editar os ativos gerados {#use-and-edit-assets}

Ao explorar os ativos gerados após a criação de uma instância de um manual de estratégia, é possível editar qualquer um dos ativos criados.

Se você ou alguém da sua equipe criar outra instância do manual de estratégia, os ativos editados serão mantidos e novos ativos serão criados para a nova instância.

O comportamento descrito acima se aplica para todos os ativos criados, exceto para esquemas. No caso de esquemas, novos esquemas não são criados quando uma nova instância de um manual de estratégia é criada. Portanto, você estará usando o esquema editado de outra instância na recém-criada.

>[!TIP]
>
>Teste na sandbox de desenvolvimento e vá para a produção quando estiver pronto.
>
>Depois que os objetos forem gerados, será possível continuar os testes nas sandboxes de desenvolvimento adicionando dados. Você pode testar os ativos conforme desejar na sandbox de desenvolvimento e pode replicar a lógica do ativo (definições de público-alvo, jornadas, esquemas e assim por diante) na sandbox de produção quando estiver pronto. Você pode mover para a sandbox de desenvolvimento e, em seguida, para a sandbox de produção usando a [funcionalidade de reconhecimento de dados](/help/use-case-playbooks/playbooks/data-awareness.md).

## Reutilizar manuais de estratégia {#reuse-playbooks}

Ao criar várias instâncias do mesmo manual de estratégia, é possível implementar o mesmo caso de uso posteriormente, sem modificar os detalhes da implementação anterior.

## Compartilhar o manual de estratégia e os ativos gerados com outros membros da equipe {#share-playbook}

É possível compartilhar a instância gerada e os ativos com outros membros da equipe. Para fazer isso, copie o link do URL do navegador e compartilhe-o com sua equipe para fornecer uma visão geral dos ativos gerados.

![URL destacado em uma visualização do manual de estratégia de caso de uso.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## Apresentação em vídeo do processo completo do manual

Assista a este vídeo para saber como descobrir, criar, publicar e solucionar problemas de instâncias de um manual de casos de uso de ponta a ponta, bem como copiar os ativos gerados pelo manual para outras sandboxes configuradas em sua organização.

>[!VIDEO](https://video.tv.adobe.com/v/3427058/?learn=on)

## Próximas etapas {#next-steps}

Ao ler o manual sobre como descobrir o manual de estratégia correto para você e este, você saberá como interpretar as várias seções de um manual de estratégia e como usar os ativos que são gerados após criar uma instância.

Em seguida, é possível navegar pelo catálogo de manuais de estratégia para encontrar o manual correto para o seu caso de uso e ler o [manual de solução de problemas](/help/use-case-playbooks/playbooks/troubleshooting.md) caso encontre algum.
