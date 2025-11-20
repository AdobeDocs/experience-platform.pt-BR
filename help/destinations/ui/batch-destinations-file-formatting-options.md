---
description: Saiba como configurar opções de formatação de arquivo ao ativar dados para destinos baseados em arquivo
title: Configurar opções de formatação de arquivo para destinos baseados em arquivo
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: 4dd6e8685ff5cc61342b20e971216416918b95da
workflow-type: tm+mt
source-wordcount: '1191'
ht-degree: 17%

---

# Configurar opções de formatação de arquivo para destinos baseados em arquivo

>[!IMPORTANT]
> 
>As opções de formatação de arquivo descritas neste documento estão disponíveis somente para arquivos CSV.

A opção para configurar várias opções de formatação de arquivo para os arquivos exportados está disponível ao [conectar](/help/destinations/ui/connect-destination.md) a um destino baseado em arquivo, como o [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect), o [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect) ou o [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect).

É possível configurar várias opções de formatação de arquivo para arquivos exportados usando a interface do usuário do Experience Platform. Você pode modificar várias propriedades dos arquivos exportados para corresponder aos requisitos do sistema de recebimento de arquivos do seu lado, a fim de ler e interpretar de maneira ideal os arquivos recebidos do Experience Platform.

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## Configuração da formatação de arquivo para arquivos CSV {#file-configuration}

Para exibir as opções de formatação de arquivo, inicie o fluxo de trabalho [conectar ao destino](/help/destinations/ui/connect-destination.md). Selecione **Tipo de dados: Segmentos** e **Tipo de arquivo: CSV** para exibir as configurações de formatação de arquivo disponíveis para os arquivos `CSV` exportados.

>[!IMPORTANT]
>
>O destino ao qual você está se conectando pode não ter todas essas opções disponíveis. Cabe ao desenvolvedor de destino determinar quais opções de formatação de arquivo ele deseja suportar em seu destino. O desenvolvedor de destino pode determinar quais opções estão disponíveis ao se conectar ao destino. As opções obrigatórias estão marcadas com um asterisco na interface do usuário do Experience Platform.
> 
>Os destinos de armazenamento na nuvem criados pela Adobe - [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [Google Cloud Storage](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP](/help/destinations/catalog/cloud-storage/sftp.md) - atualmente só oferecem suporte às seis opções de CSV destacadas abaixo.

![Imagem mostrando algumas das opções de formatação de arquivo disponíveis.](../assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### Delimitador {#delimiter}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_delimiter"
>title="Delimitador"
>abstract="Use esse controle para definir um separador para cada campo e valor. Consulte a documentação para ver exemplos de cada seleção."

Use esse controle para definir um separador para cada campo e valor nos arquivos CSV exportados. As opções disponíveis são:

* Dois pontos `(:)`
* Vírgula `(,)`
* Pipe `(|)`
* Ponto e vírgula `(;)`
* Guia `(\t)`

#### Exemplos

Veja os exemplos abaixo do conteúdo nos arquivos CSV exportados com cada uma das seleções na interface do usuário.

* Exemplo de saída com **[!UICONTROL Colon `(:)`]** selecionado: `male:John:Doe`
* Exemplo de saída com **[!UICONTROL Comma `(,)`]** selecionado: `male,John,Doe`
* Exemplo de saída com **[!UICONTROL Pipe `(|)`]** selecionado: `male|John|Doe`
* Exemplo de saída com **[!UICONTROL Semicolon `(;)`]** selecionado: `male;John;Doe`
* Exemplo de saída com **[!UICONTROL Tab `(\t)`]** selecionado: `male \t John \t Doe`

### Caractere de aspas {#quote-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_quoteCharacter"
>title="Caractere de aspas"
>abstract="Use essa opção se desejar remover as aspas duplas das strings exportadas. Consulte a documentação para ver exemplos de cada seleção."

Use essa opção para controlar se as aspas duplas devem ser removidas ou mantidas nas cadeias de caracteres exportadas.

As opções disponíveis são:

* **[!UICONTROL Null Character (\0000)]**. Use essa opção para remover aspas duplas de arquivos CSV exportados.
* **[!UICONTROL Double Quotes (")]**. Use essa opção quando os valores da string contiverem um delimitador ou aspas duplas. Essa opção ajuda a manter os delimitadores ou aspas duplas nos arquivos CSV exportados, para que você possa identificar corretamente qual valor corresponde a qual campo.

#### Exemplos

Considere o valor de entrada `Anna,"Doe,John"`.

Veja os exemplos abaixo do conteúdo de arquivos CSV exportados com cada uma das seleções na interface.

* Exemplo de saída com **[!UICONTROL Null Character (\0000)]** selecionado: `Anna,Doe,John`
* Exemplo de saída com **[!UICONTROL Double Quotes (")]** selecionado: `Anna,"Doe,John"`

### Caractere de escape {#escape-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_escapeCharacter"
>title="Caractere de escape"
>abstract="Define um caractere único usado para “escapar” citações dentro de um valor já citado. Consulte a documentação para ver exemplos de cada seleção."

Use esta opção para definir um caractere único para aspas de escape dentro de um valor já citado. Por exemplo, essa opção é útil quando você tem uma string entre aspas duplas em que parte da string já está entre aspas duplas. Esta opção determina com qual caractere substituir as aspas duplas internas. As opções disponíveis são:

* Barra invertida `(\)`
* Aspas simples `(')`

#### Exemplos

Veja os exemplos abaixo do conteúdo de arquivos CSV exportados com cada uma das seleções na interface.

* Exemplo de saída com **[!UICONTROL Back slash `(\)`]** selecionado: `"Test,\"John\",LastName"`
* Exemplo de saída com **[!UICONTROL Single quote `(')`]** selecionado: `"Test,'"John'",LastName"`

### Saída de valor vazio {#empty-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_emptyValueOutput"
>title="Saída de valor vazio"
>abstract="Use essa opção para definir como os valores vazios devem ser representados nos arquivos CSV exportados. Consulte a documentação para ver exemplos de cada seleção."

Use este controle para definir a representação da sequência de caracteres de um valor vazio. Essa opção determina como os valores vazios são representados nos arquivos CSV exportados. As opções disponíveis são:

* **[!UICONTROL Null (null)]**
* **Cadeia de Caracteres Vazia entre Aspas Duplas (&quot;&quot;)**
* **[!UICONTROL Empty string]**

#### Exemplos

Veja os exemplos abaixo do conteúdo de arquivos CSV exportados com cada uma das seleções na interface.

* Exemplo de saída com **[!UICONTROL null]** selecionado: `male,NULL,TestLastName`. Nesse caso, o Experience Platform transforma o valor vazio em um valor nulo.
* Exemplo de saída com **&quot;** selecionado: `male,"",TestLastName`. Nesse caso, o Experience Platform transforma o valor vazio em um par de aspas duplas.
* Exemplo de saída com **[!UICONTROL Empty string]** selecionado: `male,,TestLastName`. Nesse caso, o Experience Platform mantém o valor vazio e o exporta como está (sem aspas duplas).

>[!TIP]
>
>A diferença entre a saída de valor vazio e a saída de valor nulo na seção abaixo é que um valor vazio tem um valor real que está vazio. O valor NULL não tem nenhum valor. Pense no valor vazio como um vidro vazio na tabela e no valor nulo como não tendo o vidro na tabela.

### Saída de valor nulo {#null-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_nullValueOutput"
>title="Saída de valor nulo"
>abstract="Use esse controle para definir como as strings de valor nulo devem ser representadas nos arquivos exportados. Consulte a documentação para ver exemplos de cada seleção."

Use esse controle para definir como as strings de valor nulo devem ser representadas nos arquivos exportados. Essa opção determina como os valores nulos são representados nos arquivos CSV exportados. As opções disponíveis são:

* **[!UICONTROL Null (null)]**
* **Cadeia de Caracteres Vazia entre Aspas Duplas (&quot;&quot;)**
* **[!UICONTROL Empty string]**

#### Exemplos

Veja os exemplos abaixo do conteúdo de arquivos CSV exportados com cada uma das seleções na interface.

* Exemplo de saída com **[!UICONTROL null]** selecionado: `male,NULL,TestLastName`. Nesse caso, não ocorre nenhuma transformação e o arquivo CSV contém o valor nulo.
* Exemplo de saída com **&quot;** selecionado: `male,"",TestLastName`. Nesse caso, o Experience Platform substitui o valor nulo por aspas duplas em torno de uma string vazia.
* Exemplo de saída com **[!UICONTROL Empty string]** selecionado: `male,,TestLastName`. Nesse caso, o Experience Platform substitui o valor nulo por uma string vazia (sem aspas duplas).

### Formato de compactação {#compression-format}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_compressionFormat"
>title="Formato de compactação"
>abstract="Define o tipo de compactação a ser usado ao salvar dados no arquivo. As opções compatíveis são GZIP e NONE. Consulte a documentação para ver exemplos de cada seleção."

Define o tipo de compactação a ser usado ao salvar dados no arquivo. As opções compatíveis são GZIP e NONE. Essa opção determina se você exportará ou não arquivos compactados.

### Codificação

*Não mostrado na captura de tela da interface do usuário*. Especifica a codificação (conjunto de caracteres) dos arquivos CSV salvos. As opções são UTF-8 ou UTF-16.

### Caractere para aspas de escape

*Não mostrado na captura de tela da interface do usuário*. Um sinalizador que indica se os valores que contêm aspas devem sempre estar entre aspas.

O padrão é omitir todos os valores que contenham um caractere de aspas.

### Separador de linha

*Não mostrado na captura de tela da interface do usuário*. Define o separador de linha que deve ser usado para gravação. O comprimento máximo é de 1 caractere.

### Ignorar espaço em branco à esquerda

*Não mostrado na captura de tela da interface do usuário*. Um sinalizador que indica se os espaços em branco à esquerda dos valores que estão sendo exportados deve ser ignorado.

Exemplo de saída com **[!UICONTROL True]** selecionado: `"male","John","TestLastName"`
Exemplo de saída com **[!UICONTROL False]** selecionado: `" male","John","TestLastName"`

### Ignorar espaço em branco à direita

Não mostrado na captura de tela da interface do usuário. Um sinalizador que indica se espaços em branco à direita de valores que estão sendo exportados deve ser ignorado.

Exemplo de saída com **[!UICONTROL True]** selecionado: `"male","John","TestLastName"`
Exemplo de saída com **[!UICONTROL False]** selecionado: `"male ","John","TestLastName"`

### Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe como configurar as opções de exportação de arquivo para seus arquivos de dados CSV para adaptar o conteúdo do arquivo aos requisitos do sistema de recebimento de arquivos downstream. Em seguida, você pode ler o [tutorial de ativação de destinos baseados em arquivo](/help/destinations/ui/activate-batch-profile-destinations.md) para começar a exportar arquivos para seu local de armazenamento na nuvem preferido.
