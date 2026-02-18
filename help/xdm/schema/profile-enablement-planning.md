---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;esquema;conjunto de dados;planejamento;ativação
solution: Experience Platform
title: Planejamento da ativação do Perfil do cliente em tempo real
description: Revise as principais considerações que você deve avaliar antes de ativar esquemas e conjuntos de dados para o Perfil do cliente em tempo real.
source-git-commit: da40dfde57b17b6a7387451eec48569174ad544b
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 0%

---

# Planejamento da ativação do Perfil do cliente em tempo real

Use esta página para confirmar se o esquema e o conjunto de dados estão prontos antes de ativá-los para o Perfil de cliente em tempo real. Conclua esta revisão de planejamento depois de projetar os campos de esquema, mas antes de ativar o esquema para Perfil. A ativação do perfil aplica alterações comportamentais permanentes ao modelo de dados. Não é possível reverter a ativação do esquema e ativar um conjunto de dados afeta como seus registros são processados no Perfil do cliente em tempo real. Revise esta orientação para evitar ativações não intencionais, problemas de qualidade de dados ou restrições de longo prazo no design do esquema.

Ativar o Perfil determina como os dados são compilados, mesclados e ativados no Experience Platform. O Planning garante que a estrutura do esquema, a configuração da identidade e a finalidade do conjunto de dados estejam corretas antes de você fazer a alteração. Após concluir esta revisão do planejamento, você pode continuar a habilitar dados para o Perfil na interface do usuário do **[!UICONTROL Schema Editor]** ou do **[!UICONTROL Dataset]**.

## Pré-requisitos

Antes de usar este guia de planejamento, verifique se você tem:

* Projetou um esquema usando a **[!UICONTROL Schema Editor]** ou a API do Registro de Esquema. Consulte o [tutorial de criação de esquema](../tutorials/create-schema-ui.md) para começar.
* Configurado pelo menos um campo de identidade no esquema. Revise o [guia de configuração do campo de identidade](../ui/fields/identity.md) para obter instruções.
* Conhecimento básico do [Perfil do cliente em tempo real](../../profile/home.md) e de como ele usa esquemas para criar visualizações unificadas do cliente.
* Permissões apropriadas para ativar esquemas e conjuntos de dados para o Perfil. Entre em contato com o administrador do sistema se você não tiver acesso às opções de ativação de perfil.

Se você não concluiu esses pré-requisitos, comece com o [tutorial de criação de esquema](../tutorials/create-schema-ui.md) antes de prosseguir com este guia de planejamento.

## Por que o planejamento é importante {#why-planning-matters}

A ativação de perfis altera permanentemente o modo como o Experience Platform trata seus dados. As seguintes alterações permanentes se aplicam a esquemas e conjuntos de dados.

**Esquemas**: ao habilitar um esquema para Perfil, você não pode desabilitá-lo ou excluí-lo. Também não é possível remover ou renomear campos do esquema após a assimilação de dados. Essa permanência significa que o design do esquema deve ser completo e estável antes de habilitar o Perfil, pois não é possível reverter a decisão ou simplificar a estrutura posteriormente.

**Conjuntos de dados**: quando você habilita um conjunto de dados para o Perfil, o Perfil do Cliente em Tempo Real usa seus registros para criar e atualizar perfis. Revise o comportamento de habilitação do conjunto de dados no [guia do usuário do conjunto de dados](../../catalog/datasets/enable-for-profile.md). Diferentemente dos esquemas, você pode desabilitar ou excluir o conjunto de dados posteriormente, mas isso remove os registros de perfil associados e pode afetar a segmentação ou os fluxos de trabalho de ativação. Considere o impacto downstream antes de fazer alterações em um conjunto de dados habilitado.

Como essas alterações afetam os processos de downstream, verifique se um esquema e seus conjuntos de dados são apropriados para o Perfil antes de ativá-los.

### Noções básicas sobre o fluxo de trabalho de ativação

Você deve ativar o esquema E os conjuntos de dados que usam esse esquema para o Perfil. Habilitar recursos na seguinte ordem:

1. **Habilitar o esquema para o Perfil**: primeiro, habilite o Perfil no esquema no **[!UICONTROL Schema Editor]**. Isso permite que qualquer conjunto de dados que use esse esquema seja ativado para o Perfil.
2. **Habilitar conjuntos de dados individuais para o Perfil**: depois que o esquema for habilitado, habilite o Perfil em cada conjunto de dados que deve contribuir para perfis unificados do cliente.

Não é possível ativar um conjunto de dados para o Perfil se o esquema ainda não estiver ativado. O esquema atua como um pré-requisito para a ativação do conjunto de dados. Esse processo de duas etapas garante que seu modelo de dados seja validado antes que o Perfil do cliente em tempo real inicie o processamento dos registros.

## Quando ativar um esquema ou conjunto de dados para o Perfil {#when-to-enable}

Revise os critérios abaixo para confirmar se a ativação de perfil é apropriada para seus dados.

Ative o Perfil nas seguintes situações:

* Os dados contribuem para um perfil de cliente unificado.
* Os dados são necessários para workflows de segmentação ou ativação.
* O esquema inclui campos de identidade que representam uma pessoa ou chave de nível de cliente.
* O conjunto de dados contém Eventos de experiência ou atributos de perfil que devem ser compilados entre canais. Revise a [classe XDM ExperienceEvent](../classes/experienceevent.md) para confirmar os requisitos do evento.

## Quando um esquema ou conjunto de dados não deve ser habilitado para o Perfil {#when-not-to-enable}

Evite ativar o Perfil nos seguintes casos:

* O esquema representa dados de pesquisa ou somente referência.
* O conjunto de dados contém dados de teste, temporários ou de não produção.
* Os dados não identificam uma pessoa ou são usados apenas para relatórios.
* O esquema é experimental ou estruturalmente incompleto.

Ativar o Perfil nesses cenários pode criar perfis desnecessários, aumentar o uso de licenças ou introduzir restrições de esquema de longo prazo.

## Considerações principais antes de ativar o perfil {#key-considerations}

Revise as considerações nesta seção para garantir que seu esquema e conjunto de dados sejam compatíveis com Casos de uso do perfil e governança de dados a longo prazo. Antes de ativar o Perfil, verifique a estrutura do esquema, a configuração de identidade e a finalidade do conjunto de dados.

### Disponibilidade do esquema

Revise a estrutura do esquema para confirmar se ele é compatível com os requisitos de perfil. O schema deve conter os campos necessários para segmentação e ativação, enquanto exclui campos que são experimentais ou não são necessários a longo prazo. Lembre-se de que quaisquer campos adicionais adicionados após a habilitação devem ser aditivos (consulte [restrições de imutabilidade do esquema](#why-planning-matters) para obter detalhes). Essa restrição significa que você deve validar a seleção de campo com cuidado antes de habilitar o Perfil. Para obter detalhes sobre atualizações permitidas, consulte as [regras de evolução do esquema](./composition.md#evolution).

### Configuração de identidade

A configuração de identidade determina como o Perfil compila os registros nos conjuntos de dados. Comece confirmando que uma identidade principal válida está selecionada — esse campo deve ser estável, exclusivo e preenchido de forma consistente em todos os registros. Verifique se os namespaces de identidade estão atribuídos corretamente para evitar erros de compilação. Se você usar identidades secundárias, confirme se elas são compatíveis com seus casos de uso sem causar colisões de perfis, o que pode ocorrer quando indivíduos diferentes compartilham o mesmo valor de identidade. O Perfil do cliente em tempo real resolve colisões aplicando políticas de mesclagem que determinam quais dados têm precedência quando registros conflitantes são compilados.

### Finalidade do conjunto de dados

Habilite um conjunto de dados para o Perfil somente quando ele contribuir diretamente para atributos de perfil ou Eventos de experiência usados em fluxos de trabalho downstream. Evite ativar conjuntos de dados que contenham dados de pesquisa ou referência não usados na segmentação, dados de teste ou de amostra ou registros gerados pelo sistema operacional não destinados à ativação. Esses tipos de dados não contribuem para perfis unificados do cliente e criam despesas gerais desnecessárias de armazenamento. Se um conjunto de dados não contiver campos de identidade ou dados de comportamento do cliente que ofereçam suporte à segmentação e ativação, não os ative para o Perfil.

**Exemplo**:

Você habilita um conjunto de dados &quot;Eventos de compra do cliente&quot; que contém dados de transação com IDs do cliente. O Perfil do cliente em tempo real usa esses eventos para criar linhas do tempo do cliente e habilitar a segmentação com base no comportamento de compra.

Você NÃO ativa um conjunto de dados de &quot;Catálogo de produtos&quot; que contenha apenas dados de referência do SKU sem identificadores do cliente. Habilitar esse tipo de conjunto de dados cria sobrecarga de armazenamento desnecessária sem contribuir para perfis unificados do cliente.

## Lista de verificação de pré-ativação {#pre-enablement-checklist}

Use essa lista de verificação para confirmar a prontidão antes de habilitar um esquema ou conjunto de dados para o Perfil. Complete cada item antes de ativar o Perfil.

### Verificações em nível de esquema

Comece validando se o design do esquema está completo e estável. Revise seu esquema para confirmar se todos os campos obrigatórios para o seu caso de uso estão presentes e se nenhum campo experimental ou temporário foi incluído. Consulte as [práticas recomendadas de design do esquema](./best-practices.md) para garantir que o esquema siga os padrões recomendados. Obtenha aprovação de sua equipe na lista de campos final (consulte [restrições de imutabilidade do esquema](#why-planning-matters)).

Em seguida, verifique se a configuração de identidade principal está correta. Abra o esquema no **[!UICONTROL Schema Editor]** e localize o campo marcado com o ícone de identidade. Confirme se esse campo está preenchido consistentemente nos dados de origem e se o namespace de identidade é apropriado para o caso de uso. A identidade principal deve ser estável, exclusiva e estar presente de maneira confiável em todos os registros para garantir a compilação adequada do perfil.

Finalmente, confirme se não é necessário renomear ou reorganizar a estrutura do schema. As alterações na estrutura do esquema são limitadas apenas a atualizações aditivas (consulte [restrições de imutabilidade do esquema](#why-planning-matters)). Qualquer ambiguidade de longo prazo na nomenclatura ou na organização não pode ser corrigida posteriormente. Portanto, resolva esses problemas antes da ativação.

### Verificações no nível do conjunto de dados

Para cada conjunto de dados que você planeja habilitar, comece confirmando que ele contém dados relevantes para o perfil. Analise os registros de amostra para verificar se eles contêm dados de clientes ou eventos, em vez de informações meramente operacionais ou de referência. Certifique-se de que os registros incluam valores de identidade vinculados aos perfis do cliente. Conjuntos de dados sem campos de identidade ou dados de comportamento do cliente não devem ser ativados para o Perfil.

Determine se o conjunto de dados deve contribuir para a identificação ou segmentação de identidade, entendendo como seus valores de identidade se relacionam com outros conjuntos de dados em seu ambiente habilitado para perfil. Considere se os registros neste conjunto de dados devem se unir aos perfis existentes ou criar novos fragmentos de perfil. Revise a [documentação da política de mesclagem](../../profile/merge-policies/overview.md) para entender como o Perfil do cliente em tempo real compila os registros entre conjuntos de dados e como esse conjunto de dados se encaixa em sua estratégia geral de identidade.

Antes de ativar o conjunto de dados, estime o número de valores de identidade exclusivos que ele contém e verifique se esses valores de identidade representam clientes reais em vez de contas de teste ou identificadores do sistema. Confirme se a ativação desse conjunto de dados está alinhada aos seus direitos de licença, pois cada identidade exclusiva contribui para o contagem de público-alvo endereçável. A ativação do perfil aumenta os custos de armazenamento e processamento, portanto, garanta que o conjunto de dados forneça valor que justifique esse investimento.

Concluir essa lista de verificação ajuda a evitar problemas que não podem ser revertidos após a ativação.

## Ativação do perfil para seu esquema e conjunto de dados {#enable-profile}

Após concluir a lista de verificação de pré-ativação, siga estas etapas para ativar o Perfil. Conforme explicado em [Noções básicas sobre o fluxo de trabalho de habilitação](#why-planning-matters), você deve habilitar o esquema antes de habilitar qualquer conjunto de dados que use esse esquema.

### Ativar o esquema para o Perfil

Primeiro ative o Perfil no seu esquema:

1. Navegue até **[!UICONTROL Schemas]** na interface do Experience Platform.
2. Selecione seu esquema na lista para abri-lo no **[!UICONTROL Schema Editor]**.
3. Selecione a opção **[!UICONTROL Profile]** no painel direito. O painel de propriedades do esquema exibe uma caixa de diálogo de confirmação.
4. Selecione **[!UICONTROL Enable]** para confirmar. O esquema agora está ativado para Perfil.

Para obter instruções detalhadas, consulte o [guia de ativação de esquema](../ui/resources/schemas.md#profile) na documentação do Editor de esquemas.

### Ativar os conjuntos de dados para o Perfil

Depois que o esquema for ativado para o Perfil, ative cada conjunto de dados que deve contribuir para perfis unificados:

1. Navegue até **[!UICONTROL Datasets]** na interface do Experience Platform.
2. Selecione um conjunto de dados na lista para abrir a página de detalhes do conjunto de dados.
3. Selecione a opção **[!UICONTROL Profile]** no painel direito. O painel de propriedades do conjunto de dados é atualizado para mostrar que o Perfil está ativado.

Repita esse processo para cada conjunto de dados que deve contribuir com o Perfil do cliente em tempo real. Para obter instruções detalhadas e opções de ativação de API, consulte o guia do usuário do conjunto de dados referenciado na seção Pré-requisitos.

### Por que a ordem é importante

Conforme explicado em [Noções básicas sobre o fluxo de trabalho de habilitação](#why-planning-matters), você deve habilitar o esquema antes de habilitar os conjuntos de dados. Isso garante que o Perfil do cliente em tempo real valide a estrutura do esquema, que aceita operações de perfil antes de permitir a ativação do conjunto de dados, e que todos os conjuntos de dados que usam o esquema herdem as definições de campo corretas para segmentação e compilação de identidade.

Depois de ativar o esquema e os conjuntos de dados, o Perfil do cliente em tempo real começa a processar registros e criar perfis unificados do cliente. Os registros assimilados antes da ativação não são incluídos em perfis, a menos que você assimile os dados.

## Próximas etapas {#next-steps}

Você analisou os efeitos permanentes da ativação do perfil, confirmou que o esquema e os conjuntos de dados estão prontos e validou que a configuração de identidade oferece suporte aos casos de uso. Para aprofundar sua compreensão da estrutura de esquema e das relações de campo, revise as [Noções básicas da composição de esquema](../schema/composition.md), que explicam as regras de evolução do esquema e como os campos interagem dentro do modelo de dados. Se você encontrar problemas durante ou após a habilitação, consulte o [guia de solução de problemas XDM](../troubleshooting-guide.md) para obter problemas e soluções comuns. Para saber mais sobre como os namespaces de identidade afetam a compilação e a resolução de perfis, reveja a [visão geral dos namespaces de identidade](../../identity-service/features/namespaces.md).
