---
keywords: Experience Platform; JupyterLab; notebooks; Data Science Workspace; tópicos populares; Git; Github
solution: Experience Platform
title: Colaborar no JupyterLab usando Git
topic-legacy: tutorial
type: Tutorial
description: O Git é um sistema distribuído de controle de versão para rastrear alterações no código-fonte durante o desenvolvimento de software. O Git é pré-instalado no ambiente Data Science Workspace JupyterLab.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# Colabore em [!DNL JupyterLab] usando [!DNL Git]

[!DNL Git] O é um sistema distribuído de controle de versão para rastrear alterações no código-fonte durante o desenvolvimento de software. O Git é pré-instalado no ambiente [!DNL Data Science Workspace JupyterLab].

## Pré-requisitos

>[!NOTE]
>
> O servidor Git que você pretende usar precisa ser acessível pela Internet.

O ambiente [!DNL Data Science Workspace JupyterLab] é um ambiente hospedado e não é implantado em seu firewall corporativo, portanto, o servidor Git ao qual você se conecta deve estar acessível na Internet pública. Pode ser um repositório público ou privado em [GitHub](https://github.com/) ou outra instância de um servidor [!DNL Git] que você decidiu hospedar.

## Conecte [!DNL Git] ao ambiente [!DNL Data Science Workspace JupyterLab Notebooks]

Comece iniciando [!DNL Adobe Experience Platform] e navegando até o ambiente [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab).

Em [!DNL JupyterLab], selecione **[!UICONTROL File]** e passe o mouse sobre **[!UICONTROL New]**. Na lista suspensa exibida, selecione **[!UICONTROL Terminal]**.

![Navegação no JupyterLab](../images/jupyterlab/tutorials/open-terminal.png)

Em seguida, no *Terminal* navegue até o espaço de trabalho usando o seguinte comando: `cd my-workspace`.

![espaço de trabalho cd](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Para ver uma lista de comandos git disponíveis, execute o comando: `git -help` no terminal.

Em seguida, clone o repositório que deseja usar usando o comando `git clone`. Clonar seu projeto usando uma URL `https://` em vez de `ssh://`.

**Exemplo**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clone](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Para executar qualquer operação de gravação (`git push` por exemplo), os seguintes comandos de configuração precisam ser executados para cada nova sessão. Observe também que qualquer comando push solicita um nome de usuário e senha.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Próximas etapas

Após terminar de clonar seu repositório, você pode usar o Git normalmente em sua máquina local para colaborar com outras pessoas em notebooks. Para obter mais informações sobre o que você pode fazer em [!DNL JupyterLab], consulte o [[!DNL JupyterLab user guide]](./overview.md).
