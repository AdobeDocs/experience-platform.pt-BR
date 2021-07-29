---
title: Visão geral dos hosts gerenciados pela Adobe
description: Saiba mais sobre a opção de hospedagem padrão para implantar builds de bibliotecas de tags no Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 65%

---

# Visão geral dos hosts gerenciados pela Adobe

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Hosts gerenciados pelo Adobe são a configuração padrão do host para implantar builds de biblioteca de tags no Adobe Experience Platform. Ao criar uma nova propriedade por meio da interface do usuário da Coleta de dados, um host padrão gerenciado por Adobe é criado para você.

Com hosts gerenciados pela Adobe, as builds de bibliotecas são entregues a uma rede de delivery de conteúdo de terceiros (CDN) pela qual a Adobe foi contratada. Essas CDNs operam independentemente da Adobe, de modo que, mesmo quando o Platform estiver em manutenção ou estiver inativo, o código implantado continuará funcionando normalmente em seus sites e aplicativos. O código incorporado de um host gerenciado pela Adobe faz referência ao arquivo da biblioteca principal na CDN, para que um dispositivo cliente possa recuperar os arquivos no tempo de execução.

Este documento fornece uma visão geral dos hosts gerenciados pelo Adobe na plataforma e fornece etapas sobre como criar um novo host gerenciado pelo Adobe na interface do usuário.

## Akamai

Atualmente, o principal provedor de CDN da Adobe é o [Akamai](https://www.akamai.com/br/pt/). A CDN robusta da Akamai foi criada para fornecer conteúdo a um público-alvo global de alto volume de visitantes da Web. A CDN executa redes redundantes de nós otimizados geograficamente e com balanceamento de carga, a fim de fornecer conteúdo o mais rápido possível para visitantes localizados em todo o mundo.

Especificamente, a Akamai executa mais de 137.000 servidores em 87 países em mais de 1.150 redes. Em termos de redundância, a CDN não apenas roteia de um servidor para outro, mas também pode rotear de um nó de servidores para outro nó de servidores, conforme necessário. Em outras palavras, cada nó consiste em vários servidores, de modo que um servidor inativo nunca se torna um problema, pois os outros servidores no mesmo nó podem assumir o controle.

Se um nó inteiro ficar inativo, o Akamai servirá o nó mais próximo com o mesmo conteúdo em cache. Os nós são selecionados dinamicamente com base na localização do visitante, na carga de tráfego e em outros fatores, de modo que o conteúdo é veiculado consistentemente a partir do melhor nó local de cada visitante.

Os arquivos hospedados na Akamai têm como domínio `assets.adobedtm.com`. Ele pode ser referenciado com segurança ou não (`http://` ou `https://`) com base em como é chamado dentro do seu código `<script>` integrado.

>[!WARNING]
>
>Se sua biblioteca não estiver disponível na rede Akamai, o Platform não poderá impedir possíveis erros que possam surgir.

## Armazenamento em cache de build de biblioteca

Ao usar hosts gerenciados pela Adobe, as builds de biblioteca são armazenadas em cache em dois locais:

* [Armazenamento em cache de borda](#edge)
* [Armazenamento em cache do navegador](#browser)

### Armazenamento em cache de borda {#edge}

O objetivo principal de uma CDN é distribuir de forma inteligente o conteúdo para servidores geograficamente mais próximos dos usuários finais, para que o conteúdo possa ser recuperado mais rapidamente pelos dispositivos clientes. As CDNs fazem isso disponibilizando cópias do conteúdo em servidores distribuídos geograficamente ao redor do mundo (&quot;nós de borda&quot;).

Depois que a build for implantada no host gerenciado pelo Adobe, a CDN distribuirá a build em vários servidores centralizados (&quot;origem&quot;), que, em seguida, enviará cópias da build para vários nós de borda diferentes no mundo inteiro para armazenamento em cache. As versões em cache da build armazenada nesses nós de borda são, em seguida, fornecidas aos dispositivos clientes.

![](../images/cdn-diagram.png)

>[!NOTE]
>
>Para hosts gerenciados pela Adobe, a primeira biblioteca publicada em qualquer novo ambiente pode levar até cinco minutos para se propagar para a CDN global.

Quando um nó de borda recebe uma solicitação de um arquivo específico (como a build de biblioteca), o nó verifica primeiro o valor de TTL (time-to-live) no arquivo. Se o TTL não tiver expirado, o nó de borda fornecerá a versão em cache. Se o TTL tiver expirado, o nó de borda solicita uma nova cópia da origem mais próxima, fornece essa cópia atualizada e, a seguir, armazena em cache a cópia atualizada com um novo TTL.

>[!NOTE]
>
>Além do armazenamento em cache de nós de borda, também pode haver redes intermediárias (como redes corporativas ou móveis) que executam seu próprio armazenamento em cache. Se suas builds não estiverem sendo armazenadas em cache como esperado, essas redes podem ser a causa subjacente.

#### Invalidação do armazenamento em cache de borda {#invalidation}

Ao carregar uma nova build de biblioteca, os caches em todos os nós de borda aplicáveis são invalidados. Isso significa que cada nó considera sua versão em cache inválida, independentemente de quando ele recuperou uma nova cópia recentemente. Na próxima vez que um nó de borda receber uma solicitação para esse arquivo, ele recuperará uma cópia nova da origem.

Como a Akamai tem vários servidores de origem que replicam arquivos entre si, e como não há como saber qual origem recebeu seu arquivo primeiro, essas solicitações de nó podem atingir uma origem que não tem a versão mais recente. Em seguida, ele armazenaria a versão mais antiga em cache novamente. Para evitar que isso ocorra, várias invalidações de cache são executadas para cada nova build nos seguintes intervalos:

* Imediatamente após o upload
* 5 minutos após o upload
* 60 minutos após o upload

Essas invalidações de cache escalonadas dão aos grupos de servidores de origem tempo para replicar a versão mais recente do arquivo entre si, para que todos tenham a versão mais recente quando o arquivo for recuperado.

### Armazenamento em cache do navegador {#browser}

As builds de biblioteca também são armazenadas em cache no navegador por meio do uso do cabeçalho HTTP `cache-control`. Ao usar hosts gerenciados pela Adobe, você não tem controle sobre os cabeçalhos retornados nas respostas da API, portanto, o padrão da Adobe para cache é usado. Em outras palavras, não é possível utilizar cabeçalhos personalizados para hosts gerenciados pela Adobe. Se precisar de um cabeçalho `cache-control` personalizado, talvez você queira considerar a hospedagem [automática](self-hosting-libraries.md).

O TTL (time-to-live) da build de biblioteca em cache do navegador (determinado pelo cabeçalho `cache-control`) varia de acordo com o ambiente de tags que você está usando:

| Ambiente | Valor de `cache-control` |
| --- | --- |
| Desenvolvimento | `max-age=0, no-cache, no-store` |
| Armazenamento temporário | `max-age=0, no-cache, no-store` |
| Produção | `max-age=3600` |

Como a tabela acima indica, o armazenamento em cache do navegador não é compatível com ambientes de preparo e desenvolvimento. Dessa forma, você não deve usar os códigos integrados de desenvolvimento ou armazenamento temporário em contextos de alto tráfego ou produção.

Os cabeçalhos de controle de cache são aplicados apenas à build da biblioteca principal. Todos os sub-recursos abaixo da biblioteca principal são sempre considerados novos e, portanto, não há necessidade de armazená-los em cache no navegador.

## Usar a hospedagem gerenciada por Adobe na interface do usuário da coleta de dados

Quando você cria uma propriedade na [Interface do usuário da coleta de dados](https://experience.adobe.com/#/data-collection/) pela primeira vez, um host gerenciado pelo Adobe é automaticamente criado para você. Todos os ambientes disponíveis que têm propriedades imediatamente utilizáveis também são atribuídos ao host gerenciado pelo Adobe por padrão.

>[!NOTE]
>
>Se o host padrão gerenciado pela Adobe não for desatribuído de todos os ambientes, o host poderá ser excluído. Se você quiser voltar para um host gerenciado pela Adobe depois de fazer isso, crie um novo host através das seguintes etapas:
>
>1. Selecione a guia **[!UICONTROL Hosts]** na propriedade e selecione **[!UICONTROL Adicionar host]**.
>1. Forneça um nome para o host, selecione **[!UICONTROL Gerenciado pela Adobe]** como tipo de host e selecione **[!UICONTROL Salvar]**.

>
>
Em seguida, é possível atribuir novamente seus ambientes ao host gerenciado pela Adobe, conforme desejado.

## Próximas etapas

Este documento forneceu uma visão geral da hospedagem gerenciada pelo Adobe para bibliotecas de tags no Adobe Experience Platform. Para obter informações sobre outras opções de hospedagem, consulte a seguinte documentação:

* [Hospedagem SFTP](./sftp-host.md)
* [Bibliotecas de auto-hospedagem](./self-hosting-libraries.md)

Para obter detalhes sobre como gerenciar hosts para seus ambientes, consulte o [guia ambientes](../environments.md).
