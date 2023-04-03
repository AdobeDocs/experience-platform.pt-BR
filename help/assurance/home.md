---
title: Visão geral do Adobe Experience Platform Assurance
description: O Adobe Experience Platform Assurance permite inspecionar, testar, simular e validar como você coleta dados ou veicula experiências em seus aplicativos móveis.
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 2%

---


# Adobe Experience Platform Assurance

O Adobe Experience Platform Assurance é um produto de [Adobe Experience Cloud](https://www.adobe.com/br/experience-cloud.html) para ajudá-lo a inspecionar, testar, simular e validar o modo como você coleta dados ou veicula experiências em seu aplicativo móvel.

>[!IMPORTANT]
>
> O Projeto Griffon é agora conhecido como **Controle**!
>
> O Projeto Griffon está agora disponível no geral para **all** Clientes Adobe Experience Cloud como Controle. Para saber mais sobre essa transição, leia o [guia de acesso do usuário](./user-access.md).

>[!INFO]
>
>As APIs públicas de garantia estão disponíveis!
>
>[As APIs de garantia](https://developer.adobe.com/adobe-assurance-public-apis/) são uma coleção de APIs que capacitam os usuários a testar e depurar aplicativos móveis e da Web, quando equipados com o SDK móvel do Adobe Assurance.

## Disponibilidade geral

A partir de 15 de outubro de 2022, o Assurance estará disponível em geral em toda a Adobe Experience Cloud.

### O que está mudando?

Em 15 de outubro - o acesso ao Assurance será gerenciado por meio do Admin Console. Leia o [guia de acesso do usuário](./user-access.md) para garantir que você continue a ter acesso ininterrupto.

Nenhuma outra alteração ou interrupção é esperada para integrações, sessões e eventos do Assurance existentes. O controlo pode continuar a ser acessado via [https://griffon.adobe.com](https://griffon.adobe.com) **ou** você pode usar (e marcador) [https://experience.adobe.com/assurance](https://experience.adobe.com/assurance).

## O que a garantia pode fazer por você?

### Configuração rápida

Comece com pressa com poucas linhas de código. Para aplicativos móveis, o Assurance funciona com o SDK do Adobe Experience Platform Mobile para ajudá-lo a inspecionar, simular e validar eventos de aplicativos, sinais de localização, parâmetros de configuração, logs SDK, informações do dispositivo e muito mais.

### Conexão sem complicações

Com o Assurance, conectar seu aplicativo com a Platform é simples e confiável. Você não precisa usar proxies de rede, [MiTM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)) e outras ginásticas de rede - conectar seu aplicativo ao Controle é tão fácil quanto verificar um código QR ou tocar em um botão.

![](./images/index/no-hassle-connection.png)

### Inspeção, simulação e validação em tempo real

Após se conectar ao Controle de qualidade, você pode inspecionar os eventos e atividades do aplicativo transmitidos ao vivo, filtrar e pesquisar para eliminar o ruído. Os eventos contêm detalhes sobre a validação, depuração e solução de problemas da implementação do aplicativo móvel. O Controle de qualidade também permite capturar a tela, simular sinais de localização e muito mais em tempo real.

![](./images/index/real-time-insepction.png)

### Integração com a Adobe Experience Cloud

Os dados e experiências do lado do cliente recebem o contexto de como os usuários configuram regras de relatórios, atividades e campanhas em nossas interfaces de usuário focadas no profissional de marketing. Para ajudá-lo a conectar os pontos entre os dois, estamos integrando com soluções da Adobe Experience Cloud, como Adobe Experience Platform, Adobe Analytics, Adobe Target, Places Service e muito mais.

![](./images/index/integration.png)

## Recursos

### Eventos, registros e muito mais do SDK do Adobe Experience Platform Mobile

O Assurance ajuda a inspecionar eventos brutos do SDK gerados pelo SDK do Adobe Experience Platform Mobile. Todos os eventos coletados pelo SDK estão disponíveis para inspeção. Os eventos do SDK são carregados em uma exibição de lista, classificados por tempo. Cada evento tem uma exibição detalhada que fornece mais detalhes. Também são fornecidas exibições adicionais para navegar pela configuração do SDK, Elementos de dados, Estados compartilhados e versões de extensão do SDK.

### Adobe Analytics

A exibição Adobe Analytics > Eventos do Analytics é uma exibição focalizada que mostra eventos relacionados à implementação móvel do Adobe Analytics. A exibição de lista mostra o ciclo de vida ou os eventos de ação/estado, o &quot;status&quot; pós-processado, juntamente com os detalhes do evento necessários em uma exibição especialmente formatada. O status pós-processado mostra como o evento foi processado pelo Adobe Analytics depois que as regras de processamento foram aplicadas ao evento.

### Adobe Analytics para mídia de streaming

A exibição Adobe Analytics > Eventos do Media Analytics mostra eventos para a implementação da análise de áudio e vídeo. A exibição detalhada dos eventos mostra metadados padrão e personalizados que são rastreados para cada sessão de reprodução. Além disso, é possível visualizar o status pós-processado e os dados de análise de mídia pós-processada, como o tempo gasto na mídia ou a duração total do buffer.

### Places (Serviços de localização)

A exibição Serviços de localização é uma exibição no dispositivo que mostra a entrada do local do usuário e os eventos de saída para facilitar a validação. Essa visualização útil fornece uma interface conveniente para visualizar pontos de dados específicos de localização para inspeção no cliente para depuração no contexto.

## O Controle está seguro?

A garantia tem as seguintes medidas de segurança em vigor:

* O Assurance e a interface de usuário da Web Assurance têm um handshake seguro, baseado em PIN, para uma conexão. O usuário precisa criar um handshake explicitamente, o que impede que conexões de garantia &quot;acidentais&quot; sejam criadas por um usuário final.
* Somente as conexões entre o Assurance e a interface da Web do Assurance pertencentes à mesma ID da organização da Adobe Experience Cloud são compatíveis.
* Os eventos de SDKs do Adobe Experience Platform Mobile são transportados por HTTPS.
* Os SDKs do Assurance e do Adobe Experience Platform Mobile usam TLS 1.2
* As sessões de garantia são excluídas após 30 dias.
* Os dados da sessão de garantia são criptografados em repouso, seguindo as práticas recomendadas de armazenamento.

## Introdução

Para configurar o Assurance, primeiro você precisará instalar a extensão Assurance em seu aplicativo. Para saber como fazer isso, leia o tutorial em [implementação da extensão Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

Depois de adicionar o Controle ao seu aplicativo, você pode criar uma sessão de Controle que pode ser conectada ao seu dispositivo. Para saber como usar o Controle de qualidade, leia o [guia sobre a utilização do Assurance](./tutorials/using-assurance.md).
