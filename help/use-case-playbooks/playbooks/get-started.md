---
solution: Experience Platform
title: Introdução aos manuais de caso de uso
description: Saiba como começar a usar a funcionalidade dos manuais de estratégia de casos de uso.
role: Admin
exl-id: 1c39792e-49fe-4c5f-9796-fa29f60b7461
source-git-commit: 703c84e61af105bc3933e4750a3cb27df8ac19fe
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 14%

---


# Introdução

Saiba como configurar sua conta para manuais de casos de uso, projetados para Real-time Customer Data Platform e Adobe Journey Optimizer se não forem configurados automaticamente. As três etapas principais de configuração são:

* Criar uma sandbox
* Configuração de permissões de usuários e usuárias
* Configurar superfícies dos canais do Journey Optimizer para notificações por email, push e SMS (se você planeja usar os manuais do Journey Optimizer)

Para acessar uma galeria avançada de manuais de casos de uso na interface do usuário do Experience Platform, selecione **[!UICONTROL Manuais]** na navegação à esquerda. Leia a documentação sobre como [navegar nos manuais de casos de uso](../playbooks/navigate.md) e começar a usar uma [sandbox inspiradora](../playbooks/navigate.md).

## Configurar manuais de casos de uso - Apresentação em vídeo {#video}

Assista a este vídeo para saber mais sobre as etapas necessárias para criar sua sandbox, configurar permissões e configurar superfícies do canal para notificações por email, push e SMS no Journey Optimizer.

>[!VIDEO](https://video.tv.adobe.com/v/3426987?learn=on)

## Criar uma sandbox de desenvolvimento {#create-development-sandbox}

Os manuais de casos de uso usam um tipo especial de sandbox de desenvolvimento. Para começar e obter acesso à funcionalidade dos [[!UICONTROL manuais de estratégia de casos de uso]](/help/use-case-playbooks/playbooks/overview.md), [, crie uma nova sandbox de desenvolvimento](/help/sandboxes/ui/user-guide.md#create) (não selecione uma sandbox de produção) com um nome (não um título) que contenha o sufixo `-ucp` ou `-UCP`, conforme mostrado abaixo.

>[!IMPORTANT]
>
>Ao criar uma nova sandbox de desenvolvimento, verifique se o nome contém `-ucp` ou `-UCP` no sufixo.


![Criar uma sandbox de desenvolvimento para manuais de estratégia de casos de uso](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

Agora você deve ver [!UICONTROL manuais] no painel esquerdo em [!UICONTROL manuais de casos de uso].

![Manuais de estratégia de casos de uso na interface após a criação da sandbox.](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

Se não vir os [!UICONTROL Manuais de estratégia] no painel esquerdo, como mostrado acima, use o link `https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates` para obter um acesso direto. No link, `<YOUR_ORG>` é o nome da sua organização e `<YOUR_SANDBOX_NAME>` é o nome da sandbox de desenvolvimento que você criou.

## Conceda à sua equipe as permissões de acesso necessárias {#grant-access-permissions}

Para começar a usar os [!UICONTROL Livros de reprodução de caso de uso], os membros da sua equipe de marketing precisam das permissões certas para poderem exibir a lista de livros de reprodução criados ou criar livros de reprodução sozinhos.

**Permissões necessárias**

Para adicionar as permissões necessárias, na interface de Permissões, inclua a nova sandbox do manual do caso de uso em [funções que você já configurou](/help/access-control/abac/ui/permissions.md#managing-sandboxes-for-role), incluindo aquelas usadas para outras sandboxes de desenvolvimento.

![Sandbox do manual para funções já configuradas](/help/use-case-playbooks/assets/playbooks/get-started/permissions-to-existing-roles.png)

**Configurar uma função para os manuais:**

Como alternativa, você também pode considerar adicionar novas funções com [as permissões necessárias](/help/access-control/home.md#sandboxes-and-permissions).

[Configure uma nova função](/help/access-control/abac/ui/permissions.md) com as permissões necessárias para as tarefas essenciais do manual. Crie uma função e adicione a nova sandbox a ela, conforme mostrado abaixo.

![Criar uma função e adicioná-la à Sandbox](/help/use-case-playbooks/assets/playbooks/get-started/create-new-role.png)

**Permissões para instâncias do manual de reprodução**

Como parte dos manuais de casos de uso, você criará vários ativos, como esquemas, públicos, destinos e jornadas. Você e outros usuários precisarão das permissões certas para criar esses objetos.

**Permissões para esquemas**

Para criar e gerenciar esquemas, utilize as permissões de modelagem de dados; **[!UICONTROL Gerenciar esquemas]**, **[!UICONTROL Exibir esquemas]**, **[!UICONTROL Gerenciar relações]**, **[!UICONTROL Gerenciar metadados de identidade]**

**Permissões para destinos**

Para criar e gerenciar destinos, use as permissões de Destinos; **[!UICONTROL Gerenciar]**, **[!UICONTROL Destinos]**, **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Ativar Segmento sem Mapeamento]**, **[!UICONTROL Gerenciar e Ativar Destino do Conjunto de Dados]**, **[!UICONTROL Criação de Destino]**.

**Permissões para o jornada**

Para criar e gerenciar jornadas, use as permissões do Jornada; **[!UICONTROL Gerenciar Jornadas]**, **[!UICONTROL Exibir Jornadas]**, **[!UICONTROL Exibir Relatório do Jornada]**, **[!UICONTROL Gerenciar Jornadas]**, **[!UICONTROL Eventos]**, **[!UICONTROL Fontes de Dados e Ações]**, **[!UICONTROL Exibir Jornadas]**, **[!UICONTROL Eventos]**, **[!UICONTROL Fontes de Dados e Ações, Publish Jornada]**.

A imagem abaixo exibe um instantâneo das permissões recomendadas para que os usuários visualizem, criem e gerenciem manuais e ativos gerados por manuais.

![Instantâneo de todos os itens de permissão necessários para criar todas as instâncias dos manuais](/help/use-case-playbooks/assets/playbooks/get-started/permission-snapshot.png)

**Adicionar usuários à função**

Depois que você [criar uma nova função](/help/access-control/abac/ui/permissions.md#managing-users-for-role) conforme mencionado acima, adicione a si mesmo como usuário a ela. Se você criar uma função com acesso limitado para outro conjunto de usuários com acesso somente visualização, inclua apenas os itens de visualização necessários associados a essas permissões.

## Configurar sandbox e superfícies de canal no Journey Optimizer {#configure-channel-surfaces}

Se sua organização tiver uma licença do [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR) e você quiser usar os manuais criados para o Journey Optimizer, será necessário configurar as predefinições de canal em sua sandbox, que definem os parâmetros técnicos necessários para suas mensagens. [Saiba como configurar superfícies de canal no Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html?lang=pt-BR).

Para criar instâncias de manuais no Journey Optimizer, é necessário configurar superfícies de canal para notificações por email, push e SMS.

### Superfície de canal de email

Vá para `Channels` na interface do Journey Optimizer. Configure subdomínios e pools de IP separados para emails de marketing e mensagens transacionais, se ainda não estiver configurado. Essas são as práticas recomendadas para garantir que mensagens transacionais, como emails de confirmação de pedidos, sejam enviadas aos clientes. Insira nomes, endereços de email e configurações adicionais. Selecione **Enviar** no canto superior direito da página para criar a superfície de canal de marketing. Leia a documentação sobre [como configurar superfícies de canal de email](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html?lang=pt-BR).

### Superfície de canal de SMS

Para criar uma superfície de canal de SMS, primeiro crie uma credencial de API de SMS e selecione o fornecedor preferencial (por exemplo, Sinch). Nomeie a superfície de canal SMS (por exemplo, Marketing de SMS), selecione a configuração e insira um número de remetente. Selecione **Enviar** no canto superior direito da página para salvar a superfície de canal de SMS. Leia a documentação sobre [como configurar superfícies de canal de SMS](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=br#message-preset-sms).

Também configure canais para manuais que contenham mensagens transacionais, como confirmações de pedidos.

### Superfície de canal de push

Confirme se as configurações de canal estão definidas na interface Experience Platform ou na interface de Coleções de dados. É assim que as configurações de canal se parecem no ambiente de Coleções de dados.

<!-- ![Channel configurations in Data collections](/help/use-case-playbooks/assets/playbooks/get-started/.png) -->

Em seguida, selecione o canal, as plataformas e os aplicativos que você visualizou nas configurações de canal. Selecione **Enviar** para criar a superfície de canal de push.

Leia a documentação sobre [como configurar superfícies de canal de push](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html?lang=pt-BR).

## Próximas etapas {#next-steps}

Agora que você seguiu todas as etapas deste documento, deveria ter criado uma sandbox de desenvolvimento com manuais de casos de uso disponíveis na navegação à esquerda. Agora você também sabe como conceder aos membros da equipe as permissões necessárias para exibir e gerenciar manuais e gerar ativos. Como próxima etapa, leia como [escolher o manual correto](/help/use-case-playbooks/playbooks/choose.md) para você e [criar instâncias dele](/help/use-case-playbooks/playbooks/create-share-reuse.md).
