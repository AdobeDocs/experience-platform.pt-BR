---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Notas de versão de Privacy Service
topic: release notes
translation-type: tm+mt
source-git-commit: 4cfa64e3371496e2408fe8fee64d49883334917c
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 5%

---


# Notas de versão do [!DNL Privacy Service]

Este documento contém informações sobre novos recursos para o Adobe Experience Platform [!DNL Privacy Service], bem como melhorias e correções significativas de erros.

>[!NOTE]
>
>As notas de versão mais recentes para outros [!DNL Experience Platform] serviços podem ser encontradas [aqui](../release-notes/latest/latest.md).

## 8 de abril de 2020

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| Suporte a PDPA | [!DNL Privacy] as solicitações agora podem ser criadas e rastreadas sob o Personal Data Protection Act (PDPA) na Tailândia. Ao fazer solicitações de privacidade na API, a `regulation` matriz aceita o valor &quot;pdpa_tha&quot;. |
| Tipos de Namespace na interface do usuário | Agora é possível especificar diferentes tipos de namespace no Construtor de solicitações na [!DNL Privacy Service] interface do usuário. Consulte o guia [do](ui/user-guide.md) usuário para obter mais informações. |
| Substituição de ponto final antigo | O ponto de extremidade da API antiga (`data/privacy/gdpr`) foi substituído. |

## 14 de janeiro de 2020

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| [!DNL Privacy Service] nova marca | A antiga chamada &quot;GDPR Service&quot; foi substituída por [!DNL Privacy Service] que o serviço cresceu para suportar outras regulamentações além do RGPD. |
| Novos pontos de extremidade de API | O caminho básico da [!DNL Privacy Service] API foi atualizado de `/data/privacy/gdpr` para `/data/core/privacy/jobs` |
| Nova propriedade `regulation` obrigatória | Ao criar novos trabalhos na [!DNL Privacy Service] API, uma `regulation` propriedade deve ser fornecida na carga da solicitação para indicar em qual regulamento rastrear o trabalho. Os valores aceitos são `gdpr` e `ccpa`. Consulte o documento sobre trabalhos [de](api/privacy-jobs.md) privacidade no guia do [!DNL Privacy Service] desenvolvedor para obter mais informações. |
| Suporte para autenticação Adobe Primetime | [!DNL Privacy Service] agora aceita solicitações de acesso/exclusão da Autenticação Adobe Primetime, usando `primetimeAuthentication` como valor do produto. See the [Primetime Authentication documentation](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) for more information. |

### Melhorias

* [!DNL Privacy Service] Aprimoramentos da interface:
   * Separe as páginas de rastreamento de trabalho para os regulamentos de RGPD e CCPA.
   * Novo menu suspenso Tipo _de_ regulamento para alternar entre os dados de rastreamento para RGPD e CCPA.

## 25 de julho de 2019

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| Painel de métricas de solicitação | O novo painel de métricas na [!DNL Privacy Service] interface do usuário fornece visibilidade sobre solicitações de RGPD enviadas, erradas e concluídas. |
| Construtor de solicitações | Para atender organizações com usuários técnicos e não técnicos que enviam solicitações de RGPD, uma funcionalidade &quot;Criar solicitação&quot; foi adicionada à interface do usuário. O recurso de envio de arquivos JSON ainda está disponível na [!DNL Privacy Service] interface do usuário para as organizações que preferirem continuar usando-o. |
| Notificações de Evento de Trabalho do GDPR | As notificações de Eventos sobre status de trabalhos do RGPD são um elemento crítico para muitos workflows. Embora as notificações tenham sido enviadas por meio de avisos de email individuais, as notificações de evento do RGPD são mensagens que aproveitam eventos de E/S de Adobe, que são enviadas para um webhook configurado, facilitando a automação de solicitações de trabalho. [!DNL Privacy Service] Os usuários da interface do usuário podem assinar eventos RGPD de E/S de Adobe para receber atualizações quando um produto ou o trabalho RGPD for concluído. |

## 18 de abril de 2019

### Melhorias

* Intervalo padrão para a tabela de status na [!DNL Privacy Service] interface do usuário modificado para um intervalo de 7 dias.
* Melhor tratamento de exceções internas.
* Desempenho aprimorado ao introduzir o cache para chamadas internas comuns com baixas taxas de alteração de dados.

### Correções de erros

* Foram adicionadas informações de registro ausentes para query filtrados para o `GET /` endpoint na [!DNL Privacy Service] API.

## 11 de abril de 2019

### Melhorias

* Atualização da interface do usuário para oferecer suporte a novas funcionalidades para clientes beta
* Nova API de métricas para suportar recursos da interface do usuário 2.0 em beta

## 9 de abril de 2019

### Melhorias

* Atualizadas todas as chamadas da API de pesquisa (GET) para o padrão em um intervalo de pesquisa de 30 dias
* Uso restrito da API para ter um intervalo de pesquisa máximo de 45 dias

## 14 de fevereiro de 2019

### Melhorias

* Imponha o `include` campo em cada submissão de POST.
* Imponha o `include` campo ao fazer upload do JSON.

### Correções de erros

* Correção de um problema em que os clientes não podiam carregar a [!DNL Privacy Service] interface do usuário.