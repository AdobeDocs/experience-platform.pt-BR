---
keywords: Experience Platform;início;tópicos populares;serviço de identidade;Serviço de identidade;dispositivos compartilhados;Dispositivos compartilhados
title: Visão Geral De Dispositivos Compartilhados (Beta)
description: A Detecção de dispositivos compartilhados identifica diferentes usuários autenticados do mesmo dispositivo, permitindo uma representação mais precisa dos dados do cliente em gráficos de identidade
hide: true
hidefromtoc: true
exl-id: 36318163-ba07-4209-b1be-dc193ab7ba41
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# Visão geral da Detecção de dispositivo compartilhado (Beta)

>[!IMPORTANT]
>
>A variável [!DNL Shared Device Detection] O recurso está na versão beta. Seus recursos e documentação estão sujeitos a alterações.

Adobe Experience Platform [!DNL Identity Service] O ajuda você a obter uma melhor visualização do cliente e do comportamento dele, unindo identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.

[!DNL Shared Device] refere-se a dispositivos usados por mais de um indivíduo. Exemplos de dispositivos compartilhados incluem tablets, computadores de biblioteca e quiosques. Por meio da [!DNL Shared Device Detection] diferentes usuários do mesmo dispositivo podem ser impedidos de ser mesclados em uma única identidade, permitindo uma representação mais precisa de um indivíduo.

Com [!DNL Shared Device Detection] você pode:

* Criar gráficos de identidade separados para diferentes usuários do mesmo dispositivo;
* Impedir a mistura de dados de indivíduos diferentes utilizando o mesmo dispositivo;
* Gere uma visualização mais clara e precisa de seus clientes.

>[!TIP]
>
>Configurações para [!DNL Shared Device Detection] deve ser concluído antes de ativar o Perfil para o conjunto de dados, pois você não pode mais revisar as configurações depois que os gráficos forem gerados no [!DNL Identity Service].

## Introdução ao [!DNL Shared Device Detection]

Trabalhar com [!DNL Shared Device Detection] exige uma compreensão dos vários serviços de plataforma envolvidos. Antes de começar a trabalhar com [!DNL Shared Device Detection], consulte a documentação dos seguintes serviços:

* [[!DNL Identity Service]](../home.md): obtenha uma melhor visualização dos clientes individuais e do comportamento deles ao unir as identidades de vários dispositivos e sistemas.
   * [Visualizador de gráficos de identidade](./identity-graph-viewer.md): visualize e interaja com o visualizador de gráficos de identidade para entender melhor como as identidades do cliente são unidas e de que maneiras.
   * [Namespaces de identidade](../namespaces.md): veja os componentes de uma identidade totalmente qualificada e como os namespaces de identidade permitem distinguir o contexto e o tipo de uma identidade.

## Noções básicas do [!DNL Shared Device Detection]

É importante compreender a seguinte terminologia ao trabalhar com a
[!DNL Shared Device Detection]. Consulte a tabela abaixo para obter uma lista dos termos essenciais para entender [!DNL Shared Device Detection].

### Terminologia

| Termos | Definição |
| --- | --- |
| Dispositivo compartilhado | Um dispositivo compartilhado é qualquer dispositivo usado por mais de um indivíduo. Exemplos de dispositivos compartilhados incluem tablets, computadores de biblioteca e quiosques. |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] refere-se a uma definição de configuração que permite que dados de diferentes usuários do mesmo dispositivo sejam separados uns dos outros. |
| Namespace de identidade compartilhado | O Namespace de identidade compartilhado representa o dispositivo que pode ser usado por vários usuários. O Namespace de identidade compartilhado geralmente é a ECID, mas pode ser definido como outras IDs de dispositivo. |
| Namespace de identidade do usuário | O Namespace de Identidade do Usuário representa o usuário autenticado (conectado) de um dispositivo compartilhado. |
| Último usuário autenticado | O último usuário autenticado representa o usuário que fez logon pela última vez em um dispositivo, se um dispositivo estiver sendo conectado por várias contas. |

{style="table-layout:auto"}

[!DNL Shared Device Detection] funciona estabelecendo dois namespaces: o **Namespace de identidade compartilhado** e a variável **Namespace de identidade do usuário**.

* O Namespace de identidade compartilhado representa o dispositivo que pode ser usado por vários usuários. A Adobe recomenda que os clientes usem a ECID como o identificador do dispositivo compartilhado.
* O Namespace de identidade do usuário é mapeado para o namespace de identidade que corresponde à ID de logon de um usuário. Pode ser a ID de CRM, o endereço de email, o email com hash ou o número de telefone de um usuário.

Um dispositivo compartilhado, como um tablet, tem um único **Namespace de identidade compartilhado**. Por outro lado, cada usuário de um dispositivo compartilhado tem seu próprio **Namespace de identidade do usuário** que corresponde às respectivas IDs de logon. Por exemplo, um tablet que Kevin e Nora compartilham para uso de comércio eletrônico tem sua própria ECID de `1234`, enquanto Kevin tem seu próprio namespace de identidade de usuário que está mapeado para o seu `kevin@email.com` e Nora tem seu próprio namespace de identidade de usuário mapeado para ela `nora@email.com` conta.

[!DNL Shared Device Detection] O pode fazer distinções entre vários usuários do mesmo dispositivo vinculando o namespace de identidade compartilhado (por exemplo, ECID) com o último Namespace de identidade do usuário autenticado (ID de logon).

### Como os dados de identidade são enviados para um gráfico de identidade

Considere o exemplo a seguir para ajudar a entender como [!DNL Shared Device Detection] funciona:

>[!NOTE]
>
>Neste diagrama, o Namespace de identidade compartilhado é configurado para ECID e o Namespace de identidade do usuário é configurado para CRM ID.

![diagrama](../images/shared-device/diagram.png)

* Kevin e Nora compartilham um tablet para visitar um site de comércio eletrônico. No entanto, ambos têm as suas próprias contas independentes, que cada um utiliza para navegar e comprar em linha;
   * Como um dispositivo compartilhado, o tablet tem uma ECID correspondente, que representa a ID de cookie do navegador da Web do tablet;
* Suponha que Kevin use o tablet e **logon** na conta de comércio eletrônico para procurar fones de ouvido, isso significa que a ID de CRM de Kevin (**Namespace de identidade do usuário**) agora está vinculada à ECID do tablet (**Namespace de identidade compartilhado**). Os dados de navegação do tablet agora são incorporados ao gráfico de identidade de Kevin.
   * Se Kevin **fazer logoff** e Nora usa o tablet e **logon** Para sua própria conta e comprar uma câmera, a ID do CRM agora está vinculada à ECID do tablet. Portanto, os dados de navegação do tablet agora são incorporados ao gráfico de identidade de Nora.
   * If Nora **não faz logoff** Kevin usa o tablet, mas... **não faz logon**, os dados de navegação do tablet ainda são incorporados a Nora, pois ela permanece como a usuário autenticada e sua ID de CRM ainda está vinculada à ECID do tablet.
   * If Nora **faz logoff** Kevin usa o tablet, mas... **não faz logon** No entanto, os dados de navegação do tablet ainda são incorporados ao gráfico de identidade de Nora, porque, como a **último usuário autenticado**, sua ID de CRM permanece vinculada à ECID do tablet.
   * Se Kevin **logon** novamente, sua ID do CRM agora é vinculada à ECID do tablet, pois ele é o último usuário autenticado e os dados de navegação do tablet agora são incorporados ao seu gráfico de identidade.

### Como [!DNL Profile Service] mescla fragmentos de perfil com [!DNL Shared Device Detection] habilitado

[!DNL Profile Service] O toma nota dos fragmentos de perfil e perfis mesclados. Cada perfil de cliente individual é composto por vários fragmentos de perfil que foram mesclados para formar uma única visualização desse cliente. Por exemplo, se um cliente interagir com sua marca em vários canais, sua organização terá vários fragmentos de perfil relacionados a esse único cliente que aparecem em vários conjuntos de dados. Quando esses fragmentos são assimilados na Platform, eles são mesclados para criar um único perfil para esse cliente.

Quando [!DNL Shared Device Detection] está ativado, [!DNL Profile] define a identidade principal do fragmento de perfil com base no fato de o evento de experiência ser autenticado ou não autenticado

Um **evento de experiência autenticada** é uma ação concluída por um usuário enquanto está conectado a um dispositivo. Para eventos de experiência autenticados, a identidade principal é a **Namespace de identidade do usuário** (ID de login). Um **evento de experiência não autenticado** é uma ação concluída por um usuário que não está conectado a um dispositivo. Para eventos de experiência não autenticados, a identidade principal é a **Namespace de identidade compartilhado** (ECID).

Para obter mais informações, consulte  [[!DNL Real-Time Customer Profile] visão geral](../../profile/home.md).

## Interface de dispositivos compartilhados

Na interface do usuário da Platform, selecione **[!UICONTROL Identidades]** no menu de navegação esquerdo e selecione **[!UICONTROL Configurações de identidade]**.

![identity-dashboard](../images/shared-device/identity-dashboard.png)

A variável [!UICONTROL Configurações do dispositivo compartilhado] é exibida, fornecendo uma interface para definir as configurações de dispositivo compartilhado para seus dados. As configurações de dispositivo compartilhado são desabilitadas por padrão.

Quando ativadas, as configurações do dispositivo compartilhado permitem que os dados de diferentes usuários do mesmo dispositivo sejam separados uns dos outros. Essa configuração permite uma representação mais limpa e precisa de gráficos de identidade, em que as identidades de usuário do mesmo dispositivo não são combinadas.

Selecionar **[!UICONTROL Ativar]** para começar a modificar as configurações do dispositivo compartilhado.

![enable-shared-device](../images/shared-device/enable-shared-device.png)

A variável [!UICONTROL Namespace de identidade compartilhado] e [!UICONTROL Namespace de identidade do usuário] opções de configuração são exibidas, permitindo modificar os namespaces de identidade que deseja usar.

![set-namespaces](../images/shared-device/set-namespaces.png)

[!UICONTROL Namespace de identidade compartilhado] representa um único dispositivo usado por vários usuários diferentes. Este namespace é sempre definido como **[!UICONTROL ECID]** porque todos os usuários da Platform usam **[!UICONTROL ECID]** como o identificador do navegador da web.

![shared-identity-namespace](../images/shared-device/shared-identity-namespace.png)

A variável [!UICONTROL Namespace de identidade do usuário] O permite identificar diferentes usuários do mesmo dispositivo e impedir que os dados sejam combinados no mesmo gráfico de identidade.

![user-identity-namespace](../images/shared-device/user-identity-namespace.png)

Selecione o **[!UICONTROL Namespace de identidade do usuário]** barra de pesquisa e insira um namespace de identidade ou selecione um namespace de identidade no menu suspenso.

>[!TIP]
>
>A variável [!UICONTROL Namespace de identidade do usuário] deve ser mapeado para o namespace de identidade que corresponde à ID de logon do usuário final. As opções incluem ID do cliente, email e email com hash.

![emails](../images/shared-device/emails.png)

Depois de configurar suas [!UICONTROL Configurações do dispositivo compartilhado], selecione **[!UICONTROL Salvar]**.

![save](../images/shared-device/save.png)

Uma janela pop-up é exibida solicitando que você confirme sua seleção. Selecionar **[!UICONTROL Sim]** para concluir a definição de configuração.

![confirmar](../images/shared-device/confirm.png)
