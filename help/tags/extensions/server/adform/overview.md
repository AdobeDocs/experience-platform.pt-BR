---
keywords: integração adform, adform,
title: Integração do Adobe Form para redirecionamento não autenticado
description: Essa integração do Adobe Experience Platform permite redirecionar usuários com base na ECID.
last-substantial-update: 2025-03-26T00:00:00Z
exl-id: 37eb9453-fc3c-481e-94ea-54d9b1545631
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 1%

---

# Visão geral da extensão do [!DNL Adform]

A extensão [[!DNL Adform]](https://www.adformhelp.com/hc/en-us/articles/29635608709137-Use-the-Adform-S2S-Site-Tracking-Extension-With-Adobe-Experience-Cloud) permite o encaminhamento de eventos do lado do servidor no Adobe Experience Platform, permitindo que anunciantes, agências de mídia e editores sincronizem dados diretamente com o sistema Adobe ID Fusion. Essa integração permite que as empresas envolvam públicos em vários canais, melhorando o desempenho da campanha e fornece soluções personalizadas para refinar estratégias de publicidade digital e maximizar a eficácia dos gastos com anúncios.

Diferentemente do rastreamento tradicional do lado do cliente, essa extensão elimina a necessidade de cookies de terceiros aproveitando IDs primárias - especificamente, a ECID (Experience Cloud ID) que é sincronizada com o Adform. Isso permite o redirecionamento perfeito do público-alvo sem exigir a implantação do JavaScript no lado do cliente.

Este guia aborda como instalar, configurar e implantar a extensão para encaminhar eventos das propriedades digitais de uma marca por meio do Edge Network do Adobe para o Adobe Forms, a fim de permitir o redirecionamento contínuo dos visitantes.

## Redirecionamento externo

Por meio do redirecionamento externo, você pode reengajar clientes em potencial que visitaram seu site, mas não fizeram a conversão. A Adobe ajuda você a alcançar esses públicos em várias plataformas, reforçando a presença da marca e aumentando as oportunidades de conversão. Use essa integração para:

* Reconectar visitantes desconhecidos sem usar cookies de terceiros.
* Ative públicos diretamente nas ECIDs sem usar identificadores alternativos de cookies de terceiros ou tags adicionais em suas propriedades digitais.

O Adform ajuda a:

* Transforme facilmente seus públicos-alvo primários indicados em ECIDs em IDs endereçáveis para campanhas de anúncios digitais.
* Vincule ECIDs a mais de 40 soluções de ID licitáveis para otimizar seu alcance, frequência e desempenho em relação aos públicos-alvo direcionados.

### Ativação de público-alvo do lado do servidor com [!DNL Adform] {#server-side-activation}

Diferentemente das implantações tradicionais de ID do lado do cliente, essa integração não exige a implantação de uma solução de fornecedor de ID em suas propriedades digitais. Em vez disso, ele permite a ativação de público-alvo do lado do servidor, aproveitando ECIDs que já estão sincronizadas com o Adobe Form. Os principais benefícios incluem:

* **Nenhuma implantação do JavaScript no lado do cliente**: você não precisa gerenciar a lógica de reconhecimento de visitantes do lado do cliente ou descriptografar IDs do lado do cliente em versões estáveis de vida mais longa.
* **Sincronização perfeita de público-alvo**: as ECIDs são mapeadas para o gráfico de ID interno da Adobe, permitindo um redirecionamento eficiente entre plataformas.
* **Alcance e desduplicação aprimorados**: o gráfico ID Fusion conecta ECIDs a vários identificadores, garantindo uma correspondência de público-alvo de alta qualidade.

## Pré-requisitos {#prerequisites}

Antes de integrar o Adobe Form com o Adobe, verifique se os seguintes pré-requisitos foram atendidos:

1. **Configuração do Adobe Web SDK**: o Adobe Web SDK deve ser implementado para facilitar a coleta de dados e o encaminhamento de eventos.

2. **SKU de CDP ou Conexão**: você deve ter a SKU de Prime ou Ultimate da Adobe Customer Data Platform (CDP) ou a SKU de Conexão para habilitar a comunicação perfeita entre o cliente e o servidor.

3. **Configuração do Adobe Experience Platform Edge Network**:
   * Verifique se o Edge Network está configurado para suportar o encaminhamento de eventos em tempo real para redirecionamento externo. Consulte o [Guia de Introdução ao encaminhamento de eventos](https://experienceleague.adobe.com/pt-br/docs/experience-platform/tags/event-forwarding/getting-started) da Adobe para obter mais informações.
   * Essa etapa é essencial para transmitir dados ao endpoint do lado do servidor da Adobe com eficiência.

Depois que esses pré-requisitos estiverem em vigor, você poderá continuar a configurar e implantar a extensão [!DNL Adform].

## Configurar a extensão [!DNL Adform] {#configure-adform-extension}

Para configurar a extensão [!DNL Adform], siga as etapas descritas nas seções abaixo.

### Instalar e configurar a extensão

Navegue até [!DNL Adform extension] na interface do usuário do encaminhamento de eventos e insira os valores necessários:

| Entrada | Descrição |
| --- | --- |
| ID de configuração de rastreamento | O identificador exclusivo fornecido pelo Adform para eventos de rastreamento. |
| Domínio global | Use o `a1.adform.net` para otimizar o desempenho e evitar problemas de latência regional. |

Salve a configuração depois de inserir esses detalhes.

<!-- ![Installing and configuring the Adform extension in Adobe Experience Platorm]() -->

### Definir parâmetros de rastreamento

A ação &quot;rastrear&quot; é a regra do evento principal. Dispara com base em ações predefinidas, normalmente `page load.` Incluir os seguintes parâmetros:

**Parâmetros obrigatórios:**

| Parâmetros | Descrição |
| --- | --- |
| `Page Name` | Identifica a página ou a ação do usuário. |
| `User Agent` | Registra informações para correspondência de público-alvo. |
| `IP Address` | Fundamental para direcionamento e redirecionamento precisos. |

**Parâmetros recomendados:**

| Parâmetros | Descrição |
| --- | --- |
| `Page URL` | Identifica a página ou a ação do usuário. |
| `Referral URL` | Registra informações para correspondência de público-alvo. |
| `ECID` | Fundamental para direcionamento e redirecionamento precisos. |
| `Source Domain` | Fundamental para direcionamento e redirecionamento precisos. |

<!-- ![Tracking parameters for Adform]() -->

### Anexar regra

A extensão deve ser anexada a uma regra para funcionar corretamente. Se nenhuma condição for definida, crie uma regra global para garantir que ela sempre seja executada.

>[!NOTE]
>
>Se a extensão não for acionada, verifique se ela está anexada a uma regra válida na Coleção de dados da Adobe Experience Platform.

<!-- ![Attach a rule to the Adform extension]() -->

## Validar e implantar

Verifique se a extensão está instalada e configurada corretamente e se todos os elementos de dados necessários estão mapeados, incluindo:

* [ECID](/help/identity-service/features/ecid.md)
* Nome da página
* URL de referência
* Agente do usuário
* Endereço IP

Depois de inserir todos os campos obrigatórios e concluir o teste, selecione **compilação** para implantar a extensão.

## Próximas etapas

Agora você deve entender como o Adform se integra aos recursos do lado do servidor do Adobe e pode avaliar a viabilidade da integração em sua infraestrutura existente. Para obter mais informações, consulte a [documentação oficial do Adform](https://www.adformhelp.com/hc/en-us/articles/29635608709137-Use-the-Adform-S2S-Site-Tracking-Extension-With-Adobe-Experience-Cloud).
