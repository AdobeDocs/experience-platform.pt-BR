---
title: Conexão do Zendesk
description: O destino do Zendesk permite exportar seus dados de conta e ativá-los no Zendesk para suas necessidades comerciais.
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 3197eddcf9fef2870589fdf9f09276a333f30cd1
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 1%

---

# [!DNL Zendesk] conexão

[[!DNL Zendesk]](https://www.zendesk.com) O é uma solução de atendimento ao cliente e uma ferramenta de vendas.

Este [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) utiliza o [[!DNL Zendesk] API de Contatos](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/), para criar e atualizar identidades em um segmento como contatos no [!DNL Zendesk].

[!DNL Zendesk] O usa tokens de portador como um mecanismo de autenticação para se comunicar com a [!DNL Zendesk] API de contatos. Instruções para autenticar em seu [!DNL Zendesk] exemplo, são apresentados mais abaixo, no [Autenticar para destino](#authenticate) seção.

## Casos de uso {#use-cases}

Como profissional de marketing, você pode fornecer experiências personalizadas aos seus usuários com base em atributos de seus perfis do Adobe Experience Platform. Você pode criar segmentos a partir de dados offline e enviar esses segmentos para o [!DNL Zendesk], para ser exibido nos feeds dos usuários assim que os segmentos e perfis forem atualizados no Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

### Pré-requisitos do Experience Platform {#prerequisites-in-experience-platform}

Antes de ativar os dados para o [!DNL Zendesk] destino, você deve ter um [schema](/help/xdm/schema/composition.md), um [conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), e [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) criado em [!DNL Experience Platform].

Consulte a documentação do Experience Platform para [Grupo de campos de esquema Detalhes da associação do segmento](/help/xdm/field-groups/profile/segmentation.md) se você precisar de orientação sobre os status do segmento.

### [!DNL Zendesk] pré-requisitos {#prerequisites-destination}

Para exportar dados da Platform para o seu [!DNL Zendesk] conta que você precisa ter [!DNL Zendesk] conta.

#### Coletar [!DNL Zendesk] credenciais {#gather-credentials}

Anote os itens abaixo antes de autenticar na [!DNL Zendesk] destino:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| `Bearer token` | O token de acesso gerado no [!DNL Zendesk] conta. <br> Siga a documentação para [gerar um [!DNL Zendesk] token de acesso](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) se você não tiver um. | `a0b1c2d3e4...v20w21x22y23z` |

## Medidas de proteção {#guardrails}

A variável [Preços e Limites de Taxa](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) detalhes da página o [!DNL Zendesk] Limites de API associados à sua conta. Você precisa garantir que seus dados e carga estejam dentro dessas restrições.

## Identidades suportadas {#supported-identities}

[!DNL Zendesk] O oferece suporte à atualização de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade de destino | Exemplo | Descrição | Obrigatório |
|---|---|---|---|
| `email` | `test@test.com` | Endereço de email do contato. | Sim |

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | <ul><li>Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados *(por exemplo: endereço de email, número de telefone, sobrenome)*, de acordo com o mapeamento de campo.</li><li> Cada status de segmento em [!DNL Zendesk] é atualizado com o status de segmento correspondente da Platform, com base no **[!UICONTROL ID do mapeamento]** valor fornecido durante o [programação de segmentos](#schedule-segment-export-example) etapa.</li></ul> |
| Frequência de exportação | **[!UICONTROL Streaming]** | <ul><li>Os destinos de transmissão são conexões baseadas em API &quot;sempre ativas&quot;. Assim que um perfil é atualizado em Experience Platform com base na avaliação do segmento, o conector envia a atualização downstream para a plataforma de destino. Leia mais sobre [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Conectar ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

Dentro de **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** pesquisar [!DNL Zendesk]. Como alternativa, você pode localizá-lo na **[!UICONTROL CRM]** categoria.

### Autenticar para destino {#authenticate}

Preencha os campos obrigatórios abaixo. Consulte a [Coletar [!DNL Zendesk] credenciais](#gather-credentials) para obter orientação.
* **[!UICONTROL Token de portador]**: o token de acesso gerado no [!DNL Zendesk] conta.

Para autenticar no destino, selecione **[!UICONTROL Conectar ao destino]**.
![Captura de tela da interface do usuário da plataforma mostrando como autenticar.](../../assets/catalog/crm/zendesk/authenticate-destination.png)

Se os detalhes fornecidos forem válidos, a interface exibirá uma **[!UICONTROL Conectado]** com uma marca de seleção verde. Você pode prosseguir para a próxima etapa.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.
![Captura de tela da interface do usuário da plataforma mostrando os detalhes do destino.](../../assets/catalog/crm/zendesk/destination-details.png)

* **[!UICONTROL Nome]**: um nome pelo qual você reconhecerá esse destino no futuro.
* **[!UICONTROL Descrição]**: uma descrição que ajudará você a identificar esse destino no futuro.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface do](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Próxima]**.

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
>
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Ler [Ativar perfis e segmentos para destinos de exportação de segmento de transmissão](/help/destinations/ui/activate-segment-streaming-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para esse destino.

### Considerações e exemplo de mapeamento {#mapping-considerations-example}

Para enviar corretamente os dados do público-alvo do Adobe Experience Platform para a [!DNL Zendesk] destino, é necessário passar pela etapa de mapeamento de campos. O mapeamento consiste em criar um link entre os campos do esquema do Experience Data Model (XDM) na sua conta da Platform e seus equivalentes correspondentes no destino.

Atributos especificados na variável **[!UICONTROL Campo de destino]** deve ser nomeado exatamente como descrito na tabela mapeamentos de atributos, pois esses atributos formarão o corpo da solicitação.

Atributos especificados na variável **[!UICONTROL Campo de origem]** não seguem nenhuma restrição desse tipo. Você pode mapeá-lo com base na sua necessidade, no entanto, se o formato dos dados não estiver correto quando enviado para o [!DNL Zendesk] isso resultará em um erro.

Para mapear corretamente os campos XDM para o [!DNL Zendesk] campos de destino, siga estas etapas:

1. No **[!UICONTROL Mapeamento]** etapa, selecione **[!UICONTROL Adicionar novo mapeamento]**. Você verá uma nova linha de mapeamento na tela.
1. No **[!UICONTROL Selecionar campo de origem]** escolha a **[!UICONTROL Selecionar atributos]** e selecione o atributo XDM ou escolha o atributo **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade.
1. No **[!UICONTROL Selecionar campo de destino]** escolha a **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade ou escolha **[!UICONTROL Selecionar atributos personalizados]** e selecione um atributo conforme necessário.
   * Repita essas etapas para adicionar os seguintes mapeamentos entre o esquema de perfil XDM e o [!DNL Zendesk] instância: |Campo de origem|Campo de destino| Obrigatório| |—|—|—| |`xdm: person.name.lastName`|`Attribute: last_name` <br>ou `Attribute: name`| Sim | |`IdentityMap: Email`|`Identity: email`| Sim |

   * Um exemplo usando esses mapeamentos é mostrado abaixo:
      ![Exemplo de captura de tela da interface do usuário da plataforma com mapeamentos de atributo.](../../assets/catalog/crm/zendesk/mappings.png)

      >[!IMPORTANT]
      >
      >Ambos os mapeamentos de campo de destino são obrigatórios e obrigatórios para [!DNL Zendesk] para trabalhar.
      >
      >O mapeamento para *Sobrenome* ou *Nome* é obrigatório caso contrário, a variável [!DNL Zendesk] A API não responde com nenhum erro e qualquer valor de atributo transmitido é ignorado.

Quando terminar de fornecer os mapeamentos para sua conexão de destino, selecione **[!UICONTROL Próxima]**.

### Programar exportação de segmento e exemplo {#schedule-segment-export-example}

No [[!UICONTROL Agendar exportação de segmento]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) do fluxo de trabalho de ativação, você deve mapear segmentos da Platform manualmente para o atributo de campo personalizado em [!DNL Zendesk].

Para fazer isso, selecione cada segmento e insira o atributo de campo personalizado correspondente em [!DNL Zendesk] no **[!UICONTROL ID do mapeamento]** campo.

Um exemplo é mostrado abaixo:
![Exemplo de captura de tela da interface do Platform mostrando a exportação de segmento do cronograma.](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## Validar exportação de dados {#exported-data}

Para validar se você configurou o destino corretamente, siga as etapas abaixo:

1. Selecionar **[!UICONTROL Destinos]** > **[!UICONTROL Procurar]** e navegue até a lista de destinos.
1. Em seguida, selecione o destino e alterne para a guia **[!UICONTROL Dados de ativação]** e selecione um nome de segmento.
   ![Exemplo de captura de tela da interface do Platform mostrando Dados de ativação de destinos.](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. Monitore o resumo do segmento e verifique se a contagem de perfis corresponde à contagem no segmento.
   ![Exemplo de captura de tela da interface do Platform mostrando o segmento.](../../assets/catalog/crm/zendesk/segment.png)

1. Faça logon no [!DNL Zendesk] site e, em seguida, navegue até o **[!UICONTROL Contatos]** página para verificar se os perfis do segmento foram adicionados. Essa lista pode ser configurada para exibir colunas para os campos adicionais criados com o segmento **[!UICONTROL ID do mapeamento]** e status de segmento.
   ![Captura de tela da interface do Zendesk mostrando a página Contatos com os campos adicionais criados com o nome do segmento.](../../assets/catalog/crm/zendesk/contacts.png)

1. Como alternativa, você pode detalhar uma **[!UICONTROL Person]** e verifique a **[!UICONTROL Campos adicionais]** seção que exibe o nome do segmento e os status do segmento.
   ![Captura de tela da interface do Zendesk mostrando a página Pessoa com a seção de campos adicionais exibindo o nome do segmento e os status do segmento.](../../assets/catalog/crm/zendesk/contact.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte o [Visão geral da governança de dados](/help/data-governance/home.md).

## Recursos adicionais {#additional-resources}

Informações adicionais úteis do [!DNL Zendesk] A documentação do está abaixo:
* [Fazer sua primeira chamada](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [Campos personalizados](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)