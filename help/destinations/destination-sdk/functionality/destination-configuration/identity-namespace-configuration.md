---
description: Saiba como configurar as identidades de destino compatíveis para destinos criados com o Destination SDK.
title: Configuração do namespace de identidade
exl-id: 30c0939f-b968-43db-b09b-ce5b34349c6e
source-git-commit: 9f4ce2a3a8af72342683c859caa270662b161b7d
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 3%

---

# Configuração do namespace de identidade

O Experience Platform usa namespaces de identidade para descrever o tipo de identidades específicas. Por exemplo, um namespace de identidade chamado `Email` identifica um valor como `name@email.com` como um endereço de email.

Dependendo do tipo de destino que você criar (streaming ou baseado em arquivo), lembre-se dos seguintes requisitos de namespace de identidade:

* Ao criar destinos em tempo real (transmissão) por meio do Destination SDK, além de [configurar um esquema de parceiro](schema-configuration.md) para o qual os usuários podem mapear atributos de perfil e identidades, você também deve definir *pelo menos um* namespace de identidade com suporte na sua plataforma de destino. Por exemplo, se sua plataforma de destino aceitar emails com hash e [!DNL IDFA], você deverá definir essas duas identidades como [descritas mais adiante neste documento](#supported-parameters).

  >[!IMPORTANT]
  >
  >Ao ativar públicos para destinos de streaming, os usuários também devem mapear _pelo menos uma identidade de destino_, além dos atributos de perfil de destino. Caso contrário, os públicos-alvo não serão ativados para a plataforma de destino.

* Ao criar destinos baseados em arquivo por meio do Destination SDK, a configuração dos namespaces de identidade é _opcional_.

Para saber mais sobre namespaces de identidade na Experience Platform, consulte a [documentação de namespaces de identidade](../../../../identity-service/features/namespaces.md).

Ao configurar namespaces de identidade para seu destino, você pode ajustar o mapeamento de identidade de destino compatível com seu destino, como:

* Permitir que os usuários mapeiem atributos XDM para namespaces de identidade.
* Permitindo que os usuários mapeiem [namespaces de identidade padrão](../../../../identity-service/features/namespaces.md#standard) para seus próprios namespaces de identidade.
* Permitindo que os usuários mapeiem [namespaces de identidade personalizados](../../../../identity-service/features/namespaces.md#manage-namespaces) para seus próprios namespaces de identidade.

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama na documentação de [opções de configuração](../configuration-options.md) ou consulte o guia sobre como [usar o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Você pode configurar seus namespaces de identidade compatíveis por meio do ponto de extremidade `/authoring/destinations`. Consulte as seguintes páginas de referência de API para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Atualizar uma configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artigo descreve todas as opções de configuração de namespaces de identidade compatíveis que você pode usar para o seu destino e mostra o que os clientes verão na interface do Experience Platform.

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros com suporte do Destination SDK diferenciam maiúsculas de minúsculas **1}.** Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações suportam a funcionalidade descrita nesta página.

| Tipo de integração | Suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim (obrigatório) |
| Integrações baseadas em arquivo (lote) | Sim (opcional) |

## Parâmetros compatíveis {#supported-parameters}

Ao definir as identidades de público-alvo compatíveis com seu destino, você pode usar os parâmetros descritos na tabela abaixo para configurar seu comportamento.

| Parâmetro | Tipo | Obrigatório / Opcional | Descrição |
|---------|----------|---|------|
| `acceptsAttributes` | Booleano | Opcional | Indica se os clientes podem mapear atributos de perfil padrão para a identidade que você está configurando. |
| `acceptsCustomNamespaces` | Booleano | Opcional | Indica se os clientes podem mapear namespaces de identidade personalizados para o namespace de identidade que você está configurando. |
| `acceptedGlobalNamespaces` | - | Opcional | Indica quais [namespaces de identidade padrão](../../../../identity-service/features/namespaces.md#standard) (por exemplo, [!UICONTROL IDFA]) clientes podem mapear para a identidade que você está configurando. |
| `transformation` | String | Opcional | Exibe a caixa de seleção [[!UICONTROL Apply transformation]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) na interface do usuário do Experience Platform, quando o campo de origem é um atributo XDM ou um namespace de identidade personalizado. Use essa opção para conceder aos usuários a capacidade de aplicar hash aos atributos de origem na exportação. Para habilitar esta opção, defina o valor como `sha256(lower($))`. |
| `requiredTransformation` | String | Opcional | Quando os clientes selecionam este namespace de identidade de origem, a caixa de seleção [[!UICONTROL Apply transformation]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) é aplicada automaticamente ao mapeamento e os clientes não podem desabilitá-lo. Para habilitar esta opção, defina o valor como `sha256(lower($))`. |

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

Você deve indicar quais [!DNL Experience Platform] identidades os clientes podem exportar para o seu destino. Alguns exemplos são [!DNL Experience Cloud ID], email com hash, ID de dispositivo ([!DNL IDFA], [!DNL GAID]). Esses valores são [!DNL Experience Platform] namespaces de identidade que os clientes podem mapear para namespaces de identidade do seu destino.

Os namespaces de identidade não exigem uma correspondência de 1 para 1 entre [!DNL Experience Platform] e seu destino.
Por exemplo, os clientes podem mapear um namespace [!DNL Experience Platform] [!DNL IDFA] para um namespace [!DNL IDFA] de seu destino, ou podem mapear o mesmo namespace [!DNL Experience Platform] [!DNL IDFA] para um namespace [!DNL Customer ID] de seu destino.

Leia mais sobre identidades na [visão geral do namespace de identidade](../../../../identity-service/features/namespaces.md).

## Considerações de mapeamento

Se os clientes selecionarem um namespace de identidade de origem e não selecionarem um target mapping, o Experience Platform preencherá automaticamente o target mapping com um atributo com o mesmo nome.

## Configurar hash de campo de origem opcional

Os clientes do Experience Platform podem optar por assimilar dados na Experience Platform em formato com hash ou em texto sem formatação. Se sua plataforma de destino aceitar dados com hash e sem hash, você poderá dar aos clientes a opção de escolher se o Experience Platform deve aplicar hash aos valores dos campos de origem quando eles forem exportados para seu destino.

A configuração abaixo habilita a opção [Aplicar transformação](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) opcional na interface do usuário do Experience Platform, na etapa Mapeamento.

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

Ao mapear atributos de origem com hash não atribuídos para atributos de destino que o destino espera que tenham hash (por exemplo: `email_lc_sha256` ou `phone_sha256`), marque a opção **Aplicar transformação** para que o Adobe Experience Platform coloque os atributos de origem em hash automaticamente na ativação.

## Configurar hash de campo de origem obrigatório

Se o destino aceitar apenas dados com hash, você poderá configurar os atributos exportados para serem automaticamente transformados em hash pelo Experience Platform. A configuração abaixo verifica automaticamente a opção **Aplicar transformação** quando as identidades `Email` e `Phone` são mapeadas.

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
