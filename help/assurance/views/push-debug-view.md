---
title: Exibição da depuração de push
description: Este guia detalha informações sobre a exibição de Depuração por push no Adobe Experience Platform Assurance.
source-git-commit: 5778d4db27d0f57281821dc8e042a31b69745514
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---


# Exibir Depuração por Push

A Exibição de depuração por push no Adobe Experience Platform Assurance oferece a capacidade de validar a configuração de push do seu aplicativo e enviar uma mensagem de teste para o seu dispositivo.

## Clientes

![Clientes de push](./images/push-debug-view/clients.png)

A lista suspensa do cliente tem uma lista de cada cliente exclusivo que se conectou a esta sessão de Controle. Um cliente é um dispositivo exclusivo ou uma instalação de aplicativo exclusiva para um dispositivo. Por exemplo, se um dispositivo Android e um dispositivo iOS tiverem sido conectados à sessão, esses clientes aparecerão na lista suspensa Clientes .

Após reinstalar e reconectar o aplicativo em um dispositivo, outro cliente será exibido. Se um dispositivo com esse nome já existir, a nova lista suspensa anexará um nº 2 ao nome.

Essa exibição só é ativada para um único cliente, portanto, selecionar um cliente diferente alterará os detalhes na tela.

## Validar configuração

O **[!UICONTROL Validar configuração]** A guia valida e fornece detalhes adicionais sobre a configuração de push do aplicativo. Há três painéis que executam validações. Eles exibirão uma marca de seleção verde se as validações forem bem-sucedidas. Se houver três marcas de seleção verdes, o aplicativo foi configurado corretamente para mensagens de push, está gravando tokens de push para o perfil do usuário e tem uma superfície de aplicativo associada configurada.

Se algo não estiver funcionando como esperado, haverá um alerta com detalhes sobre como corrigir esse problema:

![Estado Inválido](./images/push-debug-view/invalid-state.png)

### Detalhes do cliente

Esse painel verifica se o dispositivo está configurado corretamente. Isso inclui configurar a extensão na interface do usuário da Coleta de dados, inicializar a extensão e seus pré-requisitos no aplicativo e capturar o token de push do dispositivo.

Se for válido, o painel exibirá a ECID do dispositivo, o token de push e o nome e o tipo da sandbox de borda.

### Detalhes do perfil

Depois que o cliente estiver configurado corretamente, esse painel verificará se o dispositivo está gravando no perfil. Também verifica se o token de push no perfil corresponde ao do dispositivo.

Se for válido, o painel mostrará a ECID do dispositivo, o token de push, a ID do aplicativo do aplicativo, a plataforma de mensagens e se o token de push foi incluído na lista de negação. O token pode ser listado como negação por vários motivos, como o usuário desinstalou o aplicativo ou o usuário desabilitou as mensagens de push para o aplicativo.

![Bloqueado](./images/push-debug-view/deny-list-blocked.png)

Finalmente, na parte inferior do painel, há um link que abrirá esse perfil específico em uma nova guia.

### Credenciais e configuração da AppStore

Esse painel valida que a ID do aplicativo e a plataforma de mensagens que foi salva no perfil têm uma superfície de aplicativo correspondente criada. Uma superfície do aplicativo é onde as credenciais de push do aplicativo são carregadas.

Se for válido, o perfil exibirá o nome da superfície do aplicativo, a ID do aplicativo e o nome do serviço de mensagens.

Por fim, na parte inferior do painel, há um link que abrirá a superfície específica do aplicativo em uma nova guia.

## Enviar push de teste

O **[!UICONTROL Enviar push de teste]** pode ser usada para enviar uma mensagem de teste para o seu dispositivo.

Há vários painéis que podem ser configurados para testar diferentes recursos de push do iOS e Android. Após a configuração, selecione **[!UICONTROL Enviar notificação por push de teste]** para enviar a mensagem.

![Enviar push](./images/push-debug-view/send.png)

### Mensagem

No **[!UICONTROL Mensagem]** , é possível fornecer um título e um corpo para a mensagem. O recurso de notificação silenciosa também pode ser ativado aqui.

![Painel de Mensagens](./images/push-debug-view/message-pane.png)

### Direcionamento por push

O **[!UICONTROL Direcionamento de push]** O painel permite personalizar qual token de push e a superfície do aplicativo serão usados ao enviar a mensagem de push.

Essas informações são fornecidas por padrão se a variável **[!UICONTROL Validar configuração]** mostra três marcas de seleção verdes. No entanto, você pode fornecer seu próprio token de push e superfície do aplicativo, mesmo que seu aplicativo não esteja totalmente configurado.

![Painel de Destino](./images/push-debug-view/target-pane.png)

### Comportamento de clique

No **[!UICONTROL Comportamento de cliques]** , você pode escolher qual comportamento deve ser quando a notificação por push for clicada no dispositivo. Por padrão, ele abrirá o aplicativo, mas poderá abrir um deep link ou uma página da Web.

Se você optar por usar um deep link, o desenvolvedor do aplicativo deverá criar um para você.

![Painel Comportamento](./images/push-debug-view/click-behavior.png)

### Mídia avançada

O **[!UICONTROL Mídia avançada]** O painel permite adicionar mídia extra à mensagem, como uma imagem, vídeo ou GIF. O desenvolvedor do aplicativo deve adicionar código ao aplicativo para ativar esse recurso.

![Painel Rico](./images/push-debug-view/rich-pane.png)

### Botões

O **[!UICONTROL Botões]** permite adicionar botões extras à notificação por push. Cada botão pode abrir o aplicativo, abrir um deep link no aplicativo ou abrir uma página da Web.

O desenvolvedor do aplicativo deve adicionar código ao aplicativo para ativar esse recurso.

![Painel Botões](./images/push-debug-view/buttons-pane.png)

### Dados personalizados

O **[!UICONTROL Dados personalizados]** permite adicionar dados personalizados à notificação por push. Cada par de chave/valor é enviado como metadados, juntamente com a mensagem, e pode ser usado pelos desenvolvedores para criar experiências poderosas e adicionar um rastreamento adicional.

![Painel Personalizado](./images/push-debug-view/custom-pane.png)

## Resultados dos ensaios

Depois de enviar uma mensagem, a variável **[!UICONTROL Resultados do teste]** recebe dados dos serviços de push da mensagem. Aqui você pode ver se a mensagem chegou aos serviços de mensagens da Google/iOS:

![Resultados do teste](./images/push-debug-view/test-results.png)

Se ocorrerem problemas, eles serão exibidos aqui:

![Erro de resultados de teste](./images/push-debug-view/test-error.png)

## Avançado

### Exibir carga da mensagem

Ao lado do **[!UICONTROL Enviar notificação por push de teste]** é um conjunto de reticências com um menu pop-up. A partir daqui, você poderá visualizar o payload da mensagem. Isso permite que você veja a mensagem exata que será enviada para o serviço de mensagens remoto. Você pode revisar essa carga ou até mesmo copiá-la e colá-la em uma ferramenta de teste de push de desktop.

![Painel Personalizado](./images/push-debug-view/message-payload.png)
