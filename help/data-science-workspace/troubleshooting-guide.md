---
keywords: Experience Platform;solução de problemas;Data Science Workspace;topics;;troubleshooting;Data Science Workspace;popular topics
solution: Experience Platform
title: Guia de solução de problemas da Data Science Workspace
topic: Troubleshooting
description: Este documento fornece respostas para perguntas frequentes sobre a Adobe Experience Platform Data Science Workspace.
translation-type: tm+mt
source-git-commit: 10ccccf72ff7a2fd726066332b9771dff1929af6
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 0%

---


# [!DNL Data Science Workspace] guia de solução de problemas

Este documento fornece respostas para perguntas frequentes sobre o Adobe Experience Platform [!DNL Data Science Workspace]. Para perguntas e solução de problemas relacionados às [!DNL Platform] APIs em geral, consulte o [Guia de solução de problemas da API da Adobe Experience Platform](../landing/troubleshooting.md).

## [!DNL JupyterLab] O ambiente não está sendo carregado em  [!DNL Google Chrome]

>[!IMPORTANT]
>
>Esse problema foi resolvido, mas ainda pode estar presente no navegador Google Chrome 80.x. Verifique se o navegador Chrome está atualizado.

Com a versão 80.x do navegador [!DNL Google Chrome], todos os cookies de terceiros são bloqueados por padrão. Essa política pode impedir que [!DNL JupyterLab] seja carregado no Adobe Experience Platform.

Para resolver esse problema, use as seguintes etapas:

No navegador [!DNL Chrome], navegue até o canto superior direito e selecione **Configurações** (como alternativa, você pode copiar e colar &quot;chrome://settings/&quot; na barra de endereços). Em seguida, role até a parte inferior da página e clique na lista suspensa **Avançado**.

![cromo avançado](./images/faq/chrome-advanced.png)

A seção **Privacidade e segurança** é exibida. Em seguida, clique em **Configurações do site**, seguido por **Cookies e dados do site**.

![cromo avançado](./images/faq/privacy-security.png)

![cromo avançado](./images/faq/cookies.png)

Por fim, alterne &quot;Bloquear cookies de terceiros&quot; para &quot;DESLIGADO&quot;.

![cromo avançado](./images/faq/toggle-off.png)

>[!NOTE]
>
>Como alternativa, você pode desativar cookies de terceiros e adicionar [*.]ds.adobe.net para a lista de permissões.

Navegue até &quot;chrome://flags/&quot; na barra de endereços. Procure e desative o sinalizador chamado *&quot;SameSite by default cookies&quot;* usando o menu suspenso à direita.

![desabilitar sinalizador de samesite](./images/faq/samesite-flag.png)

Após a Etapa 2, você será solicitado a reiniciar o navegador. Depois de reiniciar, [!DNL Jupyterlab] deve estar acessível.

## Por que não consigo acessar [!DNL JupyterLab] no Safari?

O Safari desativa cookies de terceiros por padrão no Safari &lt; 12. Como a instância da máquina virtual [!DNL Jupyter] reside em um domínio diferente do quadro pai, a Adobe Experience Platform atualmente exige que os cookies de terceiros sejam ativados. Ative cookies de terceiros ou mude para um navegador diferente, como [!DNL Google Chrome].

Para o Safari 12, é necessário alternar o Agente de Usuário para &#39;[!DNL Chrome]&#39; ou &#39;[!DNL Firefox]&#39;. Para alternar o Agente de Usuário, abra o menu *Safari* e selecione **Preferências**. A janela de preferências é exibida.

![Preferências do Safari](./images/faq/preferences.png)

Na janela Preferências do Safari, selecione **Avançado**. Em seguida, marque a caixa *Mostrar menu Revelação na barra de menus*. Você pode fechar a janela de preferências depois que esta etapa for concluída.

![Safari avançado](./images/faq/advanced.png)

Em seguida, na barra de navegação superior, selecione o menu **Desenvolver**. Na lista suspensa **Desenvolver**, passe o mouse sobre **Agente do usuário**. Você pode selecionar a sequência de caracteres **[!DNL Chrome]** ou **[!DNL Firefox]** do User Agent que deseja usar.

![Menu Desenvolver](./images/faq/user-agent.png)

## Por que estou vendo uma mensagem &#39;403 Proibido&#39; ao tentar carregar ou excluir um arquivo em [!DNL JupyterLab]?

Se o seu navegador estiver habilitado com software de bloqueio de anúncios, como [!DNL Ghostery] ou [!DNL AdBlock] Plus, o domínio &quot;\*.adobe.net&quot; deverá ser permitido em cada software de bloqueio de anúncios para que [!DNL JupyterLab] funcione normalmente. Isso ocorre porque as máquinas virtuais [!DNL JupyterLab] são executadas em um domínio diferente do domínio [!DNL Experience Platform].

## Por que algumas partes do meu [!DNL Jupyter Notebook] parecem embaralhadas ou não são renderizadas como código?

Isso pode acontecer se a célula em questão for acidentalmente alterada de &quot;Código&quot; para &quot;Marcação&quot;. Enquanto uma célula de código está focada, pressionar a combinação de teclas **ESC+M** altera o tipo da célula para Markdown. O tipo de célula pode ser alterado pelo indicador suspenso na parte superior do notebook para as células selecionadas. Para alterar um tipo de célula para código, selecione a célula que deseja alterar. Em seguida, clique na lista suspensa que indica o tipo atual da célula e selecione &quot;Código&quot;.

![](./images/faq/code_type.png)

## Como instalar bibliotecas personalizadas [!DNL Python]?

O kernel [!DNL Python] vem pré-instalado com muitas bibliotecas populares de aprendizado de máquina. No entanto, é possível instalar bibliotecas personalizadas adicionais executando o seguinte comando em uma célula de código:

```shell
!pip install {LIBRARY_NAME}
```

Para obter uma lista completa das bibliotecas [!DNL Python] pré-instaladas, consulte a seção [apêndice do Guia do Usuário do JupyterLab](./jupyterlab/overview.md#supported-libraries).

## É possível instalar bibliotecas PySpark personalizadas?

Infelizmente, não é possível instalar bibliotecas adicionais para o kernel do PySpark. No entanto, você pode entrar em contato com seu representante de atendimento ao cliente do Adobe para ter bibliotecas PySpark personalizadas instaladas para você.

Para obter uma lista de bibliotecas PySpark pré-instaladas, consulte a seção [apêndice do Guia do Usuário do JupyterLab](./jupyterlab/overview.md#supported-libraries).

## É possível configurar [!DNL Spark] recursos de cluster para [!DNL JupyterLab] [!DNL Spark] ou kernel do PySpark?

Você pode configurar recursos adicionando o seguinte bloco à primeira célula do seu notebook:

```python
%%configure -f 
{
    "numExecutors": 10,
    "executorMemory": "8G",
    "executorCores":4,
    "driverMemory":"2G",
    "driverCores":2,
    "conf": {
        "spark.cores.max": "40"
    }
}
```

Para obter mais informações sobre a configuração [!DNL Spark] de recursos de cluster, incluindo a lista completa de propriedades configuráveis, consulte o [Guia do Usuário do JupyterLab](./jupyterlab/overview.md#kernels).

## Por que estou recebendo um erro ao tentar executar certas tarefas para conjuntos de dados maiores?

Se você estiver recebendo um erro com um motivo como `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.`, isso normalmente significa que o driver ou um executor está ficando sem memória. Consulte a documentação Notebooks JupyterLab [acesso aos dados](./jupyterlab/access-notebook-data.md) para obter mais informações sobre limites de dados e como executar tarefas em grandes conjuntos de dados. Normalmente, esse erro pode ser resolvido alterando `mode` de `interactive` para `batch`.

## [!DNL Docker Hub] restrições de limite na Data Science Workspace

A partir de 20 de novembro de 2020, os limites de taxa para o uso autenticado anônimo e gratuito do Docker Hub entraram em vigor. Usuários anônimos e livres [!DNL Docker Hub] estão limitados a 100 solicitações de extração de imagem de container a cada seis horas. Se você for afetado por essas alterações, receberá esta mensagem de erro: `ERROR: toomanyrequests: Too Many Requests.` ou `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

Atualmente, esse limite só afetará sua organização se você estiver tentando criar 100 notebooks para receitas dentro de um período de seis horas ou se estiver usando notebooks baseados no Spark na Data Science Workspace que estão frequentemente aumentando e diminuindo. No entanto, isso é improvável, já que o cluster em execução permanece ativo por duas horas antes de ficar ocioso. Isso reduz o número de extrações necessárias quando o cluster está ativo. Se você receber algum dos erros acima, precisará aguardar até que seu limite [!DNL Docker] seja redefinido.

Para obter mais informações sobre [!DNL Docker Hub] limites de taxa, visite a [documentação do DockerHub](https://www.docker.com/increase-rate-limits). Uma solução para isso está sendo trabalhada e é esperada em uma versão subsequente.