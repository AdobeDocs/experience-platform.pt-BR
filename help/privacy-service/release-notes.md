---
keywords: Experience Platform;home;populares tópicos
solution: Experience Platform
title: Notas de versão de Privacy Service
topic: release notes
description: As notas de versão mais recentes do Adobe Experience Platform Privacy Service.
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 6%

---


# Notas de versão do [!DNL Privacy Service]

Este documento contém informações sobre novos recursos do Adobe Experience Platform [!DNL Privacy Service], bem como melhorias e correções significativas de erros.

>[!NOTE]
>
>As notas de versão mais recentes de outros [!DNL Experience Platform] serviços podem ser encontradas [aqui](../release-notes/latest/latest.md).

## 9 de setembro de 2020

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| Suporte para LGPD (Brasil) | Trabalhos de privacidade agora podem ser criados sob o regulamento [!DNL Lei Geral de Proteção de Dados] (LGPD) do Brasil. Esses trabalhos são rastreados sob o código de regulamento `lgpd_bra`. |

## 8 de abril de 2020

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| Suporte a PDPA | [!DNL Privacy] as solicitações agora podem ser criadas e rastreadas sob o Personal Data Protection Act (PDPA) na Tailândia. Ao fazer solicitações de privacidade na API, a matriz `regulation` aceita o valor &quot;pdpa_tha&quot;. |
| Tipos de namespace na interface do usuário | Agora você pode especificar diferentes tipos de namespace no Construtor de solicitações na interface do usuário [!DNL Privacy Service]. Consulte o [guia do usuário](ui/user-guide.md) para obter mais informações. |
| Substituição de ponto final antigo | O ponto final da API antiga (`data/privacy/gdpr`) foi substituído. |

## 14 de janeiro de 2020

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| [!DNL Privacy Service] nova marca | A antiga chamada &quot;GDPR Service&quot; foi substituída por [!DNL Privacy Service], já que o serviço cresceu para suportar outras regulamentações além do RGPD. |
| Novos pontos de extremidade de API | O caminho básico para a API [!DNL Privacy Service] foi atualizado de `/data/privacy/gdpr` para `/data/core/privacy/jobs` |
| Nova propriedade `regulation` necessária | Ao criar novos trabalhos na API [!DNL Privacy Service], uma propriedade `regulation` deve ser fornecida na carga da solicitação para indicar em qual regulamento rastrear o trabalho. Os valores aceitos são `gdpr` e `ccpa`. Consulte o documento em [tarefas de privacidade](api/privacy-jobs.md) no guia do desenvolvedor [!DNL Privacy Service] para obter mais informações. |
| Suporte para autenticação Adobe Primetime | [!DNL Privacy Service] agora aceita solicitações de acesso/exclusão da Autenticação Adobe Primetime, usando  `primetimeAuthentication` como valor do produto. Consulte a documentação [Autenticação Primetime](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) para obter mais informações. |

### Melhorias

* [!DNL Privacy Service] Aprimoramentos da interface:
   * Separe as páginas de rastreamento de trabalho para os regulamentos de RGPD e CCPA.
   * Nova lista suspensa *Tipo de Regulamento* para alternar entre os dados de rastreamento para o GDPR e o CCPA.

## 25 de julho de 2019

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| Painel de métricas de solicitação | O novo painel de métricas na interface do usuário [!DNL Privacy Service] fornece visibilidade sobre solicitações de RGPD enviadas, erradas e concluídas. |
| Construtor de solicitações | Para atender organizações com usuários técnicos e não técnicos que enviam solicitações de RGPD, uma funcionalidade &quot;Criar solicitação&quot; foi adicionada à interface do usuário. O recurso de envio de arquivos JSON ainda está disponível na interface do usuário [!DNL Privacy Service] para as organizações que preferem continuar a usá-lo. |
| Notificações de Evento de Trabalho do GDPR | As notificações de eventos sobre status de trabalhos do RGPD são um elemento crítico para muitos workflows. Embora as notificações tenham sido enviadas por meio de avisos de email individuais, as notificações de evento do RGPD são mensagens que aproveitam eventos do Adobe I/O, que são enviadas para um webhook configurado que facilita a automação de solicitações de trabalhos. [!DNL Privacy Service] Os usuários da interface do usuário podem assinar eventos do Adobe I/O GDPR para receber atualizações quando um produto ou o trabalho do RGPD for concluído. |

## 18 de abril de 2019

### Melhorias

* Intervalo padrão para a tabela de status na interface do usuário [!DNL Privacy Service] modificada para um intervalo de 7 dias.
* Melhor tratamento de exceções internas.
* Desempenho aprimorado ao introduzir o cache para chamadas internas comuns com baixas taxas de alteração de dados.

### Correções de erros

* Foram adicionadas informações de registro ausentes para query filtrados para o terminal `GET /` na API [!DNL Privacy Service].

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

* Imponha o campo `include` em todas as submissões de POST.
* Imponha o campo `include` ao carregar JSON.

### Correções de erros

* Correção de um problema em que os clientes não podiam carregar a interface do usuário [!DNL Privacy Service].