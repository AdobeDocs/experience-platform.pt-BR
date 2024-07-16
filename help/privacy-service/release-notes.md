---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Notas de versão do Privacy Service
description: As notas de versão mais recentes do Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 5%

---

# Notas de versão do [!DNL Privacy Service]

Este documento contém informações sobre novos recursos para o Adobe Experience Platform [!DNL Privacy Service], bem como melhorias e correções de erros significativas.

>[!NOTE]
>
>As notas de versão mais recentes para outros serviços do [!DNL Experience Platform] podem ser encontradas [aqui](../release-notes/latest/latest.md).

## 9 de setembro de 2020

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| Suporte para LGPD (Brasil) | Os trabalhos de privacidade agora podem ser criados no regulamento [!DNL Lei Geral de Proteção de Dados] (LGPD) do Brasil. Esses trabalhos são rastreados sob o código de regulamento `lgpd_bra`. |

## 8 de abril de 2020

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| Suporte a PDPA | As solicitações do [!DNL Privacy] agora podem ser criadas e rastreadas de acordo com a Lei de Proteção de Dados Pessoais (PDPA) na Tailândia. Ao fazer solicitações de privacidade na API do, a matriz `regulation` aceita o valor &quot;pdpa_tha&quot;. |
| Tipos de namespace na interface do | Agora você pode especificar diferentes tipos de namespace no Construtor de solicitações na interface do usuário do [!DNL Privacy Service]. Consulte o [guia do usuário](ui/user-guide.md) para obter mais informações. |
| Descontinuação de ponto de extremidade antigo | O ponto de extremidade da API antiga (`data/privacy/gdpr`) foi descontinuado. |

## 14 de janeiro de 2020

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| Reformulação da marca de [!DNL Privacy Service] | O anteriormente chamado &quot;Serviço do GDPR&quot; foi reformulado para [!DNL Privacy Service], à medida que o serviço se expandiu para oferecer suporte a outras regulamentações, além do GDPR. |
| Novos pontos de acesso de API | O caminho base para a API [!DNL Privacy Service] foi atualizado de `/data/privacy/gdpr` para `/data/core/privacy/jobs` |
| Nova propriedade `regulation` necessária | Ao criar novos trabalhos na API [!DNL Privacy Service], uma propriedade `regulation` deve ser fornecida na carga da solicitação para indicar em qual regulamento rastrear o trabalho. Os valores aceitos são `gdpr` e `ccpa`. Consulte o documento sobre [processos de privacidade](api/privacy-jobs.md) no guia de API do [!DNL Privacy Service] para obter mais informações. |
| Suporte para autenticação do Adobe Primetime | [!DNL Privacy Service] agora aceita solicitações de acesso/exclusão da Autenticação Adobe Primetime, usando `primetimeAuthentication` como valor de produto. Consulte a [Documentação de autenticação do Primetime](https://tve.helpdocsonline.com/how-to-make-a-privacy-request) para obter mais informações. |

### Melhorias

* [!DNL Privacy Service] aprimoramentos na interface:
   * Páginas de rastreamento de trabalho separadas para os regulamentos do GDPR e da CCPA.
   * Nova lista suspensa *Tipo de Regulamentação* para alternar entre os dados de rastreamento do GDPR e da CCPA.

## 25 de julho de 2019

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| Painel de métricas de solicitação | O novo painel de métricas na interface do usuário do [!DNL Privacy Service] fornece visibilidade sobre solicitações do GDPR enviadas, com erros e concluídas. |
| Construtor de solicitações | Para atender organizações com usuários técnicos e não técnicos que enviam solicitações do GDPR, uma funcionalidade &quot;Criar solicitação&quot; foi adicionada à interface do usuário. O recurso de envio de arquivo JSON ainda está disponível na interface do usuário do [!DNL Privacy Service] para as organizações que preferem continuar usando. |
| Notificações de eventos de trabalho do GDPR | As notificações de eventos sobre status de tarefas do GDPR são um elemento essencial para muitos workflows. Embora as notificações tenham sido enviadas usando avisos de email individuais, as notificações de eventos do GDPR são mensagens que usam eventos Adobe I/O, que são enviadas para um webhook configurado que facilita a automação de solicitação de trabalho. Os usuários da interface do usuário do [!DNL Privacy Service] podem assinar eventos do GDPR de Adobe I/O para receber atualizações quando um produto ou o trabalho do GDPR for concluído. |

## 18 de abril de 2019

### Melhorias

* Intervalo padrão para a tabela de status na interface do usuário [!DNL Privacy Service] modificada para um período de 7 dias.
* Melhor tratamento interno de exceções.
* Desempenho aprimorado com a introdução do armazenamento em cache para chamadas internas comuns com baixas taxas de alteração de dados.

### Correções de erros

* Adicionadas informações de log ausentes para consultas filtradas do ponto de extremidade `GET /` na API [!DNL Privacy Service].

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

* Imponha o campo `include` em cada envio de POST.
* Imponha o campo `include` ao carregar JSON.

### Correções de erros

* Correção de um problema em que os clientes não podiam carregar a interface do usuário [!DNL Privacy Service].
