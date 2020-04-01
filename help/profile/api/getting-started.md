---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guia do desenvolvedor da API do Perfil do cliente em tempo real
topic: guide
translation-type: tm+mt
source-git-commit: d0ccaa5511375253a2eca8f1235c2f953b734709

---


# Guia do desenvolvedor da API do Perfil do cliente em tempo real

O Perfil do cliente em tempo real permite que você veja uma visualização holística de cada um de seus clientes individuais na plataforma Adobe Experience. O Perfil permite consolidar dados de clientes diferentes de vários canais, como dados on-line, off-line, CRM e de terceiros, em uma visualização unificada que oferece uma conta acionável e com carimbos de data e hora de cada interação com o cliente.

## Introdução {#getting-started}

Usando a API Perfil do cliente em tempo real, você pode executar operações CRUD básicas em relação aos recursos do Perfil, como configurar atributos calculados, acessar entidades, exportar dados do Perfil e excluir conjuntos de dados ou lotes desnecessários.

O uso deste guia do desenvolvedor requer uma compreensão funcional dos vários serviços da plataforma Adobe Experience envolvidos no trabalho com dados do Perfil. Antes de começar a trabalhar com a API de Perfil do cliente em tempo real, consulte a documentação dos seguintes serviços:

* [Perfil](../home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o cliente, com base em dados agregados de várias fontes.
* [Serviço](../../identity-service/home.md)de identidade da plataforma Adobe Experience: Obtenha uma melhor visualização de seu cliente e de seu comportamento ao unir identidades entre dispositivos e sistemas.
* [Serviço](../../segmentation/home.md)de segmentação da plataforma Adobe Experience: Permite criar segmentos de audiência a partir de dados de Perfil do cliente em tempo real.
* [Modelo de dados de experiência (XDM)](../../xdm/home.md): A estrutura padronizada pela qual a Plataforma organiza os dados de experiência do cliente.
* [Caixas de proteção](../../sandboxes/home.md): A plataforma Experience fornece caixas de proteção virtuais que particionam uma única instância da Plataforma em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para pontos de extremidade da API do Perfil.

### Lendo chamadas de exemplo da API

A documentação da API Perfil do cliente em tempo real fornece exemplos de chamadas de API para demonstrar como formatar as solicitações corretamente. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas da plataforma Experience.

### Cabeçalhos obrigatórios

A documentação da API também exige que você tenha concluído o tutorial [de](../../tutorials/authentication.md) autenticação para fazer chamadas com êxito para os pontos de extremidade da plataforma. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em chamadas à API da plataforma Experience, conforme mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos da plataforma Experience são isolados para caixas de proteção virtuais específicas. As solicitações para APIs de plataforma exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Para obter mais informações sobre caixas de proteção na Plataforma, consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

Todas as solicitações com uma carga no corpo da solicitação (como chamadas POST, PUT e PATCH) devem incluir um `Content-Type` cabeçalho. Valores aceitos específicos para cada chamada são fornecidos nos parâmetros da chamada.

## (Alfa) Atributos calculados

>[!IMPORTANT]
>A funcionalidade de atributo calculado está em alfa e não está disponível para todos os usuários. A documentação e funcionalidade estão sujeitas a alterações.

Os atributos calculados permitem calcular automaticamente o valor dos campos com base em outros valores, cálculos e expressões. Os atributos calculados operam no nível do perfil, o que significa que você pode agregação valores em todos os registros e eventos.

Cada atributo calculado contém uma expressão, ou &quot;regra&quot;, que avalia os dados recebidos e armazena o valor resultante em um atributo de perfil ou em um evento. Esses cálculos ajudam você a responder facilmente perguntas relacionadas a coisas como valor de compra vitalícia, tempo entre compras ou número de aberturas de aplicativos, sem exigir a execução manual de cálculos complexos sempre que as informações forem necessárias.

Você pode criar, visualização, editar e excluir atributos calculados usando os `config/computedAttributes` pontos finais. Para saber como usar esses pontos de extremidade, visite o subguia [de atributos](computed-attributes.md)calculados.

## Projeções de borda

A plataforma Adobe Experience permite a personalização em tempo real das experiências do cliente, tornando os dados facilmente acessíveis em servidores estrategicamente localizados chamados &quot;bordas&quot;. A API Perfil do cliente em tempo real fornece pontos de extremidade para trabalhar com bordas através de componentes chamados &quot;projeções&quot;. Isso inclui configurações de projeção para determinar quais dados devem ser projetados para cada borda, bem como destinos de projeção para definir onde rotear uma projeção.

Para obter informações detalhadas sobre como trabalhar com projeções de borda, visite o subguia [de projeções de](edge-projections.md)borda.

## Entidades

Por meio da plataforma Adobe Experience, você pode acessar dados de Perfil do cliente em tempo real usando RESTful APIs ou a interface do usuário. Para saber como acessar entidades, mais comumente conhecidas como &quot;perfis&quot;, usando a API, siga as etapas descritas no subguia [de](entities.md)entidades.

## Mesclar políticas

Ao reunir dados de várias fontes na plataforma Experience, as políticas de mesclagem são as regras que a Plataforma usa para determinar como os dados serão priorizados e quais dados serão combinados para criar perfis individuais do cliente.

Usando a API Perfil do cliente em tempo real, você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Para saber mais sobre como trabalhar com políticas de mesclagem usando a API, visite o subguia [de políticas de](merge-policies.md)mesclagem.

Para obter um guia para trabalhar com políticas de mesclagem usando a interface do usuário da plataforma, consulte o guia [do usuário](../ui/merge-policies.md)Mesclar políticas.

## Pesquisa de Perfis

A pesquisa de Perfis é usada para pesquisar e indexar campos configuráveis contidos em várias fontes de dados e retorná-los em tempo quase real. Para começar a trabalhar com a pesquisa de Perfis, consulte o subguia [de pesquisa](profile-search.md)

## trabalhos do sistema Perfil

Os dados ingeridos na plataforma são armazenados no Data Lake e no armazenamento de dados em tempo real do Perfil do cliente. Ocasionalmente, pode ser necessário excluir um conjunto de dados ou lote do repositório de Perfis para remover dados que não são mais necessários ou que foram adicionados por erro. Isso requer o uso da API para criar um trabalho do sistema do Perfil, conhecido como &quot;solicitação de exclusão&quot;, que também pode ser, modificado, monitorado ou excluído, se necessário.

Para saber como trabalhar com solicitações de exclusão usando os `/system/jobs` pontos de extremidade na API Perfil do cliente em tempo real, siga as etapas descritas no subguia [de tarefas do sistema do](profile-system-jobs.md)perfil.

## Próximas etapas

Para começar a fazer chamadas usando a API Perfil do cliente em tempo real, selecione um dos subguias para saber como usar endpoints específicos relacionados ao Perfil. Para saber mais sobre como trabalhar com os dados do Perfil usando a interface do usuário da plataforma, consulte o guia [do usuário do Perfil do cliente em tempo](../ui/user-guide.md)real.