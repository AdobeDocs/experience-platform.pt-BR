---
title: Configuração de segredos no encaminhamento de eventos
description: Saiba como configurar segredos na interface do usuário da coleção de dados para autenticar em endpoints usados em propriedades de encaminhamento de eventos.
exl-id: eefd87d7-457f-422a-b159-5b428da54189
source-git-commit: 7cbf8cfa4ac7aeff9f1ed56777212f5203df2ce9
workflow-type: tm+mt
source-wordcount: '1449'
ht-degree: 1%

---

# Configurar segredos no encaminhamento de eventos

No encaminhamento de eventos, um segredo é um recurso que representa uma credencial de autenticação para outro sistema, permitindo a troca segura de dados. Segredos só podem ser criados nas propriedades de encaminhamento de eventos.

No momento, há três tipos secretos compatíveis:

| Tipo de segredo | Descrição |
| --- | --- |
| [!UICONTROL Token] | Uma única string de caracteres representando um valor de token de autenticação conhecido e compreendido por ambos os sistemas. |
| [!UICONTROL HTTP] | Contém dois atributos de string para um nome de usuário e senha, respectivamente. |
| [!UICONTROL OAuth2] | Contém vários atributos para suportar a variável [OAuth2](https://datatracker.ietf.org/doc/html/rfc6749) especificação de autenticação. O sistema solicita as informações necessárias e, em seguida, lida com a renovação desses tokens para você em um intervalo especificado. Atualmente, somente o [Credenciais do Cliente](https://datatracker.ietf.org/doc/html/rfc6749#section-1.3.4) A versão do OAuth2 é compatível. |

{style=&quot;table-layout:auto&quot;}

Este guia fornece uma visão geral de alto nível de como configurar segredos para um encaminhamento de evento ([!UICONTROL Edge]) na interface do usuário da coleta de dados.

>[!NOTE]
>
>Para obter orientações detalhadas sobre como gerenciar segredos na API do Reator, incluindo o JSON da estrutura de um segredo, consulte [guia da API de segredos](../../api/guides/secrets.md).

## Pré-requisitos

Este guia pressupõe que você já esteja familiarizado com o gerenciamento de recursos para tags e encaminhamento de eventos na interface do usuário da coleta de dados, incluindo como criar um elemento de dados e uma regra de encaminhamento de eventos. Consulte o guia sobre [gerenciamento de recursos](../managing-resources/overview.md) se você precisar de uma introdução.

Você também deve ter uma compreensão funcional do fluxo de publicação para tags e encaminhamento de eventos, incluindo como adicionar recursos a uma biblioteca e instalar uma build em seu site para testes. Consulte a [visão geral da publicação](../publishing/overview.md) para obter mais detalhes.

## Criar um segredo {#create}

Para criar um segredo, faça logon na interface do usuário da Coleta de dados e abra a propriedade de encaminhamento de eventos em que deseja adicionar o segredo. Em seguida, selecione **[!UICONTROL Segredos]** no painel de navegação esquerdo, seguido de **[!UICONTROL Criar novo segredo]**.

![Criar novo segredo](../../images/ui/event-forwarding/secrets/create-new-secret.png)

A próxima tela permite configurar os detalhes do segredo. Para que um segredo possa ser usado pelo encaminhamento de eventos, ele deve ser atribuído a um ambiente existente. Se você não tiver nenhum ambiente criado para sua propriedade de encaminhamento de evento, consulte o guia em [ambientes](../publishing/environments.md) para obter orientação sobre como configurá-los antes de continuar.

>[!NOTE]
>
>Se você ainda quiser criar e salvar o segredo antes de adicioná-lo a um ambiente, desative o **[!UICONTROL Anexar segredo a ambientes]** alternar antes de preencher o restante das informações. Observe que você terá que atribuí-lo a um ambiente posteriormente se quiser usar o segredo.
>
>![Desativar ambiente](../../images/ui/event-forwarding/secrets/env-disabled.png)

Em **[!UICONTROL Ambiente do Target]**, use o menu suspenso para selecionar o ambiente ao qual deseja atribuir o segredo. Em **[!UICONTROL Nome secreto]**, forneça um nome para o segredo no contexto do ambiente. Esse nome deve ser exclusivo em todos os segredos na propriedade de encaminhamento de eventos.

![Ambiente e nome](../../images/ui/event-forwarding/secrets/env-and-name.png)

Um segredo só pode ser atribuído a um ambiente por vez, mas você pode atribuir as mesmas credenciais a vários segredos em ambientes diferentes, se desejar. Selecionar **[!UICONTROL Adicionar ambiente]** para adicionar outra linha à lista.

![Adicionar ambiente](../../images/ui/event-forwarding/secrets/add-env.png)

Para cada ambiente adicionado, você deve fornecer outro nome exclusivo para o segredo associado. Se você esgotar todos os ambientes disponíveis, a variável **[!UICONTROL Adicionar ambiente]** não estará disponível.

![Adicionar ambiente indisponível](../../images/ui/event-forwarding/secrets/add-env-greyed.png)

A partir daqui, as etapas para criar o segredo diferem dependendo do tipo de segredo que você está criando. Consulte as subseções abaixo para obter detalhes:

* [[!UICONTROL Token]](#token)
* [[!UICONTROL HTTP]](#http)
* [[!UICONTROL OAuth2]](#oauth2)

### [!UICONTROL Token] {#token}

Para criar um segredo de token, selecione **[!UICONTROL Token]** do **[!UICONTROL Tipo]** lista suspensa. No **[!UICONTROL Token]** , forneça a cadeia de caracteres de credencial reconhecida pelo sistema ao qual você está autenticando. Selecionar **[!UICONTROL Criar segredo]** para salvar o segredo.

![Segredo de token](../../images/ui/event-forwarding/secrets/token-secret.png)

### [!UICONTROL HTTP] {#http}

Para criar um segredo HTTP, selecione **[!UICONTROL HTTP simples]** do **[!UICONTROL Tipo]** lista suspensa. Nos campos que aparecem abaixo, forneça um nome de usuário e senha para a credencial antes de selecionar **[!UICONTROL Criar segredo]** para salvar o segredo.

>[!NOTE]
>
>Ao ser salva, a credencial é codificada usando a variável [Esquema de autenticação HTTP &quot;básico&quot;](https://www.rfc-editor.org/rfc/rfc7617.html).

![Segredo HTTP](../../images/ui/event-forwarding/secrets/http-secret.png)

### [!UICONTROL OAuth2] {#oauth2}

Para criar um segredo OAuth2, selecione **[!UICONTROL OAuth2]** do **[!UICONTROL Tipo]** lista suspensa. Nos campos que aparecem abaixo, forneça seu [[!UICONTROL ID do cliente] e [!UICONTROL Segredo do cliente]](https://www.oauth.com/oauth2-servers/client-registration/client-id-secret/), bem como seu [URL de autorização](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) para sua integração com o OAuth. O [!UICONTROL URL de autorização] na interface do usuário da coleta de dados é uma concatenação entre o host do servidor de autorização e o caminho do token.

![Segredo OAuth2](../../images/ui/event-forwarding/secrets/oauth-secret-1.png)

Em **[!UICONTROL Opções de Credencial]**, você pode fornecer outras opções de credencial, como `scope` e `audience` na forma de pares de valores-chave. Para adicionar mais pares de valores chave, selecione **[!UICONTROL Adicionar outro]**.

![Opções de credencial](../../images/ui/event-forwarding/secrets/oauth-secret-2.png)

Por fim, você pode configurar a variável **[!UICONTROL Atualizar Deslocamento]** para o segredo. Representa o número de segundos antes da expiração do token em que o sistema executará uma atualização automática. O tempo equivalente em horas e minutos é exibido à direita do campo e é atualizado automaticamente à medida que você digita.

![Atualizar Deslocamento](../../images/ui/event-forwarding/secrets/oauth-secret-3.png)

Por exemplo, se o deslocamento de atualização estiver definido como o valor padrão de `14400` (quatro horas) e o token de acesso tem um `expires_in` valor de `86400` (24 horas), o sistema atualizará automaticamente o segredo em 20 horas.

>[!IMPORTANT]
>
>Um segredo OAuth requer pelo menos quatro horas entre as atualizações e também deve ser válido por no mínimo oito horas. Essa restrição oferece um mínimo de quatro horas para intervir se surgirem problemas com o token gerado.
>
>Por exemplo, se o deslocamento estiver definido como `28800` (oito horas) e o token de acesso tem um `expires_in` de `36000` (dez horas), a troca falharia porque a diferença resultante era menor que quatro horas.

Quando terminar, selecione **[!UICONTROL Criar segredo]** para salvar o segredo.

![Salvar Deslocamento OAuth2](../../images/ui/event-forwarding/secrets/oauth-secret-4.png)

## Editar um segredo

Depois de criar segredos para uma propriedade, você pode encontrá-los listados na **[!UICONTROL Segredos]** espaço de trabalho. Para editar os detalhes de um segredo existente, selecione seu nome na lista.

![Selecionar segredo para editar](../../images/ui/event-forwarding/secrets/edit-secret.png)

A próxima tela permite alterar o nome e as credenciais do segredo.

![Editar segredo](../../images/ui/event-forwarding/secrets/edit-secret-config.png)

>[!NOTE]
>
>Se o segredo estiver associado a um ambiente existente, você não poderá reatribuir o segredo a outro ambiente. Se desejar usar as mesmas credenciais em um ambiente diferente, será necessário [criar um novo segredo](#create) em vez disso. A única maneira de reatribuir o ambiente a partir desta tela é se você nunca atribuiu o segredo a um ambiente antecipadamente ou se excluiu o ambiente ao qual o segredo foi anexado.

### Repetir uma troca secreta

Você pode tentar novamente ou atualizar uma troca secreta na tela de edição. Esse processo varia dependendo do tipo de segredo que está sendo editado:

| Tipo de segredo | Repetir protocolo |
| --- | --- |
| [!UICONTROL Token] | Selecionar **[!UICONTROL Exchange Secret]** para tentar novamente a troca secreta. Esse controle só está disponível quando há um ambiente anexado ao segredo. |
| [!UICONTROL HTTP] | Se não houver nenhum ambiente anexado ao segredo, selecione **[!UICONTROL Exchange Secret]** para trocar a credencial para base64. Se um ambiente estiver anexado, selecione Selecionar **[!UICONTROL Trocar e Implantar Segredo]** para trocar para base64 e implantar o segredo para Cloudfare. |
| [!UICONTROL OAuth2] | Selecionar **[!UICONTROL Gerar token]** para trocar as credenciais e retornar um token de acesso do provedor de autenticação. |

## Excluir um segredo

Para excluir um segredo existente no  **[!UICONTROL Segredos]** na área de trabalho, marque a caixa de seleção ao lado do nome antes de selecionar **[!UICONTROL Excluir]**.

![Excluir segredo](../../images/ui/event-forwarding/secrets/delete.png)

## Uso de segredos no encaminhamento de eventos

Para usar um segredo no encaminhamento de eventos, primeiro crie um [elemento de dados](../managing-resources/data-elements.md) que faz referência ao próprio segredo. Depois de salvar o elemento de dados, você pode incluí-lo no encaminhamento do evento [regras](../managing-resources/rules.md) e adicionar essas regras a um [biblioteca](../publishing/libraries.md), que, por sua vez, pode ser implantado em servidores do Adobe como um [build](../publishing/builds.md).

Ao criar o elemento de dados, selecione o **[!UICONTROL Núcleo]** e selecione **[!UICONTROL Segredo]** para o tipo de elemento de dados. O painel direito atualiza e fornece controles suspensos para atribuir até três segredos ao elemento de dados: um para [!UICONTROL Desenvolvimento], [!UICONTROL Estágios]e [!UICONTROL Produção] respectivamente.

![Elemento de dados](../../images/ui/event-forwarding/secrets/data-element.png)

>[!NOTE]
>
>Somente os segredos anexados aos ambientes de desenvolvimento, armazenamento temporário e produção são exibidos para seus respectivos detalhamentos.

Ao atribuir vários segredos a um único elemento de dados e incluí-lo em uma regra, você pode ter o valor do elemento de dados alterado, dependendo de onde a biblioteca que contém está no [fluxo de publicação](../publishing/publishing-flow.md).

![Elemento de dados com vários segredos](../../images/ui/event-forwarding/secrets/multi-secret-data-element.png)

>[!NOTE]
>
>Ao criar o elemento de dados, um ambiente de desenvolvimento deve ser atribuído. Os segredos dos ambientes de armazenamento temporário e produção não são necessários, mas as criações que tentarem fazer a transição para esses ambientes falharão se os elementos de dados do tipo secreto não tiverem um segredo selecionado para o ambiente em questão.

## Próximas etapas

Este guia cobriu como gerenciar segredos na interface do usuário da coleta de dados. Para obter informações sobre como interagir com segredos usando a API do Reator, consulte o [guia do endpoint de segredos](../../api/endpoints/secrets.md).
