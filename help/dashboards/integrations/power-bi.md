---
title: Modelos de relatório do Power BI para painéis da plataforma
description: Use modelos de relatório para explorar dados do Experience Platform usando o Power BI.
source-git-commit: 19b0ce2c8125fa5253cbba34adbd2884e27b5133
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 0%

---


# Modelos de relatório do Power BI para painéis

O recurso de modelo de relatório do Power BI permite criar relatórios convincentes preenchidos com dados do Adobe Experience Platform. O processo de instalação simplificado instala automaticamente widgets padrão para Perfil do cliente em tempo real, segmentação e destinos. A instalação também conecta o Power BI aos seus modelos de dados para que você possa personalizar e estender seus modelos de relatório com facilidade. Esses relatórios podem ser compartilhados em toda a organização sem que os recipients precisem de credenciais para a organização IMS na plataforma.

Este documento fornece instruções sobre como conectar o Adobe Experience Platform ao aplicativo Power BI e usar modelos de relatório para compartilhar informações importantes dos dados da plataforma com usuários externos.

## Introdução

Antes de continuar com este tutorial, é recomendável ter uma boa compreensão de [composição de schema](../../xdm/schema/composition.md) no Experience Platform e como os atributos são incluídos no Perfil do cliente em tempo real por meio do [schema de união](../../xdm/schema/composition.md#union).

Para instalar a integração do aplicativo Power BI, os usuários devem ter adquirido primeiro as seguintes permissões da Platform:

- Gerenciar Consultas
- Gerenciar sandboxes

Para saber como atribuir essas permissões, leia o [controle de acesso](../../access-control/home.md) documentação.

Você também deve ter uma conta do Power BI para seguir este tutorial. Para criar uma conta, navegue até o [Página inicial do Power BI](https://powerbi.microsoft.com/en-us/) e siga o processo de inscrição. Os usuários dessa conta do Power BI também devem ativar a variável **Criar espaço de trabalho** nas configurações do Power BI. Essa configuração é encontrada nas configurações de locatário do portal de administração do Power BI. Se sua conta for fornecida pelo locatário ou empregador, entre em contato com o respectivo administrador para ativar essa configuração.

![O portal de administração do Power BI cria configurações do espaço de trabalho.](../images/power-bi/create-workspace-settings.png)

>[!NOTE]
>
>Para que a guia Painéis apareça na navegação à esquerda da interface do usuário da plataforma e a visualização Inventário do painel fique visível, você deve ter acesso a qualquer um dos painéis Perfil, Segmentação ou Destino como parte de sua licença da plataforma.

## Instalar a integração do aplicativo Power BI

Na interface do usuário da plataforma, selecione **[!UICONTROL Painéis]** na navegação à esquerda para abrir o [!UICONTROL Painéis] espaço de trabalho. O [!UICONTROL Procurar] exibe uma lista de exibições de painel disponíveis no momento. Para saber mais sobre como visualizar painéis disponíveis, consulte o [documentação do inventário](../inventory.md).

Em seguida, selecione o **[!UICONTROL Integrações]** guia . A página Power BI application integration é exibida. Aqui, selecione **[!UICONTROL Instalar]** para iniciar a instalação.

>[!NOTE]
>
>O [!UICONTROL Instalar] está desativado, a menos que você tenha permissões para Gerenciar serviços de consulta e Gerenciar sandboxes.

![Tela de detalhes do Power BI com o botão Instalar realçado.](../images/power-bi/details-screen.png)

### Fornecer credenciais

A primeira etapa do processo de instalação é fornecer credenciais que não expiram para a integração do aplicativo do Power BI. Há duas opções disponíveis para fornecer: [[!UICONTROL Criar novas credenciais]](#create-new-credentials) ou [[!UICONTROL Usar credenciais existentes]](#use-existing-credentials). Selecione a opção de alternância apropriada para continuar.

#### Criar novas credenciais {#create-new-credentials}

Há dois campos obrigatórios ao gerar novas credenciais: [!UICONTROL Nome] e [!UICONTROL Atribuído a]. O [!UICONTROL Atribuído a] está relacionado ao endereço de email associado à sua conta do Power BI.

![O Power BI gera nova tela de credenciais.](../images/power-bi/generate-new-credentials.png)

>[!IMPORTANT]
>
>A criação de credenciais que não estão expirando exige que você tenha determinadas permissões e funções atribuídas. As permissões necessárias são Gerenciar sandboxes e Gerenciar integração do serviço de consulta . As funções necessárias são as funções de administrador e desenvolvedor do Adobe Experience Platform. Para saber como atribuir essas permissões, leia o [controle de acesso](../../access-control/home.md) documentação.

Para saber mais sobre a geração de credenciais do Serviço de Consulta que não estão expirando, consulte o [guia de credenciais que não expiram](../../query-service/ui/credentials.md#non-expiring-credentials).

Após gerar credenciais que não expiram pela primeira vez, um arquivo JSON é baixado para essa máquina. Esse arquivo JSON pode ser compartilhado com outros usuários como credenciais para concluir o processo de instalação.

#### Usar credenciais existentes {#use-existing-credentials}

Um arquivo de credencial JSON também pode ser carregado para passar a validação. Esses arquivos JSON que contêm os valores de credenciais que não expiram são baixados no computador local que está sendo usado quando uma credencial que não expira é criada.

>[!IMPORTANT]
>
>Para usar uma credencial que não expira, o usuário já deve ter recebido uma credencial. Se o usuário não tiver uma credencial atribuída e não puder criar uma nova usando a Adobe Admin Console, ele não poderá continuar com o processo de instalação.

Selecionar **[!UICONTROL Upload do arquivo de credencial]**, em seguida, selecione o arquivo JSON apropriado a ser carregado na caixa de diálogo exibida.

![Tela de credenciais do Power BI com o botão Upload credential file realçado.](../images/power-bi/upload-credential-file.png)

Depois de fornecer as credenciais que não expiram, elas são validadas automaticamente pela Platform. Uma mensagem de confirmação é exibida assim que a validação é bem-sucedida. Selecionar **[!UICONTROL Próximo]** para rever o acordo de consentimento do pedido de Power BI.

![Tela validada com êxito das credenciais que não expiram, com o botão Next realçado.](../images/power-bi/successfully-uploaded-credential-file.png)

### Fornecer consentimento

A exibição do consentimento é exibida. Selecionar **[!UICONTROL Revisar consentimento]** para abrir uma nova janela detalhando as permissões necessárias para que o Power BI acesse e use seus dados de acordo com seus termos de serviço e declaração de privacidade.

![A tela de consentimento da entrega com o botão Revisar consentimento destacado.](../images/power-bi/provide-consent-display.png)

Selecionar **[!UICONTROL Aceitar]** para conceder permissão ao Power BI para acessar e usar os dados da plataforma.

![Solicitação de permissões para o aplicativo Power BI.](../images/power-bi/permissions.png)

>[!NOTE]
>
>Se você sair do processo de instalação em qualquer ponto antes de fornecer o consentimento, a integração do aplicativo do Power BI não será instalada no inventário de painéis.

Após fornecer o consentimento, o template do relatório é instalado automaticamente no ambiente do Power BI como parte do processo de instalação. O Power BI usa as credenciais que não expiram para acessar a Platform, executar sequencialmente todas as consultas SQL e preencher o template do relatório com os dados retornados.

Selecionar **[!UICONTROL Concluir]** para retornar ao inventário do painel.

![A tela de consentimento do provedor com o botão Finish realçado.](../images/power-bi/finish-consent-review.png)

Agora que o modelo de relatório do Power BI está instalado, ele aparece na lista de painéis disponíveis no [!UICONTROL Procurar] guia . Selecionar **[!UICONTROL Power BI]** na lista para navegar até o ambiente do Power BI.

![Power BI listadas no inventário de painéis.](../images/power-bi/power-bi-dashboard-inventory.png)

>[!IMPORTANT]
>
>Os administradores do Power BI precisam verificar se os usuários têm as permissões de acesso apropriadas para visualizar esses painéis no ambiente do Power BI.

## espaço de trabalho do Power BI

Depois de fazer logon em [o espaço de trabalho do Power BI](https://dxt.powerbi.com), os modelos de relatório estão disponíveis para cada um dos serviços aos quais você tem acesso. Os modelos de relatório incluem perfis, segmentos e painéis de destinos **only** se tiverem as permissões de exibição correspondentes.

Os widgets padrão de perfis, segmentos e destinos estão disponíveis nos relatórios de modelo do Power BI por padrão.

>[!NOTE]
>
>Você deve ter permissões de edição ativadas para um determinado painel para permitir que esse painel seja instalado no ambiente do Power BI.

![Relatório do modelo de Perfil do Power BI usando widgets de perfil de plataforma padrão.](../images/power-bi/profile-report-template.png)

Depois que um painel é instalado no Power BI, os modelos de relatório são exibidos para todos os usuários por padrão. Se quiser restringir o acesso a qualquer modelo de relatório, desative o acesso dos usuários em questão no ambiente Power BI.

## Personalizar o modelo de relatório do Power BI

Com o uso de widgets personalizados, você pode adicionar atributos personalizados ao seu modelo de dados para enriquecer os modelos de relatório fornecidos pelo Power BI.

>[!NOTE]
>
>Os atributos que você pode usar para widgets personalizados dependem do que está disponível no schema de união. Para saber como visualizar e explorar schemas de união em benefício dos widgets personalizados, consulte o [guia da interface do usuário do schema de união](../../profile/ui/union-schema.md).

### Criar um widget personalizado

Os widgets personalizados são criados por meio da Biblioteca de widgets. Consulte a [Visão geral da biblioteca de widgets](../customize/widget-library.md) para obter uma introdução ao recurso e ao [tutorial para criar um widget personalizado](../customize/custom-widgets.md) para obter instruções específicas.

>[!IMPORTANT]
>
>Os widgets personalizados recém-criados são **not** sincronizado automaticamente entre painéis do Adobe Experience Platform e modelos de relatório do Power BI. Todos os widgets personalizados criados na interface do usuário da plataforma devem ser recriados manualmente no ambiente do Power BI.

### Recrie seu widget personalizado no ambiente Power BI

Depois que o painel tiver as métricas e os atributos apropriados contidos nos widgets personalizados, você estará pronto para modificar o modelo de relatório exibido a partir do ambiente do Power BI. Consulte a [Documentação do Power BI](https://docs.microsoft.com/pt-BR/power-bi/) para obter informações sobre como editar um relatório por meio de sua interface do usuário.

## Excluir a integração do aplicativo do Power BI

Para excluir o painel, navegue até o inventário do painel e selecione o ícone excluir (![](../images/power-bi/delete-icon.png)) ao lado do nome do painel.

>[!NOTE]
>
>Somente o usuário que instalou o painel do Power BI pode excluir a integração da interface do usuário da plataforma.

![Guia de navegação da tela de inventário dos painéis exibida com o botão Procurar e o ícone Excluir realçado.](../images/power-bi/delete-power-bi-dashboard.png)

Um provedor de confirmação é exibido. Selecionar **[!UICONTROL Excluir]** para confirmar o processo.

>[!IMPORTANT]
>
>A exclusão do painel do Power BI da interface do usuário da plataforma faz isso **not** exclua os modelos de relatório disponíveis no seu ambiente Power BI. Para excluir completamente as informações contidas nos modelos de relatório do Power BI, é necessário fazer logon em sua conta do Power BI e excluir os modelos de relatório desse ambiente. Depois de excluído, o usuário pode reinstalar o painel do Power BI seguindo as mesmas instruções de instalação descritas acima.

## Próximas etapas

Ao ler este documento, você tem uma melhor compreensão de como os modelos de relatório do Power BI podem ser integrados ao Platform para compartilhar informações de dados convincentes de seus perfis, segmentos ou painéis de destinos. Consulte a [visão geral da personalização do painel](../customize/overview.md) para saber mais sobre como personalizar seus painéis.
