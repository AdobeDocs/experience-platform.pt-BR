---
title: Visão geral da Segurança da camada de transporte mútua (mTLS)
description: Saiba como você pode usar o mTLS para recuperar com segurança certificados públicos emitidos pelo Adobe para encaminhamento de eventos.
source-git-commit: 3b9ff1d41c698feadd0215ab562f87747aaa91a1
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 1%

---

# Visão geral da Segurança da Camada de Transporte Mútuo [!DNL mTLS]

Associe os certificados da Segurança da Camada de Transporte Mútuo ([!DNL mTLS]) na [!UICONTROL Interface do Usuário de Ambientes] para assumir o controle da segurança da sua extensão. O certificado [!DNL mTLS] é uma credencial digital que comprova a identidade de um servidor ou cliente em comunicações seguras. Quando você usa a API de Serviço [!DNL mTLS], esses certificados ajudam a verificar e criptografar suas interações com o Adobe Experience Platform Event Forwarding. Esse processo não só protege seus dados, mas também garante que cada conexão seja de um parceiro confiável.

## Implementar [!DNL mTLS] em um novo ambiente {#implement-mtls}

Configure o ambiente de Encaminhamento de eventos para garantir que as builds da biblioteca sejam implantadas corretamente na rede de borda. Durante a configuração, você pode selecionar a opção de hospedagem que melhor se adapta às suas necessidades de implantação. Um certificado [!DNL mTLS] também é adicionado automaticamente ao seu novo ambiente para comunicação segura.

Para criar um novo ambiente, selecione a guia **[!UICONTROL Ambientes]** no painel esquerdo das propriedades de Encaminhamento de Eventos e selecione **[!UICONTROL Adicionar Ambiente]**.

![Propriedades do encaminhamento de eventos mostrando ambientes existentes, destacando [!UICONTROL Adicionar Ambiente].](../../../images/extensions/server/cloud-connector/add-environment.png)

Na próxima página, selecione o ambiente que deseja usar para esta configuração. Três ambientes estão disponíveis:

>[!NOTE]
>
>Uma propriedade é limitada a um ambiente de desenvolvimento, de preparo e de produção.

| Ambiente | Descrição |
| --- | --- |
| Desenvolvimento | O ambiente de desenvolvimento é para os membros da equipe testarem bibliotecas ou alterações no Encaminhamento de eventos. |
| Armazenamento temporário | O ambiente de preparo é opcional e permite que os membros aprovados da equipe testem e aprovem uma biblioteca antes que ela seja publicada. |
| Produção | O ambiente de produção é usado para dados de produção em tempo real. |

![A tela de seleção do ambiente, destacando [!UICONTROL Selecionar] para Desenvolvimento.](../../../images/extensions/server/cloud-connector/select-environment.png)

Na página **[!UICONTROL Criar Ambiente]**, digite um **[!UICONTROL Nome]** e selecione ***Adobe Managed*** no menu suspenso **[!UICONTROL Selecionar Host]**. O **[!UICONTROL Certificado]** é ***Adicionado automaticamente***. Finalmente, selecione **[!UICONTROL Salvar]**.

![A página Criar Ambiente de Desenvolvimento, destacando [!UICONTROL Nome], [!UICONTROL Selecionar Host] e [!UICONTROL Salvar].](../../../images/extensions/server/cloud-connector/create-environment.png)

O ambiente foi criado com sucesso, e você retornará à guia **[!UICONTROL Ambientes]**, que exibe seu novo ambiente.

![A guia [!UICONTROL Ambientes], destacando o ambiente de Desenvolvimento.](../../../images/extensions/server/cloud-connector/new-environment-created.png)

## Exibir detalhes do certificado do ambiente {#view-certificate}

Para exibir os detalhes do certificado de um ambiente, selecione a guia **[!UICONTROL Ambientes]** no painel esquerdo das propriedades de Encaminhamento de eventos e, em seguida, selecione o ambiente para exibir os detalhes.

Os detalhes do certificado a seguir são exibidos:

| Ambiente | Descrição |
| --- | --- |
| Certificado | Detalhes do certificado, que incluem:<ul><li>**Nome**: o nome do certificado.</li><li>**Data de criação**: a data de criação do certificado.</li><li>**Status**: o status atual do certificado:<ul><li>**Atual**: o certificado está sendo usado ativamente.</li><li>**Obsoleto**: o certificado não está em uso, mas ainda não expirou. Ele ainda poderá ser selecionado para uso.</li><li>**Expirado**: o certificado expirou, está esmaecido e não está mais disponível para uso.</li></ul></ul> |
| Expira | Data em que o certificado expirará. |
| Variable Name | O nome da variável do certificado. |
| Status | O status atual do certificado:<ul><li>**Implantado**: o certificado foi implantado com êxito e está ativo.</li><li>**Implantando**: o certificado está em processo de implantação.</li><li>**Precisa da Implantação**: este status aparece quando um certificado obsoleto é selecionado.</li></ul> |

![A página Editar Ambiente de Desenvolvimento, destacando os detalhes do [!UICONTROL Certificado].](../../../images/extensions/server/cloud-connector/create-environment.png)

### Selecionar e implantar um certificado obsoleto {#deploy-obsolete-certificate}

Para usar um certificado obsoleto, navegue até a guia **[!UICONTROL Ambientes]** no painel esquerdo das propriedades de Encaminhamento de eventos e selecione o ambiente para exibir os detalhes.

![A guia [!UICONTROL Ambientes], destacando o ambiente de Desenvolvimento.](../../../images/extensions/server/cloud-connector/new-environment-created.png)

Na lista suspensa **[!UICONTROL Certificado]**, selecione um certificado obsoleto e, em seguida, **[!UICONTROL Salvar]**.

![A página Editar Ambiente de Desenvolvimento, destacando a lista suspensa [!UICONTROL Certificado] com o certificado obsoleto e Salvar realçado.](../../../images/extensions/server/cloud-connector/obsolete-certificate.png)

Para implantar o certificado, selecione **[!UICONTROL Salvar e implantar]** na caixa de diálogo **[!UICONTROL Implantar Certificado]**.

![Caixa de diálogo Implantar certificado com Salvar e implantar realçada.](../../../images/extensions/server/cloud-connector/obsolete-certificate-deploy.png)


## Próximas etapas {#next-steps}

Este documento demonstrou como criar um ambiente para sua propriedade de encaminhamento de eventos, adicionar um certificado e usar um certificado obsoleto. Para obter mais informações sobre os [!DNL mTLS] certificados, consulte [[!DNL mTLS] Visão geral da API de Serviço](../../../../data-governance/mtls-api/overview.md)

Para saber como usar certificados [!DNL mTLS] nas regras de Encaminhamento de Eventos, consulte a [Visão geral da extensão do Cloud Connector](../cloud-connector/overview.md/#mtls-rules).
