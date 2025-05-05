---
title: Possibilite um centro de excelência usando ferramentas de sandbox
description: Possibilite um centro de excelência usando ferramentas de sandbox criando um pacote de "sandbox dourada" para padronizar as práticas recomendadas em várias sandboxes.
exl-id: 6f242ad5-bb02-4a6d-b255-d196dd5fe4b8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 6%

---

# Possibilite um centro de excelência usando ferramentas de sandbox

Possibilite um centro de excelência usando ferramentas de sandbox criando um pacote de &quot;sandbox dourada&quot; para padronizar as práticas recomendadas em várias sandboxes.

![Visão geral da exportação de pacotes em diferentes organizações](../images/use-cases/packages-across-orgs.png){zoomable="yes"}

## Por que considerar este caso de uso {#why-this-use-case}

Muitas grandes empresas usam várias sandboxes para diferentes organizações, equipes, regiões ou ambientes de desenvolvimento. Com o poder da [ferramenta de sandbox](../ui/sandbox-tooling.md), você pode criar um pacote de sandbox dourado para garantir a consistência, a conformidade e o alinhamento dos padrões da sua organização em várias sandboxes.

Este pacote de sandbox dourada cria um centro de excelência para compartilhar configurações principais com eficiência. Usando ferramentas de sandbox, você pode importar facilmente seu pacote em várias sandboxes. Você também pode compartilhar seu pacote com organizações adicionais para garantir consistência abrangente.

Siga as etapas descritas neste caso de uso para criar seu próprio pacote de sandbox dourada.

## Exemplo do setor {#industry-example}

Como exemplo, considere um banco que opera em diferentes regiões, como América do Norte, Europa e África. Cada mercado ou região tem sua própria instância do Adobe Experience Platform. Esse banco deseja manter um modelo de dados centralizado gerenciado por uma equipe global de arquitetos, em que uma única versão do modelo de dados pode ser distribuída por todos os mercados.

Esse banco escolhe utilizar as ferramentas de sandbox para criar e manter um pacote de sandbox dourado. Isso ajuda na eficiência do desenvolvimento, permite modelos de dados consistentes e garante a consistência em todas as regiões.

## Pré-requisitos e planejamento {#prerequisites-and-planning}

Ao planejar criar seu próprio centro de excelência na organização, considere os seguintes pré-requisitos no processo de planejamento:

- Identifique as práticas recomendadas e as configurações a serem incluídas no pacote.
- Crie uma sandbox com todas as configurações relevantes e validadas para serem definidas como a sandbox dourada.
- Se necessário, obtenha informações das partes interessadas e concorde com seus padrões básicos.

### Funcionalidade da interface do usuário, componentes do Experience Platform e produtos da Experience Cloud que você usará {#ui-functionality-and-elements}

Para implementar com êxito esse caso de uso, você deve usar várias áreas do Adobe Experience Platform. Verifique se você tem as [permissões de controle de acesso baseadas em atributos](../../access-control/abac/overview.md) necessárias para todas essas áreas ou peça ao administrador do sistema para conceder as permissões necessárias.

- [Ferramentas de sandbox](../ui/sandbox-tooling.md)
- [Gerenciamento de sandbox](../ui/user-guide.md)
- [Conjuntos de dados](../../catalog/datasets/overview.md)
- [Esquemas](../../xdm//home.md)
- [Públicos-alvo](../../segmentation/home.md)
- [Jornadas do Adobe Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/orchestrate-journeys/journey)

## Como atingir o caso de uso: visão geral de alto nível {#achieve-the-use-case-high-level}

1. Crie a configuração de linha de base que representa suas práticas recomendadas em uma sandbox dourada. Isso pode incluir objetos como conjuntos de dados, esquemas, públicos-alvo ou jornadas.
2. Usar ferramentas de sandbox, exporte a configuração em um pacote.
3. Importe este pacote em todas as sandboxes relevantes.
4. Se você tiver várias organizações, compartilhe este pacote em todas elas.
5. Monitore importações e exportações e rastreie alterações por meio de logs de auditoria.
6. Atualize regularmente sua sandbox dourada à medida que os padrões evoluem para garantir que todas as sandboxes permaneçam alinhadas com as práticas recomendadas.

## Como atingir o caso de uso: instruções passo a passo {#step-by-step-instructions}

Leia as seções abaixo, que incluem links para documentação adicional, para concluir cada uma das etapas da visão geral de alto nível acima.

### Crie sua sandbox dourada

O primeiro passo para habilitar seu centro de excelência é criar sua sandbox dourada. Essa sandbox deve conter as configurações de linha de base que representam suas práticas recomendadas. Para criar esta sandbox dourada, siga o guia em [criando uma nova sandbox](../ui/user-guide.md#create-a-new-sandbox) no Experience Platform.

Depois que sua sandbox tiver sido criada, comece a criar suas configurações de objeto de linha de base, como [esquemas](../../xdm/ui/resources/schemas.md#create-a-new-schema), [conjuntos de dados](../../catalog/datasets/user-guide.md#create-a-dataset) ou [públicos-alvo](../../segmentation/ui/segment-builder.md). Certifique-se de revisar as configurações antes de continuar.

### Exportar sua sandbox em um pacote

Agora que sua sandbox contém suas configurações de objeto de linha de base, ela está pronta para ser exportada em um pacote usando as ferramentas de sandbox. Siga o guia em [exportando uma sandbox inteira](../ui/sandbox-tooling.md#export-an-entire-sandbox) para criar seu pacote de sandbox dourada.

### Importar o pacote para sandboxes relevantes

Agora que o pacote foi criado, você pode importá-lo para suas sandboxes relevantes. A prática recomendada é importar um pacote contendo uma sandbox inteira para uma sandbox vazia. Usando a ferramenta de sandbox, você pode [importar facilmente um pacote de sandbox inteiro](../../sandboxes/ui/sandbox-tooling.md#import-the-entire-sandbox-package) para uma sandbox diretamente no Experience Platform.

### Compartilhar pacote entre organizações

As ferramentas de sandbox permitem compartilhar pacotes criados em diferentes organizações. Siga o [guia de compartilhamento de pacotes](../../sandboxes/ui/sharing-packages-across-orgs.md) para compartilhar seu pacote de sandbox dourada.

### Monitorar importações e exportações por meio de logs de auditoria

Enquanto você importa ou exporta seu pacote, é possível monitorar o status dos trabalhos usando o painel **[!UICONTROL Trabalhos]** no Experience Platform. Para saber mais sobre o monitoramento de trabalhos, leia o guia em [monitorando detalhes da importação](../../sandboxes/ui/sandbox-tooling.md#monitor-import-details).

### Atualizar regularmente a sandbox dourada

Agora que seu pacote de sandbox dourada foi concluído, você estabeleceu um centro de excelência padronizado que pode continuar a importar para sandboxes ou compartilhar entre organizações. À medida que suas práticas recomendadas mudam e se desenvolvem, é importante atualizar regularmente as configurações de objeto da linha de base na sandbox dourada. Conforme você faz atualizações na sandbox, pode criar novas iterações do seu pacote de sandbox dourada seguindo esse mesmo processo.

>[!NOTE]
>
> As etapas acima seguem o processo na interface do usuário do Experience Platform. É possível seguir as mesmas etapas usando a API em vários endpoints. Consulte o `sandboxes` [manual de ponto de extremidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sandbox/api/sandboxes#create) e o `packages` [manual de ponto de extremidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sandbox/sandbox-tooling-api/packages) para obter informações sobre como fazer cada solicitação por meio da API.

## Outros casos de uso obtidos por meio da compatibilidade com dados de parceiros {#other-use-cases}

Veja mais casos de uso ativados pelas ferramentas de sandbox:

- [Fazer backup de configurações de objeto usando ferramentas de sandbox](./backup-object-configuration.md)
