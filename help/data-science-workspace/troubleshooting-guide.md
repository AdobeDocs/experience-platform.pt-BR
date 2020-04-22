---
keywords: Experience Platform;troubleshooting;Data Science Workspace;popular topics
solution: Experience Platform
title: Guia de solução de problemas da Data Science Workspace
topic: Troubleshooting
translation-type: tm+mt
source-git-commit: ef7c37438990d3bc42024e7fb106d781a5ebbd12

---


# Guia de solução de problemas da Data Science Workspace

Este documento fornece respostas para perguntas frequentes sobre a Adobe Experience Platform Data Science Workspace. Para perguntas e solução de problemas relacionados às APIs de plataforma em geral, consulte o guia [de solução de problemas da API da plataforma](../landing/troubleshooting.md)Adobe Experience.

## O ambiente JupyterLab não está sendo carregado no Google Chrome

>[!IMPORTANT] Esse problema foi resolvido, mas ainda pode estar presente no navegador Google Chrome 80.x. Verifique se o navegador Chrome está atualizado.

Com o navegador Google Chrome versão 80.x, todos os cookies de terceiros são bloqueados por padrão. Essa política pode impedir que o JupyterLab seja carregado na Adobe Experience Platform.

Para resolver esse problema, use as seguintes etapas:

No navegador Chrome, navegue até o canto superior direito e selecione **Configurações** (como alternativa, você pode copiar e colar &quot;chrome://settings/&quot; na barra de endereços). Em seguida, role até a parte inferior da página e clique na lista suspensa **Avançado** .

![cromo avançado](./images/faq/chrome-advanced.png)

A seção *Privacidade e segurança* é exibida. Em seguida, clique nas configurações **** do site seguidas por **Cookies e dados** do site.

![cromo avançado](./images/faq/privacy-security.png)

![cromo avançado](./images/faq/cookies.png)

Por fim, alterne &quot;Bloquear cookies de terceiros&quot; para &quot;DESLIGADO&quot;.

![cromo avançado](./images/faq/toggle-off.png)

>[!NOTE] Como alternativa, você pode desativar cookies de terceiros e a lista de permissões [*.]ds.adobe.net

Navegue até &quot;chrome://flags/&quot; na barra de endereços. Procure e desative o sinalizador *&quot;SameSite by default cookies&quot;* usando o menu suspenso à direita.

![desabilitar sinalizador de samesite](./images/faq/samesite-flag.png)

Após a Etapa 2, você será solicitado a reiniciar o navegador. Depois de reiniciar, Jupyterlab deve estar acessível.

## Por que não consigo acessar o JupyterLab no Safari?

O Safari desativa cookies de terceiros por padrão no Safari &lt; 12. Como a instância da máquina virtual de Júpiter reside em um domínio diferente do quadro pai, a Adobe Experience Platform exige atualmente que os cookies de terceiros sejam ativados. Ative cookies de terceiros ou mude para um navegador diferente, como o Google Chrome.

Para o Safari 12, é necessário alternar o Agente de Usuário para &#39;Chrome&#39; ou &#39;Firefox&#39;. Para alterar o Agente de usuário, abra o menu *Safari* e selecione **Preferências**. A janela de preferências é exibida.

![Preferências do Safari](./images/faq/preferences.png)

Na janela Preferências do Safari, selecione **Avançado**. Em seguida, marque o menu *Mostrar revelação na caixa da barra* de menus. Você pode fechar a janela de preferências depois que esta etapa for concluída.

![Safari avançado](./images/faq/advanced.png)

Em seguida, na barra de navegação superior, selecione o menu **Desenvolver** . Na lista suspensa *Desenvolver* , passe o mouse sobre o Agente ** do usuário. Você pode selecionar a sequência de caracteres do Agente de Usuário do **Chrome** ou **Firefox** que deseja usar.

![Menu Desenvolver](./images/faq/user-agent.png)

## Por que estou vendo uma mensagem &#39;403 Proibido&#39; ao tentar carregar ou excluir um arquivo no JupyterLab?

Se o seu navegador estiver habilitado com software de bloqueio de anúncios, como o Ghostery ou o AdBlock Plus, o domínio &quot;\*.adobe.net&quot; deverá ser incluído na lista de permissões em cada software de bloqueio de anúncios para que o JupyterLab funcione normalmente. Isso ocorre porque as máquinas virtuais JupyterLab são executadas em um domínio diferente do domínio da plataforma de experiência.

## Por que algumas partes do meu notebook Júpiter parecem embaralhadas ou não são renderizadas como código?

Isso pode acontecer se a célula em questão for acidentalmente alterada de &quot;Código&quot; para &quot;Marcação&quot;. Enquanto uma célula de código está focada, pressionar a combinação de teclas **ESC+M** altera o tipo da célula para Markdown. O tipo de célula pode ser alterado pelo indicador suspenso na parte superior do notebook para as células selecionadas. Para alterar um tipo de célula para código, selecione a célula que deseja alterar. Em seguida, clique na lista suspensa que indica o tipo atual da célula e selecione &quot;Código&quot;.

![](./images/faq/code_type.png)

## Como instalar bibliotecas Python personalizadas?

O kernel Python vem pré-instalado com muitas bibliotecas populares de aprendizado de máquinas. No entanto, é possível instalar bibliotecas personalizadas adicionais executando o seguinte comando em uma célula de código:

```shell
!pip install {LIBRARY_NAME}
```

Para obter uma lista completa das bibliotecas Python pré-instaladas, consulte a seção [apêndice do Guia](./jupyterlab/overview.md#supported-libraries)do Usuário do JupyterLab.

## É possível instalar bibliotecas PySpark personalizadas?

Infelizmente, não é possível instalar bibliotecas adicionais para o kernel do PySpark. No entanto, você pode entrar em contato com seu representante de atendimento ao cliente da Adobe para ter bibliotecas PySpark personalizadas instaladas para você.

Para obter uma lista de bibliotecas PySpark pré-instaladas, consulte a seção [apêndice do Guia](./jupyterlab/overview.md#supported-libraries)do Usuário do JupyterLab.

## É possível configurar os recursos de cluster do Spark para JupyterLab Spark ou para o kernel do PySpark?

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

Para obter mais informações sobre a configuração de recursos de cluster Spark, incluindo a lista completa de propriedades configuráveis, consulte o Guia [do Usuário do](./jupyterlab/overview.md#pyspark-spark-execution-resource)JupyterLab.