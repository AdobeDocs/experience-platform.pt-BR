---
keywords: Experience Platform;página inicial;tópicos populares;Adobe Experience Platform;guia de api;guia de api da plataforma;introdução à plataforma;guia do desenvolvedor
solution: Experience Platform
title: Postman no Adobe Experience Platform
description: Este documento contém etapas que descrevem como configurar um ambiente do Postman, importar coleções do Postman e uma lista de coleções disponíveis para cada serviço do Experience Platform.
role: Developer
feature: API
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# Postman no Adobe Experience Platform

O Postman é uma plataforma de colaboração para o desenvolvimento de API que permite configurar ambientes com variáveis predefinidas, compartilhar coleções de API, simplificar solicitações CRUD e muito mais. A maioria dos serviços de API do Experience Platform tem coleções do Postman que podem ser usadas para ajudar a fazer chamadas de API.

## Como configurar um ambiente do Postman para o Experience Platform

O guia de vídeo a seguir descreve a criação e a configuração do ambiente do Postman. Um ambiente do Postman contém todos os cabeçalhos necessários para fazer chamadas de API para as várias coleções fornecidas abaixo. Depois de configurado, sempre que um valor expirar (como um `ACCESS_TOKEN`), você poderá atualizar o valor atual no ambiente e esse novo valor será usado em todas as coleções.

>[!VIDEO](https://video.tv.adobe.com/v/31682?captions=por_br)

## coleções do Postman {#collections}

Uma pasta contendo todas as coleções disponíveis do Postman pode ser encontrada em, visitando o [repositório GitHub de amostras do Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Como alternativa, um link de coleção do Postman pode ser encontrado em cada arquivo do Swagger individual na [documentação de referência da API](https://www.adobe.com/go/platform-api-reference-en) no Adobe I/O.

Para baixar uma coleção do Postman, selecione **[!DNL Raw]** na página do GitHub para carregar o arquivo JSON bruto em uma nova guia. Em seguida, clique com o botão direito do mouse e selecione **[!DNL Save as]** para salvar o arquivo em um destino local de sua escolha.

![JSON bruto](./images/api-guide/raw-collection.PNG)

## Importar uma coleção do Postman {#import}

Para utilizar uma [coleção do Postman](#collections), é necessário ter um ambiente configurado. Depois de concluir a configuração do ambiente, selecione o seletor **[!DNL Manage Environments]** no canto superior direito.

![gerenciar seletor de ambiente](./images/api-guide/environment-selector.png)

Um popover é exibido e exibe todos os seus ambientes atuais. Para importar uma coleção, selecione **[!DNL import]** .

![botão Importar](./images/api-guide/import-collection.png)

Você será solicitado a escolher um arquivo para importar. Selecione o arquivo de coleção do Postman que deseja importar. Depois de selecionada, a coleção é preenchida no painel à esquerda na guia Coleções.

![coleção preenchida](./images/api-guide/imported-collection.png)

Cada coleção tem pares de chave-valor diferentes que podem ser necessários para executar uma operação CRUD bem-sucedida. Revise o [guia do desenvolvedor de API](api-guide.md#api-guides) do serviço para saber mais sobre os valores, as dicas e os exemplos necessários.

Para saber mais sobre a interface do usuário do Postman e seus recursos disponíveis, visite a [documentação do Postman](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Gerar um token de acesso com o Postman para uso de não produção

>[!WARNING]
>
>Conforme observado na coleção do Postman do Identity Management Service (IMS), os métodos de geração indicados são adequados para **uso de não produção**. A assinatura local carrega uma biblioteca do JavaScript de um host de terceiros e a assinatura remota envia a chave privada para um serviço da Web que pertence e é operado pela Adobe. Embora a Adobe não armazene essa chave privada, as chaves de produção nunca devem ser compartilhadas com ninguém.

O vídeo abaixo usa a [coleção do Postman do Identity Management Service (IMS)](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) que pode ser baixada do repositório público do GitHub.

>[!VIDEO](https://video.tv.adobe.com/v/32726/?quality=12&learn=on&captions=por_br)

## Próximas etapas

Esse documento apresentou ambientes do Postman, coleções e como importar coleções. Agora que você tem o Postman pronto, visite o [guia de introdução do Experience Platform](api-guide.md) para obter informações sobre cabeçalhos, exemplos e uma lista dos [guias de API](api-guide.md#api-guides) necessários disponíveis para cada serviço do Experience Platform.
