---
title: Mensagens de erro de origens
description: Saiba mais sobre as mensagens de erro que você pode encontrar ao usar o Serviço de fluxo para fontes.
exl-id: cfba9780-4ab9-447b-8c60-c9f813107d11
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '3057'
ht-degree: 48%

---

# Mensagens de erro de origens

Este documento fornece um catálogo de mensagens de erro, descrições e resoluções sugeridas para origens.

## Erros genéricos

| Código de erro | Título | Mensagem detalhada |
| --- | --- | --- |
| `1000-400` | Solicitação inválida | A solicitação é inválida. Verifique a solicitação e tente novamente. |
| `1001-401` | Não autorizado | O usuário não está autorizado. Entre em contato com o(a) admin para obter acesso ao recurso. |
| `1002-403` | Proibido | A operação solicitada é proibida. Verifique a operação solicitada e tente novamente. |
| `1003-404` | Recurso não encontrado | O recurso solicitado não foi encontrado. Verifique a solicitação fornecida e tente novamente. |
| `1004-415` | Tipo de mídia incompatível | O formato de conteúdo fornecido não é compatível. Verifique a solicitação fornecida e tente novamente. |
| `1005-500` | Erro interno | Ocorreu um erro interno. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1006-408` | Tempo limite da solicitação | Erro ao processar a solicitação. A solicitação atingiu o tempo limite. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1007-400` | Parâmetro de cabeçalho inválido | Um parâmetro de cabeçalho inválido: {headerName} foi recebido. Verifique os parâmetros do cabeçalho e tente novamente. |
| `1008-401` | | Token de autorização inválido | O token de autorização não tem acesso a esta organização ou a organização não existe. Certifique-se de que a organização existe ou entre em contato com seu administrador para obter acesso. |
| `1009-403` | A ID da organização IMS está ausente ou em branco | O cabeçalho de solicitação de ID da organização está ausente ou vazio. Atualize o valor do cabeçalho e tente novamente. |
| `1010-500` | Mensagem detalhada inválida | O parâmetro na mensagem detalhada não foi fornecido corretamente. Verifique o parâmetro na mensagem detalhada e tente novamente. |
| `1011-503` | Serviço indisponível | O serviço está temporariamente indisponível. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1012-504` | Tempo limite do gateway | O gateway atingiu o tempo limite. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1013-412` | Falha da pré-condição | A condição definida pelos cabeçalhos If-Unmodified-Since ou If-None-Match não foi atendida. Verifique e tente novamente. |
| `1014-400` | Argumento inválido da solicitação inválida | A solicitação não pôde ser processada. {detailedMessage} |

## Erros de estrutura

| Código de erro | Título | Mensagem detalhada |
| --- | --- | --- |
| `1100-400` | Solicitação inválida | A solicitação não pôde ser processada. {detailedMessage} |
| `1101-500` | Erro interno | Ocorreu um erro interno. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1102-404` | Recurso não encontrado | O recurso solicitado não foi encontrado. {detailedMessage} |
| `1103-503` | Serviço indisponível | O serviço está temporariamente indisponível. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1104-504` | Tempo limite do gateway | O gateway atingiu o tempo limite. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1105-401` | Não autorizado | Usuário não autorizado. {detailedMessage} |
| `1106-403` | Proibido | A operação solicitada é proibida. {detailedMessage} |
| `1107-412` | Falha da pré-condição | A condição definida pelos cabeçalhos If-Unmodified-Since ou If-None-Match não é atendida. {detailedMessage} |

## Erros de criptografia

| Código de erro | Título | Mensagem detalhada |
| --- | --- | --- |
| `1200-500` | Erro interno | Ocorreu um erro interno. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1201-400` | Solicitação inválida | O flowId não pode ser nulo ou estar em branco. Forneça um flowId válido na solicitação e tente novamente. |
| `1202-400` | Solicitação inválida | O publicKeyId está ausente nas transformações do fluxo={transformations}. Forneça publicKeyId na solicitação e tente novamente. |
| `1203-400` | Solicitação inválida | A chave de criptografia não existe em relação à keyID={keyID} nas transformações do fluxo={transformations}. Verifique a keyID fornecida e tente novamente. |
| `1204-400` | Solicitação inválida | O algoritmo de criptografia fornecido é inválido. Forneça um algoritmo de criptografia válido e tente novamente. |
| `1205-400` | Solicitação inválida | A senha está ausente na seção de parâmetros da solicitação fornecida. Forneça passPhrase nos parâmetros e tente novamente. |

## Erros de REST API

| Código de erro | Título | Mensagem detalhada |
| --- | --- | --- |
| `1300-400` | Solicitação inválida | A solicitação de conexão de patch não tem suporte para o conector {connectorType}. Verifique a solicitação fornecida e tente novamente. |
| `1301-400` | Solicitação inválida | O parâmetro authSpecType fornecido: {authSpecType} não tem suporte. Forneça um tipo de especificação de autenticação válido e tente novamente. |
| `1302-400` | Solicitação inválida | O tipo de autenticação fornecido = {authType} não tem suporte para o conector={connectorType}. Forneça um tipo de autenticação válido para o conector fornecido. |
| `1303-400` | Solicitação inválida | A URL não pôde ser codificada com os parâmetros de autenticação fornecidos porque não há suporte para a codificação de URL para {value}. Verifique seus parâmetros de autenticação e tente novamente. |
| `1304-400` | Solicitação inválida | O campo obrigatório {field} não foi fornecido. Forneça o {field} e tente novamente. |
| `1305-400` | Solicitação inválida | O tipo de conector fornecido = {connectorType} não tem suporte para esta operação. |
| `1306-400` | Solicitação inválida | A conexão de destino não pode ser nula durante a validação da ID de especificação da conexão de destino. Verifique a solicitação fornecida e tente novamente. |
| `1307-400` | Solicitação inválida | A ID de especificação da conexão de destino não é válida={targetConnectionSpecId}. Valor permitido: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `1308-400` | Solicitação inválida | A solicitação não pôde ser processada. Mensagem de erro: {msftErrorMessage} |
| `1309-400` | Solicitação inválida | A transformação de criptografia fornecida é inválida porque {requiredParam} está ausente nos parâmetros. Forneça {requiredParam} e tente novamente. |
| `1310-400` | Solicitação inválida | O publicKeyId fornecido nos parâmetros expirou. Forneça um publicKeyId válido e tente novamente. |
| `1311-400` | Solicitação inválida | A publicKeyId fornecida nos parâmetros é inválida. Forneça uma publicKeyId válida e tente novamente. |
| 1312-400 | Solicitação inválida | O valor do parâmetro fornecido {paramValue} não é uma entrada válida para a propriedade={requestParam}. Forneça um valor de parâmetro válido e tente novamente. |
| `1313-400` | Solicitação inválida | O atributo de caminho {attribute} não existe. Verifique se o atributo existe e tente novamente. |
| `1314-400` | Solicitação inválida | Um caminho complexo foi fornecido, mas não é permitido. Certifique-se de que um caminho complexo não seja fornecido e tente novamente. |
| `1315-400` | Solicitação inválida | O caminho fornecido {path} deve apontar para uma matriz de registros. Verifique se o caminho fornecido aponta para a matriz de registros e tente novamente. |
| `1316-400` | Solicitação inválida | Os parâmetros de paginação fornecidos não podem ficar vazios. Forneça parâmetros de paginação válidos e tente novamente. |
| `1317-400` | Solicitação inválida | Os parâmetros de programação fornecidos estão vazios, apesar de não poderem. Forneça parâmetros de programação válidos e tente novamente. |
| `1318-400` | Solicitação inválida | {combinedMessage}. Verifique a solicitação fornecida e tente novamente. |
| `1319-400` | Solicitação inválida | O {param} deve fazer parte da coleção pai. Forneça {param} na coleção pai e tente novamente. |
| `1320-400` | Solicitação inválida | O {idType} não pode ser nulo ou vazio. Forneça um {idType} válido e tente novamente. |
| `1321-400` | Solicitação inválida | O comprimento de {idType} deve ser um, o tamanho fornecido é {size}. Forneça um tamanho válido e tente novamente. |
| `1322-400` | Solicitação inválida | A conexão de origem não pode ser nula na criação da referência de esquema. Forneça uma conexão de origem válida e tente novamente. |
| `1323-400` | Solicitação inválida | O {entity} não pode ser nulo ou vazio na conexão de origem: {sourceConnection}. Forneça um {entity} válido e tente novamente. |
| `1324-400` | Solicitação inválida | A conexão de destino não pode ser nula ao extrair a ID do conjunto de dados. Forneça uma conexão de destino válida e tente novamente. |
| `1325-400` | Solicitação inválida | O parâmetro dataSetId não pode ser nulo ou vazio na conexão de destino: {TargetConnection}. Forneça um parâmetro dataSetId válido e tente novamente. |
| `1326-400` | Solicitação inválida | A conexão de origem não pode ser nula ao buscar o formato de origem. Forneça uma conexão de origem válida e tente novamente. |
| `1327-400` | Solicitação inválida | Não há suporte para o formato de dados de origem fornecido={sourceFormat} em SourceConnection. Valores permitidos: {values}. Forneça os valores permitidos e tente novamente. |
| `1328-400` | Solicitação inválida | A transformação de mapeamento não pode ser nula ao extrair {param}. Forneça uma transformação de mapeamento válida e tente novamente. |
| `1329-400` | Solicitação inválida | O parâmetro: {param} não pode ser nulo ou vazio na solicitação fornecida. Forneça um {param} válido e tente novamente. |
| `1330-400` | Solicitação inválida | Nenhuma coluna foi encontrada para a tabela {tableName}. Forneça um nome de tabela válido e tente novamente. |
| `1331-400` | Solicitação inválida | O delimitador de coluna não pode ter mais de um caractere em SourceConnection: {sourceConnection}. Forneça um delimitador de coluna válido e tente novamente. |
| `1332-400` | Solicitação inválida | A solicitação de conexão de origem com connectionSpecId: {connectionSpecId} não pode ter um baseConnectionId. Remova o baseConnectionId e tente novamente. |
| `1333-400` | Solicitação inválida | O flowRunAction={flowRunAction} não tem suporte para a origem com a id de especificação={specId}. Forneça uma ação de execução de fluxo válida e tente novamente. |
| `1334-400` | Solicitação inválida | O parâmetro de consulta : {param} não pode estar vazio. Forneça um {param} válido e tente novamente. |
| `1335-400` | Solicitação inválida | Erro ao serializar os parâmetros de filtro para exploração. Verifique sua solicitação de parâmetros de filtro e tente novamente. |
| `1336-400` | Solicitação inválida | A conexão de exploração não tem suporte para a ID de especificação de conexão: {connectionSpecId}. Forneça a ID de especificação de conexão compatível e tente novamente. |
| `1337-400` | Solicitação inválida | O {QueryParam} não pode ficar vazio para objectType={objectType}. Forneça um {QueryParam} válido e tente novamente. |
| `1338-400` | Solicitação inválida | A ID de conexão {connectionType} não pode ser nula em flowRequest. Forneça uma ID de conexão {connectionType} válida em flowRequest. |
| `1339-400` | Solicitação inválida | O formato da organização={imsOrg} fornecido na solicitação é inválido. Forneça uma ID de organização válida e tente novamente. |
| `1340-400` | Solicitação inválida | Erro ao analisar {time}. Verifique o formato de hora fornecido na solicitação e tente novamente. |
| `1341-400` | Solicitação inválida | O ODI Json fornecido está vazio. Forneça um ODI Json válido e tente novamente. |
| `1342-400` | Solicitação inválida | O segmento &quot;dls:folder&quot; em &quot;odi.json&quot; não tem definições. Forneça as definições apropriadas em &quot;odi.json&quot; e tente novamente. |
| `1343-400` | Solicitação inválida | Os segmentos &quot;dls:entityReferences&quot; e &quot;dls:partitionSpec&quot; em &quot;odi.json&quot; não têm definições. Forneça as definições apropriadas em &quot;odi.json&quot; e tente novamente. |
| `1344-400` | Solicitação inválida | A definição para &#39;dls:partitionSpec&#39; em &#39;odi.json&#39; é inválida porque mais de uma partitionSpecs foi encontrada. Forneça as definições apropriadas em &quot;odi.json&quot; e tente novamente. |
| `1345-400` | Solicitação inválida | Definições ausentes em um ou mais segmentos em caminhos: &#39;dls:partitionSpec/dls:fileFormat&#39;, &#39;dls:partitionSpec/dls:partitionTemplate&#39;,&#39;dls:partitionSpec/dls:fileFormat/@type&#39;, &#39;dls:partitionSpec/dls:fileFormat/dls:csvDelimiters&#39; em &#39;odi.json&#39;. Forneça as definições apropriadas em &quot;odi.json&quot; e tente novamente. |
| `1346-400` | Solicitação inválida | A definição &#39;@type&#39; fornecida em &#39;dls:fileFormat&#39; em &#39;odi.json&#39; é inválida. Forneça as definições apropriadas em &quot;odi.json&quot; e tente novamente. |
| `1347-400` | Solicitação inválida | Não há suporte para a definição dls:csvDelimiters em &#39;odi.json&#39;. Os csvDelimiters com suporte são: [&#39;,&#39;]. Forneça as definições apropriadas em &quot;odi.json&quot; e tente novamente. |
| `1348-400` | Solicitação inválida | Erro ao desserializar &#39;dls:entityReferences&#39;. Verifique se os dados estão em um formato válido e tente novamente. |
| `1349-400` | Solicitação inválida | Os parâmetros de filtro fornecidos são inválidos. Forneça parâmetros de filtro válidos e tente novamente. |
| `1350-400` | Solicitação inválida | Nenhum operador foi fornecido para o filtro na origem. Forneça uma solicitação de filtro válida com o operador apropriado e tente novamente. |
| `1351-400` | Solicitação inválida | O operador fornecido {operator} não tem suporte para o filtro na origem deste conector. Forneça um operador válido e tente novamente. |
| `1352-400` | Solicitação inválida | O operador fornecido {operator} não pode ser mapeado para nenhum operador nativo com suporte para {ql}. Forneça um operador válido e tente novamente. |
| `1353-400` | Solicitação inválida | O filtro na origem ainda não tem suporte para o conector {connectorType}. Verifique os conectores compatíveis na documentação: https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/filter.html?lang=pt-BR. |
| `1354-400` | Solicitação inválida | O idioma de consulta {ql} ainda não tem suporte para o filtro na origem. Forneça um idioma de consulta válido e tente novamente. |
| `1355-400` | Solicitação inválida | O tipo de filtro fornecido é inválido. O tipo de filtro suportado é PQL. Forneça um tipo de filtro válido e tente novamente. |
| `1356-400` | Solicitação inválida | O formato de filtro fornecido é inválido. O formato de filtro compatível é: pql/json. Forneça um formato de filtro válido e tente novamente. |
| `1357-400` | Solicitação inválida | O filtro fornecido é inválido. O valor deve ser fornecido com filtros detalhados. Forneça um filtro válido e tente novamente. |
| `1358-400` | Solicitação inválida | O parâmetro &#39;objectType&#39; fornecido é inválido. Forneça um objectType válido e tente novamente. |
| `1359-400` | Solicitação inválida | O parâmetro {param} está ausente na solicitação. Forneça um {param} válido e tente novamente. |
| `1360-400` | Solicitação inválida | A hora de início não pode ser definida no passado. Forneça uma hora de início válida e tente novamente. |
| `1361-400` | Solicitação inválida | O intervalo não é permitido com assimilações únicas. Remova o intervalo ou altere a frequência e tente novamente. |
| `1362-400` | Solicitação inválida | O intervalo não pode ser menor que {minInterval}. Forneça um valor de intervalo válido e tente novamente. |
| `1363-400` | Solicitação inválida | O intervalo {interval} não é permitido com frequência: {frequency}. Forneça um valor de intervalo válido e tente novamente. |
| `1364-400` | Solicitação inválida | O sinalizador de preenchimento retroativo não é permitido quando a frequência está definida como uma vez. Remova o sinalizador de preenchimento retroativo quando a frequência estiver definida como uma vez e tente novamente. |
| `1365-400` | Solicitação inválida | O caminho {path} fornecido em operações é inválido. Forneça um caminho válido {path} e tente novamente. |
| `1366-400` | Solicitação inválida | A hora de início já passou e a operação de atualização não é mais permitida. |
| `1367-400` | Solicitação inválida | A coluna delta é necessária na transformação de cópia ao criar um conector CRM. Forneça a coluna delta e tente novamente. |
| `1368-400` | Solicitação inválida | O modo não é permitido na solicitação de fluxo. Verifique sua solicitação e tente novamente. |
| `1369-400` | Solicitação inválida | A coluna delta na transformação de cópia não é permitida quando a frequência está definida como uma vez. Remova a coluna delta e tente novamente. |
| `1370-400` | Solicitação inválida | Não foi possível buscar as colunas de origem para assimilação porque a transformação de mapeamento está ausente. Adicione a transformação de mapeamento e tente novamente. |
| `1371-400` | Solicitação inválida | A detecção de propriedades de arquivo não tem suporte para o conector {connectorType}. Forneça as propriedades do arquivo manualmente. |
| `1372-400` | Solicitação inválida | A operação atual não é permitida. Explorar via especificação de conexão não é permitido para a especificação de conexão ID={connectionSpecId}. |
| `1373-400` | Solicitação inválida | O flowSpecType está ausente na solicitação. Forneça um flowSpecType válido e tente novamente. |
| `1374-400` | Solicitação inválida | Os parâmetros de consulta fornecidos são inválidos. Não é possível ter o sinalizador determineProperties e propriedades definidas pelo usuário na mesma solicitação. Corrija sua solicitação e tente novamente. |
| `1375-400` | Solicitação inválida | Falha na detecção das propriedades do arquivo. Insira as propriedades manualmente. |
| `1376-400` | Solicitação inválida | Não há suporte para a detecção de propriedades do arquivo para a especificação de conexão id={connectionSpecId}. Forneça as propriedades do arquivo manualmente. |
| `1377-400` | Solicitação inválida | O parâmetro de valor fornecido é nulo e não pode ser comparado com o operador {operator}. Forneça um parâmetro de valor válido e tente novamente. |
| `1378-400` | Solicitação inválida | Erro ao validar a coluna de entrada {column} para o filtro na origem. O nome da coluna deve ser válido na tabela. Forneça um nome de coluna válido e tente novamente. |
| `1379-400` | Solicitação inválida | Erro ao validar a entrada {value} para filtro na origem. A coluna DataType na origem é {columnDataType} e o valor DataType [String] não corresponde. Forneça um {value} válido e tente novamente. |
| `1380-400` | Solicitação inválida | Falha ao criar execução de fluxo. Mensagem de erro: {message} |
| `1381-400` | Solicitação inválida | WindowEndTime={endTime} não pode ser anterior a Window StartTime={startTime}. Forneça uma hora de término válida e tente novamente. |
| `1382-400` | Solicitação inválida | A coluna delta deve corresponder ao valor presente nas transformações de cópia do fluxo. Forneça uma coluna delta válida e tente novamente. |
| `1383-400` | Solicitação inválida | A coluna delta está ausente nos parâmetros recebidos para criar uma execução de fluxo. Forneça a coluna delta nos parâmetros e tente novamente. |
| `1384-400` | Solicitação inválida | Os parâmetros={params} fornecidos para a execução do fluxo de criação são inválidos ou estão vazios. Forneça parâmetros válidos e tente novamente. |
| `1385-400` | Solicitação inválida | O connectorType={connectorType} fornecido não tem suporte para a criação de execuções de fluxo. Forneça um connectorType válido e tente novamente. |
| `1386-400` | Solicitação inválida | Não há suporte para flowId={flowId} com scheduleParams frequency={frequency} para a criação de execuções de fluxo. Forneça uma frequência válida e tente novamente. |
| `1387-400` | Solicitação inválida | O flowRunId={flowRunId} está em um estado inválido={state} para disparar novamente. Tente novamente dentro de alguns minutos e entre em contato com o suporte ao cliente se o problema persistir. |
| `1388-400` | Solicitação inválida | O fluxo={flow} está no estado={state} e não pode ser disparado novamente. O fluxo deve estar no estado ativado para ser acionado novamente. |
| `1389-400` | Solicitação inválida | Erro ao analisar a string codificada na base64 fornecida. Forneça uma string de filtro codificada válida e tente novamente. |
| `1390-400` | Solicitação inválida | O operador &#39;not&#39; não pode ter mais de uma comparação. Forneça um número válido de comparações e tente novamente. |
| `1391-400` | Solicitação inválida | Falha ao analisar SchemaMetaData em sourceConnection para Id={sourceConnectionId}. Verifique o schemaMetaData em sua solicitação e tente novamente. |
| `1392-400` | Solicitação inválida | Falha ao analisar Transformações na solicitação de fluxo para flowId={flowId}. Verifique as transformações em sua solicitação e tente novamente. |
| `1393-400` | Solicitação inválida | O parâmetro fornecido {parameter} é nulo ou está vazio. Forneça um {parameter} válido e tente novamente. |
| `1394-400` | Solicitação inválida | O valor mínimo para um parâmetro {parameter} é um. Forneça um {parameter} válido e tente novamente. |
| `1395-400` | Solicitação inválida | A conexão de origem encontrada no fluxo é nula ou está vazia. Forneça uma conexão de origem válida no fluxo e tente novamente. |
| `1396-400` | Solicitação inválida | Não foi possível encontrar um formato correspondente. Forneça um formato correspondente e tente novamente. |
| `1397-400` | Solicitação inválida | A frequência fornecida: {frequency} é inválida. Forneça uma frequência válida e tente novamente. |
| `1398-400` | Solicitação inválida | A operação fornecida: {action} não tem suporte. Verifique a operação fornecida e tente novamente. |
| `1399-400` | Solicitação inválida | Não foi possível localizar um requestFileType válido. Forneça um requestFileType válido e tente novamente. |
| `1400-400` | Solicitação inválida | O parâmetro &#39;templateType&#39; fornecido é inválido. Forneça um tipo de modelo válido e tente novamente. |
| `1401-400` | Solicitação inválida | A ação de execução de fluxo fornecida={flowRunAction} não tem suporte. Forneça uma ação de execução de fluxo válida e tente novamente. |
| `1402-500` | Erro interno | Ocorreu um erro interno. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1403-400` | Solicitação inválida | A hora de início já passou e você não pode mais alterar a frequência para uma vez. |
| `1404-400` | Solicitação inválida | A hora de início já passou e você não pode mais atualizar o preenchimento retroativo. |

## Exceções do Serviço de Fluxo (1600-1699)

| Código de erro | Título | Mensagem detalhada |
| --- | --- | --- |
| `1600-400` | Solicitação inválida | A solicitação não pôde ser processada. {detailedMessage} |
| `1601-500` | Erro interno | Ocorreu um erro interno. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1602-404` | Recurso não encontrado | O recurso solicitado não foi encontrado. {detailedMessage} |
| `1603-503` | Serviço indisponível | O serviço está temporariamente indisponível. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1604-504` | Tempo limite do gateway | O gateway atingiu o tempo limite. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1605-401` | Não autorizado | Usuário não autorizado. {detailedMessage} |
| `1606-403` | Proibido | A operação solicitada é proibida. {detailedMessage} |
| `1607-412` | Falha da pré-condição | A condição definida pelos cabeçalhos If-Unmodified-Since ou If-None-Match não é atendida. {detailedMessage} |

## Erros de Data Landing Zone

| Código de erro | Título | Mensagem detalhada |
| --- | --- | --- |
| `1700-500` | Erro interno | Ocorreu um erro interno. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1701-400` | Solicitação inválida | A zona de destino fornecida está inativa. Ative a zona de destino e tente novamente. |
| `1702-400` | Solicitação inválida | O Tipo SAS={sasType} fornecido para a zona de aterrissagem não é permitido. Forneça uma SAS válida e tente novamente. |
| `1703-400` | Solicitação inválida | A atualização de credenciais não é permitida. |
| `1704-400` | Solicitação inválida | As chaves retornadas para storageAccountName={accountName} em subscriptionId={subscriptionId} e resourceGroupName={resourceGroupName} estão malformadas. Verifique sua solicitação e tente novamente. Entre em contato com o suporte se o problema persistir. |
| `1705-400` | Solicitação inválida | A ação de zona de destino de dados fornecida é incompatível. Forneça uma ação válida e tente novamente. |
| `1706-400` | Solicitação inválida | A configuração de ativações permitidas não está configurada corretamente para a zona de aterrissagem={landingZoneType}. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1707-400` | Solicitação inválida | Falha ao iniciar o serviço porque a configuração da zona de destino não pode ser nula ou estar vazia. Certifique-se de que a configuração da zona de destino não seja nula e tente novamente. |
| `1708-400` | Solicitação inválida | A configuração do contêiner não pode ser nula em landingZoneType={landingZoneType}. Verifique se a configuração do contêiner não é nula e tente novamente. |
| `1709-400` | Solicitação inválida | Os detalhes SAS não podem ser nulos para {tokenConfig} em landingZoneType={landingZoneType}. Forneça um SAS válido na configuração e tente novamente. |
| `1710-400` | Solicitação inválida | A zona de aterrissagem fornecida do tipo: {landingZoneUseCase} não tem suporte. Forneça um tipo de zona de aterrissagem válido e tente novamente. |
| `1711-400` | Solicitação inválida | Os detalhes SAS não foram encontrados para a zona de aterrissagem de dados fornecida do tipo: {landingZoneUseCase}. Verifique se os detalhes do SAS são fornecidos para o tipo de zona de aterrissagem fornecido. |
| `1712-400` | Solicitação inválida | A ação de zona de aterrissagem fornecida: {actionType} não é permitida. Forneça uma ação de zona de aterrissagem de dados válida e tente novamente. |
| `1713-400` | Solicitação inválida | O {OperationType} não é permitido para o {tokenType} fornecido. Verifique sua solicitação e tente novamente. |
| `1714-400` | Solicitação inválida | O clientId={clientId} não tem permissão para executar esta operação. Verifique sua solicitação com permissões e tente novamente. |
