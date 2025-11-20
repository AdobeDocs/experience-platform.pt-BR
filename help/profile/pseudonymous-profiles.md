---
keywords: Experience Platform;página inicial;tópicos populares;conjunto de dados;conjunto de dados;tempo de vida;ttl;tempo de vida;pseudônimo;perfis pseudônimos;expiração de dados;expiração;
solution: Experience Platform
title: Expiração de dados do perfil pseudônimo
description: Este documento fornece orientação geral sobre como configurar a expiração de dados para Perfis pseudônimos no Adobe Experience Platform.
exl-id: e8d31718-0b50-44b5-a15b-17668a063a9c
source-git-commit: 8734b85914d965eebc2f8ccd8c09dd1ffede8cf9
workflow-type: tm+mt
source-wordcount: '1260'
ht-degree: 7%

---

# Expiração de dados de perfis pseudônimos

No Adobe Experience Platform, é possível configurar as horas de expiração de dados para perfis pseudônimos, permitindo remover automaticamente dados do armazenamento de Perfis que não são mais válidos ou úteis para seus casos de uso.

## Perfil pseudônimo {#pseudonymous-profile}

>[!CONTEXTUALHELP]
>id="platform_profile_pseudonymousprofile"
>title="O que é um perfil pseudônimo?"
>abstract="Um perfil pseudônimo é um perfil que utiliza um namespace de identidade pseudônimo ou desconhecido ou um perfil que não realizou nenhuma atividade por um determinado período."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_profile_pseudonymousprofile_dataexpiration"
>title="Expiração de dados de perfil pseudônimo"
>abstract="A expiração de dados de perfil pseudônimo representa o número de dias que um perfil pseudônimo permanecerá na Adobe Experience Platform antes de ser removido. Esse valor deve ser definido como pelo menos 1. Observe que pode levar até três dias para que o perfil pseudônimo seja removido."

Um perfil é considerado para expiração de dados pseudônimos se atender às seguintes condições:

- Os namespaces de identidade do perfil compilado correspondem ao que o cliente especificou como um namespace de identidade pseudônimo ou desconhecido.
   - Por exemplo, se o namespace de identidade do perfil for `ECID`, `GAID` ou `AAID`. O perfil compilado não tem IDs de nenhum outro namespace de identidade. Neste exemplo, um perfil compilado **não** tem uma identidade de email ou CRM.
- Nenhuma atividade ocorreu em um período definido pelo usuário. A atividade é definida por qualquer evento de experiência que esteja sendo assimilado ou por atualizações iniciadas pelo cliente nos atributos do perfil.
   - Por exemplo, um novo evento de exibição de página ou atualização de atributo de página é considerado uma atividade. No entanto, uma atualização de associação de público iniciada por não usuário **não** é considerada uma atividade. Atualmente, para calcular a expiração dos dados, o rastreamento em nível de perfil se baseia na hora do evento para Eventos de experiência e na hora da assimilação dos atributos de perfil.

## Acesso {#access}

>[!AVAILABILITY]
>
>Para acessar esse recurso, você deve ter as seguintes permissões:
>
>- Gerenciar configurações do perfil
>- Exibir perfis
>- Exibir namespaces de identidade
>
>A permissão **Gerenciar Configurações de Perfil** permite definir as expirações de dados, a permissão **Exibir Perfis** permite exibir as expirações de dados e a permissão **Exibir Namespaces de Identidade** permite exibir os namespaces de identidade disponíveis que você pode usar.
>
>Mais informações sobre permissões no Experience Platform podem ser encontradas na [visão geral do controle de acesso](../access-control/home.md#permissions).

Para adicionar a expiração de dados de perfil pseudônimo à sua organização, vá para o painel Perfil e selecione **[!UICONTROL Settings]**.

![O botão Configurações no painel Perfil está realçado.](./images/pseudonymous-profiles/profile-settings.png)

O popover [!UICONTROL Profile settings] é exibido. Nesse pop-over, é possível definir o número de dias para a expiração dos dados do perfil pseudônimo, bem como o namespace de identidade usado para a expiração dos dados.

Para sandboxes de produção, a expiração padrão dos dados do perfil pseudônimo é de 14 dias, com um mínimo de 1 dia e um máximo de 365 dias. Para sandboxes de desenvolvimento, a expiração padrão dos dados do perfil pseudônimo é de 3 dias, com o mínimo de 1 dia e o máximo de 365 dias.

Selecione **[!UICONTROL Apply]** para salvar as configurações de expiração de dados.

![O popover para adicionar a expiração de dados de perfil pseudônimo aos perfis da sua organização. O botão Aplicar está realçado.](./images/pseudonymous-profiles/profile-settings-data-expiry.png){width="800" zoomable="yes"}

## Perguntas frequentes {#faq}

A seção a seguir lista as perguntas frequentes sobre a expiração dos dados de perfis pseudônimos:

### Como a expiração de dados do Perfil pseudônimo difere da expiração de dados do Evento de experiência?

+++ Resposta

A expiração de dados do perfil pseudônimo e a expiração de dados do evento de experiência são recursos complementares.

#### Granularidade

A expiração de dados do Perfil de pseudônimo funciona em um nível de **sandbox**. Como resultado, a expiração dos dados afetará todos os perfis na sandbox.

A expiração de dados do Evento de experiência funciona em um nível de **conjunto de dados**. Como resultado, cada conjunto de dados pode ter uma configuração de expiração de dados diferente.

#### Tipos de identidade

A expiração de dados de Perfil pseudônimo **only** considera perfis que têm gráficos de identidade que contêm namespaces de identidade selecionados pelo cliente, como `ECID`, `AAID` ou outros tipos de cookies. Se o perfil contiver **qualquer** namespace de identidade adicional que fosse **não** na lista selecionada pelo cliente, o perfil **não** será excluído.

A expiração de dados do Evento de experiência remove os eventos **only** com base no carimbo de data/hora do registro do evento. Os namespaces de identidade incluídos são **ignorados** para fins de expiração.

#### Itens Removidos

A expiração de dados de Perfil pseudônimo remove **ambos** registros de evento e perfil. Como resultado, os dados da classe de perfil também serão removidos.

A expiração de dados do Evento de Experiência **only** remove eventos e **not** remove dados da classe de perfil. Os dados da classe de perfil só são removidos quando todos os dados são removidos em **todos** conjuntos de dados e há **não** registros de classe de perfil restantes para o perfil.

+++

### Como a expiração de dados do perfil pseudônimo pode ser usada juntamente com a expiração de dados do evento de experiência?

+++ Resposta

A expiração de dados do perfil pseudônimo e a expiração de dados do evento de experiência podem ser usadas para se complementar.

Você deve **sempre** configurar a expiração dos dados do Evento de experiência em seus conjuntos de dados, com base nas suas necessidades de retenção de dados sobre clientes conhecidos. Depois que a expiração de dados do evento de experiência for configurada, você poderá usar a expiração de dados do perfil de pseudônimo para remover automaticamente os perfis de pseudônimo. Normalmente, o período de expiração dos dados para Perfis pseudônimos é menor que o período de expiração dos dados para Eventos de experiência.

Em um caso de uso típico, você pode definir a expiração de dados do evento de experiência com base nos valores dos dados de usuário conhecidos e pode definir a expiração de dados do perfil pseudônimo para uma duração muito mais curta, a fim de limitar o impacto dos perfis pseudônimos na conformidade com a licença do Experience Platform.

+++

### Para quais tipos de casos de uso devo usar a expiração de dados de perfis pseudônimos?

+++ Resposta

- Se você estiver usando o Web SDK para enviar dados diretamente ao Experience Platform.
- Se você tiver um site que atende clientes não autenticados em massa.
- Se você tiver contagens excessivas de perfis em seus conjuntos de dados e tiver confirmado que essa contagem excessiva de perfis se deve ao namespace de identidade anônimo baseado em cookies.
   - Para determinar isso, você deve usar o relatório de sobreposição de namespace de identidade. Mais informações sobre este relatório podem ser encontradas na [seção de relatório de sobreposição de identidade](./api/preview-sample-status.md#identity-overlap-report) do guia de API de status de amostra de visualização.

+++

### Quais são alguns avisos que você deve estar ciente antes de usar a expiração de dados de perfis pseudônimos?

+++ Resposta

- A expiração de dados de perfil pseudônimo é executada em um nível de **sandbox**. Você pode optar por ter configurações diferentes para sandboxes de produção e desenvolvimento.
- Após ativar esse recurso, a exclusão dos perfis é **permanente**. Há **não** maneira de reverter ou restaurar os perfis excluídos.
- Este é **não** um trabalho de limpeza único. A expiração de dados de perfil pseudônimo será executada uma vez por dia e excluirá perfis que correspondam à entrada do cliente.
- **Todos** os perfis definidos como pseudônimos serão afetados pela expiração dos dados do perfil pseudônimo. **não** importa se o perfil é somente Evento de Experiência ou se ele contém apenas atributos de perfil.
- Esta limpeza **somente** ocorrerá no Perfil. O Serviço de identidade pode continuar mostrando as identidades excluídas no gráfico após a limpeza nos casos em que o perfil tem duas ou mais identidades com pseudônimos associadas (como `AAID` e `ECID`). Esta discrepância será abordada num futuro próximo.
- A expiração de dados de perfis pseudônimos **não** é executada imediatamente e pode levar até três dias para ser processada.

+++

### Como a expiração de dados de perfis pseudônimos interage com as medidas de proteção para dados do Serviço de identidade?

+++ Resposta

- O sistema de exclusão &quot;primeiro a entrar, primeiro a sair&quot;[ do Serviço de Identidade ](../identity-service/guardrails.md) poderia excluir ECIDs do gráfico de identidade, que estão armazenados no Serviço de Identidade.
- Se esse comportamento de exclusão resultar no armazenamento de um perfil somente ECID no Perfil do cliente em tempo real (armazenamento de perfil), a expiração dos dados do perfil pseudônimo excluirá esse perfil do armazenamento de perfil.

+++

## Próximas etapas

Depois de ler este guia, você sabe como visualizar e criar expirações de dados de perfil pseudônimo. Para obter mais informações sobre o gerenciamento de dados no Experience Platform como um todo, leia o [Guia de práticas recomendadas de direito de licença de gerenciamento de dados](../landing/license-usage-and-guardrails/data-management-best-practices.md).

