---
title: (API) Conexão Oracle Eloqua
description: O destino (API) Oracle Eloqua permite exportar os dados da conta e ativá-los no Oracle Eloqua para as necessidades comerciais.
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 3197eddcf9fef2870589fdf9f09276a333f30cd1
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 0%

---

# [!DNL (API) Oracle Eloqua] conexão

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) O permite que os profissionais de marketing planejem e executem campanhas enquanto fornecem uma experiência personalizada para seus clientes potenciais. Com o gerenciamento integrado de leads e a fácil criação de campanhas, o modelo ajuda os profissionais de marketing a engajarem o público-alvo certo na hora certa da jornada do comprador e é dimensionado elegantemente para alcançar os públicos-alvo em todos os canais, incluindo email, pesquisa de exibição, vídeo e dispositivos móveis. As equipes de vendas podem fechar mais negócios a uma taxa mais rápida, aumentando o ROI do marketing por meio de insights em tempo real.

Este [!DNL Adobe Experience Platform] [destino](/help/destinations/home.md) utiliza o [Atualizar um contato](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) operação a partir do [!DNL Oracle Eloqua] API REST, que permite atualizar identidades em um segmento para [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] usos [Autenticação básica](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) para se comunicar com a [!DNL Oracle Eloqua] API REST. Instruções para autenticar em seu [!DNL Oracle Eloqua] exemplo, são apresentados mais abaixo, no [Autenticar para destino](#authenticate) seção.

## Casos de uso {#use-cases}

Como profissional de marketing, você pode fornecer experiências personalizadas aos seus usuários com base em atributos de seus perfis do Adobe Experience Platform. Você pode criar segmentos a partir de dados offline e enviar esses segmentos para o [!DNL Oracle Eloqua], para ser exibido nos feeds dos usuários assim que os segmentos e perfis forem atualizados no Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

### Pré-requisitos do Experience Platform {#prerequisites-in-experience-platform}

Antes de ativar os dados para o [!DNL Oracle Eloqua] destino, você deve ter um [schema](/help/xdm/schema/composition.md), um [conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), e [segmentos](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) criado em [!DNL Experience Platform].

Consulte a documentação do Experience Platform para [Grupo de campos de esquema Detalhes da associação do segmento](/help/xdm/field-groups/profile/segmentation.md) se você precisar de orientação sobre os status do segmento.

### [!DNL Oracle Eloqua] pré-requisitos {#prerequisites-destination}

Para exportar dados da Platform para o seu [!DNL Oracle Eloqua] conta que você precisa ter [!DNL Oracle Eloqua] conta.

#### Coletar [!DNL Oracle Eloqua] credenciais {#gather-credentials}

Anote os itens abaixo antes de autenticar na [!DNL Oracle Eloqua] destino:

| Credencial | Descrição |
| --- | --- |
| `Username` | O nome de usuário do seu [!DNL Oracle Eloqua] conta. |
| `Password` | A senha do seu [!DNL Oracle Eloqua] conta. |

## Medidas de proteção {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] campos de contato personalizados são criados automaticamente usando os nomes dos segmentos selecionados durante a **[!UICONTROL Selecionar segmentos]** etapa.


* [!DNL Oracle Eloqua] tem um limite máximo de 250 campos de contato personalizados.
* Antes de exportar novos segmentos, verifique se o número de segmentos da Platform e o número de segmentos existentes no [!DNL Oracle Eloqua] não excedam esse limite.
* Se esse limite for excedido, você encontrará um erro no Experience Platform. Isso ocorre porque a variável [!DNL Oracle Eloqua] A API não valida a solicitação e responde com um - *400: Erro de validação* - mensagem de erro descrevendo o problema.
* Se tiver atingido o limite especificado acima, será necessário remover os mapeamentos existentes do destino e excluir os campos de contato personalizados correspondentes no [!DNL Oracle Eloqua] antes de poder exportar mais segmentos.

* Consulte a [Oracle Eloqua Criando Campos de Contato](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) para obter informações sobre limites adicionais.

## Identidades suportadas {#supported-identities}

[!DNL Oracle Eloqua] O oferece suporte à atualização de identidades descritas na tabela abaixo. Saiba mais sobre [identidades](/help/identity-service/namespaces.md).

| Identidade de destino | Exemplo | Descrição | Obrigatório |
|---|---|---|---|
| `EloquaId` | `111111` | Identificador exclusivo do contato. | Sim |

## Conectar ao destino {#connect}

>[!IMPORTANT]
>
>Para se conectar ao destino, você precisa da variável **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md). No workflow de configuração de destino, preencha os campos listados nas duas seções abaixo.

Dentro de **[!UICONTROL Destinos]** > **[!UICONTROL Catálogo]** pesquisar [!DNL (API) Oracle Eloqua]. Como alternativa, você pode localizá-lo na **[!UICONTROL Marketing por email]** categoria.

### Autenticar para destino {#authenticate}

Preencha os campos obrigatórios abaixo. Consulte a [Coletar [!DNL Oracle Eloqua] credenciais](#gather-credentials) para obter orientação.
* **[!UICONTROL Senha]**: A senha do [!DNL Oracle Eloqua] conta.
* **[!UICONTROL Nome de usuário]**: O nome de usuário do [!DNL Oracle Eloqua] conta.

Para autenticar no destino, selecione **[!UICONTROL Conectar ao destino]**.
![Captura de tela da interface do usuário da plataforma mostrando como autenticar.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Se os detalhes fornecidos forem válidos, a interface exibirá uma **[!UICONTROL Conectado]** com uma marca de seleção verde. Você pode prosseguir para a próxima etapa.

### Preencher detalhes do destino {#destination-details}

Para configurar detalhes para o destino, preencha os campos obrigatórios e opcionais abaixo. Um asterisco ao lado de um campo na interface do usuário indica que o campo é obrigatório.
![Captura de tela da interface do usuário da plataforma mostrando os detalhes do destino.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

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

Para enviar corretamente os dados do público-alvo do Adobe Experience Platform para a [!DNL Oracle Eloqua] destino, é necessário passar pela etapa de mapeamento de campos. O mapeamento consiste em criar um link entre os campos do esquema do Experience Data Model (XDM) na sua conta da Platform e seus equivalentes correspondentes no destino.

`EloquaID` O é necessário para atualizar atributos correspondentes à Identidade. A variável `emailAddress` também é necessário, pois sem ele, a API emite um erro, conforme indicado abaixo:

```json
{
   "type":"ObjectValidationError",
   "container":{
      "type":"ObjectKey",
      "objectType":"Contact"
   },
   "property":"emailAddress",
   "requirement":{
      "type":"EmailAddressRequirement"
   },
   "value":"<null>"
}
```

Atributos especificados na variável **[!UICONTROL Campo de destino]** deve ser nomeado exatamente como descrito na tabela mapeamentos de atributos, pois esses atributos formarão o corpo da solicitação.

Atributos especificados na variável **[!UICONTROL Campo de origem]** não seguem nenhuma restrição desse tipo. Você pode mapeá-lo com base na sua necessidade, no entanto, se o formato dos dados não estiver correto quando enviado para o [!DNL Oracle Eloqua] isso resultará em um erro.

Por exemplo, você pode mapear **[!UICONTROL Campo de origem]** namespace de identidade `contact key`, `ABC ID` etc. para **[!UICONTROL Campo de destino]** : `EloquaID` após assegurar que os valores de ID estão em conformidade com o formato aceito pelo [!DNL Oracle Eloqua].

Para mapear corretamente os campos XDM para o [!DNL Oracle Eloqua] campos de destino, siga estas etapas:

1. No **[!UICONTROL Mapeamento]** etapa, selecione **[!UICONTROL Adicionar novo mapeamento]**. Você verá uma nova linha de mapeamento na tela.
1. No **[!UICONTROL Selecionar campo de origem]** escolha a **[!UICONTROL Selecionar atributos]** e selecione o atributo XDM ou escolha o atributo **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade.
1. No **[!UICONTROL Selecionar campo de destino]** escolha a **[!UICONTROL Selecionar namespace de identidade]** e selecione uma identidade ou escolha **[!UICONTROL Selecionar atributos personalizados]** e selecione um atributo conforme necessário.
   * Repita essas etapas para adicionar os seguintes mapeamentos entre o esquema de perfil XDM e o [!DNL Oracle Eloqua] instância: |Campo de origem|Campo de destino| Obrigatório| |—|—|—| |`xdm: personalEmail.address`|`Attribute: emailAddress`| Sim | |`IdentityMap: Eid`|`Identity: EloquaId`| Sim |

   * Um exemplo usando esses mapeamentos é mostrado abaixo:
      ![Exemplo de captura de tela da interface do usuário da plataforma com mapeamentos de atributo.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

      >[!IMPORTANT]
      >
      >Ambos os `emailAddress` e `EloquaId` os mapeamentos de atributo de destino são obrigatórios.

Quando terminar de fornecer os mapeamentos para sua conexão de destino, selecione **[!UICONTROL Próxima]**.

>[!NOTE]
>
>O destino coloca automaticamente um identificador exclusivo entre os nomes de segmento selecionados em cada execução ao enviar as informações do campo de contato para o [!DNL Oracle Eloqua]. Isso garante que os nomes de campo de contato correspondentes aos nomes de segmento não se sobreponham. Consulte a [Validar exportação de dados](#exported-data) seção captura de tela exemplo de um [!DNL Oracle Eloqua] Página Detalhes do contato com campo de contato personalizado criado usando os nomes do segmento.

## Validar exportação de dados {#exported-data}

Para validar se você configurou o destino corretamente, siga as etapas abaixo:

1. Selecionar **[!UICONTROL Destinos]** > **[!UICONTROL Procurar]** e navegue até a lista de destinos.
1. Em seguida, selecione o destino e alterne para a guia **[!UICONTROL Dados de ativação]** e selecione um nome de segmento.
   ![Exemplo de captura de tela da interface do Platform mostrando Dados de ativação de destinos.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Monitore o resumo do segmento e verifique se a contagem de perfis corresponde à contagem no segmento.
   ![Exemplo de captura de tela da interface do Platform mostrando o segmento.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Faça logon no [!DNL Oracle Eloqua] site e, em seguida, navegue até o **[!UICONTROL Visão geral dos contatos]** página para verificar se os perfis do segmento foram adicionados. Para ver o status do segmento, faça drill-down em uma **[!UICONTROL Detalhes de contato]** e verifique se o campo de contato com o nome do segmento selecionado como seu prefixo foi criado.

![Captura de tela da interface do usuário do Oracle Eloqua mostrando a página Detalhes do contato com o campo de contato personalizado criado com o nome do segmento.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Uso e governança de dados {#data-usage-governance}

Todos [!DNL Adobe Experience Platform] os destinos estão em conformidade com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] fiscaliza a governança de dados, consulte o [Visão geral da governança de dados](/help/data-governance/home.md).

## Erros e solução de problemas {#errors-and-troubleshooting}

Ao criar o destino, você pode receber uma das seguintes mensagens de erro: `400: There was a validation error` ou `400 BAD_REQUEST`. Isso acontece quando você excede o limite de 250 campos de contato personalizados, conforme descrito na [grades de proteção](#guardrails) seção. Para corrigir esse erro, verifique se você não está excedendo o limite do campo de contato personalizado em [!DNL Oracle Eloqua].
![Captura de tela da interface do usuário da plataforma mostrando erro.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

Consulte a [[!DNL Oracle Eloqua] Códigos de status HTTP](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) e [[!DNL Oracle Eloqua] Erros de validação](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) para obter uma lista abrangente de códigos de erro e status com explicações.

## Recursos adicionais {#additional-resources}

Informações adicionais úteis do [!DNL Oracle ELoqua] A documentação do está abaixo:
* [Automação de marketing do Oracle Eloqua](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [API REST para o serviço de Marketing Cloud Oracle Eloqua](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)