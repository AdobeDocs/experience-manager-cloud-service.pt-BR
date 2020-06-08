---
title: Manutenção de um conector do AEM
description: Manutenção de um conector do AEM
translation-type: tm+mt
source-git-commit: 629de3a9f55d2e4c52ef91c9e0bb5d439aebe84f
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 20%

---


Manutenção de um conector do AEM
============================

Este artigo contém informações sobre como manter um Conector do AEM e deve ser lido em conjunto com artigos sobre como [implementar](implement.md) e [enviar](submit.md) conectores.

Mesmo após o envio inicial, pode haver motivos para que um parceiro atualize seu AEM Connector, devido a uma nova versão do AEM ou independentemente disso - por exemplo, para adicionar recursos ou corrigir bugs. Este artigo descreve o processo para ambos os cenários e também descreve o processo típico de um cliente para validar conectores ao atualizar o AEM.

Os aplicativos AEM como serviço de nuvem são atualizados com patches de manutenção do AEM diariamente, com grandes alterações ativadas mensalmente durante uma versão de recurso. Embora as atualizações do AEM sejam compatíveis com versões anteriores e, portanto, não quebrem aplicativos, os parceiros do fornecedor são aconselhados a validar regularmente se seus conectores se comportam como esperariam. O acesso a um programa/ambiente AEM será determinado pela equipe do parceiro.