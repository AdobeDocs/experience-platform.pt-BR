---
keywords: Experience Platform;página inicial;tópicos populares;Adobe Experience Platform;guia de api;guia de api da plataforma;introdução à plataforma;guia do desenvolvedor
solution: Experience Platform
title: Postman no Adobe Experience Platform
description: Este documento contém etapas que descrevem como configurar um ambiente do Postman, importar coleções do Postman e uma lista de coleções disponíveis para cada serviço da Platform.
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---

# Postman no Adobe Experience Platform

O Postman é uma plataforma de colaboração para o desenvolvimento de API que permite configurar ambientes com variáveis predefinidas, compartilhar coleções de API, simplificar solicitações CRUD e muito mais. A maioria dos serviços de API da Platform tem coleções do Postman que podem ser usadas para ajudar a fazer chamadas de API.

## Como configurar um ambiente do Postman para o Experience Platform

O guia de vídeo a seguir descreve a criação e a configuração do ambiente do Postman. Um ambiente do Postman contém todos os cabeçalhos necessários para fazer chamadas de API para as várias coleções fornecidas abaixo. Uma vez configurado, sempre que um valor expirar (como uma variável `ACCESS_TOKEN`), você pode atualizar o valor atual no ambiente e esse novo valor será usado em todas as suas coleções.

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## coleções do Postman {#collections}

Uma pasta contendo todas as coleções disponíveis do Postman pode ser encontrada ao visitar o [Repositório GitHub de amostras do Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Como alternativa, um link de coleção do Postman pode ser encontrado em cada arquivo swagger individual no [Documentação de referência da API](https://www.adobe.com/go/platform-api-reference-en) no Adobe I/O.

Para baixar uma coleção do Postman, selecione **[!DNL Raw]** na página GitHub para carregar o arquivo JSON bruto em uma nova guia. Em seguida, clique com o botão direito e selecione **[!DNL Save as]** para salvar o arquivo em um destino local de sua escolha.

![JSON bruto](./images/api-guide/raw-collection.PNG)

## Importar uma coleção do Postman {#import}

A fim de utilizar um [Coleção Postman](#collections), é necessário configurar um ambiente. Após concluir a configuração do ambiente, selecione a opção **[!DNL Manage Environments]** no canto superior direito.

![gerenciar seletor de ambiente](./images/api-guide/environment-selector.png)

Um popover é exibido e exibe todos os seus ambientes atuais. Para importar uma coleção, selecione **[!DNL import]** .

![botão importar](./images/api-guide/import-collection.png)

Você será solicitado a escolher um arquivo para importar. Selecione o arquivo de coleção do Postman que deseja importar. Depois de selecionada, a coleção é preenchida no painel à esquerda na guia Coleções.

![coleção preenchida](./images/api-guide/imported-collection.png)

Cada coleção tem pares de chave-valor diferentes que podem ser necessários para executar uma operação CRUD bem-sucedida. Examine o nome do serviço [Guia do desenvolvedor de API](api-guide.md#api-guides) para saber mais sobre os valores, dicas e exemplos necessários.

Para saber mais sobre a interface do usuário do Postman e seus recursos disponíveis, visite o [Documentação do Postman](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Gerar um token de acesso com o Postman para uso de não produção

>[!WARNING]
>
>Conforme observado na coleção Postman do Identity Management Service (IMS), os métodos de geração indicados são adequados para **uso não relacionado à produção**. A assinatura local carrega uma biblioteca JavaScript de um host de terceiros e a assinatura remota envia a chave privada para um serviço da Web que pertence e é operado pelo Adobe. Embora o Adobe não armazene essa chave privada, as chaves de produção nunca devem ser compartilhadas com ninguém.

O vídeo abaixo usa o [Coleção Postman do Identity Management Service (IMS)](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) que pode ser baixado do repositório público do GitHub.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## Próximas etapas

Esse documento apresentou ambientes do Postman, coleções e como importar coleções. Agora que o Postman está pronto, visite o [Guia de introdução à Platform](api-guide.md) para obter informações sobre cabeçalhos, exemplos e uma lista de [Guias da API](api-guide.md#api-guides) disponível para cada serviço da Platform.
