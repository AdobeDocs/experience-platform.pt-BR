---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;tópicos populares;Git;Github
solution: Experience Platform
title: Colaborar no JupyterLab usando Git
type: Tutorial
description: O Git é um sistema de controle de versão distribuído para rastrear alterações no código-fonte durante o desenvolvimento de software. O Git é pré-instalado no ambiente JupyterLab do Data Science Workspace.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# Colaborar em [!DNL JupyterLab] usar [!DNL Git]

[!DNL Git] O é um sistema de controle de versão distribuído para rastrear alterações no código-fonte durante o desenvolvimento de software. O Git é pré-instalado no [!DNL Data Science Workspace JupyterLab] ambiente.

## Pré-requisitos

>[!NOTE]
>
> O servidor Git que você pretende usar precisa estar acessível pela Internet.

A variável [!DNL Data Science Workspace JupyterLab] O ambiente é um ambiente hospedado e não é implantado no firewall corporativo. Portanto, o servidor Git ao qual você se conecta deve ser acessível pela internet pública. Pode ser um repositório público ou privado no [GitHub](https://github.com/) ou outra instância de um [!DNL Git] servidor que você decidiu hospedar.

## Conectar [!DNL Git] para o [!DNL Data Science Workspace JupyterLab Notebooks] ambiente

Comece iniciando [!DNL Adobe Experience Platform] e navegue até o [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab) ambiente.

Dentro de [!DNL JupyterLab], selecione **[!UICONTROL Arquivo]** em seguida, passe o mouse sobre **[!UICONTROL Novo]**. Na lista suspensa exibida, selecione **[!UICONTROL Terminal]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

Em seguida, em *Terminal* navegue até o espaço de trabalho usando o seguinte comando: `cd my-workspace`.

![espaço de trabalho do cd](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Para ver uma lista de comandos Git disponíveis, execute o comando: `git -help` no terminal.

Em seguida, clone o repositório que deseja usar usando o `git clone` comando. Clonar o projeto usando um `https://` URL em vez de `ssh://`.

**Exemplo**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clone](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Para executar operações de gravação (`git push` por exemplo) os seguintes comandos de configuração precisam ser executados para cada nova sessão. Observe também que qualquer comando push solicita um nome de usuário e senha.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Próximas etapas

Após concluir a clonagem do repositório, você pode usar o Git da maneira normal em seu computador local para colaborar com outras pessoas nos blocos de anotações. Para obter mais informações sobre o que você pode fazer dentro do [!DNL JupyterLab], consulte o [[!DNL JupyterLab user guide]](./overview.md).
