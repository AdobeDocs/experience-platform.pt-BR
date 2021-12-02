---
title: Bibliotecas de auto-hospedagem
description: Saiba como implementar a auto-hospedagem para seus builds de biblioteca de tags na Adobe Experience Platform.
exl-id: 8c3bf202-de7a-46e0-801f-0cede24865fd
source-git-commit: 91b28fc284344b42020b0e49b64ac023e492d572
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 96%

---

# Bibliotecas de auto-hospedagem

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

As tags na Adobe Experience Platform permitem a produção de um conjunto de arquivos chamado [build](../builds.md). Esse conjunto de arquivos controla o comportamento do aplicativo no tempo de execução.

As criações precisam ser hospedadas em algum lugar para que os dispositivos cliente possam recuperá-las no tempo de execução, conforme necessário.

O Platform pode gerenciar a hospedagem desses arquivos para você ou você mesmo pode fazer isso.

## Administrado pela Adobe {#managed-by-adobe}

A Adobe não está no ramo de hospedagem na Web. Se optar que a Adobe gerencie a hospedagem, suas criações serão entregues a uma rede de entrega de conteúdo de terceiros (CDN) com a qual possui um contrato.

No momento, o provedor principal de CDN é o Akamai. Os arquivos hospedados na Akamai têm como domínio `assets.adobedtm.com`. 

### Por que usar a hospedagem gerenciada?

O motivo principal para usar a hospedagem gerenciada é conveniência. É mais fácil criar o host necessário e não precisar se preocupar com a manutenção.

## Auto-hospedagem

Se não quiser que a Adobe gerencie seus arquivos hospedados, você mesmo deve hospedá-los. Para hospedar os arquivos, você precisa obter os builds concluídos da Platform e ser responsável por incluir os arquivos por meio do ciclo de lançamento da empresa nos servidores gerenciados por ela.

### Por que usar a auto-hospedagem?

Há vários motivos para optar por hospedar seus próprios arquivos de criação.

* Alguns navegadores bloqueiam o domínio assets.adobedtm.com de acordo com as configurações de privacidade do usuário final
* A auto-hospedagem reduz o número necessário de pesquisas de DNS
* Você tem cabeçalhos específicos que devem ser definidos para segurança
* Seus requisitos de controle de cache são diferentes das configurações padrão da Adobe
* Você deseja ter mais controle sobre a localização dos nós de borda
* Sua organização tem requisitos legais e de segurança que impedem o uso da opção gerenciada pela Adobe

### Como hospedar automaticamente

Há dois métodos que podem ser usados para adquirir criações concluídas para que você possa hospedar automaticamente.

* Baixar
* Entrega direta

#### Baixar

Os builds podem ser entregues como um arquivo .zip empacotado (criptografia opcional). Você pode descompactar o pacote e inserir o conteúdo no ciclo de lançamento para colocá-lo em seus próprios servidores.

Use um host [Gerenciado pela Adobe](self-hosting-libraries.md) e selecione a opção [Arquivamento](../environments.md) em seu ambiente. O ambiente fornece um link de download. Sempre que ocorrer uma criação, é possível recuperá-la usando o link de download do ambiente.

#### Entrega direta

Os builds também podem ser entregues diretamente a um servidor SFTP criado por você. Você assume a responsabilidade de arquivá-las no ciclo de lançamento e enviá-las ativamente.

Para realizar uma entrega direta, você deve criar um [host SFTP](sftp-host.md) e atribuir esse host ao seu ambiente. Sempre que você cria uma biblioteca nesse ambiente, os arquivos são entregues para o servidor SFTP.
