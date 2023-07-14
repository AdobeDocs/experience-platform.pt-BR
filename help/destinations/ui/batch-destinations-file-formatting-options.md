---
description: Saiba como configurar opções de formatação de arquivo ao ativar dados para destinos baseados em arquivo
title: (Beta) Configurar opções de formatação de arquivo para destinos baseados em arquivo
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 19%

---

# (Beta) Configurar opções de formatação de arquivo para destinos baseados em arquivo

>[!IMPORTANT]
>
>A variável **[!UICONTROL Opções de formatação de arquivo]** No momento, a funcionalidade no Adobe Experience Platform está na versão beta. A documentação e a funcionalidade estão sujeitas a alterações.
>Entre em contato com o representante da Adobe para obter acesso a essa funcionalidade.
> 
>As opções de formatação de arquivo descritas neste documento estão disponíveis somente para arquivos CSV.

A opção para configurar várias opções de formatação de arquivo para os arquivos exportados está disponível quando você [conectar](/help/destinations/ui/connect-destination.md) para um destino baseado em arquivo, como [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect), [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect)ou [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect).

Você pode configurar várias opções de formatação de arquivo para arquivos exportados usando a interface do usuário do Experience Platform. Você pode modificar várias propriedades dos arquivos exportados para corresponder aos requisitos do sistema de recebimento de arquivos do seu lado, a fim de ler e interpretar de maneira ideal os arquivos recebidos do Experience Platform.

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## Configuração da formatação de arquivo para arquivos CSV {#file-configuration}

Para exibir as opções de formatação de arquivo, inicie o [conectar ao destino](/help/destinations/ui/connect-destination.md) fluxo de trabalho. Selecionar **Tipo de dados: Segmentos** e **Tipo de arquivo: CSV** para exibir as configurações de formatação de arquivo disponíveis para o `CSV` arquivos.

>[!IMPORTANT]
>
>O destino ao qual você está se conectando pode não ter todas essas opções disponíveis. Cabe ao desenvolvedor de destino determinar quais opções de formatação de arquivo ele deseja suportar em seu destino. O desenvolvedor de destino pode determinar quais opções estão disponíveis ao se conectar ao destino. As opções obrigatórias estão marcadas com um asterisco na interface do usuário do Experience Platform.
> 
>Os novos destinos de armazenamento na nuvem - [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Beta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Armazenamento do Azure Data Lake Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(Beta) Zona de aterrissagem de dados](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Armazenamento em nuvem do Google](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md) - atualmente, o suporta apenas as seis opções de CSV destacadas abaixo.

![Imagem mostrando algumas das opções de formatação de arquivo disponíveis.](../assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

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

Veja os exemplos abaixo do conteúdo nos arquivos CSV exportados com cada uma das seleções na interface do usuário.

* Exemplo de saída com **[!UICONTROL Dois pontos`(:)`]** selecionado: `male:John:Doe`
* Exemplo de saída com **[!UICONTROL Vírgula`(,)`]** selecionado: `male,John,Doe`
* Exemplo de saída com **[!UICONTROL Tubulação`(|)`]** selecionado: `male|John|Doe`
* Exemplo de saída com **[!UICONTROL Ponto e vírgula`(;)`]** selecionado: `male;John;Doe`
* Exemplo de saída com **[!UICONTROL Guia`(\t)`]** selecionado: `male \t John \t Doe`

### Caractere de aspas {#quote-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_quoteCharacter"
>title="Caractere de aspas"
>abstract="Use essa opção se desejar remover as aspas duplas das strings exportadas. Consulte a documentação para ver exemplos de cada seleção."

Use essa opção se desejar remover as aspas duplas das strings exportadas. As opções disponíveis são:

* **[!UICONTROL Caractere Nulo (\0000)]**. Use essa opção para remover aspas duplas de arquivos CSV exportados.
* **[!UICONTROL Aspas duplas (&quot;)]**. Use essa opção para manter aspas duplas nos arquivos CSV exportados.

#### Exemplos

Veja os exemplos abaixo do conteúdo de arquivos CSV exportados com cada uma das seleções na interface.

* Exemplo de saída com **[!UICONTROL Caractere Nulo (\0000)]** selecionado: `Test,John,LastName`
* Exemplo de saída com **[!UICONTROL Aspas duplas (&quot;)]** selecionado: `"Test","John","LastName"`

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

* Exemplo de saída com **[!UICONTROL Barra invertida`(\)`]** selecionado: `"Test,\"John\",LastName"`
* Exemplo de saída com **[!UICONTROL Aspas simples`(')`]** selecionado: `"Test,'"John'",LastName"`

### Saída de valor vazio {#empty-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_emptyValueOutput"
>title="Saída de valor vazio"
>abstract="Use essa opção para definir como os valores vazios devem ser representados nos arquivos CSV exportados. Consulte a documentação para ver exemplos de cada seleção."

Use este controle para definir a representação da sequência de caracteres de um valor vazio. Essa opção determina como os valores vazios são representados nos arquivos CSV exportados. As opções disponíveis são:

* **[!UICONTROL Null (null)]**
* **String vazia entre aspas duplas (&quot;&quot;)**
* **[!UICONTROL String vazia]**

#### Exemplos

Veja os exemplos abaixo do conteúdo de arquivos CSV exportados com cada uma das seleções na interface.

* Exemplo de saída com **[!UICONTROL null]** selecionado: `male,NULL,TestLastName`. Nesse caso, o Experience Platform transforma o valor vazio em um valor nulo.
* Exemplo de saída com **&quot;&quot;** selecionado: `male,"",TestLastName`. Nesse caso, Experience Platform transforma o valor vazio em um par de aspas duplas.
* Exemplo de saída com **[!UICONTROL String vazia]** selecionado: `male,,TestLastName`. Nesse caso, o Experience Platform mantém o valor vazio e o exporta como está (sem aspas duplas).

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
* **String vazia entre aspas duplas (&quot;&quot;)**
* **[!UICONTROL String vazia]**

#### Exemplos

Veja os exemplos abaixo do conteúdo de arquivos CSV exportados com cada uma das seleções na interface.

* Exemplo de saída com **[!UICONTROL null]** selecionado: `male,NULL,TestLastName`. Nesse caso, não ocorre nenhuma transformação e o arquivo CSV contém o valor nulo.
* Exemplo de saída com **&quot;&quot;** selecionado: `male,"",TestLastName`. Nesse caso, o Experience Platform substitui o valor nulo por aspas duplas em torno de uma string vazia.
* Exemplo de saída com **[!UICONTROL String vazia]** selecionado: `male,,TestLastName`. Nesse caso, o Experience Platform substitui o valor nulo por uma string vazia (sem aspas duplas).

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
Exemplo de saída com **[!UICONTROL Falso]** selecionado: `" male","John","TestLastName"`

### Ignorar espaço em branco à direita

Não mostrado na captura de tela da interface do usuário. Um sinalizador que indica se espaços em branco à direita de valores que estão sendo exportados deve ser ignorado.

Exemplo de saída com **[!UICONTROL True]** selecionado: `"male","John","TestLastName"`
Exemplo de saída com **[!UICONTROL Falso]** selecionado: `"male ","John","TestLastName"`

### Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe como configurar as opções de exportação de arquivo para seus arquivos de dados CSV para adaptar o conteúdo do arquivo aos requisitos do sistema de recebimento de arquivos downstream. Em seguida, você pode ler o [tutorial de ativação de destinos baseados em arquivo](/help/destinations/ui/activate-batch-profile-destinations.md) para começar a exportar arquivos para o local de armazenamento na nuvem de sua preferência.
