---
title: Visualizador de gráfico de identidade
description: Um gráfico de identidade é um mapa dos relacionamentos entre identidades diferentes para um cliente específico, fornecendo uma representação visual de como o cliente interage com a sua marca em diferentes canais.
exl-id: ccd5f8d8-595b-4636-9191-553214e426bd
source-git-commit: 3fe94be9f50d64fc893b16555ab9373604b62e59
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 5%

---

# Visualizador de gráficos de identidade

Um gráfico de identidade é um mapa dos relacionamentos entre identidades diferentes para um cliente específico, fornecendo uma representação visual de como o cliente interage com a sua marca em diferentes canais. Todos os gráficos de identidade do cliente são gerenciados e atualizados coletivamente pelo Serviço de identidade da Adobe Experience Platform em tempo quase real, em resposta à atividade do cliente.

O visualizador de gráficos de identidade na interface do usuário da Platform permite visualizar e entender melhor quais identidades do cliente são unidas e de que maneiras. O visualizador permite que você arraste e interaja com diferentes partes do gráfico, possibilitando examinar relacionamentos de identidade complexos, depurar com mais eficiência e aproveitar o aumento da transparência com a forma como as informações estão sendo utilizadas.

O documento a seguir fornece etapas sobre como acessar e usar o visualizador de gráficos de identidade na interface do usuário da Platform.

## Tutorial em vídeo

O vídeo a seguir é destinado a fornecer suporte à sua compreensão do visualizador de gráficos de identidade.

>[!VIDEO](https://video.tv.adobe.com/v/331030/?quality=12&learn=on)

## Introdução

Trabalhar com o visualizador de gráficos de identidade requer uma compreensão dos vários serviços da Adobe Experience Platform envolvidos. Antes de começar a trabalhar com o visualizador de gráficos de identidade, revise a documentação dos seguintes serviços:

- [[!DNL Identity Service]](../home.md): obtenha uma melhor visualização dos clientes individuais e do comportamento deles ao unir as identidades de vários dispositivos e sistemas.
- [Perfil do cliente em tempo real](../../profile/home.md): os gráficos de identidade são aproveitados pelo Perfil do cliente em tempo real para criar uma visualização abrangente e singular dos atributos e comportamento do cliente.

### Terminologia

- **Identidade (nó):** Uma identidade ou um nó são dados exclusivos de uma entidade, normalmente uma pessoa. Uma identidade é composta de um namespace de identidade e um valor de identidade. Por exemplo, uma identidade totalmente qualificada pode consistir em um namespace de identidade para **E-mail**, combinado com um valor de identidade de **robin<span>@email.com**.
- **Link (borda):** Um link ou uma borda representa a conexão entre identidades. Os links de identidade incluem propriedades como carimbos de data e hora estabelecidos pela primeira vez e atualizados pela última vez. O primeiro carimbo de data e hora estabelecido define a data e a hora em que uma nova identidade é vinculada a uma identidade existente. O carimbo de data e hora da última atualização define a data e a hora em que um link de identidade existente foi atualizado pela última vez.
- **Gráfico (cluster):** Um gráfico ou cluster é um grupo de identidades e links que representam uma pessoa.

## Acessar o visualizador de gráficos de identidade {#access-identity-graph-viewer}

Na interface do usuário da Platform, selecione **[!UICONTROL Identidades]** na navegação à esquerda e selecione **[!UICONTROL Gráfico de identidade]** na lista de guias no cabeçalho.

![O espaço de trabalho Identidades na interface do Experience Platform, com a guia Gráfico de identidade selecionada.](../images/graph-viewer/identity-graph.png)

Para exibir um gráfico de identidade, forneça um namespace de identidade e seu valor correspondente e selecione **[!UICONTROL Exibir]**.

>[!TIP]
>
>Selecione o ícone de tabela ![ícone de tabela](../images/identity-graph-viewer/table-icon.png) para ver um painel com uma lista de todos os namespaces de identidade disponíveis em sua organização. Você pode usar qualquer um dos namespaces de identidade, desde que tenha um valor de identidade válido conectado a eles. Para obter mais informações, leia a [guia de namespace de identidade](./namespaces.md).

![Um namespace de identidade e seu valor correspondente, fornecido na tela de pesquisa do Gráfico de identidade.](../images/graph-viewer/namespace-and-value.png)

## Noções básicas sobre a interface do visualizador de gráficos de identidade

A interface do visualizador de gráficos de identidade é composta por vários elementos que você pode usar para interagir e entender melhor seus dados de identidade.

![A interface do visualizador de gráficos de identidade.](../images/graph-viewer/identity-graph-viewer-main.png)

O gráfico de identidade exibe todas as identidades vinculadas à combinação de namespace e valor de identidade inserida. Cada nó consiste em um namespace de identidade e seu valor correspondente. Você pode selecionar, manter pressionado e arrastar qualquer nó para interagir com o gráfico. Como alternativa, você pode passar o mouse sobre um nó para ver informações sobre seu valor de identidade correspondente. Selecionar **[!UICONTROL Exibir gráfico]** para ocultar ou exibir o gráfico.

>[!IMPORTANT]
>
>Um gráfico de identidade exige que pelo menos duas identidades vinculadas sejam geradas e uma combinação válida de namespace e valor de identidade. O número máximo de identidades que o visualizador de gráficos pode exibir é 50. Consulte a [apêndice](#appendix) abaixo para obter mais informações.

![O visualizador de gráficos de identidade com cinco identidades vinculadas.](../images/graph-viewer/graph.png)

Selecione um link no gráfico para ver o conjunto de dados e a ID do lote que contribuem para esse link. Selecionar um link também atualiza o painel direito para fornecer mais informações sobre detalhes da fonte de dados, bem como propriedades como os carimbos de data e hora estabelecidos pela primeira vez e atualizados pela última vez.

![O link de identidade entre o email e os nós GAID selecionados.](../images/graph-viewer/identity-link.png)

A variável [!UICONTROL Identidades] A tabela fornece uma visualização diferente dos dados de identidade, listando o namespace de identidade e a combinação do valor de identidade em um formato tabular. Selecionar um nó no gráfico atualizará o item de linha realçado no [!UICONTROL Identidades] tabela.

![A tabela Identidades com a lista de identidades vinculadas no gráfico.](../images/graph-viewer/identities-table.png)

Use o menu suspenso para classificar os dados do gráfico e destacar informações sobre um namespace de identidade específico. Por exemplo, selecione **[!UICONTROL E-mail]** no menu para exibir dados específicos do namespace de identidade do email.

![A tabela Identidades foi classificada para exibir apenas os dados de email.](../images/graph-viewer/sort-email.png)

O painel direito exibe informações sobre uma identidade selecionada, incluindo seu último carimbo de data e hora atualizado. O painel direito também exibe informações sobre a fonte de dados que corresponde à identidade selecionada, incluindo a ID do lote, o nome do conjunto de dados, a ID do conjunto de dados e o nome do esquema.

A tabela a seguir fornece informações adicionais sobre as propriedades da fonte de dados exibidas no painel direito:

| Fonte de dados | Descrição |
| --- | --- | 
| ID do lote | O identificador gerado automaticamente que corresponde aos dados em lote. |
| ID do conjunto de dados | O identificador gerado automaticamente que corresponde ao seu conjunto de dados. |
| Nome do conjunto de dados | O nome do conjunto de dados que contém os dados em lote. |
| Nome do esquema | O nome do esquema. O esquema fornece um conjunto de regras que representam e validam a estrutura e o formato dos dados. |

![O painel direito, que exibe dados de identidade, bem como a fonte de dados de informações.](../images/graph-viewer/right-rail.png)

Você também pode usar a variável *[!UICONTROL Fonte de dados]* para ver uma lista de fontes de dados que contribuem para suas identidades. Selecionar [!UICONTROL Fonte de dados] para obter uma exibição em tabelas dos seus conjuntos de dados e IDs em lote.

![A guia de fonte de dados selecionada.](../images/graph-viewer/data-source-table.png)

Use o controle deslizante para filtrar os dados do gráfico pela hora em que as identidades foram estabelecidas pela primeira vez. Por padrão, o visualizador de gráficos de identidade exibe todas as identidades vinculadas no gráfico. Segure e arraste o controle deslizante para ajustar a hora até o último carimbo de data e hora em que uma nova identidade foi vinculada ao gráfico. No exemplo abaixo, o gráfico mostra que o link de identidade mais recente (GAID) foi estabelecido em **[!UICONTROL 19/08/2020, 4:29:29 PM]**.

![O controle deslizante do carimbo de data e hora do visualizador de gráficos foi selecionado.](../images/graph-viewer/slider-one.png)

Ajuste o controle deslizante para ver se outro link de identidade (Email) foi estabelecido em **[!UICONTROL 19/08/2020, 4:25:22h]**.

![O controle deslizante do carimbo de data e hora do visualizador de gráfico ajustado para o último novo link estabelecido.](../images/graph-viewer/slider-two.png)

Também é possível ajustar o controle deslizante para ver a iteração mais antiga do gráfico. No exemplo abaixo, o visualizador de gráficos de identidade exibe em que o gráfico foi criado pela primeira vez **[!UICONTROL 19/08/2020, 4:11:16H]**, cujos primeiros links são ECID, Email e Telefone.

![O controle deslizante do carimbo de data e hora do visualizador de gráfico ajustado para o primeiro novo link estabelecido.](../images/graph-viewer/slider-three.png)

## Apêndice

A seção a seguir fornece informações adicionais para trabalhar com o visualizador de gráficos de identidade.

### Noções básicas sobre mensagens de erro

Podem ocorrer erros ao acessar o visualizador de gráficos de identidade. Esta é uma lista de pré-requisitos e limitações que devem ser observados ao trabalhar com o visualizador de gráficos de identidade.

- Um valor de identidade deve existir no namespace selecionado.
- O visualizador de gráficos de identidade exige um mínimo de duas identidades vinculadas para ser gerado. É possível que haja apenas um valor de identidade e nenhuma identidade vinculada e, nesse caso, o valor só existiria em [!DNL Profile] visualizador.
- O visualizador de gráficos de identidade não pode exceder o máximo de 50 identidades.

![error-screen](../images/graph-viewer/error-screen.png)

### Acessar o visualizador de gráficos de identidade a partir de conjuntos de dados

Também é possível acessar o visualizador de gráficos de identidade usando a interface de conjuntos de dados. Dos conjuntos de dados [!UICONTROL Procurar] selecione o conjunto de dados com o qual deseja interagir e selecione **[!UICONTROL Visualizar conjunto de dados]**

![preview-dataset](../images/identity-graph-viewer/preview-dataset.png)

Na janela de visualização, selecione um ícone de impressão digital para ver as identidades representadas por meio do visualizador de gráficos de identidade.

>[!TIP]
>
>O ícone de impressão digital só será exibido se o conjunto de dados tiver duas ou mais identidades.

![impressão digital](../images/identity-graph-viewer/fingerprint.png)

## Próximas etapas

Ao ler este documento, você aprendeu a explorar os gráficos de identidade de seus clientes na interface do usuário da Platform. Para obter mais informações sobre identidades na Platform, consulte a [Visão geral do serviço de identidade](../home.md)

## Changelog

| Data | Ação |
| ---- | ------ |
| 2021-01 | <ul><li>Adição de suporte para transmissão de dados assimilados e sandbox de não produção.</li><li>Correção de erros secundários.</li></ul> |
| 2021-02 | <ul><li>O visualizador do gráfico de identidade se torna acessível por meio da visualização do conjunto de dados.</li><li>Correção de erros secundários.</li><li>O visualizador de gráficos de identidade foi disponibilizado para o público geral.</li></ul> |
| 2023-01 | <ul><li>Atualizações da interface do usuário.</li></ul> |
