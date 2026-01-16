---
title: Códigos de erro do Privacy Service no Adobe Experience Platform
description: Entenda os códigos de erro do Privacy Service para que você possa diagnosticar falhas, lidar com os resultados do trabalho de forma programática e determinar as próximas etapas ao enviar ou monitorar trabalhos de privacidade.
keywords: privacy service, códigos de erro, processos de privacidade, erros de api
solution: Experience Platform
source-git-commit: a312dabf5b8c3b52af31e2e127cd4bbeb8dd0021
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 4%

---

# Códigos de erro do Privacy Service {#privacy-service-error-codes}

Use esta referência para identificar os resultados do trabalho do Privacy Service, diagnosticar falhas e determinar as próximas etapas apropriadas ao enviar ou monitorar trabalhos de privacidade no **Adobe Experience Platform**. Para saber como criar, enviar e monitorar trabalhos de privacidade, consulte o [manual de endpoint de trabalhos de privacidade](./privacy-jobs.md) ou o [guia do usuário da interface do Privacy Service](../ui/user-guide.md).

Os códigos de erro do Privacy Service são um contrato público estável. Cada código de erro identifica exclusivamente um estado de falha ou conclusão no qual você pode confiar para manipulação programática e workflows operacionais.

As seguintes garantias se aplicam à criação de automação ou ao monitoramento de workflows:

* Os códigos de erro são estáveis após a publicação.
* As mensagens de erro podem mudar para melhorar a clareza, mas o valor do código não.
* Novos códigos de erro podem ser adicionados ao longo do tempo; os códigos existentes não são redefinidos.

Use códigos de erro, não texto de mensagem, para implementar automação ou lógica de decisão. Para obter orientação sobre como processar trabalhos de privacidade, monitorar o status do trabalho e manipular erros sem depender de sondagem ou cadeias de caracteres de mensagem, consulte [práticas recomendadas da Privacy Service](../best-practices.md).

## Formato de resposta de erro {#error-response-format}

O Privacy Service retorna informações de erro nas respostas de tarefas e solicitações. A resposta inclui um código de erro numérico e uma mensagem legível na carga de resposta.

O código de erro transmite o resultado autorizado. A mensagem fornece contexto adicional para solução de problemas.

Este documento descreve o significado e a intenção de cada código de erro. Para obter esquemas de resposta em nível de campo e detalhes da solicitação, consulte a [documentação da API do Privacy Service](https://developer.adobe.com/experience-platform-apis/references/privacy-service/).

## Domínios com erro {#error-domains}

Os códigos de erro são agrupados por domínio funcional para ajudar você a diagnosticar problemas mais rapidamente.

Os domínios usados neste documento incluem:

* **Solicitar validação**: a solicitação está malformada ou contém valores inválidos. Consulte o [manual de ponto de extremidade de trabalhos de privacidade](./privacy-jobs.md) para obter a estrutura da solicitação e os requisitos de validação.
* **Autorização e provisionamento**: sua organização ou usuário não tem o acesso necessário. Consulte [gerenciar permissões](../permissions.md) para analisar os requisitos de permissão com base em função.
* **Identidade e aplicabilidade**: identificadores ou namespaces não se aplicam à solicitação. Consulte [dados de identidade para solicitações de privacidade](../identity-data.md) para obter os tipos de identidade e os requisitos de namespace compatíveis.
* **Limitação de taxa**: o volume de envio excede os limites da plataforma. Quando esse erro ocorrer, reduza a taxa de envio e tente novamente.
* **Acesso e processamento de dados**: o sistema não pode acessar ou processar os dados solicitados. Consulte o [guia de solução de problemas](../troubleshooting-guide.md) para obter as causas comuns e as etapas de correção.
* **Criptografia e gerenciamento de chaves**: as chaves de criptografia necessárias não estão disponíveis. Consulte [Chaves gerenciadas pelo cliente](../../landing/governance-privacy-security/customer-managed-keys/overview.md) para obter orientação sobre acesso, configuração e recuperação de chaves.
* **Estado de execução do trabalho**: o trabalho foi concluído totalmente, parcialmente ou com falhas. Consulte o [manual de endpoint de trabalhos de privacidade](./privacy-jobs.md#status-categories) para obter descrições de categorias de status de trabalho e seus significados.

>[!NOTE]
>
>As atribuições de domínio refletem a intenção do código de erro, não os limites de serviço internos.

## Referência do código de erro {#error-code-reference}

A tabela a seguir lista todos os códigos de erro públicos do Privacy Service.

| Código de erro | Status HTTP | Título | Descrição |
| ---------- | ----------- | ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------| 
| 1000-400 | 400 | Erro de formatação | Um ou mais valores de dados para o aplicativo especificado têm problemas de formatação. Verifique os detalhes do trabalho para obter informações adicionais. |
| 1001-400 | 400 | Não autorizado | Sua organização não está provisionada. Entre em contato com o administrador para obter mais informações. |
| 1010-400 | 400 | Permissões ausentes | Você não tem as permissões necessárias para executar esta ação. Entre em contato com o administrador para solicitar acesso. |
| 1020-400 | 400 | Falha de upload e arquivamento | Ocorreu um problema ao carregar e arquivar dados de acesso. Carregue os dados de acesso e tente novamente. |
| 1021-400 | 400 | Falha no trabalho | Um ou mais processos de privacidade criados a partir da solicitação falharam. Revise os detalhes dos trabalhos com falha para obter mais informações. |
| 1022-400 | 400 | Falha no acesso aos dados | Ocorreu um problema ao acessar os dados especificados. Revise os detalhes do trabalho para obter informações adicionais. |
| 1023-400 | 400 | Falha no acesso aos dados | Ocorreu um problema ao acessar ou localizar as IDs do conjunto de dados especificado. Verifique se as IDs fornecidas são válidas e tente novamente. |
| 1024-400 | 400 | Erro inesperado | Ocorreu um erro inesperado. Revise os detalhes do trabalho para obter informações adicionais. |
| 1030-400 | 400 | Limite de taxa de documentos excedido | A carga de trabalho excedeu o limite de taxa do documento. Reduza a taxa de envio e tente novamente. |
| 1040-400 | 400 | Falha de acesso à criptografia de chave | Não foi possível processar os dados porque o armazenamento de dados está criptografado e o acesso à chave foi revogado. Entre em contato com o administrador do cofre de chaves para restaurar o acesso à chave do cliente. |
| 6000-200 | 200 | Sucesso | O trabalho foi concluído com sucesso. Revise os detalhes do trabalho para confirmar os registros e resultados processados. |
| 6051-200 | 200 | Não provisionado | Sua organização não está provisionada para o aplicativo solicitado. O pedido não é aplicável. |
| 6052-200 | 200 | IDs de usuário não encontradas | Algumas IDs de usuário não foram encontradas, e IDs de usuário desconhecidas não se aplicam a este produto. Verifique se as IDs de usuário são válidas e tente novamente. |
| 6053-200 | 200 | Namespace inválido | O namespace de identidade fornecido não é válido para este aplicativo. Use um namespace reconhecido pelo sistema. |
| 6054-200 | 200 | Concluído parcialmente | O trabalho foi concluído para os dados aplicáveis, mas alguns dados não foram aplicáveis à solicitação. Revise os detalhes do trabalho para obter informações adicionais. |

{style="table-layout:auto"}
