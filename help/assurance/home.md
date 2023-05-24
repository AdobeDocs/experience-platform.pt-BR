---
title: Visão geral do Adobe Experience Platform Assurance
description: O Adobe Experience Platform Assurance permite inspecionar, testar, simular e validar como você coleta dados ou veicula experiências em seus aplicativos móveis.
exl-id: e887f5f6-3db0-4521-be2d-20ef3d08e7d0
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 5%

---

# Adobe Experience Platform Assurance

O Adobe Experience Platform Assurance é um produto da [Adobe Experience Cloud](https://www.adobe.com/br/experience-cloud.html) para ajudá-lo a inspecionar, testar, simular e validar a maneira como você coleta dados ou fornece experiências em seu aplicativo móvel.

>[!IMPORTANT]
>
> O projeto Griffon agora é conhecido como **Assurance**!
>
> O projeto Griffon agora está disponível para o **all** Clientes da Adobe Experience Cloud como Assurance. Para saber mais sobre essa transição, leia o [guia de acesso do usuário](./user-access.md).

>[!INFO]
>
>As APIs públicas do Assurance estão disponíveis!
>
>[As APIs do Assurance](https://developer.adobe.com/adobe-assurance-public-apis/) são uma coleção de APIs que capacitam os usuários a testar e depurar seus aplicativos da Web e móveis, quando equipados com o SDK móvel do Adobe Assurance.

## Disponibilidade geral

A partir de 15 de outubro de 2022, o Assurance estará disponível para todas as soluções da Adobe Experience Cloud.

### O que está mudando?

No dia 15 de outubro - o acesso ao Assurance será gerenciado pelo Admin Console. Leia as [guia de acesso do usuário](./user-access.md) para garantir acesso ininterrupto.

Não são esperadas outras alterações ou interrupções nas integrações, sessões e eventos existentes do Assurance. O acesso ao Assurance pode continuar via [https://griffon.adobe.com](https://griffon.adobe.com) **ou** você pode usar (e marcador) [https://experience.adobe.com/assurance](https://experience.adobe.com/assurance).

## O que o Assurance pode fazer por você?

### Configuração rápida

Comece rápido com poucas linhas de código. Para aplicativos móveis, o Assurance funciona com o SDK móvel da Adobe Experience Platform para ajudar você a inspecionar, simular e validar eventos de aplicativo, sinais de localização, parâmetros de configuração, logs de SDK, informações de dispositivo e muito mais.

### Conexão sem problemas

Com o Assurance, conectar seu aplicativo à Platform é simples e confiável. Você não precisa usar proxies de rede, [MiTM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)) e outras ginásticas de rede - conectar seu aplicativo ao Assurance é tão fácil quanto digitalizar um código QR ou tocar em um botão.

![](./images/index/no-hassle-connection.png)

### Inspeção, simulação e validação em tempo real

Depois de se conectar ao Assurance, você pode inspecionar eventos e atividades de aplicativos transmitidos ao vivo, filtrar e pesquisar para eliminar ruídos. Eventos contêm detalhes sobre validação, depuração e solução de problemas da implementação do aplicativo móvel. O Assurance também permite capturar a tela, simular sinais de localização e muito mais em tempo real.

![](./images/index/real-time-insepction.png)

### Integração com a Adobe Experience Cloud

Os dados e experiências do lado do cliente recebem contexto sobre como os usuários configuram regras de relatórios, atividades e campanhas em nossas interfaces de usuário focadas no profissional de marketing. Para ajudar você a conectar os pontos entre os dois, estamos integrando com soluções da Adobe Experience Cloud, como Adobe Experience Platform, Adobe Analytics, Adobe Target, Places Service e muito mais.

![](./images/index/integration.png)

## Recursos

### Eventos, logs e muito mais do SDK móvel da Adobe Experience Platform

O Assurance ajuda a inspecionar eventos brutos de SDK gerados pelo SDK móvel da Adobe Experience Platform. Todos os eventos coletados pelo SDK estão disponíveis para inspeção. Os eventos do SDK são carregados em uma exibição de lista, classificados por tempo. Cada evento tem uma exibição detalhada que fornece mais detalhes. Exibições adicionais para procurar a configuração do SDK, Elementos de dados, Estados compartilhados e versões de extensão do SDK também são fornecidas.

### Adobe Analytics

A visualização Adobe Analytics > Eventos do Analytics é uma visualização focada que mostra eventos relacionados à implementação móvel do Adobe Analytics. A exibição de lista mostra o ciclo de vida ou os eventos de ação/estado, o &quot;status&quot; pós-processado, juntamente com os detalhes do evento necessários em uma exibição formatada especialmente. O status Pós-processado mostra como o evento foi processado pelo Adobe Analytics após a aplicação das regras de processamento no evento.

### Adobe Analytics para mídia de streaming

A visualização Adobe Analytics > Eventos do Media Analytics mostra eventos para a implementação da análise de áudio e vídeo. A visualização detalhada dos eventos mostra metadados padrão e personalizados que são rastreados para cada sessão de reprodução. Além disso, é possível visualizar o status pós-processado e os dados de análise de mídia pós-processados, como o tempo gasto com a mídia ou a duração total do buffer.

### Places (Serviços de localização)

A exibição Serviços de localização é uma exibição no dispositivo que mostra os eventos de entrada e saída do local do usuário para facilitar a validação. Essa visualização útil fornece uma interface conveniente para visualizar pontos de dados específicos do local para inspeção no cliente para depuração no contexto.

## O Assurance é seguro?

O Assurance tem as seguintes medidas de segurança em vigor:

* O Assurance e a interface do usuário da Web do Assurance têm um handshake seguro, baseado em PIN para uma conexão. O usuário precisa criar explicitamente um handshake, o que impede que conexões &quot;acidentais&quot; do Assurance sejam criadas por um usuário final.
* Somente as conexões entre o Assurance e a Interface do usuário da Web do Assurance pertencentes à mesma Adobe Experience Cloud Organization ID são compatíveis.
* Os eventos do SDKs do Adobe Experience Platform Mobile são transportados por HTTPS.
* Os SDKs móveis do Assurance e Adobe Experience Platform usam TLS 1.2
* As sessões do Assurance são excluídas após 30 dias.
* Os dados da sessão de garantia são criptografados em repouso, seguindo as práticas recomendadas de armazenamento.

## Introdução

Para configurar o Assurance, primeiro você precisará instalar a extensão do Assurance em seu aplicativo. Para aprender a fazer isso, leia o tutorial em [implementação da extensão do Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

Depois de adicionar o Assurance ao aplicativo, você pode criar uma sessão do Assurance que pode ser conectada ao dispositivo. Para saber como usar o Assurance, leia o [guia sobre como usar o Assurance](./tutorials/using-assurance.md).
