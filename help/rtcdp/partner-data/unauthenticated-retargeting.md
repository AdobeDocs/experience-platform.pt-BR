---
title: Redirecionamento não autenticado do lado do servidor
description: Saiba como redirecionar usuários não autenticados usando ECIDs
feature: Use Cases, Customer Acquisition
exl-id: 008f4534-29e7-49b9-b0be-9e0c3962ee21
source-git-commit: ba2154e84f24ddf4ec270121bdcbb6dd5d3dff42
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# Redirecionamento não autenticado do lado do servidor {#unauthenticated-retargeting}

À medida que os cookies de terceiros perdem a eficácia, as empresas estão fazendo a transição para soluções sem cookies para engajamento e redirecionamento personalizados. O redirecionamento externo permite que as empresas atinjam usuários de alto propósito com base em suas interações anteriores, sem depender do JavaScript do lado do cliente.

## Por que considerar redirecionar visitantes não autenticados {#why-use-case}

Ao integrar o Adobe Experience Platform Web SDK e o encaminhamento de eventos do lado do servidor, você pode simplificar a transmissão contínua de eventos e o encaminhamento de dados. Isso permite o redirecionamento perfeito de usuários não autenticados usando ECIDs (Experience Cloud IDs), garantindo um engajamento consistente em todas as plataformas. Com essa solução, você pode aumentar as oportunidades de conversão, redirecionando efetivamente usuários não autenticados com base em suas interações anteriores.

## Pré-requisitos e planejamento {#prerequisites-and-planning}

Antes de prosseguir com a implantação do Web SDK e a configuração do encaminhamento de eventos, verifique o seguinte:

1. **Configuração do Adobe com Web SDK**: o Adobe Web SDK deve ser implementado para facilitar a coleta de eventos e o encaminhamento de dados.

2. **Configuração do Adobe Experience Platform Edge Network**: verifique se o Edge Network está configurado para oferecer suporte ao encaminhamento de eventos em tempo real para redirecionamento externo.

3. **Sincronização de ECID**: verifique se as ECIDs estão sincronizadas entre as plataformas para habilitar a correspondência perfeita de público-alvo.

## Como obter redirecionamento externo {#achieve-offsite-retargeting}

1. **Implantar o Web SDK**: implemente o Adobe Web SDK no seu site para capturar dados de eventos em tempo real, incluindo interações de usuário, como exibições de página, cliques e outros comportamentos.

2. **Habilitar encaminhamento de eventos**: configure o encaminhamento de eventos na Platform para enviar dados do usuário coletados, garantindo uma transferência de dados eficiente para ativação de público-alvo.

3. **Configurar ativação do lado do servidor**: use os recursos do lado do servidor do Adobe para ativar públicos de redirecionamento com base em ECIDs, garantindo um direcionamento preciso de público em todas as plataformas.

4. **Criar públicos-alvo redirecionados**: utilize as ferramentas de segmentação de público da Platform para definir públicos-alvo focalizados com base no comportamento do usuário, como exibições, interações ou carrinhos abandonados.

5. **Ativar públicos-alvo**: depois que os públicos-alvo redirecionados forem criados, ative-os para fornecer conteúdo personalizado, garantindo que os usuários sejam reengajados com base em suas interações anteriores com o site.

## Criar um público-alvo usando o atributo calculado {#create-audience}

Para redirecionar efetivamente usuários de alta intenção, crie públicos-alvo com base em suas interações anteriores com o site. Use a Platform para segmentar usuários usando atributos computados.

1. **Identificar comportamentos de chave**: selecione as ações do usuário que serão monitoradas, como exibições de página ou cliques.

2. **Criar públicos-alvo**: use as ferramentas de segmentação de público-alvo para agrupar usuários com base em comportamentos.

3. **Sincronizar ECID**: certifique-se de que as ECIDs estejam sincronizadas entre as plataformas para uma correspondência precisa do público-alvo.

## Ativar seu público {#activate-audience}

Depois de criar seu público-alvo, ative-o nas plataformas para engajar os usuários.

1. **Revisar públicos-alvo**: verifique se os segmentos de público-alvo refletem os comportamentos corretos.

2. **Criar regras de ativação**: defina condições para quando e como os usuários serão envolvidos com base nas ações.

3. **Enviar para a plataforma**: ativar o público-alvo.

4. **Monitorar desempenho**: controle o desempenho do público-alvo e ajuste conforme necessário.

## Configurar a extensão de redirecionamento externo {#configure-extension}

### Implantar o Web SDK

Verifique se o Adobe Web SDK está integrado corretamente ao site. Essa SDK permite a coleta de dados do evento em tempo real, o que é crucial para o redirecionamento eficiente.

### Ativar o encaminhamento de eventos

Configure um encaminhamento de eventos na Platform para enviar dados coletados de comportamento do usuário às plataformas de redirecionamento. O encaminhamento de eventos garante que os dados sejam transmitidos com eficiência, permitindo que as empresas direcionem usuários de alta intenção sem depender de cookies.

### Anexar à regra de redirecionamento

Verifique se a extensão de redirecionamento externo está anexada a uma regra de evento válida na Coleção de dados da Adobe Experience Platform. Normalmente, uma regra global deve ser criada para ser acionada em ações principais, como `page load` ou interações específicas do usuário.

Para saber mais sobre como configurar a extensão, leia a documentação [Encaminhamento de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started).

## Outros casos de uso {#other-use-cases}

Este documento fornece uma visão geral dos principais casos de uso e considerações técnicas para o desenvolvimento e utilização bem-sucedidos da configuração do Web SDK e do encaminhamento de eventos. Ao seguir os procedimentos descritos e garantir que os pré-requisitos necessários sejam atendidos, é possível melhorar significativamente os recursos de rastreamento de dados e análise.

Você pode explorar mais casos de uso ativados por meio do suporte a dados de parceiros no Real-Time CDP:

- [Envolva e adquira novos clientes](./prospecting.md) usando dados de parceiros.
- [Personalize experiências no site](./offsite-retargeting.md) com reconhecimento de visitante auxiliado por parceiro.
- [Complemente perfis próprios](./supplement-first-party-profiles.md) com atributos fornecidos pelo parceiro.
