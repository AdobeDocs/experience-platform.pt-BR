---
keywords: Experience Platform; JupyterLab; Notebooks; Área de trabalho de ciência de dados; tópicos populares; Git; Github
solution: Experience Platform
title: Colabore no JupyterLab usando o Git
type: Tutorial
description: O Git é um sistema de controle de versão distribuído para rastreamento alterações no código-fonte durante o desenvolvimento de software. O Git é pré-instalado na Área de trabalho JupyterLab ambiente.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 1%

---

# Colabore no [!DNL JupyterLab] uso [!DNL Git]

>[!NOTE]
>
>O Área de trabalho de ciência de dados não está mais disponível para compra.
>
>Esta documentação destina-se a clientes existentes com direitos anteriores à Data Science Área de trabalho.

[!DNL Git] é um sistema de controle de versão distribuído para rastreamento alterações no código-fonte durante o desenvolvimento de software. O Git é pré-instalado no [!DNL Data Science Workspace JupyterLab] ambiente.

## Pré-requisitos

>[!NOTE]
>
> O servidor Git que você pretende usar precisa ser acessível através da internet.

O [!DNL Data Science Workspace JupyterLab] ambiente é um ambiente hospedado e não implantado em seu firewall corporativo e, portanto, o servidor Git ao qual você se conecta deve estar acessível a partir da internet pública. Esta pode ser uma repositório pública ou privada no [GitHub](https://github.com/) ou outra instância de um [!DNL Git] servidor que você decidiu se host.

## Conecte-se [!DNL Git] ao [!DNL Data Science Workspace JupyterLab Notebooks] ambiente

Início ao iniciar [!DNL Adobe Experience Platform] e navegar até o [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab) ambiente.

Em seguida [!DNL JupyterLab], selecione **[!UICONTROL Arquivo]** passar o mouse sobre **[!UICONTROL Novo]**. Na lista suspensa exibida, selecione **[!UICONTROL Terminal]**.

![Navegação JupyterLab](../images/jupyterlab/tutorials/open-terminal.png)

Próximo, no *Terminal* navegue até o espaço de trabalho usando o seguinte comando: `cd my-workspace`.

![cd espaço de trabalho](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Para ver uma lista de comandos git disponíveis, emite o comando: `git -help` dentro de seu Terminal.

Próximo, clone os repositório que deseja usar usando o `git clone` comando. Clonar seu projeto usando um `https://` URL ao invés de `ssh://`.

**Exemplo**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clone](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> No solicitar para executar quaisquer operações de gravação (`git push` por exemplo) os seguintes comandos de configuração precisam ser executados a cada nova sessão. Observe também que qualquer prompt de comando de push referentes a um nome de usuário e um senha.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Próximas etapas

Depois de terminar de clonar seu repositório, você pode usar o Git como faria normalmente em sua máquina local para colaborar com outros em notebooks. Para obter mais informações sobre o que você pode fazer, [!DNL JupyterLab]consulte o [[!DNL JupyterLab user guide]](./overview.md).
