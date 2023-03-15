---
title: Modelos de relatório do Power BI para painéis da plataforma
description: Use modelos de relatório para explorar dados do Experience Platform usando o Power BI.
exl-id: fb98a79f-3d82-4e11-b08a-b7cb06414462
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 0%

---

# Modelos de relatório do Power BI para painéis

O recurso de modelo de relatório Power BI permite criar relatórios atraentes preenchidos com dados do Adobe Experience Platform. O processo de instalação simplificado instala automaticamente widgets padrão para o Perfil do cliente em tempo real, segmentação e destinos. A instalação também conecta o Power BI aos seus modelos de dados para que você possa personalizar e estender facilmente seus modelos de relatório. Esses relatórios podem ser compartilhados em toda a organização sem que os recipients precisem de credenciais para a Organização IMS na plataforma.

Este documento fornece instruções sobre como conectar o Adobe Experience Platform ao aplicativo do Power BI e usar modelos de relatório para compartilhar insights de dados importantes da Platform com usuários externos.

## Introdução

Antes de continuar com este tutorial, é recomendável ter uma boa compreensão de [composição do esquema](../../xdm/schema/composition.md) no Experience Platform e como os atributos são incluídos no Perfil do cliente em tempo real por meio da [esquema de união](../../xdm/schema/composition.md#union).

Para instalar a integração de aplicativos do Power BI, os usuários devem ter adquirido primeiro as seguintes permissões da Platform:

- Gerenciar consultas
- Gerenciar sandboxes

Para saber como atribuir essas permissões, leia o [controle de acesso](../../access-control/home.md) documentação.

Você também deve ter uma conta do Power BI para seguir este tutorial. Para criar uma conta, navegue até a [página inicial do Power BI](https://powerbi.microsoft.com/en-us/) e siga o processo de inscrição. Os usuários dessa conta do Power BI também devem ativar o **Criar espaço de trabalho** em suas configurações do Power BI. Essa configuração é encontrada nas configurações de locatário do portal de administração do Power BI. Se sua conta for fornecida por seu locatário ou empregador, entre em contato com seu respectivo administrador para ativar essa configuração.

![Criar configurações do espaço de trabalho do portal de administração do Power BI.](../images/power-bi/create-workspace-settings.png)

>[!NOTE]
>
>Para que a guia Painéis apareça na navegação à esquerda da interface do usuário da Platform e a visualização Inventário do painel fique visível, é necessário ter acesso a qualquer um dos painéis Perfil, Segmentação ou Destino como parte de sua licença da Platform.

## Instalar a integração de aplicativo do Power BI

Na interface do Platform, selecione **[!UICONTROL Painéis]** na navegação à esquerda, para abrir a [!UICONTROL Painéis] espaço de trabalho. A variável [!UICONTROL Procurar] exibe uma lista de exibições de painel disponíveis no momento. Para saber mais sobre a exibição de painéis disponíveis, consulte a [documentação do inventário](../inventory.md).

Em seguida, selecione o **[!UICONTROL Integrações]** guia. A página de integração de aplicativos do Power BI é exibida. Aqui, selecione **[!UICONTROL Instalar]** para iniciar a instalação.

>[!NOTE]
>
>A variável [!UICONTROL Instalar] O botão está desabilitado, a menos que você tenha as permissões Gerenciar serviço de consulta e Gerenciar sandboxes.

![A tela de detalhes do Power BI com o botão Instalar realçado.](../images/power-bi/details-screen.png)

### Fornecer credenciais

A primeira etapa do processo de instalação é fornecer credenciais sem expiração para a integração de aplicativos do Power BI. Há duas opções disponíveis para fornecer: [[!UICONTROL Criar novas credenciais]](#create-new-credentials) ou [[!UICONTROL Usar credenciais existentes]](#use-existing-credentials). Selecione a opção apropriada para continuar.

#### Criar novas credenciais {#create-new-credentials}

Há dois campos obrigatórios ao gerar novas credenciais: [!UICONTROL Nome] e [!UICONTROL Atribuído a]. A variável [!UICONTROL Atribuído a] O campo está relacionado ao endereço de email associado à sua conta do Power BI.

![tela Power BI novas credenciais.](../images/power-bi/generate-new-credentials.png)

>[!IMPORTANT]
>
>A criação de credenciais sem expiração requer que você tenha determinadas permissões e funções atribuídas. As permissões necessárias são Gerenciar sandboxes e Gerenciar integração do serviço de consulta. As funções necessárias são de administrador e desenvolvedor do Adobe Experience Platform. Para saber como atribuir essas permissões, leia o [controle de acesso](../../access-control/home.md) documentação.

Para saber mais sobre como gerar credenciais de Serviço de Consulta sem expiração, consulte o [guia de credenciais sem expiração](../../query-service/ui/credentials.md#non-expiring-credentials).

Após gerar credenciais sem expiração pela primeira vez, um arquivo JSON é baixado para essa máquina. Esse arquivo JSON pode ser compartilhado com outros usuários como credenciais para concluir o processo de instalação.

#### Usar credenciais existentes {#use-existing-credentials}

Um arquivo de credencial JSON também pode ser carregado para passar na validação. Esses arquivos JSON que contêm valores de credencial sem expiração são baixados para o computador local que está sendo usado quando uma credencial sem expiração é criada.

>[!IMPORTANT]
>
>Para usar uma credencial existente sem expiração, o usuário já deve ter recebido uma credencial. Se o usuário não tiver uma credencial atribuída e não puder criar uma nova usando o Adobe Admin Console, ele não poderá continuar com o processo de instalação.

Selecionar **[!UICONTROL Carregar arquivo de credencial]** e, em seguida, selecione o arquivo JSON apropriado para fazer upload na caixa de diálogo exibida.

![Tela de credenciais do Power BI com o botão Carregar arquivo de credencial realçado.](../images/power-bi/upload-credential-file.png)

Depois de fornecer as credenciais sem expiração, elas são validadas automaticamente pela Platform. Uma mensagem de confirmação é exibida assim que a validação é bem-sucedida. Selecionar **[!UICONTROL Próxima]** para revisar o contrato de consentimento do aplicativo Power BI.

![As credenciais sem expiração validaram com êxito a tela com o botão Avançar realçado.](../images/power-bi/successfully-uploaded-credential-file.png)

### Fornecer consentimento

A tela de consentimento é exibida. Selecionar **[!UICONTROL Revisar consentimento]** para abrir uma nova janela detalhando as permissões necessárias para que o Power BI acesse e use seus dados de acordo com os termos de serviço e a política de privacidade.

![A tela de consentimento é exibida com o botão Review consent realçado.](../images/power-bi/provide-consent-display.png)

Selecionar **[!UICONTROL Aceitar]** para conceder permissão ao Power BI para acessar e usar os dados da plataforma.

![Solicitação de permissões para o aplicativo Power BI.](../images/power-bi/permissions.png)

>[!NOTE]
>
>Se você sair do processo de instalação a qualquer momento antes de dar o consentimento, a integração de aplicativos do Power BI não será instalada no inventário de painéis.

Após fornecer o consentimento, o modelo de relatório é instalado automaticamente no ambiente do Power BI como parte do processo de instalação. Em seguida, o Power BI usa as credenciais sem expiração para acessar a Platform, executar sequencialmente todas as consultas SQL e preencher o modelo de relatório com os dados retornados.

Selecionar **[!UICONTROL Concluir]** para retornar ao inventário do painel.

![A tela de consentimento é exibida com o botão Finish realçado.](../images/power-bi/finish-consent-review.png)

Agora que o modelo de relatório do Power BI está instalado, ele aparece na lista de painéis disponíveis no [!UICONTROL Procurar] guia. Selecionar **[!UICONTROL Power BI]** na lista para navegar até o ambiente do Power BI.

![Power BI listados no inventário de painéis.](../images/power-bi/power-bi-dashboard-inventory.png)

>[!IMPORTANT]
>
>Os administradores do Power BI precisam verificar se os usuários têm as permissões de acesso apropriadas para visualizar esses painéis no ambiente do Power BI.

## espaço de trabalho do Power BI

Depois de fazer logon no [o espaço de trabalho do Power BI](https://dxt.powerbi.com), modelos de relatório estão disponíveis para cada um dos serviços aos quais você tem acesso. Os modelos de relatório incluem perfis, segmentos e painéis de destinos **somente** se tiverem as permissões de exibição correspondentes.

Por padrão, os widgets padrão de perfis, segmentos e destinos estão disponíveis nos relatórios de modelo do Power BI.

>[!NOTE]
>
>Você deve ter permissões de edição ativadas para um determinado painel para permitir que esse painel seja instalado no ambiente do Power BI.

![Relatório de modelo de perfil do Power BI usando widgets de perfil de plataforma padrão.](../images/power-bi/profile-report-template.png)

Após a instalação de um painel no Power BI, os modelos de relatório são exibidos para todos os usuários por padrão. Se quiser restringir o acesso a qualquer modelo de relatório, desative o acesso para os usuários em questão no ambiente do Power BI.

## Personalizar o modelo de relatório do Power BI

Com o uso de widgets personalizados, é possível adicionar atributos personalizados ao modelo de dados para enriquecer os modelos de relatório fornecidos pelo Power BI.

>[!NOTE]
>
>Os atributos que você pode usar para widgets personalizados dependem do que está disponível no esquema de união. Para saber como visualizar e explorar esquemas de união em benefício de seus widgets personalizados, consulte o [guia da interface do esquema de união](../../profile/ui/union-schema.md).

### Criar um widget personalizado

Widgets personalizados são criados por meio da Biblioteca de widgets. Consulte a [Visão geral da biblioteca de widgets](../customize/widget-library.md) para obter uma introdução ao recurso e ao [tutorial para criar um widget personalizado](../customize/custom-widgets.md) para obter instruções específicas.

>[!IMPORTANT]
>
>Os widgets personalizados recém-criados são **não** sincronizado automaticamente entre os painéis do Adobe Experience Platform e os modelos de relatório do Power BI. Todos os widgets personalizados criados na interface do usuário da Platform devem ser recriados manualmente no ambiente do Power BI.

### Recriar o widget personalizado no ambiente do Power BI

Depois que o painel tiver as métricas e os atributos apropriados contidos nos widgets personalizados, você estará pronto para modificar o modelo de relatório exibido no ambiente do Power BI. Consulte a [Documentação do Power BI](https://docs.microsoft.com/pt-BR/power-bi/) para obter informações sobre como editar um relatório por meio da interface.

## Excluir a integração de aplicativos do Power BI

Para excluir o painel, navegue até o inventário do painel e selecione o ícone excluir (![](../images/power-bi/delete-icon.png)) ao lado do nome do painel.

>[!NOTE]
>
>Somente o usuário que instalou o painel do Power BI pode excluir a integração da interface do usuário da Platform.

![Tela de inventário de painéis guia Procurar exibida com o botão Procurar e o ícone Excluir realçado.](../images/power-bi/delete-power-bi-dashboard.png)

Um popover de confirmação é exibido. Selecionar **[!UICONTROL Excluir]** para confirmar o processo.

>[!IMPORTANT]
>
>A exclusão do painel de Power BI da interface do usuário da Platform faz **não** excluir os modelos de relatório disponíveis em seu ambiente do Power BI. Se você quiser excluir completamente as informações contidas nos modelos de relatório do Power BI, será necessário fazer logon na sua conta do Power BI e excluir os modelos de relatório desse ambiente. Depois de excluído, um usuário pode reinstalar o painel do Power BI seguindo as mesmas instruções de instalação descritas acima.

## Próximas etapas

Ao ler este documento, você entende melhor como os modelos de relatório do Power BI podem ser integrados à Platform para compartilhar insights de dados atraentes de seus perfis, segmentos ou painéis de destinos. Consulte a [visão geral da personalização do painel](../customize/overview.md) para saber mais sobre como personalizar seus painéis.
