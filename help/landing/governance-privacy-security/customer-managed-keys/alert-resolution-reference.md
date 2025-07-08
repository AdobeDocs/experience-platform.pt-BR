---
title: Referência de Resolução de Alerta CMK
description: Identificar, solucionar problemas e resolver alertas comuns acionados por erros de configuração da Chave gerenciada pelo cliente (CMK) no Adobe Experience Platform. Use este guia para seguir instruções claras e passo a passo e restaurar o acesso seguro à chave.
exl-id: ffe2eadc-dfb5-418b-a201-2c20dcc9cfe4
source-git-commit: e8cfed9ebd50cf50f03e232755eddef1cb8c0d3b
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# Referência de resolução de alerta CMK

Use este guia para solucionar problemas e resolver alertas acionados por configurações incorretas de Chave gerenciada pelo cliente (CMK) no Adobe Experience Platform. Ele ajuda os administradores de sistema e especialistas em implementação a identificar causas e aplicar resoluções para restaurar o acesso seguro.

## Categorias de alerta {#categories}

As seções a seguir descrevem os tipos de alertas que podem ser acionados por problemas de Chave gerenciada pelo cliente (CMK) no Adobe Experience Platform:

- [Acesso à chave desabilitado](#key-access-disabled)
- [Falha no acesso à chave](#key-access-failure)
- [Notificação de alerta](#alert-notification)

## Acesso à chave desabilitado {#key-access-disabled}

Esse alerta indica que o Adobe Experience Platform não pode acessar o CMK configurado porque a chave está desativada ou inacessível devido à sua configuração. Nesses casos, o sistema trata a condição como uma remoção intencional da chave de acesso.

### Quando ocorre

Este alerta é disparado quando a chave de criptografia no Cofre de Chaves do Azure está em um estado desabilitado, excluído ou configurado incorretamente de uma forma que impede o acesso durante as operações da plataforma.

### Possíveis causas

Veja a seguir os motivos comuns para a ocorrência desse alerta:

- A chave foi desabilitada manualmente.
- As operações de chave (wrapKey/unwrapKey) foram removidas.
- A data de ativação da chave será definida no futuro.
- A data de expiração da chave está no passado.
- A chave foi excluída.
- As permissões do aplicativo MultiTenant foram removidas ou alteradas.
- O aplicativo MultiTenant foi excluído.
- As propriedades do Aplicativo MultiTenant foram alteradas.
- O Cofre da Chave foi excluído ou não está mais acessível.

### Resolução

+++Se a tecla estiver desativada

1. Navegue até o [Cofre de Chaves do Azure](https://portal.azure.com/) que contém o CMK.
2. Selecione a chave associada ao Adobe Experience Platform.
3. Verifique se o status da chave é **Habilitado**.
4. Se a chave estiver desabilitada, habilite-a usando o portal do Azure ou o comando da CLI `az keyvault key enable`.

>[!NOTE]
>
>Personalize este comando para o seu ambiente do Azure.

+++

+++Se as operações de chave tiverem sido alteradas

1. Adicione novamente as permissões `wrapKey` e `unwrapKey` à chave.

>[!NOTE]
>
>Todas as configurações de chave, incluindo datas de ativação e expiração, devem ser válidas para que a chave funcione.

+++

+++Se a data de ativação ou expiração estiver configurada incorretamente

1. Defina a data de ativação como passado ou presente.
2. Defina a data de expiração como uma data futura.

+++

+++Se a tecla tiver sido excluída

1. Verifique se a exclusão reversível está habilitada no Cofre de Chaves do Azure.
2. Navegue até &quot;Gerenciar chaves excluídas&quot; no portal do Azure ou na CLI.
3. Selecione a chave excluída na lista de itens excluídos por software.
4. Clique em **Recuperar** para restaurar a chave.

+++

+++Se as permissões do aplicativo MultiTenant foram removidas ou alteradas

1. Restaure as permissões corretas para o aplicativo MultiTenant.
2. Verifique se a seguinte permissão foi concedida: `Key Vault Crypto Service Encryption User`

+++

+++Se o aplicativo multilocatário foi excluído

Esta é uma mudança radical. Você deve entrar em contato com a Adobe para restaurar ou regenerar o Aplicativo MultiTenant.

+++

+++Se as configurações do Aplicativo MultiTenant foram alteradas

1. Reverta as alterações nas propriedades associadas ao Aplicativo Multilocatário.

+++

+++Se o Cofre da Chave foi excluído

1. Confirme se a exclusão reversível está habilitada no Azure.
2. Navegue até &quot;Gerenciar cofres excluídos&quot; no portal ou CLI.
3. Recupere o cofre excluído dentro do período de retenção (7 a 90 dias).
4. Se a proteção contra limpeza estiver desativada, ainda será possível recuperar o cofre.

>[!NOTE]
>
>Se a proteção de exclusão reversível ou limpeza não estiver configurada corretamente, talvez a chave ou o cofre não seja recuperável.

+++

## Falha no acesso à chave {#key-access-failure}

Esse alerta indica que o Adobe Experience Platform falhou ao acessar o CMK devido à negação de acesso no nível da rede ou baseada em configuração.

>[!IMPORTANT]
>
>Isso é tratado como um erro recuperável. Os dados **não** estão limpos no SLA neste caso.

### Quando ocorre

Normalmente, esse alerta é disparado quando o firewall do Cofre de Chaves não está configurado para permitir acesso ao Adobe CMK ou quando o acesso baseado em identidade falha.

### Possíveis causas

- O firewall do Cofre de Chaves está bloqueando o IP estático da Adobe (`20.88.123.53`)
- A chave não existe mais no local esperado
- As permissões para o aplicativo multilocatário do Adobe estão ausentes
- O Cofre de Chaves foi excluído ou configurado incorretamente
- A ID de Objeto do Aplicativo MultiTenant foi alterada

### Resolução

+++Se o Cofre da Chave ou a chave não existir mais

1. Verifique se o Cofre de Chaves e a chave de criptografia ainda existem.
2. Se a chave tiver sido excluída, siga as etapas de recuperação de exclusão reversível em &quot;Acesso à chave desativado&quot;.

+++

+++Se as permissões do Aplicativo MultiTenant estiverem ausentes ou forem alteradas

1. Confirme se o aplicativo multilocatário do Adobe tem as seguintes permissões:
   - `get`, `wrapKey` e `unwrapKey` na chave.
2. Verifique se a ID de objeto do aplicativo multilocatário está correta. Se tiver sido alterado, reaplique as permissões.

+++

+++Se o firewall estiver bloqueando o Adobe

1. Revise as regras de firewall no Cofre de Chaves do Azure.
2. Certifique-se de que eles permitam acesso do IP estático da Adobe: `20.88.123.53`.

>[!NOTE]
>
>Mesmo com as permissões corretas, um IP bloqueado impedirá o acesso à chave.

+++

## Notificação de alerta {#alert-notification}

Esse alerta serve como uma notificação geral para configuração CMK ou anomalias de acesso que não correspondem a um tipo de falha conhecido.

>[!NOTE]
>
>Este alerta pode refletir um erro interno, uma nova configuração incorreta ou uma condição inesperada.

### Quando ocorre

Este alerta é exibido quando o Adobe CMK detecta um problema desconhecido, incompatível ou novo durante o acesso à chave ou o monitoramento.

### Possíveis causas

- Condições imprevistas de firewall/rede
- Alterações de chave ou cofre não cobertas por tipos de alertas predefinidos
- Interrupções na rede interna da Adobe
- Erro de configuração que o Adobe não tinha visto antes

### Resolução

+++Se a causa for desconhecida ou ambígua

1. Revise a mensagem de alerta para obter detalhes contextuais.
2. Verifique as configurações de firewall, cofre e chave para alterações recentes.
3. Se nenhuma causa clara for encontrada, entre em contato com o suporte da Adobe para obter orientação.
4. Monitore logs e o comportamento do sistema para identificar padrões.

+++

## Próximas etapas

Para entender como os alertas são acionados e como configurar o incluir na lista de permissões de IP para o CMK [!DNL Azure], consulte o guia [Configurar alertas e a inclui na lista de permissões de IP para o CMK do Azure](./azure/alerts-and-ip-access.md).
