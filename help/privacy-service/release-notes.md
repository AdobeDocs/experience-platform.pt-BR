---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Notas de versão do Privacy Service
description: As notas de versão mais recentes do Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: ht
source-wordcount: '552'
ht-degree: 100%

---

# Notas de versão do [!DNL Privacy Service]

Este documento contém informações sobre novos recursos para o Adobe Experience Platform [!DNL Privacy Service], bem como melhorias e correções de erros significativas.

>[!NOTE]
>
>As notas de versão mais recentes para outros serviços da [!DNL Experience Platform] podem ser encontradas [aqui](../release-notes/latest/latest.md).

## 9 de setembro de 2020

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| Suporte para LGPD (Brasil) | Os processos de privacidade agora podem ser criados de acordo com a [!DNL Lei Geral de Proteção de Dados] (LGPD) do Brasil. Esses processos são monitorados sob o código de regulamento `lgpd_bra`. |

## 8 de abril de 2020

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| Suporte a PDPA | As solicitações do [!DNL Privacy] agora podem ser criadas e monitoradas de acordo com a Lei de Proteção de Dados Pessoais (PDPA) da Tailândia. Ao criar solicitações de privacidade na API, a matriz `regulation` aceita o valor “pdpa_tha”. |
| Tipos de namespace na interface | Agora é possível especificar diferentes tipos de namespace no criador de solicitações da interface do [!DNL Privacy Service]. Consulte o [Guia do usuário](ui/user-guide.md) para obter mais informações. |
| Descontinuação do ponto de acesso antigo | O antigo ponto de acesso da API (`data/privacy/gdpr`) foi descontinuado. |

## 14 de janeiro de 2020

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| Mudança de identidade visual do [!DNL Privacy Service] | O antigo “Serviço do RGPD” foi reformulado para [!DNL Privacy Service] devido à expansão do serviço para oferecer suporte a outras regulamentações, além do RGPD. |
| Novos pontos de acesso de API | Atualização do caminho base para a API do [!DNL Privacy Service] de `/data/privacy/gdpr` para `/data/core/privacy/jobs` |
| Nova propriedade `regulation` necessária | Ao criar novos processos na API do [!DNL Privacy Service], é necessário fornecer uma propriedade `regulation` no conteúdo da solicitação para indicar sob qual regulamento monitorar o processo. Os valores permitidos são `gdpr` e `ccpa`. Consulte o documento sobre [processos de privacidade](api/privacy-jobs.md) no guia da API do [!DNL Privacy Service] para obter mais informações. |
| Suporte para autenticação do Adobe Primetime | O [!DNL Privacy Service] agora aceita solicitações de acesso e exclusão da autenticação do Adobe Primetime, usando `primetimeAuthentication` como o valor de produto. Consulte a [documentação de autenticação do Primetime](https://tve.helpdocsonline.com/how-to-make-a-privacy-request) para obter mais informações. |

### Melhorias

* Aprimoramentos na interface do [!DNL Privacy Service]:
   * Páginas de rastreamento de processos separadas para os regulamentos do RGPD e da CCPA.
   * Nova lista suspensa *Tipo de regulamentação* para alternar entre os dados de rastreamento do RGPD e da CCPA.

## 25 de julho de 2019

### Novos recursos

| Recurso | Descrição |
| --- | --- |
| Painel de métricas de solicitações | O novo painel de métricas na interface do [!DNL Privacy Service] fornece visibilidade sobre solicitações do RGPD enviadas, com erros e concluídas. |
| Criador de solicitações | Adição da funcionalidade “Criar solicitação” à interface para atender organizações com usuários técnicos e não técnicos que enviam solicitações do RGPD. O recurso de envio de arquivo JSON ainda está disponível na interface do [!DNL Privacy Service] para as organizações que preferem continuar a usá-lo. |
| Notificações de eventos de processos do RGPD | As notificações de eventos sobre o status de processos do RGPD são um elemento essencial para vários fluxos de trabalho. Embora as notificações tenham sido enviadas anteriormente por meio de avisos de email individuais, as notificações de eventos do RGDP utilizam eventos do Adobe I/O, que são enviados para um webhook configurado, facilitando a automação de solicitações de processos. Usuários da interface do [!DNL Privacy Service] podem assinar os eventos do RGPD do Adobe I/O para receber atualizações quando um produto ou processo do RGPD for concluído. |

## 18 de abril de 2019

### Melhorias

* Alteração do intervalo padrão da tabela de status na interface do [!DNL Privacy Service] para um período de 7 dias.
* Melhoria do tratamento interno de exceções.
* Desempenho aprimorado com a introdução do armazenamento em cache para chamadas internas comuns com baixas taxas de alteração de dados.

### Correções de erros

* Adição de informações de registro ausentes para consultas filtradas do ponto de acesso `GET /` na API do [!DNL Privacy Service].

## 11 de abril de 2019

### Melhorias

* Atualização da interface para oferecer suporte à nova funcionalidade para clientes beta
* Nova API de métricas para oferecer suporte aos recursos da interface 2.0 na versão beta

## 9 de abril de 2019

### Melhorias

* Padronização de todas as chamadas da API de pesquisa (GET) com um intervalo de pesquisa de 30 dias
* Restrição de uso da API a um intervalo de pesquisa máximo de 45 dias

## 14 de fevereiro de 2019

### Melhorias

* Imposição do campo `include` em cada envio POST.
* Imposição do campo `include` ao carregar um JSON.

### Correções de erros

* Correção de um problema em que clientes não podiam carregar a interface do [!DNL Privacy Service].
