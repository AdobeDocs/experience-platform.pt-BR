---
keywords: Experience Platform, home, tópicos populares, serviço de identidade, serviço de identidade, dispositivos compartilhados, dispositivos compartilhados
solution: Experience Platform
title: Visão geral de dispositivos compartilhados (Beta)
topic-legacy: tutorial
description: A Detecção de dispositivo compartilhado identifica diferentes usuários autenticados do mesmo dispositivo, permitindo uma representação mais precisa dos dados do cliente nos gráficos de identidade
hide: true
hidefromtoc: true
source-git-commit: 1cdab6ce71c748ae174700ce50f50b143e46b40f
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# Visão geral da detecção de dispositivo compartilhado (Beta)

>[!IMPORTANT]
>
>O recurso [!DNL Shared Device Detection] está na versão beta. Seus recursos e documentação estão sujeitos a alterações.

O Adobe Experience Platform [!DNL Identity Service] ajuda você a obter uma melhor visão de seu cliente e de seu comportamento ao unir identidades entre dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais impactantes em tempo real.

[!DNL Shared Device] refere-se aos dispositivos usados por mais de um indivíduo. Os exemplos de um dispositivo compartilhado incluem tablets, computadores de biblioteca e quiosques. Por meio do recurso [!DNL Shared Device Detection], é possível impedir que usuários diferentes do mesmo dispositivo sejam mesclados em uma única identidade, permitindo uma representação mais precisa de um indivíduo.

Com [!DNL Shared Device Detection] você pode:

* Criar gráficos de identidade separados para diferentes utilizadores do mesmo dispositivo;
* Impedir a mistura de dados de indivíduos diferentes usando o mesmo dispositivo;
* Gere uma exibição mais limpa e precisa de seus clientes.

>[!TIP]
>
>As configurações para [!DNL Shared Device Detection] devem ser concluídas antes de habilitar o Perfil para o conjunto de dados, pois não é mais possível revisar as configurações depois que os gráficos são gerados em [!DNL Identity Service].

## Introdução

Trabalhar com [!DNL Shared Device Detection] requer uma compreensão dos vários serviços da plataforma envolvidos. Antes de começar a trabalhar com [!DNL Shared Device Detection], reveja a documentação dos seguintes serviços:

* [[!DNL Identity Service]](../home.md): Obtenha uma melhor visão de clientes individuais e seu comportamento ao unir identidades em dispositivos e sistemas.
   * [Visualizador](./identity-graph-viewer.md) do gráfico de identidade: Visualize e interaja com o visualizador de gráficos de identidade para entender melhor como as identidades do cliente são unidas e de que maneiras.
   * [Namespaces](../namespaces.md) de identidade: Veja os componentes de uma identidade totalmente qualificada e como os namespaces de identidade permitem distinguir o contexto e o tipo de uma identidade.

### Terminologia

A tabela a seguir contém uma lista de termos essenciais para entender [!DNL Shared Device Detection]:

| Termos | Definição |
| --- | --- |
| Dispositivo compartilhado | Um dispositivo compartilhado é qualquer dispositivo usado por mais de um indivíduo. Os exemplos de dispositivos compartilhados incluem tablets, computadores de biblioteca e quiosques. |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] refere-se a uma configuração que permite que dados de usuários diferentes do mesmo dispositivo sejam separados um do outro. |
| [!UICONTROL Namespace de identidade compartilhada] | Um [!UICONTROL Namespace de identidade compartilhada] é usado para representar um único dispositivo compartilhado por vários usuários diferentes. |
| [!UICONTROL Namespace de identidade do usuário] | Um [!UICONTROL Namespace de identidade do usuário] é usado para representar o usuário autenticado ou conectado de um dispositivo compartilhado. |

## Interface do usuário de dispositivos compartilhados

Na interface do usuário da plataforma, selecione **[!UICONTROL Identities]** no menu de navegação esquerdo e selecione **[!UICONTROL Configurações de identidade]**.

![identity-dashboard](../images/shared-device/identity-dashboard.png)

A página [!UICONTROL Configurações de dispositivo compartilhado] é exibida, fornecendo uma interface para definir as configurações de dispositivo compartilhado para seus dados. As configurações de dispositivo compartilhado são desabilitadas por padrão.

Quando ativadas, as configurações de dispositivo compartilhado permitem que os dados de usuários diferentes do mesmo dispositivo sejam separados um do outro. Essa configuração permite uma representação mais limpa e precisa dos gráficos de identidade, em que as identidades do usuário do mesmo dispositivo não são combinadas.

Selecione **[!UICONTROL Ativar]** para começar a modificar as definições do dispositivo partilhado.

![enable-shared-device](../images/shared-device/enable-shared-device.png)

As opções de configuração [!UICONTROL Namespace de identidade compartilhada] e [!UICONTROL Namespace de identidade de usuário] são exibidas, permitindo modificar os namespace de identidade que você deseja usar.

![set-namespaces](../images/shared-device/set-namespaces.png)

[!UICONTROL O ] Namespace de identidade compartilhada representa um único dispositivo usado por vários usuários diferentes. Esse namespace é sempre definido como **[!UICONTROL ECID]** porque todos os usuários da plataforma usam **[!UICONTROL ECID]** como o identificador do navegador da Web.

![shared-identity-namespace](../images/shared-device/shared-identity-namespace.png)

O [!UICONTROL Namespace de identidade do usuário] permite identificar usuários diferentes do mesmo dispositivo e impedir que os dados sejam combinados no mesmo gráfico de identidade.

![user-identity-namespace](../images/shared-device/user-identity-namespace.png)

Selecione a barra de pesquisa **[!UICONTROL Namespace de identidade do usuário]** e insira um namespace de identidade ou selecione um namespace de identidade no menu suspenso.

>[!TIP]
>
>O [!UICONTROL Namespace de identidade do usuário] deve ser mapeado para o namespace de identidade que corresponde à ID de logon do usuário final. As opções incluem ID do cliente, email e email com hash.

![emails](../images/shared-device/emails.png)

Depois de configurar as [!UICONTROL Configurações do dispositivo compartilhado], selecione **[!UICONTROL Salvar]**.

![salvar](../images/shared-device/save.png)

Uma janela pop-up é exibida, solicitando que você confirme sua seleção. Selecione **[!UICONTROL Yes]** para concluir a configuração.

![confirmar](../images/shared-device/confirm.png)
