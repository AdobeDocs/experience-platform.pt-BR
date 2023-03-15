---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Notas de versão do Privacy Service
description: As notas de versão mais recentes do Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 5%

---

# Notas de versão do [!DNL Privacy Service]

Este documento contém informações sobre novos recursos do Adobe Experience Platform [!DNL Privacy Service], bem como melhorias e correções de erros significativas.

>[!NOTE]
>
>As notas de versão mais recentes de outros [!DNL Experience Platform] serviços podem ser encontrados [aqui](../release-notes/latest/latest.md).

## 9 de setembro de 2020

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| Suporte para LGPD (Brasil) | Os trabalhos de privacidade agora podem ser criados no [!DNL Lei Geral de Proteção de Dados] (LGPD). Essas tarefas são rastreadas sob o código de regulamento `lgpd_bra`. |

## 8 de abril de 2020

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| Suporte a PDPA | [!DNL Privacy] As solicitações do agora podem ser criadas e rastreadas de acordo com a Lei de Proteção de Dados Pessoais (PDPA) na Tailândia. Ao fazer solicitações de privacidade na API, a variável `regulation` aceita o valor &quot;pdpa_tha&quot;. |
| Tipos de namespace na interface do | Agora você pode especificar diferentes tipos de namespace no Criador de solicitações na [!DNL Privacy Service] IU. Consulte a [guia do usuário](ui/user-guide.md) para obter mais informações. |
| Descontinuação de ponto de extremidade antigo | O endpoint da API antiga (`data/privacy/gdpr`) foi descontinuado. |

## 14 de janeiro de 2020

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| [!DNL Privacy Service] rebranding | O anteriormente chamado &quot;Serviço GDPR&quot; foi reformulado para [!DNL Privacy Service] à medida que o serviço se expandiu para oferecer suporte a outras regulamentações além do GDPR. |
| Novos pontos de acesso de API | Caminho base para o [!DNL Privacy Service] A API foi atualizada de `/data/privacy/gdpr` para `/data/core/privacy/jobs` |
| Novo obrigatório `regulation` propriedade | Ao criar novos trabalhos na [!DNL Privacy Service] API, uma `regulation` A propriedade deve ser fornecida na carga da solicitação para indicar em qual regulamento rastrear o trabalho. Os valores aceitos são `gdpr` e `ccpa`. Consulte o documento sobre [processos de privacidade](api/privacy-jobs.md) no [!DNL Privacy Service] Guia de API para obter mais informações. |
| Suporte para autenticação do Adobe Primetime | [!DNL Privacy Service] O agora aceita solicitações de acesso/exclusão da Autenticação Adobe Primetime, usando `primetimeAuthentication` como seu valor do produto. Consulte a [Documentação de autenticação do Primetime](https://tve.helpdocsonline.com/how-to-make-a-privacy-request) para obter mais informações. |

### Melhorias

* [!DNL Privacy Service] Melhorias na interface:
   * Páginas de rastreamento de trabalho separadas para os regulamentos do GDPR e da CCPA.
   * Novo *Tipo de regulamento* lista suspensa para alternar entre dados de rastreamento do GDPR e da CCPA.

## 25 de julho de 2019

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| Painel de métricas de solicitação | O novo painel de métricas no [!DNL Privacy Service] A interface do usuário do fornece visibilidade sobre solicitações do GDPR enviadas, com erros e concluídas. |
| Construtor de solicitações | Para atender organizações com usuários técnicos e não técnicos que enviam solicitações do GDPR, uma funcionalidade &quot;Criar solicitação&quot; foi adicionada à interface do usuário. O recurso de envio de arquivo JSON ainda está disponível no [!DNL Privacy Service] Interface para as organizações que preferem continuar usando. |
| Notificações de eventos de trabalho do GDPR | As notificações de eventos sobre status de tarefas do GDPR são um elemento essencial para muitos workflows. Embora as notificações tenham sido enviadas usando avisos de email individuais, as notificações de eventos do GDPR são mensagens que usam eventos Adobe I/O, que são enviadas para um webhook configurado que facilita a automação de solicitação de trabalho. [!DNL Privacy Service] Os usuários de interface do usuário podem assinar eventos do GDPR do Adobe I/O para receber atualizações quando um produto ou a tarefa do GDPR for concluída. |

## 18 de abril de 2019

### Melhorias

* Intervalo padrão para a tabela de status na variável [!DNL Privacy Service] Interface modificada para um período de 7 dias.
* Melhor tratamento interno de exceções.
* Desempenho aprimorado com a introdução do armazenamento em cache para chamadas internas comuns com baixas taxas de alteração de dados.

### Correções de erros

* Adição de informações de log ausentes para consultas filtradas para o `GET /` endpoint na variável [!DNL Privacy Service] API.

## 11 de abril de 2019

### Melhorias

* Atualização da interface do usuário para oferecer suporte à nova funcionalidade para clientes beta
* Nova API de métricas para oferecer suporte aos recursos da interface do usuário 2.0 na versão beta

## 9 de abril de 2019

### Melhorias

* Atualização de todas as chamadas de API de pesquisa (GET) para o padrão de um intervalo de pesquisa de 30 dias
* Uso da API restrito para ter um intervalo de pesquisa máximo de 45 dias

## 14 de fevereiro de 2019

### Melhorias

* Impor o `include` em cada envio de POST.
* Impor o `include` ao carregar o JSON.

### Correções de erros

* Correção de um problema em que os clientes não podiam carregar o [!DNL Privacy Service] IU.
