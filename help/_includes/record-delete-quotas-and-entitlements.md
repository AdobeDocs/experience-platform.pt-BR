---
source-git-commit: 1ab56cf2495238385d726277f6409d2e0c0cb017
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 3%

---
# Trechos

## Cotas e cronogramas de processamento {#quotas}

As solicitações de exclusão de registros estão sujeitas a limites diários e mensais de envio de identificadores, determinados pelo direito de licença da organização. Esses limites se aplicam às solicitações de exclusão baseadas em interface e API.

>[!NOTE]
>
>Você pode enviar até **1.000.000 identificadores por dia**, mas somente se sua cota mensal restante permitir. Se o limite mensal for inferior a 1 milhão, os envios diários não poderão exceder esse limite.

### Direito de envio mensal por produto {#quota-limits}

A tabela abaixo descreve os limites de envio de identificadores por produto e nível de direito. Para cada produto, o limite mensal é o menor de dois valores: um limite de identificador fixo ou um limite baseado em porcentagem vinculado ao volume de dados licenciado.

| Produto | Descrição do Direito | Limite mensal (o que for menor) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP ou Adobe Journey Optimizer | Sem o Privacy and Security Shield ou o complemento Healthcare Shield | 2.000.000 identificadores ou 5% do público endereçável |
| Real-Time CDP ou Adobe Journey Optimizer | Com o Privacy and Security Shield ou o complemento Healthcare Shield | 15.000.000 identificadores ou 10% do público endereçável |
| Customer Journey Analytics | Sem o Privacy and Security Shield ou o complemento Healthcare Shield | 2.000.000 identificadores ou 100 identificadores por milhão de linhas de direito do CJA |
| Customer Journey Analytics | Com o Privacy and Security Shield ou o complemento Healthcare Shield | 15.000.000 identificadores ou 200 identificadores por milhão de linhas de direito do CJA |

>[!NOTE]
>
> A maioria das organizações terá limites mensais mais baixos com base no público-alvo endereçável real ou nos direitos de linha do CJA.

As cotas são redefinidas no primeiro dia de cada mês. Cota não utilizada **não** é transferida.

>[!NOTE]
>
>As cotas são baseadas no direito mensal licenciado de sua organização para **identificadores enviados**. Esses procedimentos não são aplicados pelas medidas de proteção do sistema, mas podem ser monitorados e revisados.
>
>A Exclusão de Registro é um **serviço compartilhado**. Seu limite mensal reflete os direitos mais altos no Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics e em qualquer complemento do Shield aplicável.

### Processamento de cronogramas para envios de identificadores {#sla-processing-timelines}

Após o envio, as solicitações de exclusão de registro são enfileiradas e processadas com base no seu nível de direito.

| Descrição do produto e dos direitos | Duração da Fila | Tempo máximo de processamento (SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| Sem o Privacy and Security Shield ou o complemento Healthcare Shield | Até 15 dias | 30 dias |
| Com o Privacy and Security Shield ou o complemento Healthcare Shield | Normalmente, 24 horas | 15 dias |

Se sua organização exigir limites mais altos, entre em contato com o representante da Adobe para obter uma revisão de direito.
