---
keywords: Experience Platform, home, tópicos populares, Adobe Experience Platform, guia de api, guia de api da plataforma, introdução à plataforma, guia do desenvolvedor
solution: Experience Platform
title: Postman no Adobe Experience Platform
topic-legacy: api guide
description: Este documento contém etapas que descrevem como configurar um ambiente do Postman, importar coleções do Postman e uma lista de coleções disponíveis para cada serviço da plataforma.
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: 9f00bff31f9e7d2da1294d3d1f24cba7870a4614
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# Postman no Adobe Experience Platform

O Postman é uma plataforma de colaboração para desenvolvimento de API que permite configurar ambientes com variáveis predefinidas, compartilhar coleções de API, simplificar solicitações de CRUD e muito mais. A maioria dos serviços de API da Platform tem coleções do Postman que podem ser usadas para ajudar a fazer chamadas de API.

## Como configurar um ambiente Postman para o Experience Platform

O guia de vídeo a seguir descreve a criação e a configuração do ambiente Postman. Um ambiente Postman contém todos os cabeçalhos necessários para fazer chamadas de API para as várias coleções fornecidas abaixo. Depois de configurado, sempre que um valor expirar (como um `ACCESS_TOKEN`) é possível atualizar o valor atual no ambiente e esse novo valor é usado em todas as suas coleções.

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Coleções de carteiro {#collections}

Uma pasta contendo todas as coleções disponíveis do Postman pode ser encontrada ao acessar o [Repositório GitHub de amostras do Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Como alternativa, um link de coleção do Postman pode ser encontrado em cada arquivo de swagger individual na variável [Documentação de referência da API](https://www.adobe.com/go/platform-api-reference-en) na Adobe I/O.

Para baixar uma coleção do Postman, selecione **[!DNL Raw]** na página GitHub para carregar o arquivo JSON bruto em uma nova guia. Em seguida, clique com o botão direito do mouse e selecione **[!DNL Save as]** para salvar o arquivo em um destino local de sua escolha.

![JSON bruto](./images/api-guide/raw-collection.PNG)

## Importar uma coleção do Postman {#import}

Para utilizar um [Coleção Postman](#collections), é necessário ter um ambiente configurado. Depois de concluir a configuração do ambiente, selecione o **[!DNL Manage Environments]** no canto superior direito.

![gerenciar seletor de ambiente](./images/api-guide/environment-selector.png)

Um fornecedor é exibido e exibe todos os seus ambientes atuais. Para importar uma coleção, selecione **[!DNL import]** .

![botão importar](./images/api-guide/import-collection.png)

Você deve escolher um arquivo para importar. Selecione o arquivo de coleção do Postman que deseja importar. Depois de selecionada, a coleção é preenchida no painel à esquerda, na guia Collections .

![coleção preenchida](./images/api-guide/imported-collection.png)

Cada coleção tem pares de valores chave diferentes que podem ser necessários para executar uma operação CRUD bem-sucedida. Revise os [Guia do desenvolvedor de API](api-guide.md#api-guides) para saber mais sobre os valores obrigatórios, dicas e ver exemplos.

Para saber mais sobre a interface do usuário do Postman e seus recursos disponíveis, visite o [Documentação do Postman](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Gerar um token de acesso com o Postman para uso não relacionado à produção

>[!WARNING]
>
>Conforme observado na coleção Postman da geração de token de acesso ao Adobe I/O, os métodos de geração indicados são adequados para **uso não relacionado à produção**. A assinatura local carrega uma biblioteca do JavaScript de um host de terceiros e a assinatura remota envia a chave privada para um serviço da Web que é de propriedade e operado pelo Adobe. Embora o Adobe não armazene essa chave privada, as chaves de produção nunca devem ser compartilhadas com ninguém.

O vídeo abaixo usa a variável [Coleção de geração de token de acesso ao Adobe I/O](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Adobe%20IO%20Access%20Token%20Generation.postman_collection.json) que podem ser baixadas do repositório público do GitHub.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## Próximas etapas

Este documento apresentou ambientes Postman, coleções e como importar coleções. Agora que o Postman está pronto, visite o [Guia de introdução à plataforma](api-guide.md) para obter informações sobre cabeçalhos obrigatórios, exemplos e uma lista de [Guias da API](api-guide.md#api-guides) disponível para cada serviço da plataforma.
