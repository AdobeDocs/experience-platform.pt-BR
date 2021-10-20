---
keywords: Experience Platform, solução de problemas, Data Science Workspace, tópicos populares
solution: Experience Platform
title: Guia de solução de problemas do Data Science Workspace
topic-legacy: Troubleshooting
description: Este documento fornece respostas a perguntas frequentes sobre o Adobe Experience Platform Data Science Workspace.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: ec42d80e695ccf57c10c539ae1b5104c7948c473
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# [!DNL Data Science Workspace] guia de solução de problemas

Este documento fornece respostas a perguntas frequentes sobre o Adobe Experience Platform [!DNL Data Science Workspace]. Para dúvidas e solução de problemas relacionados a [!DNL Platform] Em geral, consulte as APIs [Guia de solução de problemas da API do Adobe Experience Platform](../landing/troubleshooting.md).

## Status de consulta do Bloco de Notas JupyterLab travado no estado de execução

Um notebook JupyterLab pode indicar que uma célula está no estado de execução indefinidamente, em algumas condições de falta de memória. Por exemplo, ao consultar um grande conjunto de dados ou executar várias consultas subsequentes, o Bloco de Notas JupyterLab pode ficar sem memória disponível para armazenar o objeto dataframe resultante. Há alguns indicadores que podem ser vistos nesta situação. Primeiro, o kernel entra no estado inativo mesmo que a célula seja exibida como executada indicado pelo [`*`] ícone ao lado da célula. Além disso, a barra inferior indica a quantidade de RAM usada/disponível.

![RAM disponível](./images/jupyterlab/user-guide/allocate-ram.png)

Durante a leitura de dados, a memória pode aumentar até atingir a quantidade máxima de memória alocada. A memória é liberada assim que a memória máxima é atingida e o kernel é reiniciado. Isso significa que a memória usada neste cenário pode ser mostrada como muito baixa devido à reinicialização do kernel, enquanto logo antes da reinicialização, a memória estaria muito próxima da RAM máxima alocada.

Para resolver esse problema, selecione o ícone de engrenagem na parte superior direita de JupyterLab e deslize o controle deslizante para a direita seguido por selecionar **[!UICONTROL Atualizar configurações]** para alocar mais RAM. Além disso, se você estiver executando várias consultas e o valor da RAM estiver se aproximando do valor máximo alocado, a menos que precise dos resultados de consultas anteriores, reinicie o kernel para redefinir a quantidade disponível de RAM. Isso garante que você tenha a quantidade máxima de RAM disponível para a consulta atual.

![alocar mais ram](./images/jupyterlab/user-guide/notebook-gpu-config.png)

Caso esteja alocando a quantidade máxima de memória (RAM) e ainda tendo esse problema, você pode modificar seu query para operar em um tamanho de conjunto de dados menor, reduzindo as colunas ou o intervalo de dados. Para usar a quantidade total de dados, é recomendável utilizar um notebook Spark.

## [!DNL JupyterLab] o ambiente não está sendo carregado no [!DNL Google Chrome]

>[!IMPORTANT]
>
>Esse problema foi resolvido, mas ainda pode estar presente no navegador Google Chrome 80.x. Verifique se o navegador Chrome está atualizado.

Com o [!DNL Google Chrome] versão 80.x do navegador, todos os cookies de terceiros são bloqueados por padrão. Esta política pode evitar [!DNL JupyterLab] do carregamento no Adobe Experience Platform.

Para solucionar esse problema, siga as etapas abaixo:

Em seu [!DNL Chrome] navegue até o canto superior direito e selecione **Configurações** (como alternativa, você pode copiar e colar &quot;chrome://settings/&quot; na barra de endereços). Em seguida, role até a parte inferior da página e clique no botão **Avançado** lista suspensa.

![chrome avançado](./images/faq/chrome-advanced.png)

O **Privacidade e segurança** é exibida. Em seguida, clique em **Configurações do site** seguida de **Cookies e dados do site**.

![chrome avançado](./images/faq/privacy-security.png)

![chrome avançado](./images/faq/cookies.png)

Por fim, alterne &quot;Bloquear cookies de terceiros&quot; para &quot;DESLIGADO&quot;.

![chrome avançado](./images/faq/toggle-off.png)

>[!NOTE]
>
>Como alternativa, você pode desativar cookies de terceiros e adicionar [*.]ds.adobe.net para a lista de permissões.

Navegue até &quot;chrome://flags/&quot; na barra de endereços. Procure e desative o sinalizador chamado *&quot;Cookies SameSite por padrão&quot;* usando o menu suspenso à direita.

![desativar sinalizador de samesite](./images/faq/samesite-flag.png)

Após a Etapa 2, você será solicitado a reiniciar o navegador. Depois de reiniciar, [!DNL Jupyterlab] deve estar acessível.

## Por que não consigo acessar o [!DNL JupyterLab] no Safari?

O Safari desativa cookies de terceiros por padrão no Safari &lt; 12. Porque seu [!DNL Jupyter] a instância da máquina virtual reside em um domínio diferente de seu quadro pai, no momento, o Adobe Experience Platform exige que os cookies de terceiros sejam habilitados. Ative cookies de terceiros ou mude para um navegador diferente, como [!DNL Google Chrome].

Para o Safari 12, é necessário alternar o Agente de Usuário para &#39;[!DNL Chrome]&#39; ou &#39;[!DNL Firefox]&quot;. Para alternar o Agente do usuário, comece abrindo o *Safari* e selecione **Preferências**. A janela de preferências é exibida.

![Preferências do Safari](./images/faq/preferences.png)

Na janela de preferências do Safari, selecione **Avançado**. Em seguida, verifique a *Mostrar menu Desenvolver na barra de menus* caixa. Você pode fechar a janela de preferências após a conclusão desta etapa.

![Safari avançado](./images/faq/advanced.png)

Em seguida, na barra de navegação superior, selecione o **Desenvolver** menu. No **Desenvolver** lista suspensa, passar o mouse sobre **Agente do usuário**. Você pode selecionar a variável **[!DNL Chrome]** ou **[!DNL Firefox]** Sequência de caracteres do Agente do usuário que você deseja usar.

![Menu Desenvolver](./images/faq/user-agent.png)

## Por que estou vendo uma mensagem &quot;403 Proibido&quot; ao tentar fazer upload ou excluir um arquivo em [!DNL JupyterLab]?

Se seu navegador estiver habilitado com software de bloqueio de anúncios, como [!DNL Ghostery] ou [!DNL AdBlock] Além disso, o domínio &quot;\*.adobe.net&quot; deve ser permitido em cada software de bloqueio de anúncios para [!DNL JupyterLab] para funcionar normalmente. Isso ocorre porque [!DNL JupyterLab] máquinas virtuais são executadas em um domínio diferente do [!DNL Experience Platform] domínio.

## Por que fazer algumas partes da minha [!DNL Jupyter Notebook] parece confuso ou não é renderizado como código?

Isso pode acontecer se a célula em questão for acidentalmente alterada de &quot;Código&quot; para &quot;Markdown&quot;. Enquanto uma célula de código está focada, pressionando a combinação de teclas **ESC+M** altera o tipo da célula para Markdown. O tipo de célula pode ser alterado pelo indicador suspenso na parte superior do bloco de anotações para a(s) célula(s) selecionada(s). Para alterar um tipo de célula para código, comece selecionando a célula que deseja alterar. Em seguida, clique na lista suspensa que indica o tipo atual da célula e selecione &quot;Código&quot;.

![](./images/faq/code_type.png)

## Como instalar o [!DNL Python] bibliotecas?

O [!DNL Python] o kernel vem pré-instalado com muitas bibliotecas populares de aprendizado de máquina. No entanto, é possível instalar bibliotecas personalizadas adicionais executando o seguinte comando em uma célula de código:

```shell
!pip install {LIBRARY_NAME}
```

Para obter uma lista completa de pré-instalados [!DNL Python] bibliotecas, consulte as [seção de apêndice do Guia do Usuário do JupyterLab](./jupyterlab/overview.md#supported-libraries).

## Posso instalar bibliotecas PySpark personalizadas?

Infelizmente, não é possível instalar bibliotecas adicionais para o kernel do PySpark. No entanto, você pode entrar em contato com o representante do serviço de atendimento ao cliente do Adobe para ter bibliotecas PySpark personalizadas instaladas para você.

Para obter uma lista de bibliotecas PySpark pré-instaladas, consulte o [seção de apêndice do Guia do Usuário do JupyterLab](./jupyterlab/overview.md#supported-libraries).

## É possível configurar [!DNL Spark] recursos de cluster para [!DNL JupyterLab] [!DNL Spark] ou kernel PySpark?

Você pode configurar recursos adicionando o seguinte bloco à primeira célula do seu bloco de anotações:

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

Para obter mais informações sobre [!DNL Spark] configuração de recursos do cluster, incluindo a lista completa de propriedades configuráveis, consulte o [Guia do usuário do JupyterLab](./jupyterlab/overview.md#kernels).

## Por que estou recebendo um erro ao tentar executar determinadas tarefas para conjuntos de dados maiores?

Se você estiver recebendo um erro com um motivo como `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` Isso normalmente significa que o driver ou um executor está ficando sem memória. Veja os notebooks JupyterLab [acesso aos dados](./jupyterlab/access-notebook-data.md) documentação para obter mais informações sobre limites de dados e como executar tarefas em grandes conjuntos de dados. Normalmente, esse erro pode ser resolvido alterando a variável `mode` from `interactive` para `batch`.

Além disso, ao gravar grandes conjuntos de dados do Spark/PySpark, armazenando seus dados em cache (`df.cache()`) antes de executar o código de gravação, o desempenho pode ser consideravelmente melhorado.

<!-- remove this paragraph at a later date once the sdk is updated -->

Se você estiver tendo problemas ao ler dados e estiver aplicando transformações aos dados, tente armazenar seus dados em cache antes das transformações. O armazenamento de dados em cache impede várias leituras na rede. Comece lendo os dados. Em seguida, cache (`df.cache()`) os dados. Por fim, execute suas transformações.

## Por que meus notebooks Spark/PySpark estão demorando tanto para ler e gravar dados?

Se você estiver executando transformações nos dados, como `fit()`, as transformações podem estar sendo executadas várias vezes. Para aumentar o desempenho, armazene os dados em cache usando `df.cache()` antes de executar a `fit()`. Isso garante que as transformações sejam executadas apenas uma única vez e impede várias leituras na rede.

**Ordem recomendada:** Comece lendo os dados. Em seguida, execute transformações seguidas pelo armazenamento em cache (`df.cache()`) os dados. Por fim, execute um `fit()`.

## Por que meus notebooks Spark/PySpark estão falhando na execução?

Se você estiver recebendo um dos seguintes erros:

- Trabalho anulado devido a falha de estágio ... Só é possível compactar RDDs com o mesmo número de elementos em cada partição.
- Cliente RPC remoto desassociado e outros erros de memória.
- Mau desempenho ao ler e gravar conjuntos de dados.

Verifique se você está armazenando os dados em cache (`df.cache()`) antes de gravar os dados. Ao executar código em blocos de notas, usando `df.cache()` antes de uma ação como `fit()` pode melhorar muito o desempenho do notebook. Usando `df.cache()` antes de gravar um conjunto de dados, o garante que as transformações sejam executadas apenas uma única vez em vez de várias vezes.

## [!DNL Docker Hub] restrições de limite no Data Science Workspace

A partir de 20 de novembro de 2020, os limites de taxa para o uso anônimo e gratuito autenticado do Docker Hub entraram em vigor. Anônimo e livre [!DNL Docker Hub] os usuários estão limitados a 100 solicitações de extração de imagem do contêiner a cada seis horas. Se você for afetado por essas alterações, receberá esta mensagem de erro: `ERROR: toomanyrequests: Too Many Requests.` ou `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

No momento, esse limite só afetará sua organização se você estiver tentando criar 100 notebooks para receitas dentro do período de seis horas ou se estiver usando notebooks baseados em Spark no Data Science Workspace que frequentemente estão aumentando e diminuindo. No entanto, isso é improvável, pois o cluster em execução permanece ativo por duas horas antes de ficar inativo. Isso reduz o número de pulsos necessários quando o cluster está ativo. Se você receber qualquer um dos erros acima, será necessário aguardar até que [!DNL Docker] limite é redefinido.

Para obter mais informações sobre [!DNL Docker Hub] limites de taxa, visite o [Documentação do DockerHub](https://www.docker.com/increase-rate-limits). Uma solução para isso está sendo trabalhada e é esperada em uma versão subsequente.
