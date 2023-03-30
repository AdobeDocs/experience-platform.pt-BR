---
title: Mensagens de erro das fontes
description: Saiba mais sobre as mensagens de erro que podem ser encontradas ao usar o Serviço de fluxo para fontes.
source-git-commit: 10edb5dfd9ce99b69cf5bb014f4903942c9bff3e
workflow-type: tm+mt
source-wordcount: '3192'
ht-degree: 8%

---

# Mensagens de erro das fontes

Este documento fornece um catálogo de mensagens de erro, descrições e resoluções sugeridas para fontes.

## Erros genéricos

| Código de erro | Título | Mensagem detalhada |
| --- | --- | --- |
| `1000-400` | Solicitação inválida | A solicitação é inválida. Verifique a solicitação e tente novamente. |
| `1001-401` | Não autorizado | O usuário não está autorizado. Entre em contato com o administrador para obter acesso ao recurso. |
| `1002-403` | Proibido | A operação solicitada é proibida. Verifique a operação solicitada e tente novamente. |
| `1003-404` | Recurso não encontrado | O recurso solicitado não foi encontrado. Verifique a solicitação fornecida e tente novamente. |
| `1004-415` | Tipo de mídia não suportado | Não há suporte para o formato de carga útil fornecido. Verifique a solicitação fornecida e tente novamente. |
| `1005-500` | Erro interno | Ocorreu um erro interno. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1006-408` | Tempo limite da solicitação | Erro ao processar a solicitação. O tempo limite da solicitação foi excedido. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1007-400` | Parâmetro de cabeçalho inválido | Um parâmetro de cabeçalho inválido: {headerName} foi recebido. Verifique os parâmetros do cabeçalho e tente novamente. |
| `1008-401` |  | Token de autorização inválido | O token de autorização não tem acesso a esta organização ou a organização não existe. Certifique-se de que a organização existe ou entre em contato com o administrador para obter acesso. |
| `1009-403` | A ID da organização IMS está ausente ou vazia | O cabeçalho da solicitação de ID da organização está ausente ou vazio. Atualize o valor do cabeçalho e tente novamente. |
| `1010-500` | Mensagem detalhada inválida | O parâmetro na mensagem detalhada não foi fornecido corretamente. Verifique o parâmetro na mensagem detalhada e tente novamente. |
| `1011-503` | Serviço Indisponível | O serviço está temporariamente indisponível. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1012-504` | Tempo limite do gateway | Ocorreu um tempo limite de gateway. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1013-412` | Falha na Pré-Condição | A condição definida pelos cabeçalhos If-Unmodified-Since ou If-None-Match não é cumprida. Verifique e tente novamente. |
| `1014-400` | Argumento inválido de solicitação incorreta | Não foi possível processar a solicitação. {detailMessage} |

## Erros de estrutura

| Código de erro | Título | Mensagem detalhada |
| --- | --- | --- |
| `1100-400` | Solicitação inválida | Não foi possível processar a solicitação. {detailMessage} |
| `1101-500` | Erro interno | Ocorreu um erro interno. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1102-404` | Recurso não encontrado | O recurso solicitado não foi encontrado. {detailMessage} |
| `1103-503` | Serviço Indisponível | O serviço está temporariamente indisponível. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1104-504` | Tempo limite do gateway | Ocorreu um tempo limite de gateway. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1105-401` | Não autorizado | O usuário não está autorizado. {detailMessage} |
| `1106-403` | Proibido | A operação solicitada é proibida. {detailMessage} |
| `1107-412` | Falha na Pré-Condição | A condição definida pelos cabeçalhos If-Unmodified-Since ou If-None-Match não é cumprida. {detailMessage} |

## Erros de criptografia

| Código de erro | Título | Mensagem detalhada |
| --- | --- | --- |
| `1200-500` | Erro interno | Ocorreu um erro interno. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1201-400` | Solicitação inválida | O flowId não pode ser nulo ou vazio. Forneça um flowId válido na solicitação e tente novamente. |
| `1202-400` | Solicitação inválida | O publicKeyId está ausente nas transformações do fluxo={transformações}. Forneça publicKeyId na solicitação e tente novamente. |
| `1203-400` | Solicitação inválida | A chave de criptografia não existe em relação a keyID={keyID} nas transformações do fluxo={transformações}. Verifique sua keyID fornecida e tente novamente. |
| `1204-400` | Solicitação inválida | O algoritmo de criptografia fornecido é inválido. Forneça um algoritmo de criptografia válido e tente novamente. |
| `1205-400` | Solicitação inválida | A senha está ausente na seção params na solicitação fornecida. Forneça passPhrase em parâmetros e tente novamente. |

## Erros da API REST

| Código de erro | Título | Mensagem detalhada |
| --- | --- | --- |
| `1300-400` | Solicitação inválida | A solicitação de conexão de patch não é suportada para o conector {connectorType}. Verifique a solicitação fornecida e tente novamente. |
| `1301-400` | Solicitação inválida | O parâmetro authSpecType fornecido: {authSpecType} não é suportado. Forneça um tipo de especificação de autenticação válido e tente novamente. |
| `1302-400` | Solicitação inválida | O tipo de autenticação fornecido = {authType} não é suportado para connector={connectorType}. Forneça um tipo de autenticação válido para o conector especificado. |
| `1303-400` | Solicitação inválida | Não foi possível codificar o URL com os parâmetros de autenticação fornecidos porque a codificação de URL não é suportada para {value}. Verifique seus parâmetros de autenticação e tente novamente. |
| `1304-400` | Solicitação inválida | O campo obrigatório {field} não foi fornecido. Forneça o {field} e tente novamente. |
| `1305-400` | Solicitação inválida | O tipo de conector fornecido = {connectorType} não é suportado para esta operação. |
| `1306-400` | Solicitação inválida | A conexão de destino não pode ser nula ao validar a ID de especificação da conexão de destino. Verifique a solicitação fornecida e tente novamente. |
| `1307-400` | Solicitação inválida | A ID de especificação da conexão de destino não é válida={targetConnectionSpecId}. O valor permitido é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `1308-400` | Solicitação inválida | Não foi possível processar a solicitação. Mensagem de erro: {msftErrorMessage} |
| `1309-400` | Solicitação inválida | A transformação de criptografia fornecida é inválida porque {requiredParam} está ausente nos parâmetros. Forneça {requiredParam} e tente novamente. |
| `1310-400` | Solicitação inválida | O publicKeyId fornecido nos parâmetros expirou. Forneça um publicKeyId válido e tente novamente. |
| `1311-400` | Solicitação inválida | O publicKeyId fornecido em params é inválido. Forneça um publicKeyId válido e tente novamente. |
| 1312-400 | Solicitação inválida | O valor de parâmetro fornecido {paramValue} não é uma entrada válida para a propriedade={requestParam}. Forneça um valor de parâmetro válido e tente novamente. |
| `1313-400` | Solicitação inválida | O atributo de caminho {attribute} não existe. Verifique se o atributo existe e tente novamente. |
| `1314-400` | Solicitação inválida | Um caminho complexo foi fornecido, mas não é permitido. Verifique se o caminho complexo não foi fornecido e tente novamente. |
| `1315-400` | Solicitação inválida | O caminho fornecido {path} deve apontar para uma matriz de registros. Certifique-se de que o caminho fornecido aponta para a matriz de registros e tente novamente. |
| `1316-400` | Solicitação inválida | Os parâmetros de paginação fornecidos não devem estar vazios. Forneça parâmetros de paginação válidos e tente novamente. |
| `1317-400` | Solicitação inválida | Os parâmetros de programação fornecidos estão vazios, mas não devem estar vazios. Forneça parâmetros de programação válidos e tente novamente. |
| `1318-400` | Solicitação inválida | {CombinationMessage}. Verifique a solicitação fornecida e tente novamente. |
| `1319-400` | Solicitação inválida | O {param} deve fazer parte da coleção principal. Forneça {param} na coleção principal e tente novamente. |
| `1320-400` | Solicitação inválida | O {idType} não pode ser nulo ou vazio. Forneça {idType} válido e tente novamente. |
| `1321-400` | Solicitação inválida | O comprimento de {idType} deve ser um, o tamanho fornecido é {size}. Forneça um tamanho válido e tente novamente. |
| `1322-400` | Solicitação inválida | A conexão de origem não pode ser nula para criar a referência do esquema. Forneça uma conexão de origem válida e tente novamente. |
| `1323-400` | Solicitação inválida | {entity} não pode ser nulo ou vazio na conexão de origem: {sourceConnection}. Forneça {entity} válida e tente novamente. |
| `1324-400` | Solicitação inválida | A conexão de destino não pode ser nula ao extrair a ID do conjunto de dados. Forneça uma conexão de destino válida e tente novamente. |
| `1325-400` | Solicitação inválida | O parâmetro dataSetId não pode ser nulo ou vazio na conexão de destino: {TargetConnection}. Forneça um parâmetro dataSetId válido e tente novamente. |
| `1326-400` | Solicitação inválida | A conexão de origem não pode ser nula ao buscar o formato de origem. Forneça uma conexão de origem válida e tente novamente. |
| `1327-400` | Solicitação inválida | Não há suporte para o formato de dados de origem fornecido={sourceFormat} em SourceConnection. Os valores permitidos são: {values}. Forneça os valores permitidos e tente novamente. |
| `1328-400` | Solicitação inválida | A transformação de mapeamento não pode ser nula ao extrair {param}. Forneça uma transformação de mapeamento válida e tente novamente. |
| `1329-400` | Solicitação inválida | O parâmetro: {param} não pode ser nulo ou vazio na solicitação fornecida. Forneça {param} válido e tente novamente. |
| `1330-400` | Solicitação inválida | Não foram encontradas colunas para a tabela {tableName}. Forneça um nome de tabela válido e tente novamente. |
| `1331-400` | Solicitação inválida | O Delimitador de Coluna não pode ter mais de um caractere em SourceConnection: {sourceConnection}. Forneça um delimitador de coluna válido e tente novamente. |
| `1332-400` | Solicitação inválida | A solicitação de conexão de origem com connectionSpecId: {connectionSpecId} não pode ter um baseConnectionId. Remova o baseConnectionId e tente novamente. |
| `1333-400` | Solicitações inválidas | O flowRunAction={flowRunAction} não é suportado para a origem com o ID de especificação={specId}. Forneça uma ação válida de execução de fluxo e tente novamente. |
| `1334-400` | Solicitação inválida | O parâmetro de consulta : {param} não pode estar vazio. Forneça {param} válido e tente novamente. |
| `1335-400` | Solicitação inválida | Ocorreu um erro ao serializar os parâmetros de filtro para exploração. Verifique a solicitação de parâmetro de filtro e tente novamente. |
| `1336-400` | Solicitação inválida | A conexão de exploração não é compatível com a ID de especificação de conexão: {connectionSpecId}. Forneça a ID de especificação de conexão compatível e tente novamente. |
| `1337-400` | Solicitação inválida | O {QueryParam} não pode estar vazio para objectType={objectType}. Forneça {QueryParam} válido e tente novamente. |
| `1338-400` | Solicitação inválida | A ID de conexão {connectionType} não pode ser nula em flowRequest. Forneça uma ID de conexão {connectionType} válida no flowRequest. |
| `1339-400` | Solicitação inválida | O formato da organização={imsOrg} fornecido na solicitação é inválido. Forneça uma ID de organização válida e tente novamente. |
| `1340-400` | Solicitação inválida | Erro ao analisar {time}. Verifique o formato de hora fornecido na solicitação e tente novamente. |
| `1341-400` | Solicitação inválida | O Json ODI fornecido está vazio. Forneça um Json ODI válido e tente novamente. |
| `1342-400` | Solicitação inválida | O segmento &#39;dls:folder&#39; em &#39;odi.json&#39; não tem definições. Forneça as definições apropriadas em &#39;odi.json&#39; e tente novamente. |
| `1343-400` | Solicitação inválida | Os segmentos &quot;dls:entityReferences&quot; e &quot;dls:partitionSpec&quot; em &quot;odi.json&quot; estão ausentes nas definições. Forneça as definições apropriadas em &#39;odi.json&#39; e tente novamente. |
| `1344-400` | Solicitação inválida | A definição de &#39;dls:partitionSpec&#39; em &#39;odi.json&#39; é inválida porque foram encontradas mais de uma partitionSpecs. Forneça as definições apropriadas em &#39;odi.json&#39; e tente novamente. |
| `1345-400` | Solicitação inválida | As definições estão ausentes em 1 ou mais segmentos em caminhos: &#39;dls:partitionSpec/dls:fileFormat&#39;, &#39;dls:partitionSpec/dls:partitionTemplate&#39;,&#39;dls:partitionSpec/dls:fileFormat/@type&#39;, &#39;dls:partitionSpec/dls:fileFormat/dls:csvDelimiters&#39; em &#39;odi.json&#39;. Forneça as definições apropriadas em &#39;odi.json&#39; e tente novamente. |
| `1346-400` | Solicitação inválida | A definição &#39;@type&#39; fornecida em &#39;dls:fileFormat&#39; em &#39;odi.json&#39; é inválida. Forneça as definições apropriadas em &#39;odi.json&#39; e tente novamente. |
| `1347-400` | Solicitação inválida | A definição de dls:csvDelimiters em &#39;odi.json&#39; não é suportada. Os csvDelimitadores compatíveis são: [&#39;,&#39;]. Forneça as definições apropriadas em &#39;odi.json&#39; e tente novamente. |
| `1348-400` | Solicitação inválida | Ocorreu um erro ao desserializar &#39;dls:entityReferences&#39;. Verifique se os dados estão no formato válido e tente novamente. |
| `1349-400` | Solicitação inválida | Os parâmetros de filtro fornecidos são inválidos. Forneça parâmetros de filtro válidos e tente novamente. |
| `1350-400` | Solicitação inválida | Nenhum operador foi fornecido para filtro na origem. Forneça uma solicitação de filtro válida com o operador apropriado e tente novamente. |
| `1351-400` | Solicitação inválida | O operador fornecido {operator} não é suportado para o filtro na origem deste conector. Forneça um operador válido e tente novamente. |
| `1352-400` | Solicitação inválida | O operador fornecido {operator} não pode ser mapeado para nenhum operador nativo suportado para {ql}. Forneça um operador válido e tente novamente. |
| `1353-400` | Solicitação inválida | O filtro na origem ainda não é suportado para o conector {connectorType}. Verifique os conectores compatíveis na documentação: https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/filter.html. |
| `1354-400` | Solicitação inválida | O idioma de consulta {ql} ainda não é suportado para o filtro na origem. Forneça um idioma de consulta válido e tente novamente. |
| `1355-400` | Solicitação inválida | O tipo de filtro fornecido é inválido. O tipo de filtro suportado é: PQL. Forneça um tipo de filtro válido e tente novamente. |
| `1356-400` | Solicitação inválida | O formato de filtro fornecido é inválido. O formato de filtro compatível é : pql/json. Forneça um formato de filtro válido e tente novamente. |
| `1357-400` | Solicitação inválida | O filtro fornecido é inválido. O valor deve ser fornecido com filtros detalhados. Forneça um filtro válido e tente novamente. |
| `1358-400` | Solicitação inválida | O parâmetro fornecido &#39;objectType&#39; é inválido. Forneça um objectType válido e tente novamente. |
| `1359-400` | Solicitação inválida | O parâmetro {param} está ausente na solicitação. Forneça um {param} válido e tente novamente. |
| `1360-400` | Solicitação inválida | A hora de início não pode ser definida no passado. Forneça uma hora de início válida e tente novamente. |
| `1361-400` | Solicitação inválida | O intervalo não é permitido com uma ingestão única. Remova o intervalo ou altere a frequência e tente novamente. |
| `1362-400` | Solicitação inválida | O intervalo não pode ser inferior a {minInterval}. Forneça um valor de intervalo válido e tente novamente. |
| `1363-400` | Solicitação inválida | Intervalo {intervalo} não é permitido com frequência: {frequência}. Forneça um valor de intervalo válido e tente novamente. |
| `1364-400` | Solicitação inválida | O sinalizador de preenchimento retroativo não é permitido quando a frequência é definida como um. Remova o sinalizador de preenchimento retroativo quando a frequência estiver definida como uma vez e tente novamente. |
| `1365-400` | Solicitação inválida | O caminho {path} fornecido em ops é inválido. Forneça um caminho válido {path} e tente novamente. |
| `1366-400` | Solicitação inválida | A hora de início passou e a operação de atualização não é mais permitida. |
| `1367-400` | Solicitação inválida | A coluna delta é necessária na transformação de cópia ao criar um conector CRM. Forneça a coluna delta e tente novamente. |
| `1368-400` | Solicitação inválida | O modo não é permitido na solicitação de fluxo. Verifique sua solicitação e tente novamente. |
| `1369-400` | Solicitação inválida | A coluna delta na transformação de cópia não é permitida quando a frequência é definida como uma vez. Remova a coluna delta e tente novamente. |
| `1370-400` | Solicitação inválida | Não foi possível buscar as colunas de origem para assimilação porque a transformação de mapeamento está ausente. Adicione a transformação do mapeamento e tente novamente. |
| `1371-400` | Solicitação inválida | A detecção de propriedades de arquivo não é compatível com o conector {connectorType}. Forneça as propriedades do arquivo manualmente. |
| `1372-400` | Solicitação inválida | A operação atual não é permitida. Não é permitido explorar por meio de especificação de conexão para a ID de especificação de conexão={connectionSpecId}. |
| `1373-400` | Solicitação inválida | O flowSpecType está ausente na solicitação. Forneça um flowSpecType válido e tente novamente. |
| `1374-400` | Solicitação inválida | Os parâmetros de consulta fornecidos são inválidos. Não é possível ter o sinalizador determineProperties e as propriedades definidas pelo usuário na mesma solicitação. Corrija sua solicitação e tente novamente. |
| `1375-400` | Solicitação inválida | Falha na detecção de propriedades do arquivo. Insira as propriedades manualmente. |
| `1376-400` | Solicitação inválida | Não há suporte para a detecção de propriedades de arquivo para a especificação de conexão id={connectionSpecId}. Forneça as propriedades do arquivo manualmente. |
| `1377-400` | Solicitação inválida | O parâmetro de valor fornecido é nulo e não pode ser comparado com o operador {operator}. Forneça um parâmetro de valor válido e tente novamente. |
| `1378-400` | Solicitação inválida | Erro ao validar a coluna de entrada {column} para filtro na origem. O nome da coluna deve ser uma coluna válida na tabela. Forneça um nome de coluna válido e tente novamente. |
| `1379-400` | Solicitação inválida | Erro ao validar a entrada {value} para filtro na origem. A coluna DataType na origem é {columnDataType} e o valor DataType [String] não corresponde. Forneça um {value} válido e tente novamente. |
| `1380-400` | Solicitação inválida | Falha ao criar execução de fluxo. Mensagem de erro: {message} |
| `1381-400` | Solicitação inválida | WindowEndTime={endTime} não pode ser anterior a Window StartTime={startTime}. Forneça uma hora de término válida e tente novamente. |
| `1382-400` | Solicitação inválida | A coluna delta deve corresponder ao valor presente nas transformações Copiar do fluxo. Forneça uma coluna delta válida e tente novamente. |
| `1383-400` | Solicitação inválida | A coluna delta está ausente nos parâmetros recebidos para criar uma execução de fluxo. Forneça a coluna delta em params e tente novamente. |
| `1384-400` | Solicitação inválida | Os params={params} fornecidos para criação de execução de fluxo são inválidos ou vazios. Forneça parâmetros válidos e tente novamente. |
| `1385-400` | Solicitação inválida | O connectorType={connectorType} fornecido não é suportado para criar execuções de fluxo. Forneça um connectorType válido e tente novamente. |
| `1386-400` | Solicitação inválida | O flowId={flowId} com scheduleParams frequency={frequency} não é suportado para criar execuções de fluxo. Forneça uma frequência válida e tente novamente. |
| `1387-400` | Solicitação inválida | O flowRunId={flowRunId} está em um estado inválido={state} para reacionar. Tente novamente mais tarde e entre em contato com o suporte ao cliente se o problema persistir. |
| `1388-400` | Solicitação inválida | O fluxo={flow} está em estado={state} e não pode ser reacionado. O fluxo deve estar no estado ativado para ser reacionado. |
| `1389-400` | Solicitação inválida | Ocorreu um erro ao analisar a cadeia de caracteres codificada em base64 fornecida. Forneça uma cadeia de caracteres de filtro codificada válida e tente novamente. |
| `1390-400` | Solicitação inválida | O operador &quot;não&quot; não pode ter mais de uma comparação. Forneça um número válido de comparações e tente novamente. |
| `1391-400` | Solicitação inválida | Falha ao analisar SchemaMetaData em sourceConnection para Id={sourceConnectionId}. Verifique o schemaMetaData em sua solicitação e tente novamente. |
| `1392-400` | Solicitação inválida | Falha ao analisar Transformações na solicitação de fluxo para flowId={flowId}. Verifique as transformações na solicitação e tente novamente. |
| `1393-400` | Solicitação inválida | O parâmetro fornecido {parameter} é nulo ou está vazio. Forneça um {parameter} válido e tente novamente. |
| `1394-400` | Solicitação inválida | O valor mínimo de um parâmetro {parameter} é um. Forneça um {parameter} válido e tente novamente. |
| `1395-400` | Solicitação inválida | A conexão de origem encontrada no fluxo é nula ou está vazia. Forneça uma conexão de origem válida no fluxo e tente novamente. |
| `1396-400` | Solicitação inválida | Não foi possível localizar um formato correspondente. Forneça um formato correspondente e tente novamente. |
| `1397-400` | Solicitação inválida | A frequência fornecida: {frequency} é inválido. Forneça uma frequência válida e tente novamente. |
| `1398-400` | Solicitação inválida | A operação fornecida : {action} não é suportado. Verifique a operação fornecida e tente novamente. |
| `1399-400` | Solicitação inválida | Não foi possível localizar um requestFileType válido. Forneça um requestFileType válido e tente novamente. |
| `1400-400` | Solicitação inválida | O parâmetro fornecido &#39;templateType&#39; é inválido. Forneça um tipo de modelo válido e tente novamente. |
| `1401-400` | Solicitação inválida | A ação de execução de fluxo fornecida={flowRunAction} não é suportada. Forneça uma ação válida de execução de fluxo e tente novamente. |
| `1402-500` | Erro interno | Ocorreu um erro interno. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1403-400` | Solicitação inválida | A hora de início passou e não é possível alterar a frequência para uma vez. |
| `1404-400` | Solicitação inválida | A hora de início passou e você não pode mais atualizar o preenchimento retroativo. |

## Exceções de Serviço de Fluxo (1600-1699)

| Código de erro | Título | Mensagem detalhada |
| --- | --- | --- |
| `1600-400` | Solicitação inválida | Não foi possível processar a solicitação. {detailMessage} |
| `1601-500` | Erro interno | Ocorreu um erro interno. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1602-404` | Recurso não encontrado | O recurso solicitado não foi encontrado. {detailMessage} |
| `1603-503` | Serviço Indisponível | O serviço está temporariamente indisponível. Tente novamente. Entre em contato com o suporte ao cliente se o problema persistir. |
| `1604-504` | Tempo limite do gateway | Ocorreu um tempo limite de gateway. Tente novamente. Entre em contato com o suporte ao cliente se o problema persistir. |
| `1605-401` | Não autorizado | O usuário não está autorizado. {detailMessage} |
| `1606-403` | Proibido | A operação solicitada é proibida. {detailMessage} |
| `1607-412` | Falha na Pré-Condição | A condição definida pelos cabeçalhos If-Unmodified-Since ou If-None-Match não é cumprida. {detailMessage} |

## Erros da zona de aterrissagem de dados

| Código de erro | Título | Mensagem detalhada |
| --- | --- | --- |
| `1700-500` | Erro interno | Ocorreu um erro interno. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1701-400` | Solicitação inválida | A zona de aterrissagem fornecida está inativa. Ative a zona de aterrissagem e tente novamente. |
| `1702-400` | Solicitação inválida | O Tipo SAS={sasType} fornecido para a zona de aterrissagem não é permitido. Forneça um SAS válido e tente novamente. |
| `1703-400` | Solicitação inválida | A atualização de Credenciais não é permitida. |
| `1704-400` | Solicitação inválida | As chaves retornadas para storageAccountName={accountName} em subscriptionId={subscriptionId} e resourceGroupName={resourceGroupName} estão malformadas. Verifique sua solicitação e tente novamente. Entre em contato com o suporte se o problema persistir. |
| `1705-400` | Solicitação inválida | A ação de zona de aterrissagem de dados fornecida não é suportada. Forneça uma ação válida e tente novamente. |
| `1706-400` | Solicitação inválida | A configuração de ativações permitidas não está configurada corretamente para landing zone={landingZoneType}. Tente novamente e entre em contato com o suporte ao cliente se o problema persistir. |
| `1707-400` | Solicitação inválida | Falha ao iniciar o serviço porque a configuração da zona de aterrissagem não pode ser nula ou vazia. Certifique-se de que a configuração da zona de aterrissagem não é nula e tente novamente. |
| `1708-400` | Solicitação inválida | A configuração do contêiner não pode ser nula em landingZoneType={landingZoneType}. Verifique se a configuração do contêiner não é nula e tente novamente. |
| `1709-400` | Solicitação inválida | Os detalhes SAS não podem ser nulos para {tokenConfig} em landingZoneType={landingZoneType}. Forneça um SAS válido na configuração e tente novamente. |
| `1710-400` | Solicitação inválida | Zona de aterrissagem do tipo: {landingZoneUseCase} não é suportado. Forneça um tipo de zona de aterrissagem válido e tente novamente. |
| `1711-400` | Solicitação inválida | Os detalhes SAS não foram encontrados para a zona de aterrissagem de dados do tipo fornecida: {landingZoneUseCase}. Verifique se os detalhes SAS são fornecidos para o tipo de zona de aterrissagem fornecido. |
| `1712-400` | Solicitação inválida | A ação da zona de aterrissagem fornecida: {actionType} não é permitido. Forneça uma ação válida de zona de aterrissagem de dados e tente novamente. |
| `1713-400` | Solicitação inválida | {OperationType} não é permitido para o {tokenType} fornecido. Verifique sua solicitação e tente novamente. |
| `1714-400` | Solicitação inválida | O clientId={clientId} não tem permissão para executar esta operação. Verifique sua solicitação com permissões e tente novamente. |