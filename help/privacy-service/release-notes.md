---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Notas de versão do Privacy Service
topic-legacy: release notes
description: As notas de versão mais recentes para o Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 6%

---

# Notas de versão do [!DNL Privacy Service]

Este documento contém informações sobre novos recursos do Adobe Experience Platform [!DNL Privacy Service], bem como aprimoramentos e correções de erros significativas.

>[!NOTE]
>
>As notas de versão mais recentes para outras [!DNL Experience Platform] os serviços podem ser encontrados [here](../release-notes/latest/latest.md).

## 9 de setembro de 2020

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| Suporte para LGPD (Brasil) | Trabalhos de privacidade agora podem ser criados no Brasil [!DNL Lei Geral de Proteção de Dados] (LGPD). Esses trabalhos são rastreados pelo código do regulamento `lgpd_bra`. |

## 8 de abril de 2020

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| Suporte a PDPA | [!DNL Privacy] As solicitações agora podem ser criadas e rastreadas de acordo com a Lei de Proteção de Dados Pessoais (PDPA) na Tailândia. Ao fazer solicitações de privacidade na API, a variável `regulation` A matriz aceita o valor &quot;pdpa_tha&quot;. |
| Tipos de namespace na interface do usuário | Agora você pode especificar diferentes tipos de namespace no Construtor de solicitações na [!DNL Privacy Service] IU. Consulte a [guia do usuário](ui/user-guide.md) para obter mais informações. |
| Substituição antiga do terminal | O endpoint da antiga API (`data/privacy/gdpr`) foi substituída. |

## 14 de janeiro de 2020

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| [!DNL Privacy Service] reformulação da marca | O antigo serviço chamado &quot;GDPR&quot; foi renomeado para [!DNL Privacy Service] à medida que o serviço cresceu para suportar outras regulamentações além do GDPR. |
| Novos endpoints de API | Caminho base para o [!DNL Privacy Service] A API foi atualizada de `/data/privacy/gdpr` para `/data/core/privacy/jobs` |
| Novo obrigatório `regulation` propriedade | Ao criar novos trabalhos na [!DNL Privacy Service] API, um `regulation` deve ser fornecida na carga da solicitação para indicar em qual regulamento rastrear a tarefa. Os valores aceitos são `gdpr` e `ccpa`. Consulte o documento em [tarefas de privacidade](api/privacy-jobs.md) no [!DNL Privacy Service] Guia de API para obter mais informações. |
| Suporte para autenticação do Adobe Primetime | [!DNL Privacy Service] agora aceita solicitações de acesso/exclusão da Autenticação Adobe Primetime, usando `primetimeAuthentication` como valor do produto. Consulte a [Documentação de autenticação do Primetime](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) para obter mais informações. |

### Melhorias

* [!DNL Privacy Service] Aprimoramentos da interface do usuário:
   * Páginas de rastreamento de trabalho separadas para regulamentos do GDPR e da CCPA.
   * Novo *Tipo de regulamento* lista suspensa para alternar entre os dados de rastreamento do GDPR e da CCPA.

## 25 de julho de 2019

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| Solicitar painel de métricas | O novo painel de métricas na [!DNL Privacy Service] A interface do usuário fornece visibilidade sobre solicitações do GDPR enviadas, erradas e concluídas. |
| Construtor de solicitações | Para atender organizações com usuários técnicos e não técnicos enviando solicitações do GDPR, uma funcionalidade &quot;Criar solicitação&quot; foi adicionada à interface do usuário. O recurso de envio de arquivo JSON ainda está disponível na variável [!DNL Privacy Service] Interface do usuário para as organizações que preferem continuar a usá-la. |
| Notificações de evento de trabalho do GDPR | As notificações de eventos sobre os status de trabalho do GDPR são um elemento essencial para muitos fluxos de trabalho. Embora as notificações tenham sido veiculadas anteriormente por meio de avisos de email individuais, as notificações de evento do GDPR são mensagens que aproveitam eventos do Adobe I/O, que são enviadas para um webhook configurado, facilitando a automação de solicitações de trabalho. [!DNL Privacy Service] Usuários da interface do usuário podem assinar eventos do GDPR do Adobe I/O para receber atualizações quando um produto ou um trabalho do GDPR for concluído. |

## 18 de abril de 2019

### Melhorias

* Intervalo padrão para a tabela de status na [!DNL Privacy Service] A interface do usuário foi modificada para um período de 7 dias.
* Melhor tratamento interno de exceções.
* Desempenho aprimorado ao introduzir o armazenamento em cache para chamadas internas comuns com taxas de alteração de dados baixas.

### Correções de erros

* Foram adicionadas informações de registro ausentes para consultas filtradas para o `GET /` endpoint no [!DNL Privacy Service] API.

## 11 de abril de 2019

### Melhorias

* Atualização da interface do usuário para oferecer suporte à nova funcionalidade para clientes beta
* Nova API de métricas para suportar recursos da interface do usuário 2.0 em beta

## 9 de abril de 2019

### Melhorias

* Atualização de todas as chamadas de API de pesquisa (GET) para o padrão de um intervalo de pesquisa de 30 dias
* Uso restrito da API para ter um intervalo de lookback máximo de 45 dias

## 14 de fevereiro de 2019

### Melhorias

* Impor o `include` em cada envio de POST.
* Impor o `include` ao fazer upload do JSON.

### Correções de erros

* Correção de um problema em que os clientes não podiam carregar o [!DNL Privacy Service] IU.
