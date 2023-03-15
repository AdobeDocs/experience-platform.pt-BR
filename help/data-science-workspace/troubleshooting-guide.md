---
keywords: Experience Platform;solução de problemas;Data Science Workspace;tópicos populares
solution: Experience Platform
title: Guia de solução de problemas do Data Science Workspace
description: Este documento fornece respostas a perguntas frequentes sobre o Espaço de trabalho de ciência de dados da Adobe Experience Platform.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# [!DNL Data Science Workspace] guia de solução de problemas

Este documento fornece respostas a perguntas frequentes sobre o Adobe Experience Platform [!DNL Data Science Workspace]. Para perguntas e solução de problemas relacionados a [!DNL Platform] APIs em geral, consulte a [Guia de solução de problemas da API do Adobe Experience Platform](../landing/troubleshooting.md).

## O status de consulta do JupyterLab Notebook está preso no estado de execução

Um JupyterLab Notebook pode indicar que uma célula está no estado de execução, indefinidamente, em algumas condições de memória insuficiente. Por exemplo, ao consultar um grande conjunto de dados ou executar várias consultas subsequentes, o JupyterLab Notebook pode ficar sem memória disponível para armazenar o objeto de quadro de dados resultante. Há alguns indicadores que podem ser vistos nesta situação. Primeiro, o kernel entra no estado ocioso mesmo que a célula apareça como executável indicado pelo [`*`] ícone ao lado da célula. Além disso, a barra inferior indica a quantidade de RAM usada/disponível.

![RAM disponível](./images/jupyterlab/user-guide/allocate-ram.png)

Durante a leitura dos dados, a memória pode aumentar até atingir a quantidade máxima de memória alocada. A memória é liberada assim que a memória máxima é atingida e o kernel é reiniciado. Isso significa que a memória usada nesse cenário pode parecer muito baixa devido à reinicialização do kernel, enquanto que, pouco antes da reinicialização, a memória estaria muito próxima do máximo de RAM alocado.

Para resolver esse problema, selecione o ícone de engrenagem na parte superior direita do JupyterLab e deslize o controle deslizante para a direita, seguido pela seleção **[!UICONTROL Atualizar configurações]** para alocar mais RAM. Além disso, se você estiver executando várias consultas e seu valor de RAM estiver se aproximando da quantidade máxima alocada, a menos que você precise dos resultados de consultas anteriores, reinicie o kernel para redefinir a quantidade disponível de RAM. Isso garante que você tenha a quantidade máxima de RAM disponível para a consulta atual.

![alocar mais ram](./images/jupyterlab/user-guide/notebook-gpu-config.png)

Caso esteja alocando a quantidade máxima de memória (RAM) e ainda encontre esse problema, você poderá modificar seu query para operar em um tamanho de conjunto de dados menor, reduzindo as colunas ou o intervalo de dados. Para usar a quantidade total de dados, é recomendável usar um notebook Spark.

## [!DNL JupyterLab] o ambiente não está carregando no [!DNL Google Chrome]

>[!IMPORTANT]
>
>Esse problema foi resolvido, mas ainda pode estar presente no navegador Google Chrome 80.x. Verifique se o navegador Chrome está atualizado.

Com o [!DNL Google Chrome] navegador versão 80.x, todos os cookies de terceiros são bloqueados por padrão. Essa política pode impedir [!DNL JupyterLab] do carregamento no Adobe Experience Platform.

Para solucionar esse problema, siga as etapas abaixo:

No seu [!DNL Chrome] navegue até o canto superior direito e selecione **Configurações** (como alternativa, você pode copiar e colar &quot;chrome://settings/&quot; na barra de endereços). Em seguida, role até a parte inferior da página e clique no botão **Avançado** lista suspensa.

![chrome avançado](./images/faq/chrome-advanced.png)

A variável **Privacidade e segurança** é exibida. Clique em **Configurações do site** seguido por **Cookies e dados do site**.

![chrome avançado](./images/faq/privacy-security.png)

![chrome avançado](./images/faq/cookies.png)

Por fim, alterne &quot;Bloquear cookies de terceiros&quot; para &quot;DESATIVADO&quot;.

![chrome avançado](./images/faq/toggle-off.png)

>[!NOTE]
>
>Como alternativa, você pode desativar cookies de terceiros e adicionar [*.]ds.adobe.net para a lista de permissões.

Navegue até &quot;chrome://flags/&quot; na barra de endereços. Procure e desative o sinalizador intitulado *&quot;Cookies SameSite por padrão&quot;* usando o menu suspenso à direita.

![desativar sinalizador samesite](./images/faq/samesite-flag.png)

Após a Etapa 2, você será solicitado a reiniciar o navegador. Depois de reiniciar, [!DNL Jupyterlab] devem estar acessíveis.

## Por que não consigo acessar o [!DNL JupyterLab] no Safari?

O Safari desativa cookies de terceiros por padrão no Safari &lt; 12. Porque o seu [!DNL Jupyter] a instância da máquina virtual reside em um domínio diferente de seu quadro principal. no momento, o Adobe Experience Platform exige que os cookies de terceiros estejam ativados. Ative cookies de terceiros ou alterne para um navegador diferente, como [!DNL Google Chrome].

Para o Safari 12, é necessário alternar o Agente do usuário para &#39;[!DNL Chrome]&#39; ou &#39;[!DNL Firefox]&#39;. Para trocar o agente do usuário, comece abrindo o *Safari* e selecione **Preferências**. A janela Preferências é exibida.

![Preferências do Safari](./images/faq/preferences.png)

Na janela Preferências do Safari, selecione **Avançado**. Verifique a *Mostrar menu Desenvolver na barra de menus* caixa. Você poderá fechar a janela de preferências depois que esta etapa estiver concluída.

![Safari avançado](./images/faq/advanced.png)

Em seguida, na barra de navegação superior, selecione a **Desenvolver** menu. De dentro do **Desenvolver** lista suspensa, passe o mouse sobre **Agente do usuário**. É possível selecionar a variável **[!DNL Chrome]** ou **[!DNL Firefox]** Sequência de agente do usuário que você deseja usar.

![Menu Desenvolver](./images/faq/user-agent.png)

## Por que vejo uma mensagem de &quot;403 proibido&quot; ao tentar fazer upload ou excluir um arquivo no [!DNL JupyterLab]?

Se o navegador estiver habilitado com software de bloqueio de anúncios, como [!DNL Ghostery] ou [!DNL AdBlock] Além disso, o domínio &quot;\*.adobe.net&quot; deve ser permitido em cada software de bloqueio de anúncios para [!DNL JupyterLab] para funcionar normalmente. Isso ocorre porque [!DNL JupyterLab] as máquinas virtuais são executadas em um domínio diferente do [!DNL Experience Platform] domínio.

## Por que algumas partes do meu [!DNL Jupyter Notebook] parecer embaralhado ou não renderizar como código?

Isso pode acontecer se a célula em questão for alterada acidentalmente de &quot;Código&quot; para &quot;Markdown&quot;. Enquanto uma célula de código está focalizada, pressionar a combinação de teclas **ESC+M** altera o tipo de célula para Markdown. O tipo de uma célula pode ser alterado pelo indicador suspenso na parte superior do bloco de anotações para a(s) célula(s) selecionada(s). Para alterar um tipo de célula para código, comece selecionando a célula que deseja alterar. Em seguida, clique na lista suspensa que indica o tipo atual da célula e selecione &quot;Código&quot;.

![](./images/faq/code_type.png)

## Como instalar o personalizado [!DNL Python] bibliotecas?

A variável [!DNL Python] o kernel vem pré-instalado com muitas bibliotecas populares de aprendizado de máquina. No entanto, você pode instalar bibliotecas personalizadas adicionais executando o seguinte comando em uma célula de código:

```shell
!pip install {LIBRARY_NAME}
```

Para obter uma lista completa das versões [!DNL Python] bibliotecas, consulte a seção [seção de apêndice do Guia do usuário do JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Posso instalar bibliotecas personalizadas do PySpark?

Infelizmente, você não pode instalar bibliotecas adicionais para o kernel do PySpark. Entretanto, você pode entrar em contato com o representante de atendimento ao cliente da Adobe para obter bibliotecas personalizadas do PySpark instaladas para você.

Para obter uma lista de bibliotecas PySpark pré-instaladas, consulte o [seção de apêndice do Guia do usuário do JupyterLab](./jupyterlab/overview.md#supported-libraries).

## É possível configurar [!DNL Spark] recursos de cluster para [!DNL JupyterLab] [!DNL Spark] ou kernel PySpark?

Você pode configurar recursos adicionando o seguinte bloco à primeira célula do bloco de anotações:

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

Para obter mais informações sobre [!DNL Spark] configuração de recursos de cluster, incluindo a lista completa de propriedades configuráveis, consulte [Guia do usuário do JupyterLab](./jupyterlab/overview.md#kernels).

## Por que estou recebendo um erro ao tentar executar determinadas tarefas para conjuntos de dados maiores?

Se você estiver recebendo um erro com um motivo como `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` Normalmente, isso significa que o driver ou um executor está ficando sem memória. Veja os notebooks JupyterLab [acesso aos dados](./jupyterlab/access-notebook-data.md) documentação para obter mais informações sobre limites de dados e como executar tarefas em conjuntos de dados grandes. Normalmente, esse erro pode ser resolvido alterando o `mode` de `interactive` para `batch`.

Além disso, ao gravar grandes conjuntos de dados do Spark/PySpark, armazenar seus dados em cache (`df.cache()`) antes de executar o código de gravação pode melhorar muito o desempenho.

<!-- remove this paragraph at a later date once the sdk is updated -->

Se estiver tendo problemas ao ler dados e estiver aplicando transformações aos dados, tente armazenar os dados em cache antes das transformações. O armazenamento em cache de seus dados impede várias leituras na rede. Comece lendo os dados. Em seguida, o cache (`df.cache()`) os dados. Por fim, execute uma das transformações.

## Por que meus notebooks Spark/PySpark estão demorando tanto para ler e gravar dados?

Se você estiver executando transformações nos dados, como usando `fit()`, as transformações podem ser executadas várias vezes. Para aumentar o desempenho, armazene seus dados em cache usando o `df.cache()` antes de executar a `fit()`. Isso garante que as transformações sejam executadas apenas uma vez e impede várias leituras na rede.

**Ordem recomendada:** Comece lendo os dados. Em seguida, execute as transformações seguidas de armazenamento em cache (`df.cache()`) os dados. Por último, execute uma `fit()`.

## Por que meus notebooks Spark/PySpark não estão sendo executados?

Se você estiver recebendo algum dos seguintes erros:

- Trabalho anulado devido a falha no estágio... Só é possível compactar RDDs com o mesmo número de elementos em cada partição.
- Cliente RPC remoto desassociado e outros erros de memória.
- Desempenho insatisfatório ao ler e gravar conjuntos de dados.

Verifique se os dados estão sendo armazenados em cache (`df.cache()`) antes de gravar os dados. Ao executar código em blocos de anotações, usando `df.cache()` antes de uma ação como `fit()` pode melhorar muito o desempenho do notebook. Usar `df.cache()` antes de gravar um conjunto de dados, garante que as transformações sejam executadas apenas uma vez, em vez de várias vezes.

## [!DNL Docker Hub] restrições de limite no Espaço de trabalho de ciência de dados

A partir de 20 de novembro de 2020, os limites de taxa para o uso anônimo e autenticado gratuito do Docker Hub entraram em vigor. Anônimo e gratuito [!DNL Docker Hub] Os usuários do são limitados a 100 solicitações de pull de imagem de contêiner a cada seis horas. Se for afetado por essas alterações, você receberá esta mensagem de erro: `ERROR: toomanyrequests: Too Many Requests.` ou `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

Atualmente, esse limite só afetará sua organização se você estiver tentando criar 100 notebooks para receitas dentro do período de seis horas ou se estiver usando notebooks baseados no Spark no Espaço de trabalho de ciência de dados que estão aumentando e diminuindo com frequência. No entanto, isso é improvável, pois o cluster no qual eles são executados permanece ativo por duas horas antes de ficar ocioso. Isso reduz o número de extrações necessárias quando o cluster está ativo. Se você receber qualquer um dos erros acima, será necessário aguardar até que seu [!DNL Docker] o limite é redefinido.

Para obter mais informações sobre [!DNL Docker Hub] limites de taxa, visite o [Documentação do DockerHub](https://www.docker.com/increase-rate-limits). Uma solução para isso está sendo trabalhada e esperada em uma versão subsequente.
