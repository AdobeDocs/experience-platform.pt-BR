---
title: Migrar de JWT para credenciais de servidor para servidor do OAuth
description: Saiba como migrar credenciais JWT sem expiração para credenciais OAuth de servidor para servidor no Adobe Experience Platform para manter o acesso seguro e ininterrupto ao Serviço de consulta antes que o suporte ao JWT termine em 30 de junho de 2025. Este guia fornece instruções passo a passo, explica o comportamento após a migração e responde perguntas comuns.
source-git-commit: 264d3b12d8fd3bd100018513af1576b3de1cbb33
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 1%

---

# Migrar do JWT para credenciais de servidor para servidor do OAuth

>[!IMPORTANT]
>
>A Adobe está descontinuando o suporte para credenciais de Conta de Serviço (JWT) usadas pelo Serviço de consulta. Depois de 30 de junho de 2025, as credenciais sem expiração baseadas em JWT não atualizarão mais ou autenticarão solicitações de API. Para evitar interrupções do serviço, migre cada credencial qualificada para a autenticação de servidor para servidor OAuth.

Este guia mostra como migrar credenciais JWT sem expiração para credenciais de servidor para servidor OAuth no Adobe Experience Platform. A conclusão desse processo garante o acesso ininterrupto ao Serviço de consulta antes que o suporte às credenciais JWT termine em 30 de junho de 2025.

Este documento fornece instruções passo a passo para executar a migração, entender o impacto e verificar suas credenciais atualizadas.

## Quem precisa migrar {#who-needs-to-migrate}

Se você usar credenciais sem expiração no Serviço de consulta, migre cada uma delas. Isso se aplica às credenciais usadas em fluxos de trabalho automatizados, consultas agendadas ou integrações de API personalizadas.

Se você vir credenciais listadas na seção **[!UICONTROL Credenciais sem expiração]** da guia **[!UICONTROL Credenciais]**, essas credenciais serão afetadas.

## Como migrar uma credencial {#how-to-migrate}

Você pode migrar credenciais diretamente na interface do usuário do Experience Platform. Para fazer isso, navegue até **[!UICONTROL Consultas]** na navegação à esquerda e selecione a guia **[!UICONTROL Credenciais]**. Na seção **[!UICONTROL Credenciais sem expiração]**, identifique uma credencial marcada como qualificada para migração e selecione **[!UICONTROL Migrar]** ao lado dela.

>[!NOTE]
>
>A migração leva de 8 a 10 segundos e não pode ser cancelada depois de iniciada.

![O espaço de trabalho de Credenciais do Serviço de Consulta com Consultas, Credenciais e Migração foi realçado.](../images/ui/migrate-jwt-to-oauth/migrate.png)

Após a migração, o sistema atualiza a credencial para usar a autenticação de servidor para servidor do OAuth. O método baseado em JWT é removido automaticamente, e o status é atualizado para **[!UICONTROL Migrado]**.

Nenhuma reconfiguração é necessária. As tarefas e integrações existentes continuam a funcionar sem interrupção.

## O que acontece após a migração {#after-migration}

Após concluir a migração:

- Suas credenciais continuam a funcionar perfeitamente, de modo que não são necessárias alterações em seus trabalhos ou integrações.
- O Serviço de consulta usa automaticamente a autenticação de servidor para servidor OAuth.
- O método de autenticação baseado em JWT foi removido e não está mais em uso.

>[!IMPORTANT]
>
>Não é possível desfazer essa alteração. Depois de migrada, a credencial não pode ser revertida para JWT.

## Perguntas frequentes {#faq}

Essas perguntas abordam preocupações comuns e ajudam a garantir uma migração tranquila e sem interrupções.

### Por que a Adobe está substituindo as credenciais JWT?

O OAuth Server-to-Server é um método de autenticação mais seguro e padronizado. Ele oferece melhor gerenciamento do ciclo de vida e oferece suporte a uma consistência mais ampla da plataforma.

### O que acontece se eu não migrar até 30 de junho de 2025?

As credenciais JWT interromperão a atualização e as integrações que dependem delas falharão. O Adobe não pode migrar credenciais em seu nome, a menos que você inicie o processo.

### Como saberei se preciso migrar?

Se uma credencial for exibida na seção **[!UICONTROL Credenciais sem expiração]** da guia Credenciais, essas credenciais deverão ser migradas.

### Preciso atualizar minhas integrações ou reconfigurar algo?

Não. Após a migração, a credencial OAuth assume o controle automaticamente. Não são necessárias alterações manuais em suas tarefas ou integrações.

### Posso migrar todas as credenciais de uma só vez?

Não. Você deve migrar cada credencial individualmente usando o botão **[!UICONTROL Migrar]**.

### Posso continuar usando credenciais que estão expirando?

Sim. Credenciais que expiram não são afetadas por essa alteração. Somente credenciais JWT sem expiração devem ser migradas.

### Vejo uma mensagem dizendo &quot;[!UICONTROL Nenhuma credencial sem expiração encontrada.]&quot; O que isso significa? Preciso realizar alguma ação?

Esta mensagem significa que você ainda não criou credenciais sem expiração, portanto, não há nada que você precise fazer.

### Vejo uma mensagem dizendo &quot;[!UICONTROL falha na verificação do administrador do AEP]...&quot; O que isso significa? Preciso realizar alguma ação?

Esta mensagem indica que você não é um Administrador ou não tem as permissões necessárias para criar credenciais sem expiração.

- Se suas permissões não foram alteradas recentemente, significa que você nunca teve acesso para criar credenciais, portanto, nenhuma ação é necessária.
- Se suas permissões foram alteradas recentemente, entre em contato com o administrador da organização e solicite a migração das credenciais para você.

### Posso migrar credenciais sem expiração para outra pessoa?

Sim, mas somente se você for um administrador. Somente os administradores têm as permissões necessárias para criar e migrar credenciais sem expiração para outros usuários, para que possam continuar trabalhando sem interrupções.

## Próximas etapas {#next-steps}

Revise cada credencial sem expiração na guia [!UICONTROL Credenciais] e migre-a individualmente antes de 30 de junho de 2025. Se tiver dúvidas ou tiver suporte, entre em contato com o representante de conta da Adobe.
