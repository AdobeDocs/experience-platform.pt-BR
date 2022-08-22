---
keywords: crm; CRM; destinos crm; alcance; destino do crm de alcance geral
title: Conexão de saída
description: O Destino de alcance geral permite que você exporte seus dados de conta e ative-os dentro do Outreach para suas necessidades comerciais.
source-git-commit: 27da0f8d7896fd32e8a1b828630db7e5e08185c2
workflow-type: tm+mt
source-wordcount: '1714'
ht-degree: 1%

---


# [!DNL Outreach] conexão

## Visão geral {#overview}

[[!DNL Outreach]](https://www.outreach.io/) é uma Sales Execution Platform com os dados de interação mais vendidos pelo comprador B2B no mundo e investimentos significativos em tecnologias de IA proprietárias para traduzir dados de vendas em inteligência. [!DNL Outreach] ajuda as organizações a automatizarem o envolvimento de vendas e agirem com a inteligência de receita para melhorar sua eficiência, previsibilidade e crescimento.

Essa [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) utiliza o [API de recursos de atualização de alcance externo](https://api.outreach.io/api/v2/docs#update-an-existing-resource), que permite atualizar identidades em um segmento correspondente a prospetos em [!DNL Outreach].

[!DNL Outreach] O usa o OAuth 2 com a concessão de autorização como mecanismo de autenticação para se comunicar com o [!DNL Outreach] [!DNL Update Resource API]. Instruções para autenticação em seu [!DNL Outreach] instâncias estão mais abaixo, dentro de [Autenticar para destino](#authenticate) seção.

## Casos de uso {#use-cases}

Como profissional de marketing, você pode fornecer experiências personalizadas para seus prospetos, com base em atributos de seus perfis do Adobe Experience Platform. Você pode criar segmentos a partir de seus dados offline e enviar esses segmentos para [!DNL Outreach], para exibir nos feeds de prospetos assim que os segmentos e os perfis forem atualizados no Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

### Pré-requisitos do Experience Platform {#prerequisites-in-experience-platform}

Antes de ativar os dados para o [!DNL Outreach] destino, você deve ter um [schema](/help/xdm/schema/composition.md), a [conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)e [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) criado em [!DNL Experience Platform].

Consulte a documentação do Adobe para obter [Grupo de campos Detalhes da associação ao segmento](/help/xdm/field-groups/profile/segmentation.md) se você precisar de orientação sobre os status do segmento.

### Pré-requisitos de alcance {#prerequisites-destination}

Observe os seguintes pré-requisitos em [!DNL Outreach]para exportar dados da Platform para seu [!DNL Outreach] conta:

#### Você precisa ter uma conta do Outreach {#prerequisites-account}

Vá para o [!DNL Outreach] [fazer logon](https://accounts.outreach.io/users/sign_in) para registrar e criar uma conta, se você ainda não tiver uma. Consulte também a [!DNL Outreach] suporte [página](https://support.outreach.io/hc/en-us/articles/207238607-Claim-Your-Outreach-Account) para obter mais detalhes.

Anote os itens abaixo antes de autenticar para o [!DNL Outreach] Destino do CRM:

| Credencial | Descrição |
|---|---|
| Email | Seu [!DNL Outreach] email da conta |
| Senha | Seu [!DNL Outreach] senha da conta |

#### Configurar rótulos de campo personalizados {#prerequisites-custom-fields}

[!DNL Outreach] suporta campos personalizados para [prospetos](https://support.outreach.io/hc/en-us/articles/360001557554-Outreach-Prospect-Profile-Overview). Consulte [Como adicionar um campo personalizado no Outlook](https://support.outreach.io/hc/en-us/articles/219124908-How-To-Add-a-Custom-Field-in-Outreach) para obter orientações adicionais. Para facilitar a identificação, é recomendável atualizar manualmente os rótulos para seus nomes de segmento correspondentes em vez de manter os padrões. Por exemplo, conforme abaixo:

[!DNL Outreach] página de configurações para prospetos exibindo campos personalizados.
![Captura de tela da interface do usuário do Outreach mostrando os campos personalizados na página de configurações.](../../assets/catalog/crm/outreach/outreach-custom-fields.png)

[!DNL Outreach] página de configurações para prospetos exibindo campos personalizados com *fácil de usar* rótulos correspondentes aos nomes dos segmentos. Você pode exibir o status do segmento na página de prospecto em relação a esses rótulos.
![Captura de tela da interface do usuário do Outreach mostrando campos personalizados com rótulos associados na página de configurações.](../../assets/catalog/crm/outreach/outreach-custom-field-labels.png)

>[!NOTE]
>
> Os nomes dos rótulos são apenas para facilitar a identificação. Eles não são usados ao atualizar prospetos.

## Medidas de proteção

O [!DNL Outreach] A API tem um limite de taxa de 10.000 solicitações por hora e por usuário. Se atingir esse limite, você receberá uma `429` com a seguinte mensagem: `You have exceeded your permitted rate limit of 10,000; please try again at 2017-01-01T00:00:00.`.

Se você recebeu esta mensagem, é necessário atualizar seu cronograma de exportação de segmento para estar em conformidade com o limite de taxa.

Consulte a [[!DNL Outreach] documentação](https://api.outreach.io/api/v2/docs#rate-limiting) para obter mais detalhes.

## Identidades suportadas {#supported-identities}

[!DNL Outreach] O suporta a atualização de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade do Target | Descrição | Considerações |
|---|---|---|
| `OutreachId` | <ul><li>[!DNL Outreach] identificador. Este é um valor numérico correspondente ao perfil do prospecto.</li><li>A ID deve corresponder à ID na variável [!DNL Outreach] URL do prospecto que está sendo atualizado.</li><li>Consulte a [[!DNL Outreach] documentação](https://api.outreach.io/api/v2/docs#update-an-existing-resource) para obter mais detalhes.</li></ul> | Obrigatório |

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | <ul><li> Você está exportando todos os membros de um segmento, junto com os campos de esquema desejados *(por exemplo: endereço de email, número de telefone, sobrenome)*, de acordo com o mapeamento de campo.</li><li> Cada status de segmento em [!DNL Outreach] é atualizado com o status de segmento correspondente da Platform, com base no [!UICONTROL ID de mapeamento] valor fornecido durante a [agendamento de segmento](#schedule-segment-export-example) etapa.</li></ul> |
| Frequência de exportação | **[!UICONTROL Streaming]** | <ul><li> Os destinos de transmissão são conexões &quot;sempre ativas&quot; baseadas em API. Assim que um perfil é atualizado no Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
> Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow para configurar destino , preencha os campos listados nas duas seções abaixo.

Within **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** pesquisar por [!DNL Outreach]. Como alternativa, você pode localizá-lo na categoria CRM .

### Autenticar para destino {#authenticate}

Para autenticar para o destino, selecione **[!UICONTROL Ligar ao destino]**.

![Captura de tela da interface do usuário da plataforma que mostra como autenticar para o Outreach.](../../assets/catalog/crm/outreach/authenticate-destination.png)

Você verá o [!DNL Outreach] página de logon. Forneça seu email.

![Captura de tela da interface do usuário do Outreach mostrando o campo para inserir email para autenticação no Outreach.](../../assets/catalog/crm/outreach/authenticate-destination-login-email.png)

Em seguida, forneça sua senha.

![Captura de tela da interface do usuário do Outreach mostrando o campo para inserir a etapa de senha para autenticar para o Outreach.](../../assets/catalog/crm/outreach/authenticate-destination-login-password.png)

* **[!UICONTROL Nome do usuário]**: Seu [!DNL Outreach] email da conta.
* **[!UICONTROL Senha]**: Seu [!DNL Outreach] senha da conta.

Se os detalhes fornecidos forem válidos, a interface do usuário exibirá uma **Conectado** status com uma marca de seleção verde. Você pode prosseguir para a próxima etapa.

### Preencha os detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.
![Captura de tela da interface do usuário da plataforma que mostra como preencher os detalhes para o destino de alcance geral.](../../assets/catalog/crm/outreach/destination-details.png)

* **[!UICONTROL Nome]**: Um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: Uma descrição que ajudará a identificar esse destino no futuro.

### Ativar alertas {#enable-alerts}

Você pode habilitar alertas para receber notificações sobre o status do fluxo de dados para seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de destinos usando a interface do usuário](../../ui/alerts.md).

Quando terminar de fornecer detalhes para a conexão de destino, selecione **[!UICONTROL Próximo]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
> Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmentos de fluxo](../../ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Considerações e exemplo de mapeamento {#mapping-considerations-example}

Para enviar corretamente os dados de público-alvo do Adobe Experience Platform para a [!DNL Outreach] , é necessário percorrer a etapa de mapeamento de campo . O mapeamento consiste em criar um link entre os campos do esquema do Modelo de dados de experiência (XDM) na conta da plataforma e os equivalentes correspondentes do destino. Para mapear corretamente os campos XDM para a variável [!DNL Outreach] campos de destino, siga estas etapas:

1. No [!UICONTROL Mapeamento] etapa , clique em **[!UICONTROL Adicionar novo mapeamento]**. Você verá uma nova linha de mapeamento na tela.
   ![Captura de tela da interface do usuário da plataforma que mostra como adicionar novo mapeamento](../../assets/catalog/crm/outreach/add-new-mapping.png)

1. No [!UICONTROL Selecionar campo de origem] escolha a **[!UICONTROL Selecionar namespace de identidade]** e adicione os mapeamentos desejados.
   ![Captura de tela da interface do usuário da plataforma mostrando o mapeamento da fonte](../../assets/catalog/crm/outreach/source-mapping.png)

1. No [!UICONTROL Selecionar campo de destino] selecione o tipo de campo de destino para o qual deseja mapear o campo de origem.
   * **[!UICONTROL Selecionar namespace de identidade]**: selecione essa opção para mapear o campo de origem para um namespace de identidade da lista.
      ![Captura de tela da interface do usuário da plataforma que mostra o mapeamento do Target usando o OutreachId.](../../assets/catalog/crm/outreach/target-mapping.png)

   * Adicione o seguinte mapeamento entre o esquema de perfil XDM e o [!DNL Outreach] instância: |Esquema de Perfil XDM|[!DNL Outreach] Instância| Obrigatória| |—|—| |`Oid`|`OutreachId`| Sim |

   * **[!UICONTROL Selecionar atributos personalizados]**: selecione essa opção para mapear o campo de origem para um atributo personalizado definido na variável [!UICONTROL Nome do atributo] campo. Consulte [[!DNL Outreach] documentação do prospecto](https://api.outreach.io/api/v2/docs#prospect) para obter uma lista abrangente dos atributos suportados.
      ![Captura de tela da interface do usuário da plataforma que mostra o mapeamento do Target usando LastName.](../../assets/catalog/crm/outreach/target-mapping-lastname.png)

   * Por exemplo, dependendo dos valores que deseja atualizar, adicione o seguinte mapeamento entre o esquema de perfil XDM e o [!DNL Outreach] instância: |Esquema de Perfil XDM|[!DNL Outreach] Instância| |—|—| |`person.name.firstName`|`firstName`| |`person.name.lastName`|`lastName`|

   * Um exemplo de uso desses mapeamentos é mostrado abaixo:
      ![Exemplo de captura de tela da interface do usuário da plataforma que mostra os mapeamentos do Target.](../../assets/catalog/crm/outreach/mappings.png)

### Programar exportação de segmento e exemplo {#schedule-segment-export-example}

* Ao executar o [Agendar exportação de segmentos](../../ui/activate-segment-streaming-destinations.md) etapa você deve mapear manualmente os segmentos da Platform para o atributo de campo personalizado em [!DNL Outreach].

* Para fazer isso, selecione cada segmento e insira o valor numérico correspondente que corresponde à variável *Campo personalizado `N` Rótulo* campo de [!DNL Outreach] no **[!UICONTROL ID de mapeamento]** campo.

   >[!IMPORTANT]
   >
   > * O valor numérico *(`N`)* usada na variável [!UICONTROL ID de mapeamento] deve corresponder à chave do atributo personalizado com o sufixo do valor numérico em [!DNL Outreach]. Exemplo: *Campo personalizado `N` Rótulo*.
   > * Você só precisa especificar o valor numérico, não todo o rótulo de campo personalizado.
   > * [!DNL Outreach] O suporta no máximo 150 campos de rótulo personalizados.
   > * Consulte [[!DNL Outreach] documentação do prospecto](https://api.outreach.io/api/v2/docs#prospect) para obter detalhes.


   * Por exemplo:

      | [!DNL Outreach] Campo | ID de mapeamento de plataforma |
      |---|---|
      | Campo personalizado `4` Rótulo | `4` |

      ![Captura de tela da interface do usuário da plataforma que mostra um exemplo de ID de mapeamento durante a exportação do segmento Programação.](../../assets/catalog/crm/outreach/schedule-segment-export.png)

## Validar exportação de dados {#exported-data}

Para validar se você configurou o destino corretamente, siga as etapas abaixo:

1. Selecionar **[!UICONTROL Destinos]** > **[!UICONTROL Procurar]** para navegar até a lista de destinos.
   ![Captura de tela da interface do usuário da plataforma que mostra os Destinos de navegação.](../../assets/catalog/crm/outreach/browse-destinations.png)

1. Selecione o destino e valide se o status é **[!UICONTROL ativado]**.
   ![Captura de tela da interface do usuário da plataforma que mostra a Execução do fluxo de dados de destinos para o destino selecionado.](../../assets/catalog/crm/outreach/destination-dataflow-run.png)

1. Alterne para **[!DNL Activation data]** e selecione um nome de segmento.
   ![Captura de tela da interface do usuário da plataforma que mostra os dados de Ativação de destinos.](../../assets/catalog/crm/outreach/destinations-activation-data.png)

1. Monitore o resumo do segmento e garanta que a contagem de perfis corresponda à contagem criada no segmento.
   ![Captura de tela da interface do usuário da plataforma que mostra o resumo do segmento.](../../assets/catalog/crm/outreach/segment.png)

1. Faça logon no [!DNL Outreach] e navegue até o [!DNL Apps] > [!DNL Contacts] e verificar se os perfis do segmento foram adicionados. Você pode ver que cada status de segmento em [!DNL Outreach] foi atualizado com o status de segmento correspondente da Platform, com base no [!UICONTROL ID de mapeamento] valor fornecido durante a [agendamento de segmento](#schedule-segment-export-example) etapa.

![Captura de tela da interface do usuário do Outreach mostrando a página Perspectivas de alcance de saída com os status de segmento atualizados.](../../assets/catalog/crm/outreach/outreach-prospect.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] Os destinos são compatíveis com as políticas de uso de dados ao manipular os dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, consulte [Visão geral da governança de dados](/help/data-governance/home.md).

## Erros e solução de problemas {#errors-and-troubleshooting}

Ao verificar uma execução de fluxo de dados, você poderá ver a seguinte mensagem de erro: `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![Captura de tela da interface do usuário da plataforma que mostra o erro de solicitação incorreta.](../../assets/catalog/crm/outreach/error.png)

Para corrigir esse erro, verifique se a variável [!UICONTROL ID de mapeamento] fornecido na plataforma para a [!DNL Outreach] é válido e existe em [!DNL Outreach].

## Recursos adicionais {#additional-resources}

O [[!DNL Outreach] documentação](https://api.outreach.io/api/v2/docs/) tem detalhes sobre [Respostas de erro](https://api.outreach.io/api/v2/docs#error-responses) que você pode usar para depurar qualquer problema.
