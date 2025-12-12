---
title: Visão geral dos hosts gerenciados pela Adobe
description: Saiba mais sobre a opção de hospedagem padrão para implantar builds de biblioteca de tags na Adobe Experience Platform.
exl-id: 9042c313-b0d3-4f6e-963d-0051d760fd16
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 82%

---

# Visão geral dos hosts gerenciados pela Adobe

Hosts gerenciados pela Adobe são a configuração padrão do host para implantar builds de biblioteca de tags na Adobe Experience Platform. Quando você cria uma nova propriedade por meio da interface da coleção de dados, um host padrão gerenciado pela Adobe é criado para você.

Com hosts gerenciados pela Adobe, as builds de bibliotecas são entregues a uma rede de entrega de conteúdo (CDN) de terceiros pela qual a Adobe foi contratada. Essas CDNs operam independentemente da Adobe, de modo que, mesmo quando o Experience Platform estiver em manutenção ou estiver inativo, o código implantado continuará funcionando normalmente em seus sites e aplicativos. O código incorporado de um host gerenciado pela Adobe faz referência ao arquivo da biblioteca principal na CDN, para que um dispositivo cliente possa recuperar os arquivos no tempo de execução.

Este documento fornece uma visão geral dos hosts gerenciados pela Adobe no Experience Platform e fornece etapas sobre como criar um novo host gerenciado pela Adobe na interface do usuário.

## Akamai

Atualmente, o principal provedor de CDN da Adobe é o [Akamai](https://www.akamai.com/br/pt/). A CDN robusta da Akamai foi criada para fornecer conteúdo a um público-alvo global de alto volume de visitantes da Web. A CDN executa redes redundantes de nós otimizados geograficamente e com balanceamento de carga, a fim de fornecer conteúdo o mais rápido possível para visitantes localizados em todo o mundo.

Especificamente, a Akamai executa mais de 137.000 servidores em 87 países em mais de 1.150 redes. Em termos de redundância, a CDN não apenas roteia de um servidor para outro, mas também pode rotear de um nó de servidores para outro, conforme necessário. Em outras palavras, cada nó consiste em vários servidores, de modo que um servidor inativo nunca se torna um problema, pois os outros servidores no mesmo nó podem assumir o controle.

Se um nó inteiro ficar inativo, o Akamai servirá por meio do nó mais próximo com o mesmo conteúdo em cache. Os nós são selecionados dinamicamente com base na localização do visitante, na carga de tráfego e em outros fatores, de modo que o conteúdo é veiculado consistentemente a partir do melhor nó local de cada visitante.

Os arquivos hospedados na Akamai têm como domínio `assets.adobedtm.com`. Ele pode ser referenciado com segurança ou não (`http://` ou `https://`) com base em como é chamado dentro do seu código `<script>` integrado.

>[!WARNING]
>
>Se sua biblioteca não estiver disponível na rede Akamai, o Experience Platform não poderá impedir possíveis erros que possam surgir.

## Armazenamento em cache de build de biblioteca

Ao usar hosts gerenciados pela Adobe, as builds de biblioteca são armazenadas em cache em dois locais:

* [Armazenamento em cache de borda](#edge)
* [Armazenamento em cache do navegador](#browser)

### Armazenamento em cache de borda {#edge}

O objetivo principal de uma CDN é distribuir de forma inteligente o conteúdo para servidores geograficamente mais próximos dos usuários finais, para que ele possa ser recuperado mais rapidamente pelos dispositivos dos clientes. As CDNs fazem isso disponibilizando cópias do conteúdo em servidores distribuídos geograficamente ao redor do mundo (&quot;nós de borda&quot;).

Depois que a build for implantada no host gerenciado pelo Adobe, a CDN distribuirá a build em vários servidores centralizados (&quot;origem&quot;), que, em seguida, enviará cópias da build para vários nós de borda diferentes no mundo inteiro para armazenamento em cache. As versões em cache da build armazenada nesses nós de borda são, em seguida, fornecidas aos dispositivos clientes.

![](../images/cdn-diagram.png)

>[!NOTE]
>
>Para hosts gerenciados pela Adobe, a primeira biblioteca publicada em qualquer novo ambiente pode levar até cinco minutos para se propagar para a CDN global.

Quando um nó de borda recebe uma solicitação de um arquivo específico (como a build de biblioteca), o nó verifica primeiro a hora de expiração no arquivo. Se o tempo não tiver expirado, o nó de borda fornecerá a versão em cache. Se o tempo tiver expirado, o nó de borda solicitará uma nova cópia da origem mais próxima, enviará essa cópia atualizada e a armazenará em cache com um novo tempo de expiração.

>[!NOTE]
>
>Além do armazenamento em cache de nós de borda, também pode haver redes intermediárias (como redes corporativas ou móveis) que executam seu próprio armazenamento em cache. Se suas builds não estiverem sendo armazenadas em cache como esperado, essas redes podem ser a causa subjacente.

#### Invalidação do armazenamento em cache de borda {#invalidation}

Quando você carrega um novo build de biblioteca, os caches em todos os nós de borda aplicáveis são invalidados. Isso significa que cada nó considera sua versão em cache inválida, independentemente de quando ele recuperou uma nova cópia recentemente. Na próxima vez que um nó de borda receber uma solicitação para esse arquivo, ele recuperará uma cópia nova da origem.

Como o Akamai tem vários servidores de origem que replicam arquivos entre si e não há como saber qual origem recebeu seu arquivo primeiro, é possível que essas novas solicitações de nós acessem uma origem que não tenha a versão mais recente. Em seguida, ele armazenaria a versão mais antiga em cache novamente. Para evitar que isso ocorra, várias invalidações de cache são executadas para cada novo build nos seguintes intervalos:

* Imediatamente após o upload
* 5 minutos após o upload
* 60 minutos após o upload

Essas invalidações de cache escalonadas dão aos grupos de servidores de origem tempo para replicar a versão mais recente do arquivo entre si, para que todos tenham a versão mais recente quando o arquivo for recuperado.

### Armazenamento em cache do navegador {#browser}

As builds de biblioteca também são armazenadas em cache no navegador por meio do uso do cabeçalho HTTP `cache-control`. Ao usar hosts gerenciados pela Adobe, você não tem controle sobre os cabeçalhos retornados nas respostas da API, portanto, o padrão da Adobe para cache é usado. Em outras palavras, não é possível utilizar cabeçalhos personalizados para hosts gerenciados pela Adobe. Se precisar de um cabeçalho `cache-control` personalizado, talvez você queira considerar a hospedagem [automática](self-hosting-libraries.md).

O tempo de expiração da build de biblioteca em cache do navegador (determinado pelo cabeçalho `cache-control`) varia de acordo com o ambiente de tag que você está usando:

| Ambiente | Valor de `cache-control` |
| --- | --- |
| Desenvolvimento | `max-age=0, no-cache, no-store` |
| Armazenamento temporário | `max-age=0, no-cache, no-store` |
| Produção | `max-age=3600` |

Como a tabela acima indica, o armazenamento em cache do navegador não é compatível com ambientes de preparo e desenvolvimento. Dessa forma, você não deve usar os códigos incorporados de desenvolvimento ou armazenamento temporário em contextos de alto tráfego ou produção.

Os cabeçalhos de controle de cache são aplicados apenas ao build da biblioteca principal. Todos os sub-recursos abaixo da biblioteca principal são sempre considerados novos e, portanto, não há necessidade de armazená-los em cache no navegador.

## Usar a hospedagem gerenciada pela Adobe na interface

Ao criar uma propriedade na interface do usuário do Experience Platform ou na interface da Coleção de dados pela primeira vez, um host gerenciado pela Adobe é automaticamente criado para você. Todos os ambientes disponíveis que têm propriedades imediatamente utilizáveis também são atribuídos ao host gerenciado pela Adobe por padrão.

>[!NOTE]
>
>Se o host padrão gerenciado pela Adobe não for desatribuído de todos os ambientes, o host poderá ser excluído. Se você quiser voltar para um host gerenciado pela Adobe depois de fazer isso, crie um novo host através das seguintes etapas:
>
>1. Selecione a guia **[!UICONTROL Hosts]** em sua propriedade e, em seguida, selecione **[!UICONTROL Add Host]**.
>1. Forneça um nome para o host, selecione **[!UICONTROL Managed by Adobe]** como o tipo de host e selecione **[!UICONTROL Save]**.
>
>Em seguida, é possível atribuir novamente seus ambientes ao host gerenciado pela Adobe, conforme desejado.

## Próximas etapas

Este documento forneceu uma visão geral da hospedagem gerenciada pela Adobe para bibliotecas de tags na Adobe Experience Platform. Para obter informações sobre outras opções de hospedagem, consulte a seguinte documentação:

* [Hospedagem SFTP](./sftp-host.md)
* [Bibliotecas de auto-hospedagem](./self-hosting-libraries.md)

Para obter detalhes sobre como gerenciar hosts para seus ambientes, consulte o [guia ambientes](../environments.md).
