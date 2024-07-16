---
solution: Experience Platform
title: Navegar até os manuais de casos de uso
description: Saiba como navegar em uma galeria de manuais e começar a usar uma sandbox inspiradora.
role: User
exl-id: 1f5dae75-1136-4be3-9132-01d36a4066ca
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 2%

---

# Navegar até os manuais de casos de uso

Os manuais de casos de uso estão disponíveis sem custo extra para todos os clientes do Adobe Experience Platform. Para acessar uma galeria avançada de manuais de casos de uso na interface do usuário do Experience Platform, selecione **[!UICONTROL Manuais]** na navegação à esquerda.

![Galeria de manuais de caso de uso.](/help/use-case-playbooks/assets/playbooks/discover/playbooks-gallery.png)

![Acesso direto aos manuais de caso de uso na barra de navegação à esquerda.](/help/use-case-playbooks/assets/playbooks/discover/left-nav-playbooks.png)

Selecione qualquer manual para ir para a página de detalhes e selecione **[!UICONTROL Ir para uma sandbox inspiradora]**. Uma modal de confirmação é exibida. Selecione **Confirmar** para ir para a sandbox inspiradora, onde você pode explorar e experimentar os diferentes casos de uso.

Se você não tiver permissão para criar sandboxes, entre em contato com o administrador para obter assistência na criação de uma sandbox inspiradora.

>[!TIP]
>
>Uma sandbox inspiradora é uma sandbox de desenvolvimento no Adobe Experience Platform em que você pode criar, testar e experimentar diferentes casos de uso antes de implementá-los em um ambiente de produção em tempo real.

![Ir para sandbox inspiradora.](/help/use-case-playbooks/assets/playbooks/discover/inspirational-sandbox.png)

Se você ainda não tiver configurado nenhuma sandbox inspiradora, selecione **[!UICONTROL Criar uma sandbox inspiradora]**. Uma modal é exibida. Insira o **Nome** e o **Título** nas caixas de campo necessárias e selecione **Criar**. Depois de criar a sandbox inspiradora, certifique-se de [definir permissões](/help/access-control/home.md) antes de voltar para a página de detalhes dos manuais de caso de uso para criar uma instância.

![Criar uma sandbox inspiradora.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox.png)

![Insira o nome e o título para criar uma sandbox inspiradora.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox-modal.png)

Se você selecionar um manual de casos de uso de fora de uma sandbox inspiradora, não será possível criar uma instância. Na página de detalhes, selecione **Ir para sandbox inspiracional** para ir para uma sandbox inspiracional existente e selecione **[!UICONTROL Criar instância]**.

Se você não tiver permissão para criar sandboxes, entre em contato com o administrador para obter assistência na criação de uma sandbox inspiradora.

![Nenhuma permissão para criar sandbox.](/help/use-case-playbooks/assets/playbooks/discover/no-permissions-to-create-sandbox.png)

Se você tiver atingido o limite do número de sandboxes que foram alocadas para você, será exibida uma mensagem solicitando que você entre em contato com o administrador da organização para aumentar o limite ou desativar ou remover algumas sandboxes ativas. Depois que o limite da sandbox for ajustado ou o número de sandboxes ativas for reduzido, você pode continuar a criar a sandbox inspiradora.

![Limite de sandbox atingido.](/help/use-case-playbooks/assets/playbooks/discover/sandbox-limit-reached.png)

Observe que, ao criar uma sandbox inspiradora, as superfícies de canal para notificações por email, push e SMS não são configuradas automaticamente. Entre em contato com o administrador de TI para configurá-los manualmente ou a criação da instância pode falhar.

![Configurar predefinições de canal.](/help/use-case-playbooks/assets/playbooks/discover/configure-channel-presets.png)

## Configurar sandbox e superfícies de canal no Journey Optimizer {#configure-channel-surfaces}

Se sua organização tiver uma licença do [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR) e você quiser usar os manuais criados para o Journey Optimizer, será necessário configurar as predefinições de canal em sua sandbox, que definem os parâmetros técnicos necessários para suas mensagens. [Saiba como configurar superfícies de canal no Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html?lang=pt-BR).

Para criar instâncias de manuais no Journey Optimizer, é necessário configurar superfícies de canal para notificações por email, push e SMS.

### Superfície de canal de email

Vá para `Channels` na interface do Journey Optimizer. Configure subdomínios e pools de IP separados para emails de marketing e mensagens transacionais, se ainda não estiver configurado. Essas são as práticas recomendadas para garantir que mensagens transacionais, como emails de confirmação de pedidos, sejam enviadas aos clientes. Insira nomes, endereços de email e configurações adicionais. Selecione **Enviar** no canto superior direito da página para criar a superfície de canal de marketing. Leia a documentação sobre [como configurar superfícies de canal de email](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html).

### Superfície de canal de SMS

Para criar uma superfície de canal de SMS, primeiro crie uma credencial de API de SMS e selecione o fornecedor preferencial (por exemplo, Sinch). Nomeie a superfície de canal SMS (por exemplo, Marketing de SMS), selecione a configuração e insira um número de remetente. Selecione **Enviar** no canto superior direito da página para salvar a superfície de canal de SMS. Leia a documentação sobre [como configurar superfícies de canal de SMS](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=br#message-preset-sms).

Também configure canais para manuais que contenham mensagens transacionais, como confirmações de pedidos.

### Superfície de canal de push

Confirme se as superfícies do aplicativo estão configuradas na interface Experience Platform ou Coleções de dados. É assim que as superfícies do aplicativo se parecem no ambiente de Coleções de dados.

## Próximas etapas {#next-steps}

Agora que você leu este documento, deve saber como configurar uma sandbox inspiradora e conhecer diferentes maneiras de acessar manuais de casos de uso na Platform. Como próxima etapa, leia sobre como [escolher](/help/use-case-playbooks/playbooks/choose.md) o manual correto.
