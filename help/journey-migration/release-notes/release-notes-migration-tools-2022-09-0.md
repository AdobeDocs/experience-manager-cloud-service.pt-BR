---
title: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.9.0
description: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.9.0
feature: Release Information
exl-id: 581370ba-e3e8-487e-af83-a1eacbda2763
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 10%

---

# Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.9.0 {#release-notes}

Esta página descreve as Notas de versão das Ferramentas de migração no AEM as a Cloud Service 2022.9.0.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.34 é 12 de setembro de 2022.

### Novidades {#what-is-new-bpa}

* Agora, o BPA pode detectar e relatar se o cliente adicionou uma configuração de agente personalizada. O AEM as a Cloud Service não oferece suporte a arquivos de log personalizados. Todos os arquivos de log precisam ser canalizados para `error.log`
* Agora, o BPA pode relatar os diferentes tipos MIME binários presentes no repositório do cliente e as contagens associadas a eles.

### Correções de erros {#bug-fixes-bpa}

* A interface do usuário do BPA tinha problemas de renderização ao exibir um grande número de conclusões em um único padrão. Isso foi corrigido.
* O BPA relatava incorretamente algumas conclusões como alterações não compatíveis com severidade crítica. Isso foi corrigido.
