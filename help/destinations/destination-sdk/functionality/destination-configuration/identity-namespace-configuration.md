---
description: Saiba como configurar as identidades de destino compatíveis para destinos criados com o Destination SDK.
title: Configuração do namespace de identidade
exl-id: 30c0939f-b968-43db-b09b-ce5b34349c6e
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 4%

---

# Configuração do namespace de identidade

O Experience Platform usa namespaces de identidade para descrever o tipo de identidades específicas. Por exemplo, um namespace de identidade chamado `Email` identifica um valor como `name@email.com` como um endereço de email.

Ao criar um destino por meio do Destination SDK, além do [configuração de um schema de parceiro](schema-configuration.md) para que os usuários possam mapear atributos de perfil e identidades, você também pode definir namespaces de identidade compatíveis com sua plataforma de destino.

Ao fazer isso, os usuários têm a opção adicionada de selecionar identidades de destino, além de atributos de perfil de destino.

Para saber mais sobre namespaces de identidade no Experience Platform, consulte [documentação de namespaces de identidade](../../../../identity-service/features/namespaces.md).

Ao configurar namespaces de identidade para seu destino, você pode ajustar o mapeamento de identidade de destino compatível com seu destino, como:

* Permitir que os usuários mapeiem atributos XDM para namespaces de identidade.
* Permitindo que os usuários mapeiem [namespaces de identidade padrão](../../../../identity-service/features/namespaces.md#standard) aos seus próprios namespaces de identidade.
* Permitindo que os usuários mapeiem [namespaces de identidade personalizados](../../../../identity-service/features/namespaces.md#manage-namespaces) aos seus próprios namespaces de identidade.

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama no [opções de configuração](../configuration-options.md) ou consulte o guia sobre como [usar o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Você pode configurar os namespaces de identidade compatíveis por meio da `/authoring/destinations` terminal. Consulte as seguintes páginas de referência de API para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Atualizar uma configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artigo descreve todas as opções de configuração de namespaces de identidade compatíveis que você pode usar para o seu destino e mostra o que os clientes verão na interface do usuário da Platform.

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros compatíveis com o Destination SDK são **diferencia maiúsculas de minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações suportam a funcionalidade descrita nesta página.

| Tipo de integração | Suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (lote) | Sim |

## Parâmetros compatíveis {#supported-parameters}

Ao definir as identidades de público-alvo compatíveis com seu destino, você pode usar os parâmetros descritos na tabela abaixo para configurar seu comportamento.

| Parâmetro | Tipo | Obrigatório / Opcional | Descrição |
|---------|----------|---|------|
| `acceptsAttributes` | Booleano | Opcional | Indica se os clientes podem mapear atributos de perfil padrão para a identidade que você está configurando. |
| `acceptsCustomNamespaces` | Booleano | Opcional | Indica se os clientes podem mapear namespaces de identidade personalizados para o namespace de identidade que você está configurando. |
| `acceptedGlobalNamespaces` | - | Opcional | Indica qual [namespaces de identidade padrão](../../../../identity-service/features/namespaces.md#standard) (por exemplo, [!UICONTROL IDFA]) podem mapear para a identidade que você está configurando. |
| `transformation` | String | Opcional | Exibe o [[!UICONTROL Aplicar transformação]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) na interface da Platform, quando o campo de origem é um atributo XDM ou um namespace de identidade personalizado. Use essa opção para conceder aos usuários a capacidade de aplicar hash aos atributos de origem na exportação. Para ativar essa opção, defina o valor como `sha256(lower($))`. |
| `requiredTransformation` | String | Opcional | Quando os clientes selecionam esse namespace de identidade de origem, a variável [[!UICONTROL Aplicar transformação]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) A caixa de seleção é aplicada automaticamente ao mapeamento e os clientes não podem desativá-lo. Para ativar essa opção, defina o valor como `sha256(lower($))`. |

{style="table-layout:auto"}


```json
"identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   }
```

Você deve indicar qual [!DNL Platform] identidades que os clientes podem exportar para o seu destino. Alguns exemplos são [!DNL Experience Cloud ID], email com hash, ID de dispositivo ([!DNL IDFA], [!DNL GAID]). Esses valores são [!DNL Platform] namespaces de identidade que os clientes podem mapear para namespaces de identidade do seu destino.

Os namespaces de identidade não exigem uma correspondência de 1 para 1 entre [!DNL Platform] e seu destino.
Por exemplo, os clientes podem mapear um [!DNL Platform] [!DNL IDFA] namespace para um [!DNL IDFA] namespace do seu destino ou eles podem mapear o mesmo [!DNL Platform] [!DNL IDFA] namespace para um [!DNL Customer ID] namespace no seu destino.

Leia mais sobre identidades na [visão geral do namespace de identidade](../../../../identity-service/features/namespaces.md).

## Considerações de mapeamento

Se os clientes selecionarem um namespace de identidade de origem e não selecionarem um target mapping, o Platform preencherá automaticamente o target mapping com um atributo com o mesmo nome.

## Configurar hash de campo de origem opcional

Os clientes do Experience Platform podem optar por assimilar dados na Platform em formato com hash ou em texto simples. Se sua plataforma de destino aceitar dados com hash e sem hash, você poderá dar aos clientes a opção de escolher se a Platform deverá fazer o hash dos valores do campo de origem quando eles forem exportados para seu destino.

A configuração abaixo habilita a configuração [Aplicar transformação](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) na interface do usuário da Platform, na etapa Mapeamento.

```json {line-numbers="true" highlight="5"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
            },
            "Phone":{
            }
         }
      }
   }
```

Marque essa opção ao usar campos de origem sem hash, para que a Adobe Experience Platform faça o hash automaticamente na ativação.

Ao mapear atributos de origem com hash não atribuídos para atributos de destino que o destino espera que tenham hash (por exemplo: `email_lc_sha256` ou `phone_sha256`), verifique a **Aplicar transformação** opção para que o Adobe Experience Platform coloque automaticamente os atributos de origem em hash na ativação.

## Configurar hash de campo de origem obrigatório

Se o destino aceitar apenas dados com hash, você poderá configurar os atributos exportados para serem automaticamente transformados em hash pela Platform. A configuração abaixo verifica automaticamente o **Aplicar transformação** quando a variável `Email` e `Phone` identidades são mapeadas.

```json {line-numbers="true" highlight="8,11"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation": "sha256(lower($))"
            },
            "Phone":{
               "requiredTransformation": "sha256(lower($))"
            }
         }
      }
   }
```

## Próximas etapas {#next-steps}

Depois de ler este artigo, você deve entender melhor como configurar seus namespaces de identidade para destinos criados com o Destination SDK.

Para saber mais sobre os outros componentes de destino, consulte os seguintes artigos:

* [Autenticação do cliente](customer-authentication.md)
* [Autorização OAuth2](oauth2-authorization.md)
* [Campos de dados do cliente](customer-data-fields.md)
* [Atributos da interface](ui-attributes.md)
* [Configuração do esquema](schema-configuration.md)
* [Configuração do namespace de identidade](identity-namespace-configuration.md)
* [Configurações de mapeamento compatíveis](supported-mapping-configurations.md)
* [Entrega de destino](destination-delivery.md)
* [Configuração de metadados de público](audience-metadata-configuration.md)
* [Política de agregação](aggregation-policy.md)
* [Configuração em lote](batch-configuration.md)
* [Qualificações do perfil histórico](historical-profile-qualifications.md)
