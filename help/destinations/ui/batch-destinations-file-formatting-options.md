---
description: Saiba como configurar as opções de formatação de arquivo ao ativar dados em destinos com base em arquivo
title: (Beta) Configurar opções de formatação de arquivo para destinos com base em arquivo
source-git-commit: 23a7a1997e05d2bde26de5b73a23ea051bf2b3bb
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

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

## Configuração de formatação de arquivo {#file-configuration}

>[!IMPORTANT]
>
>O destino ao qual você está se conectando pode não ter todas essas opções disponíveis. Cabe ao desenvolvedor de destino determinar quais opções de formatação de arquivo deseja suportar no destino. O desenvolvedor de destino pode determinar quais opções estão disponíveis ao se conectar ao destino. As opções necessárias são marcadas com um asterisco na interface do usuário do Experience Platform.

Para exibir as opções de formatação de arquivo, inicie o [conectar-se ao destino](/help/destinations/ui/connect-destination.md) e selecione segmentos como **Tipo de arquivo**. Esta seção descreve as configurações de formatação de arquivo disponíveis para o arquivo exportado `CSV` arquivos.

![Imagem mostrando algumas das opções disponíveis de formatação de arquivo.](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### Delimitador

Define um separador para cada campo e valor. Por exemplo, `,` para valores separados por vírgula ou `/t` para valores separados por tabulação.

### Caractere de citação

Define um caractere único usado para escapar de valores entre aspas, onde o separador pode fazer parte do valor.

### Caractere de escape

Define um caractere único usado para evitar aspas dentro de um valor já citado.

### Saída de valor vazio

Define a representação da string de um valor vazio.

### Saída de valor nulo

Define a representação da string de um valor nulo nos arquivos exportados.

Exemplo de saída com **[!UICONTROL null]** selecionado: `male,NULL,TestLastName`
Exemplo de saída com **&quot;&quot;** selecionado: `male,"",TestLastName`
Exemplo de saída com **[!UICONTROL Sequência de caracteres vazia]** selecionado: `male,,TestLastName`

### Formato de compactação

Define qual codec de compactação usar ao salvar dados no arquivo. As opções compatíveis são GZIP e NONE.

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
