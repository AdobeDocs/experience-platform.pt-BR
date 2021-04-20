---
keywords: Experience Platform, home, tópicos populares, Adobe Experience Platform, guia da api, guia da api da plataforma, introdução à plataforma, guia do desenvolvedor
solution: Experience Platform
title: Postman na Adobe Experience Platform
topic: api guide
description: Este documento contém etapas que descrevem como configurar um ambiente Postman, importar coleções Postman e uma lista de coleções disponíveis para cada serviço da Plataforma.
translation-type: tm+mt
source-git-commit: effc8fef666ffbf62c2e0874d048245f19c12111
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---


# Postman na Adobe Experience Platform

O Postman é uma plataforma de colaboração para desenvolvimento de API que permite configurar ambientes com variáveis predefinidas, compartilhar coleções de API, simplificar solicitações de CRUD e muito mais. A maioria dos serviços de API da Platform tem coleções Postman que podem ser usadas para ajudar a fazer chamadas de API.

## Como configurar um ambiente Postman para a Experience Platform

O guia de vídeo a seguir descreve a criação e a configuração do ambiente Postman. Um ambiente Postman contém todos os cabeçalhos necessários para fazer chamadas de API para as várias coleções fornecidas abaixo. Depois de configurado, sempre que um valor expirar (como `ACCESS_TOKEN`), você poderá atualizar o valor atual no ambiente e esse novo valor será usado em todas as suas coleções.

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Coleções de postman {#collections}

Uma pasta contendo todas as coleções disponíveis do Postman pode ser encontrada ao visitar o [repositório GitHub de amostras do Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Como alternativa, um link de coleção do Postman pode ser encontrado em cada arquivo swagger individual na [API reference documentation](http://www.adobe.com/go/platform-api-reference-en) no Adobe I/O.

Para baixar uma coleção Postman, selecione **[!DNL Raw]** na página GitHub para carregar o arquivo JSON bruto em uma nova guia. Em seguida, clique com o botão direito do mouse e selecione **[!DNL Save as]** para salvar o arquivo em um destino local de sua escolha.

![JSON bruto](./images/api-guide/raw-collection.PNG)

## Importar uma coleção Postman {#import}

Para utilizar uma [coleção Postman](#collections), é necessário ter um ambiente configurado. Depois de concluir a configuração do ambiente, selecione o seletor **[!DNL Manage Environments]** no canto superior direito.

![gerenciar seletor de ambiente](./images/api-guide/environment-selector.png)

Um fornecedor é exibido e exibe todos os seus ambientes atuais. Para importar uma coleção, selecione **[!DNL import]** .

![botão importar](./images/api-guide/import-collection.png)

Você deve escolher um arquivo para importar. Selecione o arquivo de coleção Postman que deseja importar. Depois de selecionada, a coleção é preenchida no painel à esquerda, na guia Collections .

![coleção preenchida](./images/api-guide/imported-collection.png)

Cada coleção tem pares de valores chave diferentes que podem ser necessários para executar uma operação CRUD bem-sucedida. Revise o [Guia do desenvolvedor de API](api-guide.md#api-guides) do serviço para saber mais sobre os valores necessários, dicas e ver exemplos.

Para saber mais sobre a interface do usuário do Postman e seus recursos disponíveis, visite a [documentação do Postman](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Gerar um token de acesso com o Postman para uso não relacionado à produção

>[!WARNING]
>
>Conforme observado na coleção Postman da geração de tokens de acesso do Adobe I/O, os métodos de geração indicados são adequados para **uso não relacionado à produção**. A assinatura local carrega uma biblioteca do JavaScript de um host de terceiros e a assinatura remota envia a chave privada para um serviço da Web que é de propriedade e operado pela Adobe. Embora a Adobe não armazene essa chave privada, as chaves de produção nunca devem ser compartilhadas com ninguém.

O vídeo abaixo usa a [coleção de geração de token de acesso do Adobe I/O](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Adobe%20IO%20Access%20Token%20Generation.postman_collection.json) que pode ser baixada do repositório público do GitHub.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## Próximas etapas

Este documento apresentou ambientes Postman, coleções e como importar coleções. Agora que o Postman está pronto, visite o [Guia de introdução à plataforma](api-guide.md) para obter informações sobre cabeçalhos, exemplos necessários e uma lista de [guias de API](api-guide.md#api-guides) disponíveis para cada serviço da plataforma.