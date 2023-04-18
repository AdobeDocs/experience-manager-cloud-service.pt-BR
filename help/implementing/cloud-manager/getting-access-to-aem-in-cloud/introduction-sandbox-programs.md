---
title: Introdução aos programas de sandbox
description: Saiba o que são programas de sandbox e como se diferem dos programas de produção.
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: 18c5d2ba77a97413d0d83235ad2baec9fe4b0238
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 88%

---


# Introdução aos programas de sandbox {#sandbox-programs}

Saiba o que são programas de sandbox e como se diferem dos programas de produção.

## Introdução {#introduction}

Um programa de sandbox é normalmente criado para fins de treinamento, execução de demonstrações, capacitação, provas de conceito (POCs) ou documentação e não se destina a transportar tráfego direto.

Um programa de sandbox é um dos dois tipos de programas disponíveis no AEM Cloud Service, sendo o outro um [programa de produção.](introduction-production-programs.md) Consulte o documento [Noções básicas sobre programas e tipos de programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) para saber mais sobre tipos de programas.

## Criação automática {#auto-creation}

Os programas de sandbox incluem criação automática. Sempre que você cria um novo programa de sandbox, automaticamente o Cloud Manager:

* Adiciona o AEM Sites e o AEM Assets como soluções em seu programa.
* Configura um repositório Git de projeto com um projeto de amostra baseado no [Arquétipo de projetos AEM.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR)
* Cria um ambiente de desenvolvimento.
* Cria um pipeline de não produção que é implantado no ambiente de desenvolvimento.

Um programa de sandbox terá apenas um ambiente de desenvolvimento.

## Limitações e condições {#limitations}

Como não se destinam ao tráfego direto, os programas de sandbox têm determinadas limitações e condições de uso que os diferenciam dos programas de produção.

### Sem tráfego direto {#live-traffic}

Os programas de sandbox não se destinam a transportar tráfego direto e, por conseguinte, não estão sujeitos aos [compromissos do AEM as a Cloud Service.](https://www.adobe.com/pt/legal/service-commitments.html)

### Sem dimensionamento automático {#auto-scaling}

Os ambientes criados em um programa de sandbox não estão configurados para dimensionamento automático. Portanto, esses ambientes não são adequados para testes de desempenho ou carga.

### Sem domínios personalizados ou listas de permissões de IP {#ip-allow}

Domínios personalizados e listas de permissões IP não estão disponíveis em programas de sandbox.

### Sem rede avançada {#advanced-networking}

[Recursos avançados de rede](/help/security/configuring-advanced-networking.md) (por exemplo, provisionamento de VPNs via autoatendimento, portas não padrão, endereços IP de saída dedicados etc.) não estão disponíveis em programas de sandbox.

### Atualizações manuais do AEM {#updates}

As atualizações do AEM não são enviadas automaticamente para programas de sandbox, mas podem ser aplicadas manualmente aos ambientes em seu programa de sandbox.

* Uma atualização manual somente pode ser executada quando o ambiente de destino tem um pipeline configurado corretamente.
* Uma atualização manual em um ambiente de produção ou de preparo atualizará automaticamente o outro. O conjunto de ambientes de Produção+Preparo deve ter a mesma versão do AEM.

Consulte o documento [Atualizações de versão do AEM](/help/implementing/deploying/aem-version-updates.md) para obter mais detalhes.

Consulte o documento [Atualização do ambiente](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment) para saber como atualizar um ambiente.

### Hibernação e exclusão {#hibernation}

Os ambientes em um programa de sandbox hibernam automaticamente após 8 horas de inatividade. Uma vez
hibernados, eles podem ter sua hibernação cancelada manualmente.

Os programas de sandbox são excluídos após seis meses em modo de hibernação contínua, depois disso, podem ser recriados.

Consulte [Hibernação e cancelamento da hibernação de ambientes de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md) para obter mais detalhes.

### Sem suporte técnico {#no-support}

Como um programa de sandbox é normalmente criado para servir aos propósitos de treinamento, execução de demonstrações, ativação ou prova de conceitos (POCs), o suporte técnico não está disponível para problemas enfrentados em um programa de sandbox.

Se tiver problemas ao criar e gerenciar os programas do sandbox, isso ainda estará dentro do escopo do suporte técnico.
