---
title: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2021.7.0
description: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2021.7.0
feature: Informações da versão
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: 673ac234f0e9bfc0f5e6878abf5d01d38cbe918f
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 4%

---

# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2021.6.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.7.0.

>[!NOTE]
>Para ver as Notas de versão atuais do Adobe Experience Manager como um Cloud Service, clique [aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=pt-BR).

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.7.0 é 15 de julho de 2021.
A próxima versão está planejada para 12 de agosto de 2021.

### Novidades {#what-is-new}

* Os clientes agora podem usar os JDKs do Azul 8 e 11 para seus processos de build do Cloud Manager e podem optar por usar um desses JDKs para plug-ins Maven compatíveis com cadeias de ferramentas *ou* em toda a execução do processo Maven.

* O IP de saída agora será registrado no arquivo de log da etapa de compilação.

* Ambientes de Preparo e Produção que executam versões antigas de AEM agora relatarão um status de &quot;Atualização disponível&quot;.

* O número máximo de certificados SSL suportados aumentou para 20 por programa.

* Aumentar O número máximo de domínios que podem ser configurados aumentou para 500 por ambiente.

* Os botões Gerenciar Git foram intitulados Informações do Git de Acesso e a caixa de diálogo foi atualizada visualmente.

### Correções de erros {#bug-fixes}

* Em algumas situações, a Visualização não era uma opção disponível ao vincular uma Lista de permissões IP a um ambiente.

* Navegar manualmente para a página de detalhes da execução de uma execução não existente não exibia um erro, apenas uma tela de carregamento infinita.

* A mensagem de erro exibida quando o número máximo de certificados SSL foi atingido não foi útil.

* Em algumas circunstâncias, pode haver uma discrepância na versão exibida no cartão do pipeline na página de visão geral.

* O assistente de adição de programa declarou incorretamente que o nome não pode ser alterado após a criação.

* Em algumas situações, a Visualização não era uma opção disponível ao vincular uma Lista de permissões IP a um ambiente.

### Problemas conhecidos {#known-issues}

Os clientes que alternam para usar os JDKs do Azul devem estar cientes de que nem todos os aplicativos existentes serão compilados sem erro no JDK do Azul. É altamente recomendável testar localmente antes de trocar.

