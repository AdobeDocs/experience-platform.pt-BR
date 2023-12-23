---
title: Práticas recomendadas para o Privacy Service
description: Saiba como reduzir o tempo de processamento e os custos incorridos com sua organização ao concluir solicitações de privacidade seguindo estas diretrizes de uso ideal.
source-git-commit: c6507a39ba5ae5ca6aa2bf02cf8844a4592152ac
workflow-type: tm+mt
source-wordcount: '1234'
ht-degree: 0%

---

# Práticas recomendadas para o Privacy Service

Use o Privacy Service para automatizar a conformidade com as regulamentações de privacidade de dados quando os clientes desejarem acessar ou excluir seus dados pessoais dos armazenamentos de dados. Para atender a essas necessidades comerciais em evolução, o Privacy Service oferece uma API RESTful e uma interface para enviar solicitações de acesso e exclusão para dados do cliente em aplicativos Adobe Experience Cloud.

Este guia descreve as práticas recomendadas para processar com eficiência as solicitações de privacidade e otimizar os tempos de resposta de conclusão ao gerenciar solicitações de dados do cliente.

## Introdução {#getting-started}

Este guia requer uma compreensão funcional de [Privacy Service](./home.md) e como ele permite gerenciar o acesso e excluir solicitações de titulares de dados (clientes) nos aplicativos da Adobe Experience Cloud. Também é recomendável que você leia o guia em [criação de uma solicitação de acesso a dados pessoais na interface](./ui/user-guide.md#create-a-new-privacy-job-request) ou [a API](./api/overview.md)e saiba como executar essas operações de forma programática.

## Pré-requisitos {#prerequisites}

O acesso ao Adobe Experience Platform Privacy Service é controlado por meio de permissões granulares baseadas em funções no Adobe Admin Console. Você precisa das permissões relevantes em um perfil de produto para usar recursos específicos na interface e API do Privacy Service. Entre em contato com o administrador do sistema se precisar de permissões adicionais.

Os administradores podem consultar o guia em [gerenciamento de permissões para o Privacy Service](./permissions.md) para obter mais informações.

## Diretrizes de criação de trabalho de privacidade {#creation-guidelines}

Para simplificar o processamento de solicitações e melhorar os tempos de resposta, considere as seguintes diretrizes ao criar processos de privacidade. Isso se aplica aos métodos da API e da interface do usuário.

1. **Maximizar titulares de dados por solicitação:** Inclua o máximo possível de titulares de dados, até 1000, por solicitação.
2. **IDs de grupo para eficiência:** Agrupar várias IDs para um único titular de dados (até nove) em cada solicitação. A variável **As IDs podem vir de diferentes serviços da Adobe na mesma solicitação**.
3. **Combinar trabalhos de acesso e exclusão:** Inclua os tipos de trabalho &quot;acesso&quot; e &quot;exclusão&quot; em uma única solicitação, se solicitado pelo titular dos dados.
4. **Incluir somente os produtos necessários:** Inclua somente os produtos necessários ou licenciados. Outros produtos podem prolongar o tempo de processamento e aumentar os custos.

## Monitorar status de trabalhos de privacidade {#monitor-status}

Para monitorar com eficácia os processos de privacidade e verificar seu status, o Privacy Service fornece três métodos. Os métodos disponíveis são listados abaixo, a fim de monitorar a eficiência e a produtividade. Cada método inclui diretrizes de práticas recomendadas para melhorar a experiência, seguidas por um exemplo de cenário ideal que combina todas as abordagens.

### Receber notificações em tempo real {#real-time-notifications}

**Eventos de E/S** A oferece monitoramento de status quase em tempo real por meio de eventos de status. Esse é o método mais eficiente, pois evita a necessidade de implementar mecanismos de polling e gera tráfego de API adicional.

**Recommendations:**

- **Configuração do Webhook:** Configure webhooks para receber notificações por push quando ocorrerem alterações de status para trabalhos enviados. Isso auxilia na monitoração em tempo real.
- **Notificações:** Use notificações no nível do trabalho e do produto para ajudar a monitorar o progresso das solicitações.

Consulte a documentação em [inscrição em eventos Privacy Service](./privacy-events.md) para obter instruções sobre como configurar um registro de evento para notificações Privacy Service e como interpretar payloads de notificação.

### Recuperar todos os trabalhos com base em filtros {#retrieve-filtered-responses-for-all-jobs}

Para recuperar todos os dados do seu trabalho de privacidade com base em qualquer filtro especificado, **execute uma solicitação do GET para o `/jobs` endpoint**. Essa chamada de API é útil para fornecer uma exibição de alto nível do status do trabalho atual para grandes conjuntos de IDs de trabalho com apenas uma única solicitação. Não há respostas detalhadas do produto, mas elas podem ser encontradas usando o [`/jobs/{jobID}` endpoint](#retrieve-detailed-responses-for-specific-jobs).

Uma solicitação GET para o `/jobs` O endpoint é melhor usado para coletar ou comparar os dados de status de um grande conjunto de IDs de trabalho, mas é **não** destinado a atividades do tipo sondagem regular.

**Recommendations:**

- **Parâmetros de consulta:** Use filtros específicos para restringir seus resultados, por exemplo: intervalos de dados, tipos de regulamentos e status (processamento, concluído etc.).

Você pode ver uma lista de todos os processos de privacidade atuais em sua organização por meio da interface do Privacy Service. Consulte a [gerenciamento de processos de privacidade na documentação da interface do usuário](./ui/user-guide.md#job-requests) para obter informações sobre como filtrar a lista de solicitações de trabalho. Como alternativa, consulte a documentação no [uso do endpoint /job na API Privacy Service](./api/privacy-jobs.md).

A documentação da API do Privacy Service contém detalhes sobre [os filtros de parâmetro de consulta disponíveis](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#tag/Privacy-jobs/operation/listPrivacyJobs).

### Recuperar respostas detalhadas para um único trabalho {#retrieve-detailed-responses-for-specific-jobs}

Para recuperar respostas detalhadas para um único job, **execute uma solicitação GET para o /jobs/{jobID} endpoint**. Esse método tem como objetivo obter informações mais detalhadas, como respostas específicas a produtos e mensagens de sucesso. Uma chamada para esse endpoint é a melhor maneira de ver quais produtos responderam e quais ainda estão pendentes, embora seja **não** destinado à atividade de pesquisa regular.

Consulte a `/jobs/{JOB_ID}` documentação do endpoint para obter detalhes sobre [como verificar o status de um trabalho específico](./api/privacy-jobs.md#check-status).

### Exemplo de cenário ideal {#ideal-scenario}

Use um webhook para que o sistema possa atualizar automaticamente os registros e fornecer relatórios ou alertas quando os grupos das IDs de uma solicitação forem concluídos. Se os trabalhos ainda estiverem pendentes, o sistema recuperará esses status de trabalho com uma solicitação GET para a API Privacy Service `/jobs` e fornece uma atualização de alto nível da lista.

Se um job específico ainda estiver pendente ou tiver retornado um erro, você poderá recuperar a resposta detalhada com uma solicitação GET para o `/job/{jobId}` terminal.

## Acessar dados de solicitação {#access-request-data}

Quando as informações do titular dos dados são solicitadas, cada serviço retorna dados em um formato consistente com a maneira como eles armazenam e usam esses dados. Depois que todos os serviços concluírem a solicitação, um URL de arquivo .ZIP será fornecido nos detalhes do trabalho para permitir que esses dados sejam baixados. Consulte o guia de solução de problemas para obter informações sobre [como baixar resultados do trabalho de privacidade](https://experienceleague.adobe.com/docs/experience-platform/privacy/troubleshooting-guide.html?lang=en#how-do-i-download-the-results-of-my-completed-privacy-jobs%3F).

A seguir, os principais itens de observação relacionados à gestão do arquivo de dados:

- Todos os arquivos são excluídos dos servidores Experience Platform após 30 dias. Não é possível consultar dados do cliente com mais de 30 dias.
- A estrutura do arquivo de arquivamento inclui pastas para cada produto incluído na solicitação e os arquivos de dados contidos nela. Os arquivos ou pastas podem estar vazios se nenhum dado for encontrado para a ID especificada.
- Os dados de trabalhos criados anteriormente só podem ser acessados por 30 dias após a data de conclusão. Depois disso, os dados serão removidos do sistema e uma nova solicitação deverá ser feita.

**Recommendations:**

- **Arquivos de dados do Protect:** O URL e o arquivo .ZIP devem ser protegidos, pois podem conter informações de identificação pessoal (PII) do titular dos dados.

## Considerações técnicas {#technical-considerations}

Há algumas considerações técnicas que devem ser levadas em conta ao concluir solicitações Privacy Service:

- **Período de retenção de dados:** O período máximo de pesquisa é de 60 dias para qualquer grupo de jobs e o período máximo de uma consulta é de 30 dias (as datas de/até).
- **Tempo limite do gateway:** Lembre-se de que sua solicitação pode ser descartada do gateway se exceder 60 segundos.
- **Tratamento de erros:** Revise as mensagens de erro detalhadamente e reenvie solicitações quando apropriado. O Privacy Service não reprocessa trabalhos automaticamente após um erro.
- **Entendendo os erros HTTP 429:** Familiarize-se com mensagens de erro HTTP 429 e as etapas necessárias para atenuar problemas. Os erros HTTP 429 são o resultado de &quot;Muitas solicitações&quot;. Consulte a [Mensagens de erro comuns](./troubleshooting-guide.md#common-error-messages) seção do guia de solução de problemas para obter mais informações sobre como resolver o problema.

## Próximas etapas

Ao ler este documento, você agora tem o conhecimento e as práticas necessárias para o uso eficiente e eficaz do Privacy Service. Em seguida, consulte o [guia de solução de problemas](./troubleshooting-guide.md) para obter respostas a perguntas frequentes sobre o Privacy Service e informações sobre erros encontrados com frequência na API.
