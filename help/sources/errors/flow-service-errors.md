---
title: Mensagens de Erro do Serviço de Fluxo
description: Saiba mais sobre as mensagens de erro que podem ser encontradas ao usar o Serviço de fluxo para fontes.
source-git-commit: 10edb5dfd9ce99b69cf5bb014f4903942c9bff3e
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 1%

---

# Mensagens de erro do Serviço de Fluxo

O Serviço de fluxo é usado para coletar e centralizar dados do cliente de várias fontes diferentes no Platform. O serviço fornece uma interface de usuário e uma RESTful API que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar sistemas de terceiros, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

Este documento fornece um catálogo de mensagens de erro, descrições e resoluções sugeridas relacionadas ao Serviço de Fluxo.

## Erros de validação interna no Serviço de Fluxo

A tabela a seguir descreve erros relacionados à validação interna no Serviço de Fluxo.

| Código de erro | Título | Mensagem detalhada |
| --- | --- | --- |
| `1100-400` | Solicitação inválida | Não foi possível processar a solicitação. Erro do provedor de fluxo: Não tem direito a esta operação. |
| `1101-404` | Recurso não encontrado | O recurso solicitado não foi encontrado. Erro do provedor de fluxo: O recurso com a id fornecida não existe. |
| `1102-500` | Erro interno | Ocorreu um erro interno. Tente novamente. Se o problema persistir, entre em contato com o suporte ao cliente. |
| `1103-503` | Serviço Indisponível | O serviço está temporariamente indisponível. Tente novamente. Se o problema persistir, entre em contato com o suporte ao cliente. |
| `1104-504` | Tempo limite do gateway | Ocorreu um tempo limite de gateway. Tente novamente. Se o problema persistir, entre em contato com o suporte ao cliente. |
| `1400-500` | Erro interno | Ocorreu um erro interno. Tente novamente. Se o problema persistir, entre em contato com o suporte ao cliente. |
| `1401-400` | Solicitação inválida | Os parâmetros de limite e contagem não podem ser fornecidos juntos na mesma solicitação. Forneça somente o limite ou o parâmetro de contagem e tente novamente. |
| `1402-400` | Solicitação inválida | A ação &quot;finalizar&quot; é suportada apenas para solicitações do provedor. |
| `1403-400` | Cabeçalho ausente | O cabeçalho &#39;If-Match&#39; está ausente na solicitação. Forneça o cabeçalho e tente novamente. |
| `1404-412` | Versão não correspondente | A versão fornecida &#39;v1&#39; não corresponde à versão atual na entidade &#39;cc01fc2c-0000-0200&#39;. Certifique-se de que a versão fornecida corresponde à versão atual na entidade e tente novamente. |
| `1405-400` | Solicitação inválida | O corpo da solicitação não pode ser nulo ou vazio. Forneça um corpo de solicitação e tente novamente. |
| `1406-400` | Solicitação inválida | A suboperação &quot;progress&quot; não pode ser aplicada com outras suboperações. Atualize a lista de suboperações e tente novamente. |
| `1407-400` | Solicitação inválida | O status falhou não pode ser usado com o `progress` sub-Op. Remova o `progress` subOp ou use o status=&#39;inProgress&#39; e tente novamente. |
| `1408-400` | Solicitação inválida | A porcentagem concluída deve ser 100 para os estados concluídos ou com falha. Atualize a porcentagem concluída e tente novamente. |
| `1409-400` | Solicitação inválida | A operação &#39;finalize&#39; não pode ser aplicada no estado atual ativado-finalizando. Atualize a operação e tente novamente. |
| `1410-400` | Solicitação inválida | `State` não é permitido na solicitação de criação de fluxo. |
| `1411-400` | Solicitação inválida | Não é possível recuperar entityId. Solicitação inválida recebida com o caminho &#39;baseConnections/123&#39;. |
| `1412-400` | Solicitação inválida | Versão de mapeamento inválida na solicitação. Forneça a versão correta do mapeamento. |
| `1413-400` | Solicitação inválida | A ID de especificação fornecida é inválida. Forneça uma ID de especificação válida e tente novamente. |
| `1414-400` | Solicitação inválida | Não é possível atualizar a especificação de ligação de uma ligação. |
| `1415-400` | Solicitação inválida | Não foi possível encontrar a especificação de autenticação &#39;authConnection&#39; para a ID de especificação de conexão ba6e206f-f233-ab16. |
| `1416-400` | Solicitação inválida | A opção Excluir ou Atualizar só pode ser aplicada em conexão com o estado ativado, desativado ou de inicialização. |
| `1417-400` | Solicitação inválida | Excluir ou atualizar em conexões em `initializing` não são permitidos estados com UserToken. |
| `1418-400` | Solicitação inválida | A conexão base com a ID 35dcaad3-122a-4278 não pode ser excluída porque a conexão base está sendo usada em um ou mais fluxos. Certifique-se de que os fluxos correspondentes sejam excluídos antes de excluir uma conexão base. |
| `1419-400` | Solicitação inválida | Erro ao validar o mapeamento com id 45d90285d2d249acb87a72a2f12f7401, versão 0. Isso pode ser devido a permissões inadequadas em campos mapeados. Verifique seu mapeamento ou entre em contato com seu administrador. |
| `1420-400` | Solicitação inválida | Não é possível atualizar o estado atual de desativação. |
| `1421-400` | Solicitação inválida | A atualização de estado atual não pode ser transferida. |
| `1422-400` | Solicitação inválida | A desativação da ação não pode ser aplicada no estado atual {state}. Atualize a ação e tente novamente. |
| `1423-400` | Solicitação inválida | Um campo não manipulado baseSpec foi fornecido em ConnectionSpecFiltering. Atualize o campo {field} e tente novamente. |
| `1424-400` | Solicitação inválida | O OrderBy não é compatível com a consulta de sandbox cruzada. |
| `1425-400` | Solicitação inválida | Erro ao corresponder o esquema no conjunto de dados de destino 64ef1a3c0ef com o esquema no mapeamento 91ac5a2c0eb. Esquema com a mesma id e versão devem ser usados no mapeamento e no conjunto de dados de destino. |
| `1426-400` | Solicitação inválida | O token de usuário não está autorizado a criar/atualizar a especificação de conexão. Certifique-se de que o token de usuário está autorizado e tente novamente. |
| `1427-400` | Solicitação inválida | O token de usuário não está autorizado a criar/atualizar fluxos em execução. Certifique-se de que o token de usuário está autorizado e tente novamente. |
| `1428-400` | Solicitação inválida | Fluxo do antecessor não encontrado com id aa6a206f-f233-4c2d. |
| `1429-400` | Solicitação inválida | Fluxo do antecessor não encontrado com id aa6a206f-f233-4c2d. |
| `1430-400` | Solicitação inválida | Fluxo não encontrado com id aa6a206f-f233-4c2d. |
| `1431-400` | Solicitação inválida | &#39;campos&#39; de matriz vazios não é permitido na política. |
| `1432-400` | Solicitação inválida | A ordem de classificação especificada não está correta, anexe + em ordem crescente e - em ordem decrescente no fieldName. |
| `1433-400` | Solicitação inválida | Campo incorreto= #id transmitido em orderBy, por exemplo, são +name, -name, name. |
| `1434-400` | Solicitação inválida | Operação &#39;mover&#39; não suportada recebida. Use um dos tipos de operação suportados e tente novamente. |
| `1435-400` | Solicitação inválida | Sub-ação &#39;reversa&#39; não suportada recebida. Use um dos tipos de sub-ação compatíveis e tente novamente. |
| `1436-400` | Solicitação inválida | O PROGRESS de sub-operação não suportado foi recebido para ativar a operação. |
| `1437-400` | Solicitação inválida | Valor de status &#39;iniciado&#39; não suportado recebido. Atualize o valor de status e tente novamente. |
| `1438-400` | Solicitação inválida | Operação de agregação sem suporte &quot;média&quot; recebida. |
| `1439-400` | Recurso não encontrado | O recurso de fluxos solicitados 3f4ae131-b384-4e73 não foi encontrado. Verifique a ID do recurso antes de tentar novamente. |
| `1440-400` | Solicitação inválida | Operador &#39;~&#39; não implementado. |
| `1441-400` | Solicitação inválida | Função agregada &quot;média&quot; não implementada. |
| `1442-400` | Solicitação inválida | Agregação não permitida na id do campo. |
| `1443-400` | Solicitação inválida | O operador &#39;&lt;=&#39; não é permitido para vários valores. |
| `1444-400` | Solicitação inválida | O fluxo 3f4ae131-b384-4e73 não está no estado esperado pendente. |
| `1445-400` | Solicitação inválida | Recurso de Conexão PATCH não habilitado. |
| `1446-400` | Solicitação inválida | A ID de fluxo não pode ser nula ou vazia. Atualize o ID de fluxo e tente novamente. |
| `1447-400` | Solicitação inválida | Foram encontrados fluxos ativos contendo id aa6a206f-f233-4c2d. |
| `1448-400` | Solicitação inválida | Operador >= não é compatível com a id de campo. |
| `1449-400` | Solicitação inválida | Conexões de campo inválidas em parâmetros de filtro. |
| `1450-400` | Solicitação inválida | Operador inválido !> em parâmetros de filtro. |
| `1451-400` | Solicitação inválida | Params inválidos testParam fornecido em parâmetros de consulta. |
| `1452-400` | Solicitação inválida | Valor inválido 1676643256,1676643210 para campo createdAt. |
| `1453-400` | Solicitação inválida | Valor de consulta inválido criadoAt= fornecido no parâmetro de consulta. |
| `1454-400` | Solicitação inválida | Tipo de valor de filtro não manipulado fornecido. |
| `1455-400` | Solicitação inválida | Ocorreu um erro ao validar as instruções de correção: Campo ausente &quot;keyWhichDoesNotExist&quot;. |
| `1456-400` | Solicitação inválida | A finalização da exclusão de estado não é um valor válido. Os valores permitidos são [ativado, desativado, inicializando]. |
| `1457-400` | Solicitação inválida | A atualização da operação não pode ser aplicada no estado delete-finalizing. |
| `1458-400` | Solicitação inválida | A exclusão da operação não pode ser aplicada na finalização da exclusão de estado. |

{style="table-layout:auto"}


## Erros de verificação do token de usuário para autorização

A tabela a seguir descreve os erros relativos à verificação do token de usuário para autorização

| Código de erro | Título | Mensagem detalhada |
| --- | --- | --- |
| `2000-401` | Token de autorização inválido | O token de autorização não tem acesso a esta organização ou a organização não existe. Certifique-se de que a organização existe ou entre em contato com o administrador para obter acesso. |
| `2001-401` | Cabeçalho ausente ou vazio | O cabeçalho x-gw-ims-org-id está ausente ou vazio. Atualize o valor do cabeçalho e tente novamente. |
| `2002-401` | Cabeçalho ausente | O cabeçalho x-gw-ims-org-id está ausente na solicitação. Atualize o valor do cabeçalho e tente novamente. |
| `2100-404` | Sandbox não encontrada | Não foi possível encontrar a sandbox com o nome &#39;dev&#39;. Certifique-se de que o nome da sandbox está correto e tente novamente. |
| `2101-404` | Sandbox não encontrada | Não foi possível encontrar a sandbox com o nome &#39;dev&#39;. Erro da API de gerenciamento de sandbox: Sandbox com o nome &#39;dev&#39; não presente. Verifique se o recurso existe. |
| `2102-500` | Obter sandbox por erro de nome | Ocorreu um problema ao obter uma sandbox com o nome &#39;dev&#39;. Erro da API de gerenciamento de sandbox: Algo deu errado. Tente novamente. |
| `2103-404` | Sandbox não encontrada | Não foi possível encontrar a sandbox com ID 8da3ef09-b469-404a e nome dev. Certifique-se de que os valores de ID e nome da sandbox estejam corretos e tente novamente. |
| `2104-500` | Obter sandbox por erro de identificador | Ocorreu um problema ao recuperar uma sandbox com o id &#39;8da3ef09-b469-404a&#39; e o nome &#39;dev&#39;. Erro da API de gerenciamento de sandbox: Algo deu errado. Tente novamente. |
| `2105-400` | Cabeçalho ausente | O cabeçalho x-sandbox-name está ausente na solicitação. Adicione o cabeçalho na solicitação e tente novamente. |
| `2106-404` | Obter erro de sandbox padrão | Não foi possível encontrar as informações da sandbox predefinida. |
| `2107-500` | Obter erro de sandbox padrão | Ocorreu um problema ao obter uma sandbox predefinida. Erro da API de gerenciamento de sandbox: Algo deu errado. Tente novamente. |
| `2108-500` | Erro ao obter sandboxes ativas | Ocorreu um problema ao obter uma sandbox ativa. Erro da API de gerenciamento de sandbox: Algo deu errado. Tente novamente. |
| `2110-400` | Cabeçalhos não permitidos | O x-sandbox-id do cabeçalho não é permitido com o token de usuário. Atualize o cabeçalho e tente novamente. |
| `2111-403` | Cabeçalhos com valor restrito | O cabeçalho x-sandbox-name com valor * é restrito com o token de usuário. Atualize o cabeçalho e o valor e tente novamente. |
| `2112-400` | Cabeçalhos com valor diferente não permitidos | Os cabeçalhos x-sandbox-name e x-sandbox-id devem ter o valor * para consulta entre sandboxes. Atualize os cabeçalhos e tente novamente. |
| `2113-400` | Cabeçalhos com valor não permitido | Os cabeçalhos x-sandbox-id e x-sandbox-name com valor * não são permitidos para a solicitação. Atualize os cabeçalhos e tente novamente. |
| `2114-400` | Token vazio | Token vazio fornecido. Forneça um token e tente novamente. |
| `2115-400` | Token inválido | Token inválido fornecido. Forneça um token válido e tente novamente. |
| `2116-500` | Erro interno | Ocorreu um erro interno durante a decodificação offline do token portador para resolução do escopo. |
| `2117-500` | Erro interno | Ocorreu um erro interno ao verificar as permissões do utilizador. Tente novamente. Se o problema persistir, entre em contato com o suporte ao cliente. |
| `2118-403` | Permissão ausente | A gravação de permissão está ausente. Entre em contato com o administrador para resolver as permissões e tente novamente. |
| `2119-400` | Parâmetro de consulta ausente | O contexto da solicitação não contém o parâmetro de consulta obrigatório specId. Forneça o parâmetro de consulta ausente e tente novamente. |
| `2120-403` | Proibido | Você não tem permissões suficientes para executar a operação. Entre em contato com o administrador para resolver as permissões e tente novamente. |
| `2121-403` | Proibido | O gerenciamento de permissões é negado no recurso Origem Empresarial. Entre em contato com o administrador para resolver as permissões e tente novamente. |
| `2200-500` | Erro de solicitação de serviço externo | Ocorreu um problema ao chamar o serviço Catálogo para validar o esquema. |
| `2250-500` | Erro de solicitação de serviço externo | Ocorreu um problema ao chamar o serviço de Preparação de dados para validar o mapeamento. |

{style="table-layout:auto"}