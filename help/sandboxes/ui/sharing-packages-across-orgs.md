---
title: Compartilhamento De Pacotes Entre Organizações Usando Ferramentas De Sandbox
description: Saiba como usar as ferramentas de sandbox na Adobe Experience Platform para compartilhar pacotes em diferentes organizações.
badge: Beta
source-git-commit: 492f1d9dc08965dba3f1c5b6e1d479ef645afd04
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# Compartilhar pacotes entre organizações usando as ferramentas de sandbox

>[!NOTE]
>
>O compartilhamento de pacotes entre organizações está atualmente na versão beta e só está disponível para clientes beta selecionados.

Este documento aborda como usar ferramentas de sandbox no Adobe Experience Platform para compartilhar pacotes em diferentes organizações.

Melhore a precisão da configuração em sandboxes e exporte e importe configurações de sandbox facilmente entre sandboxes em diferentes organizações com o recurso de ferramenta sandbox. Há dois tipos de pacotes compartilhados:

**Pacote privado**

Os pacotes privados só podem ser compartilhados com organizações que aprovaram a solicitação de compartilhamento da organização de origem por meio de uma lista de permissões de aceitação.

**Pacote público**

Pacotes públicos estão disponíveis para importação sem nenhuma aprovação adicional. Esses pacotes podem ser compartilhados no site, blog ou plataforma de um parceiro. A carga do pacote permite que os pacotes sejam copiados e colados desses canais na organização de destino.

## Pacotes privados

>[!NOTE]
>
>Para iniciar e aprovar uma solicitação de compartilhamento e compartilhar pacotes entre organizações, será necessário ter a permissão de controle de acesso baseado em função **compartilhamento de pacotes**.

O recurso de ferramentas de sandbox oferece a capacidade de criar parcerias organizacionais, acompanhar as estatísticas de uma solicitação de parceria, gerenciar parcerias existentes e compartilhar pacotes com organizações parceiras.

### Criar uma solicitação de parceria de organização

Para criar uma solicitação de parceria de organização, navegue até a guia [!UICONTROL Sandboxes] **[!UICONTROL Organizações de parceiros]**. Em seguida, selecione **[!UICONTROL Gerenciar organizações do parceiro]**.

![A interface de sandboxes, com a guia Organizações de parceiro e Gerenciar organizações de parceiro realçadas.](../images/ui/sandbox-tooling/private-manage-partner-orgs.png)

Na caixa de diálogo [!UICONTROL Gerenciamento de parceiro de pacote], digite a ID da organização em **[!UICONTROL Insira a ID da organização]** e pressione Enter. A ID da organização é mostrada na seção **[!UICONTROL IDs de organização selecionadas]** abaixo. Depois de adicionar as IDs, selecione **[!UICONTROL Confirmar]**.

>[!TIP]
>
>Várias IDs de organização podem ser inseridas por vez usando listas separadas por vírgulas ou inserindo cada ID de organização seguida por inserir.

![A caixa de diálogo Organizações do Parceiro do Pacote com Inserir ID da Organização, IDs da Organização Selecionadas e Confirmar foi realçada.](../images/ui/sandbox-tooling/private-enter-org-id.png)

A solicitação de compartilhamento foi enviada com êxito para a organização parceira, e você retornou à guia [!UICONTROL Sandboxes] **[!UICONTROL Organizações do parceiro]**, que exibe a **[!UICONTROL Solicitação de saída]**.

![A guia Organizações do parceiro com a solicitação de saída realçada.](../images/ui/sandbox-tooling/private-outgoing-request.png)

### Autorizar uma solicitação de parceria

Para autorizar uma solicitação de parceria de organização, navegue até a guia [!UICONTROL Sandboxes] **[!UICONTROL Organizações de parceiros]**. Em seguida, selecione **[!UICONTROL Solicitação de entrada]**.

![A interface de sandboxes com a guia Organizações do parceiro e a solicitação de entrada foram realçadas.](../images/ui/sandbox-tooling/private-authorise-partner-org.png)

O **[!UICONTROL Status]** atual da solicitação é **Pendente**. Para aprovar a solicitação, selecione as reticências (`...`) ao lado da solicitação selecionada e selecione **[!UICONTROL Aprovar]** na lista suspensa.

![Lista de solicitações de entrada mostrando o menu suspenso com Aprovar realçado.](../images/ui/sandbox-tooling/private-approve-partner-org.png)

A caixa de diálogo **[!UICONTROL Revisar solicitação de organização do parceiro]** exibe detalhes sobre a solicitação de parceria da organização. Insira um [!UICONTROL Motivo] para aprovação e selecione **[!UICONTROL Aprovar]**.

![A caixa de diálogo Revisar solicitação de organização do parceiro com Motivo e Aprovar está realçada.](../images/ui/sandbox-tooling/private-approval-partner-org.png)

Você retornou à página [!UICONTROL Solicitação de entrada] e o status da solicitação foi atualizado para **[!UICONTROL Aprovado]**.

![Lista de solicitações de entrada com Aprovado realçado.](../images/ui/sandbox-tooling/private-approved-partner-org.png)

Agora é possível compartilhar pacotes entre sua organização e a organização de origem.

### Compartilhar pacotes para organizações parceiras

>[!NOTE]
>
>Somente pacotes com o status **Publicado** podem ser compartilhados.

Para compartilhar um pacote com uma organização parceira aprovada, navegue até a guia [!UICONTROL Sandboxes] **[!UICONTROL Pacotes]**. Em seguida, selecione as reticências (`...`) ao lado do pacote e selecione **[!UICONTROL Compartilhar pacote]** no menu suspenso.

![Lista de pacotes mostrando o menu suspenso com a opção Compartilhar pacote realçada.](../images/ui/sandbox-tooling/private-share-package.png)

Na caixa de diálogo **[!UICONTROL Compartilhar pacote]**, selecione o pacote a ser compartilhado na lista suspensa **[!UICONTROL Configurações de compartilhamento]** e selecione **[!UICONTROL Confirmar]**.

![Caixa de diálogo Compartilhar pacote com as configurações de compartilhamento e Confirmar realçada.](../images/ui/sandbox-tooling/private-share-package-confirm.png)

>[!TIP]
>
>É possível selecionar mais de uma organização. As organizações selecionadas aparecerão abaixo da lista suspensa [!UICONTROL Configurações de compartilhamento].

## Próximas etapas

Este documento demonstrou como usar o recurso de ferramenta Sandbox para compartilhar pacotes em diferentes organizações. Para obter mais informações, consulte o [guia de ferramentas da sandbox](../ui/sandbox-tooling.md).

Para obter etapas sobre como executar operações diferentes usando a API de sandbox, consulte o [guia do desenvolvedor da sandbox](../api/getting-started.md). Para obter uma visão geral de alto nível das sandboxes no Experience Platform, consulte a [documentação de visão geral](../home.md).
