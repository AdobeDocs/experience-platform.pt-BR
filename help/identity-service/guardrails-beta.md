---
title: Medidas de proteção do Serviço de identidade (com lógica de exclusão)
description: Saiba mais sobre as medidas de proteção do Serviço de identidade.
hide: true
hidefromtoc: true
source-git-commit: db8edbbc3ea5d8fcec3de95b9a37387bea493693
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 2%

---

# Medidas de proteção para [!DNL Identity Service] dados (com lógica de exclusão)

Este documento fornece informações sobre limites de uso e taxa para [!DNL Identity Service] dados para ajudá-lo a otimizar o uso do gráfico de identidade. Ao revisar as medidas de proteção a seguir, presume-se que você tenha modelado os dados corretamente. Em caso de dúvidas sobre como modelar os dados, entre em contato com o representante do Atendimento ao cliente.

## Introdução

Os seguintes serviços Experience Platform estão envolvidos na modelagem de dados de identidade:

* [Identidades](home.md): identidades de ponte de fontes de dados diferentes, à medida que são assimiladas na Platform.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): crie perfis de consumidores unificados usando dados de várias fontes.

## Limites do modelo de dados

As tabelas abaixo fornecem orientação sobre medidas de proteção para limites estáticos, bem como regras de validação a serem consideradas para namespaces de identidade.

### Limites estáticos

A tabela a seguir descreve os limites estáticos aplicados aos dados de identidade.

| Grade de Proteção | Limite | Notas |
| --- | --- | --- |
| Número de identidades em um gráfico [!BADGE Beta]{type=Informative} | 50 | Quando um gráfico com 50 identidades vinculadas é atualizado, o Serviço de identidade aplica um mecanismo &quot;primeiro a entrar, primeiro a sair&quot; e exclui a identidade mais antiga para abrir espaço para a identidade mais recente. A exclusão se baseia no tipo de identidade e no carimbo de data e hora. O limite é aplicado no nível da sandbox. Leia o [apêndice](#appendix) para obter mais informações sobre como o Serviço de identidade exclui identidades quando o limite é atingido. |
| Número de identidades em um registro XDM | 20 | O número mínimo de registros XDM necessários é dois. |
| Número de namespaces personalizados | None | Não há limites para o número de namespaces personalizados que você pode criar. |
| Número de gráficos | None | Não há limites para o número de gráficos de identidade que podem ser criados. |
| Número de caracteres para um nome para exibição de namespace ou símbolo de identidade | None | Não há limites para o número de caracteres de um nome para exibição de namespace ou símbolo de identidade. |

### Validação do valor de identidade

A tabela a seguir descreve as regras existentes que devem ser seguidas para garantir uma validação bem-sucedida do valor de identidade.

| Namespace | Regra de validação | Comportamento do sistema quando a regra é violada |
| --- | --- | --- |
| ECID | <ul><li>O valor de identidade de uma ECID deve ter exatamente 38 caracteres.</li><li>O valor de identidade de uma ECID deve consistir apenas em números.</li></ul> | <ul><li>Se o valor de identidade da ECID não tiver exatamente 38 caracteres, o registro será ignorado.</li><li>Se o valor de identidade da ECID contiver caracteres não numéricos, o registro será ignorado.</li></ul> |
| Não ECID | O valor de identidade não pode exceder 1024 caracteres. | Se o valor de identidade exceder 1024 caracteres, o registro será ignorado. |

### Assimilação do namespace de identidade

A partir de 31 de março de 2023, o Serviço de identidade bloqueará a assimilação da Adobe Analytics ID (AAID) para novos clientes. Normalmente, essa identidade é assimilada por meio do [Origem do Adobe Analytics](../sources/connectors/adobe-applications/analytics.md) e a variável [Origem do Adobe Audience Manager](../sources//connectors/adobe-applications/audience-manager.md) e é redundante porque a ECID representa o mesmo navegador da Web. Se quiser alterar essa configuração padrão, entre em contato com a equipe de conta do Adobe.

## Próximas etapas

Consulte a documentação a seguir para obter mais informações sobre [!DNL Identity Service]:

* [Visão geral do [!DNL Identity Service]](home.md)
* [Visualizador de gráficos de identidade](ui/identity-graph-viewer.md)

## Apêndice {#appendix}

A seção a seguir contém informações adicionais sobre as medidas de proteção do Serviço de identidade.

### [!BADGE Beta]{type=Informative} Noções básicas sobre a lógica de exclusão quando um gráfico de identidade na capacidade é atualizado {#deletion-logic}

Quando um gráfico de identidade completo é atualizado, o Serviço de identidade exclui a identidade mais antiga no gráfico antes de adicionar a identidade mais recente. Isso é para manter a precisão e a relevância dos dados de identidade. Esse processo de exclusão segue duas regras principais:

#### A exclusão da regra #1 é priorizada com base no tipo de identidade de um namespace

A prioridade de exclusão é a seguinte:

1. ID de cookies
2. ID do dispositivo
3. ID entre dispositivos, email e telefone

#### A exclusão da regra #2 é baseada no carimbo de data e hora armazenado na identidade

Cada identidade vinculada em um gráfico tem seu próprio carimbo de data e hora correspondente. Quando um gráfico completo é atualizado, o Serviço de identidade exclui a identidade com o carimbo de data e hora mais antigo.

Quando um gráfico completo é atualizado com uma nova identidade, essas duas regras funcionam em conjunto para designar qual identidade mais antiga será excluída. O Serviço de identidade exclui primeiro a ID de cookie mais antiga, em seguida a ID de dispositivo mais antiga e, por fim, a ID/email/telefone entre dispositivos mais antiga.

>[!NOTE]
>
>Se a identidade designada para ser excluída estiver vinculada a várias outras identidades no gráfico, os links que conectam essa identidade também serão excluídos.

No exemplo abaixo, antes que o gráfico à esquerda possa ser atualizado com uma nova identidade, o Serviço de identidade deve primeiro excluir a identidade existente com o carimbo de data e hora mais antigo. No entanto, como a identidade mais antiga é uma ID de dispositivo, o Serviço de identidade ignora essa identidade até que chegue ao namespace com um tipo que esteja mais alto na lista de prioridade de exclusão, que nesse caso é `ecid-3`. Depois que a identidade mais antiga com um tipo de prioridade de exclusão mais alta é removida, o gráfico é atualizado com um novo link, `ecid-51`.

>[!NOTE]
>
>No raro caso de haver duas identidades com o mesmo carimbo de data e hora e tipo de identidade, o Serviço de identidade classificará as IDs com base no XID e realizará a exclusão.

![Um exemplo da identidade mais antiga sendo excluída para acomodar a identidade mais recente](./images/graph-limits-v3.png)