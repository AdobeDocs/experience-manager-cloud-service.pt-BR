---
title: Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2022.9.0
description: Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2022.9.0
feature: Release Information
exl-id: 581370ba-e3e8-487e-af83-a1eacbda2763
source-git-commit: dd4515bdbba81dcec0868c3058c7745775cc80ff
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 10%

---

# Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2022.9.0 {#release-notes}

Esta página descreve as Notas de versão para as Ferramentas de migração AEM as a Cloud Service 2022.9.0.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.34 é 12 de setembro de 2022.

### Novidades {#what-is-new-bpa}

* O BPA agora pode detectar e relatar se o cliente adicionou uma configuração de logger personalizada. AEM as a Cloud Service não suporta arquivos de log personalizados. Todos os arquivos de log precisam ser canalizados para `error.log`
* O BPA agora pode gerar relatórios sobre os diferentes tipos MIME binários presentes no repositório do cliente e as contagens associadas a eles.

### Correções de erros {#bug-fixes-bpa}

* A interface do usuário do BPA tinha problemas de renderização ao exibir um grande número de conclusões em um único padrão. Isso foi corrigido.
* O BPA relatava incorretamente algumas descobertas como alterações não compatíveis com a gravidade crítica. Isso foi corrigido.
