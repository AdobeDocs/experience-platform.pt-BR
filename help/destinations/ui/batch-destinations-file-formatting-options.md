---
description: Saiba como configurar as opções de formatação de arquivo ao ativar dados em destinos com base em arquivo
title: (Beta) Configurar opções de formatação de arquivo para destinos com base em arquivo
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: b1e9b781f3b78a22b8b977fe08712d2926254e8c
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 2%

---

# (Beta) Configurar opções de formatação de arquivo para destinos com base em arquivo

>[!IMPORTANT]
>
>O **[!UICONTROL Opções de formatação de arquivo]** no Adobe Experience Platform está atualmente em versão beta. A documentação e a funcionalidade estão sujeitas a alterações.
>Entre em contato com o representante do Adobe para obter acesso a essa funcionalidade.
> 
>As opções de formatação de arquivos descritas neste documento estão disponíveis apenas para arquivos CSV.

A opção para configurar várias opções de formatação de arquivo para os arquivos exportados está disponível para você quando [connect](/help/destinations/ui/connect-destination.md) para um destino com base em arquivo, como [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect), [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect)ou [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect).

Você pode configurar várias opções de formatação de arquivos para arquivos exportados usando a interface do usuário do Experience Platform. Você pode modificar várias propriedades dos arquivos exportados para corresponder aos requisitos do sistema de recepção de arquivos no seu lado, a fim de ler e interpretar de maneira ideal os arquivos recebidos do Experience Platform.

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## Configuração de formatação de arquivo para arquivos CSV {#file-configuration}

Para exibir as opções de formatação de arquivo, inicie o [conectar-se ao destino](/help/destinations/ui/connect-destination.md) fluxo de trabalho. Selecionar **Tipo de dados: Segmentos** e **Tipo de arquivo: CSV** para exibir as configurações de formatação de arquivo disponíveis para o arquivo exportado `CSV` arquivos.

>[!IMPORTANT]
>
>O destino ao qual você está se conectando pode não ter todas essas opções disponíveis. Cabe ao desenvolvedor de destino determinar quais opções de formatação de arquivo deseja suportar no destino. O desenvolvedor de destino pode determinar quais opções estão disponíveis ao se conectar ao destino. As opções necessárias são marcadas com um asterisco na interface do usuário do Experience Platform.
> 
>Os novos destinos de armazenamento em nuvem - [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Beta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Armazenamento Azure Data Lake Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Zona de aterrissagem de dados (Beta)](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Armazenamento em nuvem Google](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP (Beta)](/help/destinations/catalog/cloud-storage/sftp.md) - atualmente, suporta apenas as seis opções de CSV destacadas abaixo.

![Imagem mostrando algumas das opções disponíveis de formatação de arquivo.](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### Delimitador {#delimiter}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_delimiter"
>title="Delimitador"
>abstract="Use esse controle para definir um separador para cada campo e valor. Consulte a documentação para ver exemplos de cada seleção."

Use esse controle para definir um separador para cada campo e valor nos arquivos CSV exportados. As opções disponíveis são:

* Dois-pontos `(:)`
* Vírgula `(,)`
* Estágio `(|)`
* Ponto e vírgula `(;)`
* Guia `(\t)`

#### Exemplos

Visualize os exemplos abaixo do conteúdo nos arquivos CSV exportados com cada uma das seleções na interface do usuário.

* Exemplo de saída com **[!UICONTROL Dois`(:)`]** selecionado: `male:John:Doe`
* Exemplo de saída com **[!UICONTROL Vírgula`(,)`]** selecionado: `male,John,Doe`
* Exemplo de saída com **[!UICONTROL Pipe`(|)`]** selecionado: `male|John|Doe`
* Exemplo de saída com **[!UICONTROL Ponto e vírgula`(;)`]** selecionado: `male;John;Doe`
* Exemplo de saída com **[!UICONTROL Tabulação`(\t)`]** selecionado: `male \t John \t Doe`

### Caractere de citação {#quote-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_quoteCharacter"
>title="Caractere de citação"
>abstract="Use essa opção se desejar remover aspas duplas das cadeias de caracteres exportadas. Consulte a documentação para ver exemplos de cada seleção."

Use essa opção se desejar remover aspas duplas das cadeias de caracteres exportadas. As opções disponíveis são:

* **[!UICONTROL Caractere Nulo (\0000)]**. Use essa opção para remover aspas duplas de arquivos CSV exportados.
* **[!UICONTROL Aspas duplas (&quot;)]**. Use essa opção para manter aspas duplas em seus arquivos CSV exportados.

#### Exemplos

Visualize os exemplos abaixo do conteúdo de arquivos CSV exportados com cada uma das seleções na interface do usuário.

* Exemplo de saída com **[!UICONTROL Caractere Nulo (\0000)]** selecionado: `Test,John,LastName`
* Exemplo de saída com **[!UICONTROL Aspas duplas (&quot;)]** selecionado: `"Test","John","LastName"`

### Caractere de escape {#escape-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_escapeCharacter"
>title="Caractere de escape"
>abstract="Define um caractere único usado para evitar aspas dentro de um valor já citado. Consulte a documentação para ver exemplos de cada seleção."

Use essa opção para definir um caractere único para evitar aspas dentro de um valor já citado. Por exemplo, essa opção é útil quando há uma string entre aspas duplas, na qual parte da string já está entre aspas duplas. Essa opção determina por qual caractere substituir as aspas duplas internas. As opções disponíveis são:

* Barra invertida `(\)`
* Cotação única `(')`

#### Exemplos

Visualize os exemplos abaixo do conteúdo de arquivos CSV exportados com cada uma das seleções na interface do usuário.

* Exemplo de saída com **[!UICONTROL Barra invertida`(\)`]** selecionado: `"Test,\"John\",LastName"`
* Exemplo de saída com **[!UICONTROL Cotação única`(')`]** selecionado: `"Test,'"John'",LastName"`

### Saída de valor vazio {#empty-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_emptyValueOutput"
>title="Saída de valor vazio"
>abstract="Use essa opção para definir como os valores vazios devem ser representados nos arquivos CSV exportados. Consulte a documentação para ver exemplos de cada seleção."

Use esse controle para definir a representação da string de um valor vazio. Essa opção determina como os valores vazios são representados em seus arquivos CSV exportados. As opções disponíveis são:

* **[!UICONTROL nulo]**
* **&quot;&quot;**
* **[!UICONTROL Sequência de caracteres vazia]**

#### Exemplos

Visualize os exemplos abaixo do conteúdo de arquivos CSV exportados com cada uma das seleções na interface do usuário.

* Exemplo de saída com **[!UICONTROL null]** selecionado: `male,NULL,TestLastName`. Nesse caso, Experience Platform transforma o valor vazio em um valor nulo.
* Exemplo de saída com **&quot;&quot;** selecionado: `male,"",TestLastName`. Nesse caso, o Experience Platform transforma o valor vazio em um par de aspas duplas.
* Exemplo de saída com **[!UICONTROL Sequência de caracteres vazia]** selecionado: `male,,TestLastName`. Nesse caso, o Experience Platform mantém o valor vazio e o exporta como está (sem aspas duplas).

>[!TIP]
>
>A diferença entre a saída do valor vazio e a saída do valor nulo na seção abaixo é que um valor vazio tem um valor real que está vazio. O valor NULL não tem nenhum valor. Considere o valor vazio como um vidro vazio na tabela e o valor nulo como não tendo o vidro na tabela.

### Saída de valor nulo {#null-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_nullValueOutput"
>title="Saída de valor nulo"
>abstract="Use esse controle para definir a representação da string de um valor nulo nos arquivos exportados. Consulte a documentação para ver exemplos de cada seleção."

Use esse controle para definir a representação da string de um valor nulo nos arquivos exportados. Essa opção determina como os valores nulos são representados nos arquivos CSV exportados. As opções disponíveis são:

* **[!UICONTROL nulo]**
* **&quot;&quot;**
* **[!UICONTROL Sequência de caracteres vazia]**

#### Exemplos

Visualize os exemplos abaixo do conteúdo de arquivos CSV exportados com cada uma das seleções na interface do usuário.

* Exemplo de saída com **[!UICONTROL null]** selecionado: `male,NULL,TestLastName`. Nesse caso, nenhuma transformação ocorre e o arquivo CSV contém o valor nulo.
* Exemplo de saída com **&quot;&quot;** selecionado: `male,"",TestLastName`. Nesse caso, Experience Platform substitui o valor nulo por aspas duplas em torno de uma string vazia.
* Exemplo de saída com **[!UICONTROL Sequência de caracteres vazia]** selecionado: `male,,TestLastName`. Nesse caso, Experience Platform substitui o valor nulo por uma string vazia (sem aspas duplas).

### Formato de compactação {#compression-format}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_compressionFormat"
>title="Formato de compactação"
>abstract="Define o tipo de compactação a ser usado ao salvar dados no arquivo. As opções compatíveis são GZIP e NONE. Consulte a documentação para ver exemplos de cada seleção."

Define o tipo de compactação a ser usado ao salvar dados no arquivo. As opções compatíveis são GZIP e NONE. Essa opção determina se você exportará ou não arquivos compactados.

### Codificação

*Não mostrado na captura de tela da interface do usuário*. Especifica a codificação (charset) de arquivos CSV salvos. As opções são UTF-8 ou UTF-16.

### Caractere de escape entre aspas

*Não mostrado na captura de tela da interface do usuário*. Um sinalizador que indica se os valores contendo aspas devem sempre ser entre aspas.

O padrão é omitir todos os valores que contenham um caractere de aspas.

### Separador de linha

*Não mostrado na captura de tela da interface do usuário*. Define o separador de linha que deve ser usado para gravação. O comprimento máximo é de 1 caractere.

### Ignorar espaço em branco à esquerda

*Não mostrado na captura de tela da interface do usuário*. Um sinalizador que indica se os espaços em branco à esquerda de valores que estão sendo exportados devem ser ignorados.

Exemplo de saída com **[!UICONTROL Verdadeiro]** selecionado: `"male","John","TestLastName"`
Exemplo de saída com **[!UICONTROL Falso]** selecionado: `" male","John","TestLastName"`

### Ignorar espaço em branco à direita

Não mostrado na captura de tela da interface do usuário. Um sinalizador que indica se os espaços em branco à direita de valores que estão sendo exportados devem ser ignorados.

Exemplo de saída com **[!UICONTROL Verdadeiro]** selecionado: `"male","John","TestLastName"`
Exemplo de saída com **[!UICONTROL Falso]** selecionado: `"male ","John","TestLastName"`

### Próximas etapas {#next-steps}

Após a leitura deste documento, você agora sabe configurar as opções de exportação de arquivos para seus arquivos de dados CSV para adaptar o conteúdo do arquivo às necessidades do seu sistema de recepção de arquivos downstream. Em seguida, você pode ler o [tutorial de ativação de destinos com base em arquivo](/help/destinations/ui/activate-batch-profile-destinations.md) para começar a exportar arquivos para o local de armazenamento de nuvem preferencial.
