---
description: Saiba como configurar opções de formatação de arquivo ao ativar dados para destinos baseados em arquivo
title: (Beta) Configurar opções de formatação de arquivo para destinos baseados em arquivo
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: 14ce4a11f53ef24b3008b3f775cc926d05ea8f8e
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 1%

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

## Configuração da formatação de arquivo {#file-configuration}

Para exibir as opções de formatação de arquivo, inicie o [conectar ao destino](/help/destinations/ui/connect-destination.md) fluxo de trabalho. Selecionar **Tipo de dados: Segmentos** e **Tipo de arquivo: CSV** para exibir as configurações de formatação de arquivo disponíveis para o `CSV` arquivos.

>[!IMPORTANT]
>
>O destino ao qual você está se conectando pode não ter todas essas opções disponíveis. Cabe ao desenvolvedor de destino determinar quais opções de formatação de arquivo ele deseja suportar em seu destino. O desenvolvedor de destino pode determinar quais opções estão disponíveis ao se conectar ao destino. As opções obrigatórias estão marcadas com um asterisco na interface do usuário do Experience Platform.
> 
>Os novos destinos de armazenamento na nuvem - [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Beta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Armazenamento do Azure Data Lake Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(Beta) Zona de aterrissagem de dados](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Armazenamento em nuvem do Google](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md) - atualmente, o suporta apenas as seis opções de CSV destacadas abaixo.

![Imagem mostrando algumas das opções de formatação de arquivo disponíveis.](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### Delimitador {#delimiter}

Define um separador para cada campo e valor. As opções disponíveis são:

* Dois-pontos `(:)`
* Vírgula `(,)`
* Estágio `(|)`
* Ponto e vírgula `(;)`
* Guia `(\\t)`

### Caractere de citação

Define um caractere único usado para sair de valores entre aspas onde o separador pode ser parte do valor.

### Caractere de escape

Define um caractere único usado para fazer o escape de aspas dentro de um valor já citado.

### Saída de valor vazia

Define a representação da cadeia de caracteres de um valor vazio.

### Saída de valor nulo

Define a representação da cadeia de caracteres de um valor nulo nos arquivos exportados.

Exemplo de saída com **[!UICONTROL null]** selecionado: `male,NULL,TestLastName`
Exemplo de saída com **&quot;&quot;** selecionado: `male,"",TestLastName`
Exemplo de saída com **[!UICONTROL String vazia]** selecionado: `male,,TestLastName`

### Formato de compactação

Define qual codec de compactação usar ao salvar dados no arquivo. As opções compatíveis são GZIP e NONE.

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
