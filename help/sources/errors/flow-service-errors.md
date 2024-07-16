---
title: Mensagens de Erro do Serviço de Fluxo
description: Saiba mais sobre as mensagens de erro que você pode encontrar ao usar o Serviço de fluxo para fontes.
exl-id: af79c547-25d0-459a-8de7-eb14206a8694
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 35%

---

# Mensagens de erro do Serviço de fluxo

O Serviço de fluxo é usado para coletar e centralizar dados do cliente de várias fontes diferentes na plataforma. O serviço fornece uma interface de usuário e API RESTful que permite configurar conexões de origem com vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar seus sistemas de terceiros, definir tempos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

Este documento fornece um catálogo de mensagens de erro, descrições e resoluções sugeridas relacionadas ao Serviço de Fluxo.

## Erros de validação interna no Serviço de Fluxo

A tabela a seguir descreve os erros relacionados à validação interna no Serviço de Fluxo.

| Código de erro | Título | Mensagem detalhada |
| --- | --- | --- |
| `1100-400` | Solicitação inválida | A solicitação não pôde ser processada. Erro do provedor de fluxo: não tem direito a esta operação. |
| `1101-404` | Recurso não encontrado | O recurso solicitado não foi encontrado. Erro do provedor de fluxo: o recurso com a ID fornecida não existe. |
| `1102-500` | Erro interno | Erro interno. Tente novamente. Se o problema persistir, entre em contato com o suporte ao cliente. |
| `1103-503` | Serviço indisponível | O serviço está temporariamente indisponível. Tente novamente e se o problema persistir, entre em contato com o suporte ao cliente. |
| `1104-504` | Tempo limite do gateway | O gateway atingiu o tempo limite. Tente novamente e se o problema persistir, entre em contato com o suporte ao cliente. |
| `1400-500` | Erro interno | Erro interno. Tente novamente. Se o problema persistir, entre em contato com o suporte ao cliente. |
| `1401-400` | Solicitação inválida | Os parâmetros de limite e contagem não podem ser fornecidos juntos na mesma solicitação. Forneça apenas o parâmetro de limite ou de contagem e tente novamente. |
| `1402-400` | Solicitação inválida | A ação &#39;finalize&#39; é suportada somente para solicitações de provedor. |
| `1403-400` | O cabeçalho está ausente | O cabeçalho &quot;If-Match&quot; está ausente na solicitação. Forneça o cabeçalho e tente novamente. |
| `1404-412` | Versão não correspondente | A versão &#39;v1&#39; fornecida não corresponde à versão atual na entidade &#39;cc01fc2c-0000-0200&#39;. Verifique se a versão fornecida corresponde à versão atual na entidade e tente novamente. |
| `1405-400` | Solicitação inválida | O corpo de solicitação não pode ser nulo ou vazio. Forneça um corpo de solicitação e tente novamente. |
| `1406-400` | Solicitação inválida | A sub-operação &#39;progress&#39; não pode ser aplicada com outras sub-operações. Atualize a lista de suboperações e tente novamente. |
| `1407-400` | Solicitação inválida | O status de falha não pode ser usado com a subOp `progress`. Remova a subOp `progress` ou use o status=&#39;inProgress&#39; e tente novamente. |
| `1408-400` | Solicitação inválida | A porcentagem concluída deve ser 100 para os estados “concluído” ou “com falha”. Atualize a porcentagem concluída e tente novamente. |
| `1409-400` | Solicitação inválida | A operação &#39;finalize&#39; não pode ser aplicada no estado atual habilitado-finalizando. Atualize a operação e tente novamente. |
| `1410-400` | Solicitação inválida | `State` não é permitido na solicitação criar fluxo. |
| `1411-400` | Solicitação inválida | Não é possível recuperar entityId. Solicitação inválida recebida com o caminho &#39;baseConnections/123&#39;. |
| `1412-400` | Solicitação inválida | Versão de mapeamento inválida na solicitação. Forneça a versão de mapeamento correta. |
| `1413-400` | Solicitação inválida | A ID de especificação fornecida é inválida. Forneça uma ID de especificação válida e tente novamente. |
| `1414-400` | Solicitação inválida | Não é possível atualizar a especificação de uma conexão. |
| `1415-400` | Solicitação inválida | A especificação de autenticação &#39;authConnection&#39; não foi encontrada para a ID de especificação de conexão ba6e206f-f233-ab16. |
| `1416-400` | Solicitação inválida | Só é possível excluir ou atualizar uma conexão que esteja habilitada, desabilitada ou inicializando. |
| `1417-400` | Solicitação inválida | Excluir ou Atualizar em Conexões no estado `initializing` não é permitido com UserToken. |
| `1418-400` | Solicitação inválida | A conexão base com a ID 35dcaad3-122a-4278 não pode ser excluída porque a conexão base está sendo usada em um ou mais fluxos. Verifique se os fluxos correspondentes foram excluídos antes de excluir uma conexão base. |
| `1419-400` | Solicitação inválida | Erro ao validar o mapeamento com id 45d90285d2d249acb87a72a2f12f7401, versão 0. Isso pode ocorrer devido a permissões inadequadas em campos mapeados. Verifique seu mapeamento ou entre em contato com seu administrador. |
| `1420-400` | Solicitação inválida | A desabilitação do estado atual não pode ser atualizada. |
| `1421-400` | Solicitação inválida | Não é possível fazer a transição da atualização do estado atual. |
| `1422-400` | Solicitação inválida | A ação de desabilitação não pode ser aplicada ao estado atual {state}. Atualize a ação e tente novamente. |
| `1423-400` | Solicitação inválida | Um campo baseSpec não tratado foi fornecido em ConnectionSpecFiltering. Atualize o campo {field} e tente novamente. |
| `1424-400` | Solicitação inválida | OrderBy é incompatível com a consulta entre sandboxes. |
| `1425-400` | Solicitação inválida | Erro ao corresponder o esquema no conjunto de dados de destino 64ef1a3c0ef com o esquema no mapeamento 91ac5a2c0eb. O esquema com a mesma ID e versão deve ser usado no mapeamento e no conjunto de dados de destino. |
| `1426-400` | Solicitação inválida | O token de usuário não está autorizado a criar/atualizar a especificação de conexão. Certifique-se de que o token do usuário está autorizado e tente novamente. |
| `1427-400` | Solicitação inválida | O token do usuário não está autorizado a criar/atualizar execuções de fluxo. Certifique-se de que o token do usuário está autorizado e tente novamente. |
| `1428-400` | Solicitação inválida | Execução de fluxo predecessora não encontrada com a id aa6a206f-f233-4c2d. |
| `1429-400` | Solicitação inválida | Fluxo predecessor não encontrado com a id aa6a206f-f233-4c2d. |
| `1430-400` | Solicitação inválida | Fluxo não encontrado com id aa6a206f-f233-4c2d. |
| `1431-400` | Solicitação inválida | A matriz vazia “fields” não é permitida na política. |
| `1432-400` | Solicitação inválida | A ordem de classificação especificada não está correta. No fieldName, prefixe + para ordem crescente ou - para ordem decrescente. |
| `1433-400` | Solicitação inválida | Campo incorreto= #id passado em orderBy, por exemplo são +name, -name, name. |
| `1434-400` | Solicitação inválida | Operação &#39;move&#39; recebida sem suporte. Use um dos tipos de operação compatíveis e tente novamente. |
| `1435-400` | Solicitação inválida | Sub-ação não suportada &#39;reverse&#39; recebida. Use um dos tipos de subação compatíveis e tente novamente. |
| `1436-400` | Solicitação inválida | PROGRESSO de suboperação sem suporte recebido para habilitação de operação. |
| `1437-400` | Solicitação inválida | Valor de status &#39;iniciado&#39; não aceito recebido. Atualize o valor de status e tente novamente. |
| `1438-400` | Solicitação inválida | Operação de agregação não suportada &#39;average&#39; recebida. |
| `1439-400` | Recurso não encontrado | O recurso de fluxos solicitado 3f4ae131-b384-4e73 não foi encontrado. Verifique a ID do recurso antes de tentar novamente. |
| `1440-400` | Solicitação inválida | Operador &#39;~&#39; não implementado. |
| `1441-400` | Solicitação inválida | Função agregada &#39;average&#39; não implementada. |
| `1442-400` | Solicitação inválida | Agregação não permitida na ID do campo. |
| `1443-400` | Solicitação inválida | O operador &#39;&lt;=&#39; não é permitido para valores múltiplos. |
| `1444-400` | Solicitação inválida | O fluxo 3f4ae131-b384-4e73 não está no estado esperado pendente. |
| `1445-400` | Solicitação inválida | Recurso de conexão PATCH não habilitado. |
| `1446-400` | Solicitação inválida | A ID do fluxo não pode ser nula ou vazia. Atualize a ID do fluxo e tente novamente. |
| `1447-400` | Solicitação inválida | Encontrados fluxos ativos contendo id aa6a206f-f233-4c2d. |
| `1448-400` | Solicitação inválida | Operador >= não compatível com a ID de campo. |
| `1449-400` | Solicitação inválida | Conexões de campo inválidas em parâmetros de filtro. |
| `1450-400` | Solicitação inválida | Operador inválido!> nos parâmetros de filtro. |
| `1451-400` | Solicitação inválida | Parâmetros inválidos testParam fornecidos em parâmetros de consulta. |
| `1452-400` | Solicitação inválida | Valor inválido 1676643256,1676643210 para o campo createdAt. |
| `1453-400` | Solicitação inválida | Valor de consulta inválido createdAt== fornecido no parâmetro de consulta. |
| `1454-400` | Solicitação inválida | Tipo de valor de filtro sem tratamento fornecido. |
| `1455-400` | Solicitação inválida | Ocorreu um erro ao validar as instruções do patch: Campo ausente &quot;keyWhichDoesNotExist&quot;. |
| `1456-400` | Solicitação inválida | Estado de exclusão-finalização não é um valor válido. Os valores permitidos são [habilitado, desabilitado, inicializando]. |
| `1457-400` | Solicitação inválida | A atualização da operação não pode ser aplicada no estado de exclusão-finalização. |
| `1458-400` | Solicitação inválida | A exclusão da operação não pode ser aplicada no estado de exclusão-finalização. |

{style="table-layout:auto"}


## Erros de verificação do token do usuário para autorização

A tabela a seguir descreve os erros relacionados à verificação do token do usuário para autorização

| Código de erro | Título | Mensagem detalhada |
| --- | --- | --- |
| `2000-401` | Token de autorização inválido | O token de autorização não tem acesso a esta organização ou a organização não existe. Certifique-se de que a organização existe ou entre em contato com seu administrador para obter acesso. |
| `2001-401` | O cabeçalho está ausente ou vazio | O cabeçalho x-gw-ims-org-id está ausente ou vazio. Atualize o valor do cabeçalho e tente novamente. |
| `2002-401` | O cabeçalho está ausente | O cabeçalho x-gw-ims-org-id está ausente na solicitação. Atualize o valor do cabeçalho e tente novamente. |
| `2100-404` | Sandbox não encontrada | Não foi possível encontrar a sandbox com o nome &#39;dev&#39;. Verifique se o nome da sandbox está correto e tente novamente. |
| `2101-404` | Sandbox não encontrada | Não foi possível encontrar a sandbox com o nome &#39;dev&#39;. Erro da API de gerenciamento de sandbox: não há sandbox com o nome &quot;dev&quot;. Verifique se o recurso existe. |
| `2102-500` | Erro de busca de sandbox por nome | Ocorreu um problema ao recuperar uma sandbox com o nome &quot;dev&quot;. Erro da API de gerenciamento de sandbox: Algo deu errado. Tente novamente. |
| `2103-404` | Sandbox não encontrada | A sandbox com a ID 8da3ef09-b469-404a e o nome dev não foi encontrada. Verifique se a ID e os valores de nome da sandbox estão corretos e tente novamente. |
| `2104-500` | Erro de busca de sandbox por identificador | Houve um problema ao recuperar uma sandbox com a id &#39;8da3ef09-b469-404a&#39; e o nome &#39;dev&#39;. Erro da API de gerenciamento de sandbox: Algo deu errado. Tente novamente. |
| `2105-400` | O cabeçalho está ausente | O cabeçalho x-sandbox-name está ausente na solicitação. Adicione o cabeçalho na solicitação e tente novamente. |
| `2106-404` | Erro de busca de sandbox padrão | Não foi possível encontrar as informações da sandbox padrão. |
| `2107-500` | Erro de busca de sandbox padrão | Ocorreu um problema ao recuperar uma sandbox padrão. Erro da API de gerenciamento de sandbox: Algo deu errado. Tente novamente. |
| `2108-500` | Erro de busca de sandboxes ativas | Ocorreu um problema ao recuperar uma sandbox ativa. Erro da API de gerenciamento de sandbox: Algo deu errado. Tente novamente. |
| `2110-400` | Cabeçalhos não permitidos | O cabeçalho x-sandbox-id não é permitido com o token do usuário. Atualize o cabeçalho e tente novamente. |
| `2111-403` | Cabeçalhos com valor restrito | O cabeçalho x-sandbox-name com o valor * é restrito com o token do usuário. Atualize o cabeçalho e o valor e tente novamente. |
| `2112-400` | Cabeçalhos com valores diferentes não permitidos | Os cabeçalhos x-sandbox-name e x-sandbox-id devem ter o valor * para consulta entre sandboxes. Atualize os cabeçalhos e tente novamente. |
| `2113-400` | Cabeçalhos com valor não permitido | Os cabeçalhos x-sandbox-id e x-sandbox-name com valor * não são permitidos para a solicitação. Atualize os cabeçalhos e tente novamente. |
| `2114-400` | Token vazio | Token vazio fornecido. Forneça um token e tente novamente. |
| `2115-400` | Token inválido | Token inválido fornecido. Forneça um token válido e tente novamente. |
| `2116-500` | Erro interno | Ocorreu um erro interno durante a decodificação offline do token de portador para a resolução do escopo. |
| `2117-500` | Erro interno | Erro interno ao verificar as permissões do usuário. Tente novamente. Se o problema persistir, entre em contato com o suporte ao cliente. |
| `2118-403` | Permissão ausente | A gravação de permissão está ausente. Entre em contato com o administrador para obter as permissões e tente novamente. |
| `2119-400` | Parâmetro de consulta ausente | O contexto da solicitação não contém o parâmetro de consulta necessário specId. Forneça o parâmetro de consulta ausente e tente novamente. |
| `2120-403` | Proibido | Você não tem permissões suficientes para executar essa operação. Entre em contato com seu administrador para obter as permissões e tente novamente. |
| `2121-403` | Proibido | O gerenciamento de permissões foi negado no recurso Enterprise Source. Entre em contato com o administrador para obter as permissões e tente novamente. |
| `2200-500` | Erro de solicitação de serviço externo | Ocorreu um problema ao chamar o Serviço de catálogo para validar o esquema. |
| `2250-500` | Erro de solicitação de serviço externo | Ocorreu um problema ao chamar o serviço de Preparação de dados para validar o mapeamento. |

{style="table-layout:auto"}
