---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;Git;Github
solution: Experience Platform
title: Colaborar no JupyterLab usando Git
topic: Tutorial
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 1%

---


# Colaborar no JupyterLab usando Git

O Git é um sistema distribuído de controle de versão para rastrear alterações no código fonte durante o desenvolvimento de software. O Git é pré-instalado no ambiente JupyterLab da Data Science Workspace.

## Pré-requisitos

>[!NOTE]
> O servidor Git que você pretende usar precisa estar acessível pela Internet.

O ambiente JupyterLab da Data Science Workspace é um ambiente hospedado e não implantado em seu firewall corporativo, e, portanto, o servidor Git ao qual você se conecta deve estar acessível na Internet pública. Este pode ser um repositório público ou privado no [GitHub](https://github.com/) ou em outra instância de um servidor Git que você mesmo tenha decidido hospedar.

## Conecte o Git ao ambiente Notebooks JupyterLab da Data Science

Start iniciando [!DNL Adobe Experience Platform] e navegando até o ambiente Notebooks [JupyterLabs](https://platform.adobe.com/notebooks/jupyterLab) .

No JupyterLab, selecione **[!UICONTROL Arquivo]** e passe o mouse sobre **[!UICONTROL Novo]**. Na lista suspensa que é exibida, selecione **[!UICONTROL Terminal]**.

![Navegação no JupyterLab](../images/jupyterlab/tutorials/open-terminal.png)

Em seguida, no *Terminal* , navegue até o seu espaço de trabalho usando o seguinte comando: `cd my-workspace`.

![espaço de trabalho cd](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
> Para ver uma lista de comandos git disponíveis, execute o comando: `git -help` no terminal.

Em seguida, clone o repositório que deseja usar usando o `git clone` comando. Clonar o projeto usando um `https://` URL em vez de `ssh://`.

**Exemplo**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clone](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
> Para executar quaisquer operações de gravação (`git push` por exemplo), os seguintes comandos de configuração precisam ser executados para cada nova sessão. Observe também que qualquer comando push solicita um nome de usuário e senha.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Próximas etapas

Depois de terminar de clonar seu repositório, você pode usar o Git como normalmente usaria em sua máquina local para colaborar com outras pessoas em notebooks. Para obter mais informações sobre o que você pode fazer dentro do JupyterLab, consulte o guia [do usuário do](./overview.md)JupyterLab.
