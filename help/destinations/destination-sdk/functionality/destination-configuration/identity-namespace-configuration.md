---
description: Saiba como configurar as identidades de destino compatíveis para destinos criados com o Destination SDK.
title: Configuração do namespace de identidade
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 4%

---


# Configuração do namespace de identidade

O Experience Platform usa namespaces de identidade para descrever o tipo de identidades específicas. Por exemplo, um namespace de identidade chamado `Email` identifica um valor como `name@email.com` como endereço de email.

Ao criar um destino por meio do Destination SDK, além de [configuração de um schema de parceiros](schema-configuration.md) para os quais os usuários podem mapear atributos e identidades de perfil, você também pode definir namespaces de identidade compatíveis com sua plataforma de destino.

Ao fazer isso, os usuários têm a opção adicional de selecionar identidades de destino, além dos atributos de perfil de direcionamento.

Para saber mais sobre os namespaces de identidade no Experience Platform, consulte o [documentação dos namespaces de identidade](../../../../identity-service/namespaces.md).

Ao configurar namespaces de identidade para o seu destino, você pode ajustar o mapeamento de identidade do destino suportado pelo seu destino, como:

* Permitir que usuários mapeiem atributos XDM para namespaces de identidade.
* Permitir mapeamento de usuários [namespaces de identidade padrão](../../../../identity-service/namespaces.md#standard) para seus próprios namespaces de identidade.
* Permitir mapeamento de usuários [namespaces de identidade personalizados](../../../../identity-service/namespaces.md#manage-namespaces) para seus próprios namespaces de identidade.

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama no [opções de configuração](../configuration-options.md) ou consulte o guia sobre como [use o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Você pode configurar seus namespaces de identidade compatíveis por meio do `/authoring/destinations` endpoint . Consulte as páginas de referência da API a seguir para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Atualizar uma configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artigo descreve todas as opções de configuração de namespaces de identidade compatíveis que podem ser usadas para o seu destino e mostra quais clientes verão na interface do usuário da plataforma.

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações oferecem suporte à funcionalidade descrita nesta página.

| Tipo de integração | Oferece suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (em lote) | Sim |

## Parâmetros compatíveis {#supported-parameters}

Ao definir as identidades de destino compatíveis com seu destino, você pode usar os parâmetros descritos na tabela abaixo para configurar seu comportamento.

| Parâmetro | Tipo | Obrigatório / Opcional | Descrição |
|---------|----------|---|------|
| `acceptsAttributes` | Booleano | Opcional | Indica se os clientes podem mapear atributos de perfil padrão para a identidade que você está configurando. |
| `acceptsCustomNamespaces` | Booleano | Opcional | Indica se os clientes podem mapear namespaces de identidade personalizados para o namespace de identidade que você está configurando. |
| `acceptedGlobalNamespaces` | - | Opcional | Indica que [namespaces de identidade padrão](../../../../identity-service/namespaces.md#standard) (por exemplo, [!UICONTROL IDFA]) os clientes podem mapear para a identidade que você está configurando. |
| `transformation` | String | Opcional | Exibe a [[!UICONTROL Aplicar transformação]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) na interface do usuário da plataforma, quando o campo de origem for um atributo XDM ou um namespace de identidade personalizado. Use essa opção para fornecer aos usuários a capacidade de fazer hash dos atributos de origem na exportação. Para ativar essa opção, defina o valor como `sha256(lower($))`. |
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

Você deve indicar qual [!DNL Platform] identidades que os clientes podem exportar para o seu destino. Alguns exemplos são [!DNL Experience Cloud ID], email com hash, ID do dispositivo ([!DNL IDFA], [!DNL GAID]). Esses valores são [!DNL Platform] namespaces de identidade que os clientes podem mapear para namespaces de identidade a partir do seu destino.

Os namespaces de identidade não exigem uma correspondência de 1 para 1 entre [!DNL Platform] e seu destino.
Por exemplo, os clientes podem mapear uma [!DNL Platform] [!DNL IDFA] namespace para um [!DNL IDFA] namespace do seu destino ou podem mapear o mesmo [!DNL Platform] [!DNL IDFA] namespace para um [!DNL Customer ID] namespace no seu destino.

Leia mais sobre identidades na [visão geral do namespace de identidade](../../../../identity-service/namespaces.md).

## Considerações de mapeamento

Se os clientes selecionarem um namespace de identidade de origem e não selecionarem um target mapping, a Platform preencherá automaticamente o target mapping com um atributo com o mesmo nome.

## Configurar o hash do campo de origem opcional

Os clientes do Experience Platform podem optar por assimilar dados na Platform em formato com hash ou em texto sem formatação. Se a plataforma de destino aceitar dados com hash e sem hash, você poderá dar aos clientes a opção de escolher se a Platform deve hash nos valores do campo de origem quando eles forem exportados para seu destino.

A configuração abaixo ativa o [Aplicar transformação](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) na interface do usuário da plataforma, na etapa Mapeamento .

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

Quando você está mapeando atributos de origem sem hash para atributos de destino que o destino espera ter hash (por exemplo: `email_lc_sha256` ou `phone_sha256`), marque a opção **Aplicar transformação** para que o Adobe Experience Platform faça o hash automático dos atributos de origem na ativação.

## Configurar o hash do campo de origem obrigatório

Se o destino aceitar apenas dados com hash, você poderá configurar os atributos exportados para serem automaticamente atribuídos a hash pela Platform. A configuração abaixo verifica automaticamente o **Aplicar transformação** quando a variável `Email` e `Phone` identidades são mapeadas.

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

Após ler este artigo, você deve ter uma melhor compreensão de como configurar seus namespaces de identidade para destinos criados com o Destination SDK.

Para saber mais sobre os outros componentes de destino, consulte os seguintes artigos:

* [Autenticação do cliente](customer-authentication.md)
* [Autenticação OAuth2](oauth2-authentication.md)
* [Campos de dados do cliente](customer-data-fields.md)
* [Atributos da interface do usuário](ui-attributes.md)
* [Configuração do esquema](schema-configuration.md)
* [Configuração do namespace de identidade](identity-namespace-configuration.md)
* [Configurações de mapeamento suportadas](supported-mapping-configurations.md)
* [Delivery de destino](destination-delivery.md)
* [Configuração de metadados de público-alvo](audience-metadata-configuration.md)
* [Política de agregação](aggregation-policy.md)
* [Configuração em lote](batch-configuration.md)
* [Qualificações de perfil histórico](historical-profile-qualifications.md)
