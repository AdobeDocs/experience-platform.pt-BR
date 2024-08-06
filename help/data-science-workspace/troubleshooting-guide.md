---
keywords: Experience Platform;solução de problemas;Data Science Workspace;tópicos populares
solution: Experience Platform
title: Guia de solução de problemas do data science Área de trabalho
description: Esta documento fornece respostas a perguntas frequentes sobre Adobe Experience Platform Área de trabalho de Ciência de Dados.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 0%

---

# [!DNL Data Science Workspace] guia de solução de problemas

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

Este documento fornece respostas a perguntas frequentes sobre o Adobe Experience Platform [!DNL Data Science Workspace]. Para perguntas e soluções de problemas relacionadas às APIs do [!DNL Platform] em geral, consulte o [guia de solução de problemas da API do Adobe Experience Platform](../landing/troubleshooting.md).

## O status de consulta do JupyterLab Notebook está preso no estado de execução

Um JupyterLab Notebook pode indicar que uma célula está no estado de execução, indefinidamente, em algumas condições de memória insuficiente. Por exemplo, ao consultar um grande conjunto de dados ou executar várias consultas subsequentes, o JupyterLab Notebook pode ficar sem memória disponível para armazenar o objeto de quadro de dados resultante. Há alguns indicadores que podem ser vistos nesta situação. Primeiro, o kernel entra no estado ocioso, mesmo que a célula seja exibida como em execução, indicado pelo ícone [`*`] ao lado da célula. Além disso, a barra inferior indica a quantidade de RAM usada/disponível.

![RAM disponível](./images/jupyterlab/user-guide/allocate-ram.png)

Durante a leitura dos dados, a memória pode aumentar até atingir a quantidade máxima de memória alocada. A memória é liberada assim que a memória máxima é atingida e o kernel é reiniciado. Isso significa que a memória usada nesse cenário pode parecer muito baixa devido à reinicialização do kernel, enquanto que, pouco antes da reinicialização, a memória estaria muito próxima do máximo de RAM alocado.

Para resolver esse problema, selecione o ícone de engrenagem na parte superior direita do JupyterLab e slide o controle deslizante à direita, seguido pela seleção de **[!UICONTROL configurações]** de atualização para alocar mais RAM. Além disso, se você estiver executando várias consultas e seu valor de RAM estiver próximo do valor máximo alocado, a menos que precise dos resultados de consultas anteriores, reinicie o kernel para redefinir a quantidade disponível de RAM. Isso garante que você tenha a quantidade máxima de RAM disponível para a query atual.

![alocar mais ram](./images/jupyterlab/user-guide/notebook-gpu-config.png)

No evento você está alocando a quantidade máxima de memória (RAM) e ainda encontrando esse problema, você pode modificar seus query para operar em um tamanho de conjunto de dados menor, reduzindo as colunas ou o intervalo de dados. Para usar toda a quantidade de dados, recomenda-se usar um notebook Spark.

## O ambiente [!DNL JupyterLab] não está carregando em [!DNL Google Chrome]

>[!IMPORTANT]
>
>Esse problema foi resolvido, mas ainda pode estar presente no navegador Google Chrome 80.x. Certifique-se de que seu navegador Chrome esteja atualizado.

Com a versão 80.x do navegador [!DNL Google Chrome], todos os cookies de terceiros são bloqueados por padrão. Esta política pode impedir o carregamento de [!DNL JupyterLab] no Adobe Experience Platform.

Para solucionar esse problema, siga as etapas abaixo:

No navegador [!DNL Chrome], navegue até o canto superior direito e selecione **Configurações** (como alternativa, você pode copiar e colar &quot;chrome://settings/&quot; na barra de endereços). Em seguida, role até a parte inferior da página e clique na lista suspensa **Avançado**.

![cromo avançado](./images/faq/chrome-advanced.png)

A seção **Privacidade e segurança** é exibida. Em seguida, clique em **Configurações do site** seguido por **Cookies e dados do site**.

![cromo avançado](./images/faq/privacy-security.png)

![cromo avançado](./images/faq/cookies.png)

Por fim, alterne &quot;Bloquear cookies de terceiros&quot; para &quot;DESATIVADO&quot;.

![cromo avançado](./images/faq/toggle-off.png)

>[!NOTE]
>
>Como alternativa, você pode desativar cookies de terceiros e adicionar [*.]ds.adobe.net para a lista de permissões.

Navegue até &quot;chrome://flags/&quot; na barra de endereços. Procure e desabilite o sinalizador *&quot;Cookies SameSite por padrão&quot;* usando o menu suspenso à direita.

![desabilitar sinalizador samesite](./images/faq/samesite-flag.png)

Após a Etapa 2, você será solicitado a reiniciar o navegador. Depois de reiniciar, [!DNL Jupyterlab] deve estar acessível.

## Por que não consigo acessar o [!DNL JupyterLab] no Safari?

O Safari desativa cookies de terceiros por padrão no Safari &lt; 12. Como a instância da máquina virtual [!DNL Jupyter] reside em um domínio diferente do quadro pai, o Adobe Experience Platform exige que os cookies de terceiros estejam habilitados. Habilite cookies de terceiros ou mude para um navegador diferente, como o [!DNL Google Chrome].

Para o Safari 12, você precisa alternar seu Agente do Usuário para &#39;[!DNL Chrome]&#39; ou &#39;[!DNL Firefox]&#39;. Para trocar o Agente do Usuário, comece abrindo o menu do *Safari* e selecione **Preferências**. A janela Preferências é exibida.

![Preferências do Safari](./images/faq/preferences.png)

Na janela de preferências do Safari, selecione **Avançado**. Em seguida, marque o *menu Exibir Desenvolver na caixa da barra de* menus. Você pode fechar a janela de preferências após a conclusão desta etapa.

![Safari avançado](./images/faq/advanced.png)

Próximo, na barra de navegação superior, selecione o **menu Desenvolver** . Na lista suspensa Desenvolver **, passe o mouse sobre** o **Agente** do usuário. Você pode selecionar a cadeia de caracteres Agente do Usuário **[!DNL Chrome]** ou **[!DNL Firefox]** que deseja usar.

![Menu Desenvolver](./images/faq/user-agent.png)

## Por que vejo uma mensagem &#39;403 Proibido&#39; ao tentar carregar ou excluir um arquivo em [!DNL JupyterLab]?

Se o seu navegador estiver habilitado com software de bloqueio de anúncios como o [!DNL Ghostery] ou o [!DNL AdBlock] Plus, o domínio &quot;\*.adobe.net&quot; deverá ser permitido em cada software de bloqueio de anúncios para que o [!DNL JupyterLab] funcione normalmente. Isso ocorre porque [!DNL JupyterLab] máquinas virtuais são executadas em um domínio diferente do [!DNL Experience Platform].

## Por que algumas partes do meu [!DNL Jupyter Notebook] parecem embaralhadas ou não são renderizadas como código?

Isso pode acontecer se a célula em questão for alterada acidentalmente de &quot;Código&quot; para &quot;Markdown&quot;. Enquanto uma célula de código é focalizada, pressionar a combinação de teclas **ESC+M** altera o tipo de célula para Markdown. O tipo de uma célula pode ser alterado pelo indicador suspenso na parte superior do bloco de anotações para a(s) célula(s) selecionada(s). Para alterar um tipo de célula para código, comece selecionando a célula que deseja alterar. Em seguida, clique na lista suspensa que indica o tipo atual da célula e selecione &quot;Código&quot;.

![](./images/faq/code_type.png)

## Como instalar bibliotecas [!DNL Python] personalizadas?

O kernel [!DNL Python] vem pré-instalado com muitas bibliotecas populares de aprendizado de máquina. No entanto, você pode instalar bibliotecas personalizadas adicionais executando o seguinte comando em uma célula de código:

```shell
!pip install {LIBRARY_NAME}
```

Para obter uma lista completa das bibliotecas [!DNL Python] pré-instaladas, consulte a seção [apêndice do Guia do Usuário do JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Posso instalar bibliotecas personalizadas do PySpark?

Infelizmente, você não pode instalar bibliotecas adicionais para o espaço do PySpark. Entretanto, você pode entrar em contato com o representante de atendimento ao cliente da Adobe para obter bibliotecas personalizadas do PySpark instaladas para você.

Para uma lista de bibliotecas pré-instalado do PySpark, consulte a [seção apêndice do Guia do Usuário](./jupyterlab/overview.md#supported-libraries) JupyterLab.

## É possível configurar [!DNL Spark] recursos de cluster para [!DNL JupyterLab] [!DNL Spark] o espaço do PySpark ou do PySpark?

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

Para obter mais informações sobre a configuração de recursos de cluster [!DNL Spark], incluindo a lista completa de propriedades configuráveis, consulte o [Guia do Usuário do JupyterLab](./jupyterlab/overview.md#kernels).

## Por que estou recebendo um erro ao tentar executar determinadas tarefas para conjuntos de dados maiores?

Se você estiver recebendo um erro com uma razão como `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` Isso normalmente significa que o driver ou um executor está ficando sem memória. Consulte a documentação do JupyterLab Notebooks [acesso aos dados](./jupyterlab/access-notebook-data.md) para obter mais informações sobre limites de dados e como executar tarefas em conjuntos de dados grandes. Normalmente, este erro pode ser resolvido alterando-se o `mode` de `interactive` para `batch`.

Além disso, ao gravar grandes conjuntos de dados do Spark/PySpark, o armazenamento em cache de seus dados (`df.cache()`) antes da execução do código de gravação pode melhorar muito o desempenho.

<!-- remove this paragraph at a later date once the sdk is updated -->

Se estiver tendo problemas ao ler dados e estiver aplicando transformações aos dados, tente armazenar os dados em cache antes das transformações. O armazenamento em cache de seus dados impede várias leituras na rede. Comece lendo os dados. Em seguida, armazene em cache (`df.cache()`) os dados. Por fim, execute uma das transformações.

## Por que meus notebooks Spark/PySpark estão demorando tanto para ler e gravar dados?

Se você estiver executando transformações nos dados, por exemplo, usando o `fit()`, as transformações poderão ser executadas várias vezes. Para aumentar o desempenho, armazene seus dados em cache usando o `df.cache()` antes de executar o `fit()`. Isso garante que as transformações sejam executadas apenas uma única vez e impeça várias leituras na rede.

**Solicitar recomendado:** Início lendo os dados. Próximo, realize transformações seguidas de armazenamento em cache (`df.cache()`) os dados. Por fim, execute um `fit()`.

## Por que meus cadernos Spark/PySpark não estão sendo executados?

Se você estiver recebendo qualquer um dos seguintes erros:

- Tarefa abortada devido à falha estágio... Só é possível compactar RDDs com o mesmo número de elementos em cada partição.
- Cliente RPC remoto desassociado e outros erros de memória.
- Desempenho insatisfatório ao ler e gravar conjuntos de dados.

Verifique se você está armazenando os dados em cache (`df.cache()`) antes de gravar os dados. Ao executar código em blocos de anotações, usar `df.cache()` antes de uma ação como `fit()` pode melhorar muito o desempenho do bloco de anotações. Usar `df.cache()` antes de gravar um conjunto de dados garante que as transformações sejam executadas apenas uma vez, em vez de várias vezes.

## [!DNL Docker Hub] restrições de limite no Data Science Workspace

A partir de 20 de novembro de 2020, os limites de taxa para o uso anônimo e autenticado gratuito do Docker Hub entraram em vigor. Usuários [!DNL Docker Hub] anônimos e gratuitos estão limitados a 100 solicitações de pull de imagem de contêiner a cada seis horas. Se você for afetado por essas alterações, receberá esta mensagem de erro: `ERROR: toomanyrequests: Too Many Requests.` ou `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

Atualmente, esse limite só afetará sua organização se você estiver tentando criar 100 notebooks para receitas dentro do período de seis horas ou se estiver usando notebooks baseados no Spark no Data Science Workspace que estão sendo escalonados com frequência para cima e para baixo. No entanto, isso é improvável, pois o cluster no qual eles são executados permanece ativo por duas horas antes de ficar ocioso. Isso reduz o número de extrações necessárias quando o cluster está ativo. Se você receber qualquer um dos erros acima, será necessário aguardar até que o limite [!DNL Docker] seja redefinido.

Para obter mais informações sobre limites de taxa de [!DNL Docker Hub], visite a [documentação do DockerHub](https://www.docker.com/increase-rate-limits). Uma solução para isso está sendo trabalhada e esperada em uma versão subsequente.
