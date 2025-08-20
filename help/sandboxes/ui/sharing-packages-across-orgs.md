---
title: Compartilhamento De Pacotes Entre Organizações Usando Ferramentas De Sandbox
description: Saiba como usar as ferramentas de sandbox na Adobe Experience Platform para compartilhar pacotes em diferentes organizações.
exl-id: 02826a8d-f01d-44cb-9ae0-0fcde24de83e
source-git-commit: 3183d265eda36df9b08d920ba731bd9e63d150cc
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 0%

---

# Compartilhar pacotes entre organizações usando as ferramentas de sandbox

Melhore a precisão da configuração em sandboxes e exporte e importe configurações de sandbox facilmente entre sandboxes em diferentes organizações com o recurso de ferramenta sandbox. Este documento aborda como usar ferramentas de sandbox no Adobe Experience Platform para compartilhar pacotes em diferentes organizações. Há dois tipos de pacotes compartilhados:

- **Pacote privado**

[Pacotes privados](#private-packages) só podem ser compartilhados com organizações que aprovaram a solicitação de compartilhamento da organização de origem.

- **Pacote público**

[Pacotes públicos](#public-packages) estão disponíveis para importação sem nenhuma aprovação adicional. Esses pacotes podem ser compartilhados no site, blog ou plataforma de um parceiro. A carga do pacote permite que os pacotes sejam copiados e colados desses canais na organização de destino.

## Pacotes privados {#private-packages}

>[!NOTE]
>
>Para iniciar e aprovar uma solicitação de compartilhamento e compartilhar pacotes entre organizações, será necessário ter a permissão de controle de acesso baseado em função **compartilhamento de pacotes**.

Use o recurso Sandbox Tooling para criar parcerias, rastrear estatísticas de solicitação de parceria, gerenciar parcerias existentes e compartilhar pacotes com organizações parceiras.

### Criar uma solicitação de parceria de organização

Para criar uma solicitação de parceria de organização, navegue até a guia **[!UICONTROL Sandboxes]** **[!UICONTROL Organizações de parceiros]**. Em seguida, selecione **[!UICONTROL Gerenciar organizações do parceiro]**.

![A interface de sandboxes, com a guia Organizações de parceiro e Gerenciar organizações de parceiro realçadas.](../images/ui/sandbox-tooling/private-manage-partner-orgs.png)

Na caixa de diálogo [!UICONTROL Gerenciamento de parceiro de pacote], digite a ID da organização em **[!UICONTROL Digite a ID da Organização]** e pressione Enter (Windows) ou Return (Mac). A ID da organização é mostrada na seção **[!UICONTROL IDs de organização selecionadas]** abaixo. Depois de adicionar as IDs, selecione **[!UICONTROL Confirmar]**.

>[!TIP]
>
>Várias IDs de organização podem ser inseridas por vez usando listas separadas por vírgulas ou inserindo cada ID de organização seguida por inserir.

![A caixa de diálogo Organizações do Parceiro do Pacote com Inserir ID da Organização, IDs da Organização Selecionadas e Confirmar foi realçada.](../images/ui/sandbox-tooling/private-enter-org-id.png)

A solicitação de compartilhamento foi enviada com êxito para a organização parceira, e você retornou à guia [!UICONTROL Sandboxes] **[!UICONTROL Organizações do parceiro]**, que exibe a **[!UICONTROL Solicitação de saída]**.

![A guia Organizações do parceiro com a solicitação de saída realçada.](../images/ui/sandbox-tooling/private-outgoing-request.png)

### Autorizar uma solicitação de parceria {#authorize-request}

Para autorizar uma solicitação de parceria de organização, navegue até a guia [!UICONTROL Sandboxes] **[!UICONTROL Organizações de parceiros]**. Em seguida, selecione **[!UICONTROL Solicitação de entrada]**.

![A interface de sandboxes com a guia Organizações do parceiro e a solicitação de entrada foram realçadas.](../images/ui/sandbox-tooling/private-authorise-partner-org.png)

O **[!UICONTROL Status]** atual da solicitação, neste estágio, é **Pendente**. Para aprovar a solicitação, selecione as reticências (`...`) ao lado da solicitação selecionada e selecione **[!UICONTROL Aprovar]** na lista suspensa.

![Lista de solicitações de entrada mostrando o menu suspenso com Aprovar realçado.](../images/ui/sandbox-tooling/private-approve-partner-org.png)

A caixa de diálogo **[!UICONTROL Revisar solicitação de organização do parceiro]** exibe detalhes sobre a solicitação de parceria da organização. Insira um [!UICONTROL Motivo] para aprovação e selecione **[!UICONTROL Aprovar]**.

![A caixa de diálogo Revisar solicitação de organização do parceiro com Motivo e Aprovar está realçada.](../images/ui/sandbox-tooling/private-approval-partner-org.png)

Você retornou à página [!UICONTROL Solicitação de entrada] e o status da solicitação foi atualizado para **[!UICONTROL Aprovado]**.

![Lista de solicitações de entrada com Aprovado realçado.](../images/ui/sandbox-tooling/private-approved-partner-org.png)

Use esse fluxo de trabalho/processo para compartilhar pacotes entre sua organização e a organização de origem.

### Compartilhar pacotes para organizações parceiras {#share-package}

>[!NOTE]
>
>Somente pacotes com o status **Publicado** podem ser compartilhados.

#### Compartilhar pacotes de vários objetos {#multi-object-packages}

Para compartilhar um pacote de vários objetos com uma organização parceira aprovada, navegue até a guia [!UICONTROL Sandboxes] **[!UICONTROL Pacotes]**. Em seguida, selecione as reticências (`...`) ao lado do pacote e selecione **[!UICONTROL Compartilhar pacote]** no menu suspenso.

![Lista de pacotes mostrando o menu suspenso com a opção Compartilhar pacote realçada.](../images/ui/sandbox-tooling/private-share-package.png)

Na caixa de diálogo **[!UICONTROL Compartilhar pacote]**, selecione as organizações com as quais compartilhar o pacote na lista suspensa **[!UICONTROL Configurações de compartilhamento]** e selecione **[!UICONTROL Confirmar]**.

>[!TIP]
>
>É possível selecionar mais de uma organização. As organizações selecionadas aparecerão abaixo da lista suspensa [!UICONTROL Configurações de compartilhamento].

![Caixa de diálogo Compartilhar pacote com as configurações de compartilhamento e Confirmar realçada.](../images/ui/sandbox-tooling/private-share-package-confirm.png)

#### Compartilhar pacotes completos de sandbox {#entire-sandbox-packages}

Para compartilhar um pacote inteiro de sandbox com uma organização parceira aprovada, navegue até a guia [!UICONTROL Sandboxes] **[!UICONTROL Pacotes]**. Em seguida, selecione as reticências (`...`) ao lado do pacote e selecione **[!UICONTROL Compartilhar pacote]** no menu suspenso.

![Guia Pacotes mostrando uma lista de pacotes, mostrando o menu suspenso.](../images/ui/sandbox-tooling/private-share-entire-sandbox.png)

Na caixa de diálogo **[!UICONTROL Compartilhar pacote]**, selecione as organizações com as quais compartilhar o pacote na lista suspensa **[!UICONTROL Configurações de compartilhamento]** e selecione **[!UICONTROL Confirmar]**.

>[!TIP]
>
>É possível selecionar mais de uma organização. As organizações selecionadas aparecerão abaixo da lista suspensa [!UICONTROL Configurações de compartilhamento].

![Caixa de diálogo Compartilhar pacote com as configurações de compartilhamento e Confirmar realçada.](../images/ui/sandbox-tooling/private-share-entire-sandbox-confirm.png)


## Pacotes públicos {#public-packages}

Use o recurso Sandbox Tooling para criar pacotes públicos compartilháveis que não exigem aprovação adicional e são facilmente importados com o uso da carga do pacote.

### Atualizar a disponibilidade do pacote para público {#update-package}

Para atualizar o tipo de disponibilidade de um pacote, navegue até a guia [!UICONTROL Sandboxes] **[!UICONTROL Pacotes]**. Em seguida, selecione as reticências (`...`) ao lado do pacote e selecione **[!UICONTROL Atualizar para pacote público]** no menu suspenso.

![A interface de usuário de Sandboxes com a guia Pacotes e o menu suspenso de opções com a opção Atualizar para pacote público realçada.](../images/ui/sandbox-tooling/update-to-public.png)

Na caixa de diálogo **[!UICONTROL Alterar disponibilidade do pacote para público]**, verifique se o nome do pacote está correto e selecione **[!UICONTROL Confirmar]**.

>[!IMPORTANT]
>
> Depois que um pacote é tornado público, ele não pode ser alterado para privado.

![Altere a disponibilidade do pacote para uma caixa de diálogo pública com a opção Confirmar realçada.](../images/ui/sandbox-tooling/change-package-availability.png)

### Compartilhar pacotes usando a carga do pacote

Para compartilhar o pacote público, selecione as reticências (`...`) ao lado do pacote e selecione **[!UICONTROL Copiar carga do pacote]**.

![A interface de Sandboxes mostrando um menu suspenso de pacotes individuais com a carga Copiar pacote realçada.](../images/ui/sandbox-tooling/copy-package-payload.png)

A caixa de diálogo **[!UICONTROL Copiar carga do pacote]** exibe o nome e a carga do pacote. Selecione **[!UICONTROL Copiar carga do pacote]** para copiar a carga associada ao pacote.

![Caixa de diálogo Copiar carga do pacote mostrando a carga JSON com a carga Copiar pacote realçada.](../images/ui/sandbox-tooling/confirm-payload-copy.png)

### Criar um novo pacote usando uma carga de pacote

Para criar um pacote usando uma carga de pacote, navegue até a guia [!UICONTROL Sandboxes] **[!UICONTROL Pacotes]**. Em seguida, selecione **[!UICONTROL Criar pacote]**.

![A interface do usuário de Sandboxes mostrando Criar pacote realçada.](../images/ui/sandbox-tooling/create-package.png)

Na caixa de diálogo **[!UICONTROL Criar pacote]**, selecione a opção para **[!UICONTROL Colar carga do pacote]** e selecione **[!UICONTROL Selecionar]**.

![Criar caixa de diálogo de pacote com carga de pacote de colagem selecionada e Selecionar realçado.](../images/ui/sandbox-tooling/create-package-options.png)

Cole a carga do pacote copiado no campo de texto e selecione **[!UICONTROL Criar]**.

![Caixa de diálogo Criar pacote com o campo de texto vazio e Criar realçado.](../images/ui/sandbox-tooling/paste-payload.png)

Para exibir o status atual da sua solicitação de compartilhamento, navegue até o **[!UICONTROL Status de compartilhamento]**. O status atual da solicitação é mostrado na coluna **[!UICONTROL Status de compartilhamento]**.

![A guia Status de compartilhamento mostrando uma solicitação de carga pendente.](../images/ui/sandbox-tooling/sharing-status.png)

## Próximas etapas {#next-steps}

Este documento demonstrou como usar o recurso de ferramenta Sandbox para compartilhar pacotes em diferentes organizações. Para obter mais informações, consulte o [guia de ferramentas da sandbox](../ui/sandbox-tooling.md).

Para saber como executar operações diferentes usando a API de sandbox, consulte o [guia do desenvolvedor da sandbox](../api/getting-started.md). Para obter uma visão geral de alto nível das sandboxes no Experience Platform, consulte a [documentação de visão geral](../home.md).
