---
keywords: mobile; braze; messaging;
title: Destino do Brasil
seo-title: Destino do Brasil
description: O Brasil é uma plataforma abrangente de envolvimento do cliente que potencializa experiências relevantes e memoráveis entre os clientes e as marcas que eles adoram.
seo-description: O Brasil é uma plataforma abrangente de envolvimento do cliente que potencializa experiências relevantes e memoráveis entre os clientes e as marcas que eles adoram.
translation-type: tm+mt
source-git-commit: 9126a9b3a27aa0a0ecefb5d490475423d7840791
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 1%

---


# (Beta) [!DNL Braze] destino

>[!IMPORTANT]
>
>O destino brasileiro no Adobe Experience Platform está atualmente em Beta. A documentação e a funcionalidade estão sujeitas a alterações.

## Visão geral {#overview}

O [!DNL Braze] destino ajuda a enviar dados do perfil para [!DNL Braze].

[!DNL Braze] é uma plataforma abrangente de envolvimento do cliente que fornece experiências relevantes e memoráveis entre os clientes e as marcas que eles adoram.

Para enviar dados de perfil para [!DNL Braze], primeiro conecte-se ao destino.

## Especificações de destino {#destination-specs}

Observe os seguintes detalhes específicos do [!DNL Braze] destino:

* Você pode enviar qualquer [identidade](../../identity-service/namespaces.md) para o [!DNL Braze] destino, contanto que a mapeie para o destino [!DNL Braze][`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation).
* [!DNL Adobe Experience Platform] segmentos são exportados para [!DNL Braze] sob o `AdobeExperiencePlatformSegments` atributo.

## Casos de uso {#use-cases}

Como profissional de marketing, quero público alvo os usuários em um destino de envolvimento móvel, com segmentos integrados [!DNL Adobe Experience Platform]. Além disso, quero fornecer experiências personalizadas a elas, com base em atributos de seus [!DNL Adobe Experience Platform] perfis, assim que os segmentos e perfis forem atualizados em [!DNL Adobe Experience Platform].

## Tipo de exportação {#export-type}

**[!DNL Profile-based]** - você está exportando todos os membros de um segmento, juntamente com os campos de schema desejados (por exemplo: endereço de email, número de telefone, sobrenome) e/ou identidades, de acordo com o mapeamento de campo.
[!DNL Adobe Experience Platform] segmentos são exportados para [!DNL Braze] sob o `AdobeExperiencePlatformSegments` atributo.


## Conectar ao destino {#connect-destination}

1. Em **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]**, selecione [!DNL Braze]e selecione **[!UICONTROL Configurar]**.

   ![Configurar Destino do Brasil](assets/braze-destination-configure.png)

   >[!NOTE]
   >
   >Se já existir uma conexão com esse destino, você poderá ver um botão **[!UICONTROL Ativar]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Ativar]** e **[!UICONTROL Configurar]**, consulte a seção [Catálogo](../destinations/destinations-workspace.md#catalog) da documentação da área de trabalho de destino.
   >
   >![Ativar Destino do Brasil](assets/braze-destination-activate.png)

1. Na etapa [!UICONTROL Conta] , é necessário fornecer o token da sua [!DNL Braze] conta. Esta é a sua [!DNL Braze][!DNL API] chave. Você pode encontrar instruções detalhadas sobre como obter sua [!DNL API] chave aqui: [Visão geral](https://www.braze.com/docs/api/api_key/)da chave da API REST. Digite o token e clique em **[!UICONTROL Conectar-se ao destino]**.
   ![Etapa da Conta de Destino Brasileira](assets/braze-destination-account.png)

1. Clique em **[!UICONTROL Próximo]**.

1. Na etapa [!UICONTROL Autenticação] , é necessário inserir os detalhes da [!DNL Braze] conexão:
   * **[!UICONTROL Nome]**: insira um nome pelo qual você reconhecerá esse destino no futuro.
   * **[!UICONTROL Descrição]**: insira uma descrição que o ajudará a identificar esse destino no futuro.
   * **[!UICONTROL Instância]** do Ponto de Extremidade: pergunte ao seu [!DNL Braze] representante qual instância de endpoint você deve usar.
   * **[!UICONTROL Caso]** de uso de marketing: os casos de uso de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar de casos de uso de marketing definidos pelo Adobe ou criar seu próprio caso de uso de marketing. Para obter mais informações sobre casos de uso de marketing, consulte o [Data Governance na página do Adobe Experience Platform](../privacy/data-governance-overview.md#destinations) . Para obter informações sobre casos individuais de uso de marketing definidos pelo Adobe, consulte a visão geral [das políticas de uso de](../../data-governance/policies/overview.md#core-actions)dados.

   ![Etapa de autenticação do site](assets/braze-destination-authentication.png)

1. Clique em **[!UICONTROL Criar destino]**. Seu destino agora é criado. Você pode clicar em **[!UICONTROL Salvar e sair]** se quiser ativar segmentos posteriormente, ou selecionar **[!UICONTROL Próximo]** para continuar o fluxo de trabalho e selecionar segmentos para ativar. Em ambos os casos, consulte a próxima seção, [Ativar segmentos](#activate-segments), para o restante do fluxo de trabalho.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](activate-destinations.md#select-attributes) para obter informações sobre o fluxo de trabalho da ativação de segmentos.

## Mapeamento de campos {#field-mapping}

Para enviar corretamente seus dados de audiência [!DNL Adobe Experience Platform] para o [!DNL Braze] destino, é necessário percorrer a etapa de mapeamento de campo.

O mapeamento consiste em criar um link entre os campos do schema [!DNL Experience Data Model] (XDM) na sua [!DNL Platform] conta e seus equivalentes correspondentes do destino do público alvo.

Para mapear corretamente seus campos XDM para os campos de [!DNL Braze] destino, siga estas etapas:

1. Na etapa [!UICONTROL Mapeamento] , clique em **[!UICONTROL Adicionar novo mapeamento]**.

   ![Mapeamento de adição de destino de brasileiro](assets/braze-destination-mapping.png)

2. Na seção Campo [!UICONTROL de] origem, clique no botão de seta ao lado do campo vazio.

   ![Mapeamento de origem de destino do Brasil](assets/braze-destination-mapping-source.png)

3. Na janela [!UICONTROL Selecionar campo] de origem, você pode escolher entre duas categorias de campos XDM:
   * [!UICONTROL Selecionar atributos]: use essa opção para mapear um campo específico do seu schema XDM para um [!DNL Braze] atributo.

      ![Atributo de Origem do Mapeamento de Destino Brasileiro](assets/braze-destination-mapping-attributes.png)

   * [!UICONTROL Selecionar namespace]de identidade: Use esta opção para mapear uma namespace de [!DNL Platform] identidade para uma [!DNL Braze] namespace.

      ![Namespace de Origem do Mapeamento de Destino Brasileiro](assets/braze-destination-mapping-namespaces.png)
   Escolha o campo de origem e clique em **[!UICONTROL Selecionar]**.

4. Na seção Campo [!UICONTROL do] Público alvo, clique no ícone de mapeamento à direita do campo.

   ![Target mapping de Destino Brasileiro](assets/braze-destination-mapping-target.png)

5. Na janela [!UICONTROL Selecionar campo] público alvo, é possível escolher entre três categorias de campos públicos alvos:
   * [!UICONTROL Selecionar atributos]: Use essa opção para mapear seus atributos XDM para [!DNL Braze] atributos padrão.
   * [!UICONTROL Selecionar namespace]de identidade: Use esta opção para mapear namespaces de [!DNL Platform] identidade para namespaces de [!DNL Braze] identidade.
   * [!UICONTROL Selecionar atributos]personalizados: Use essa opção para mapear atributos XDM para atributos personalizados [!DNL Braze] que você definiu na sua [!DNL Braze] conta.
      * Você também pode usar essa opção para renomear atributos XDM existentes para [!DNL Braze]. Por exemplo, mapear um atributo `lastName` XDM para um `Last_Name` atributo personalizado em [!DNL Braze], criará o `Last_Name` atributo em [!DNL Braze], se ele ainda não existir, e mapeará o atributo `lastName` XDM para ele.

   ![Campos de Target mapping de Destino Brasileiro](assets/braze-destination-mapping-target-fields.png)

   Escolha o campo público alvo e clique em **[!UICONTROL Selecionar]**.

6. Agora você deve ver o mapeamento de campo na lista.

   ![Mapeamento de Destino da Brasileira Concluído](assets/braze-destination-mapping-complete.png)

7. Para adicionar mais mapeamentos, repita as etapas de 1 a 6.

### Exemplo {#mapping-example}

Digamos que seu schema de perfil XDM e sua [!DNL Braze] instância contenham os seguintes atributos e identidades:

|  | Schema de Perfil XDM | [!DNL Braze] Instância |
|---|---|---|
| Atributos | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>NúmeroTelefone</code></li></ul> |
| Identidades | <ul><li>Email</code></li><li>Google Ad ID (GAID)</code></li><li>ID da Apple para anunciantes (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

O mapeamento correto seria semelhante a:

![Exemplo de mapeamento de destino do Brasil](assets/braze-destination-mapping-example.png)

## Dados exportados {#exported-data}

Para verificar se os dados foram exportados com êxito para o [!DNL Braze] destino, verifique sua [!DNL Braze] conta. [!DNL Adobe Experience Platform] segmentos são exportados para [!DNL Braze] sob o `AdobeExperiencePlatformSegments` atributo.

## Uso e governança de dados {#data-usage-governance}

Todos os [!DNL Adobe Experience Platform] destinos são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplicar o controle de dados, consulte [Controle de dados em CDP](/help/rtcdp/privacy/data-governance-overview.md)em tempo real.

