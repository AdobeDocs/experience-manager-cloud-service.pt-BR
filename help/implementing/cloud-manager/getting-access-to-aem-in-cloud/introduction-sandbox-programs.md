---
title: Introdução aos programas de sandbox
description: Saiba o que são programas de sandbox e como eles se diferem dos programas de produção.
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 32%

---


# Introdução a programas de sandbox {#sandbox-programs}

Saiba o que são programas de sandbox e como eles se diferem dos programas de produção.

## Introdução {#introduction}

Um programa de sandbox é normalmente criado para fins de treinamento, execução de demonstrações, capacitação, provas de conceito (POCs) ou documentação e não se destina a transportar tráfego direto.

Um programa de sandbox é um dos dois tipos de programas disponíveis no AEM Cloud Service, sendo o outro um [programa de produção](introduction-production-programs.md). Consulte [Noções Básicas sobre Programas e Tipos de Programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) para saber mais sobre tipos de programas.

## Criação automática {#auto-creation}

Os programas de sandbox incluem criação automática. Sempre que você [cria um programa de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md), o Cloud Manager automaticamente:

* Adiciona o AEM Sites, o Assets e o Edge Delivery Services como soluções padrão ao seu programa.

  ![Selecionar soluções e complementos para uma sandbox](assets/sandbox-solutions-add-ons.png)

* Configura um repositório Git de projeto com um projeto de amostra baseado no [Arquétipo de Projetos AEM](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/developing/archetype/overview).
* Cria um ambiente de desenvolvimento.
* Cria um pipeline de não produção que é implantado no ambiente de desenvolvimento.

Um programa de sandbox tem apenas um ambiente de desenvolvimento.

## Notas e condições de uso {#usage-notes-conditions}

Como não se destinam ao tráfego direto, os programas de sandbox têm determinadas limitações e condições de uso que os diferenciam dos programas de produção.

| Limitação/condição | Descrição |
| --- | --- |
| Sem tráfego direto | Os programas de sandbox não se destinam a transportar tráfego direto e, portanto, não estão sujeitos aos [Compromissos da AEM as a Cloud Service](https://www.adobe.com/pt/legal/service-commitments.html). |
| Sem dimensionamento automático | Os ambientes criados em um programa de sandbox não estão configurados para dimensionamento automático. Portanto, esses ambientes não são adequados para testes de desempenho ou carga. |
| Não há domínios personalizados nem Listas de permissões IP | [Domínios personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md) e [Listas de permissões IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) não estão disponíveis em programas de sandbox. |
| Nenhuma região de publicação adicional | [Regiões de publicação adicionais](/help/operations/additional-publish-regions.md) não estão disponíveis em programas de sandbox. |
| Sem SLA de 99,99% | O [99.99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla) não se aplica a programas de sandbox. |
| Sem rede avançada | [Recursos avançados de rede](/help/security/configuring-advanced-networking.md) (por exemplo, provisionamento de VPNs por autoatendimento, portas não padrão, endereços IP de saída dedicados e assim por diante) não estão disponíveis em programas de sandbox. |
| Nenhuma atualização automática do AEM | As atualizações do AEM não são enviadas automaticamente para programas de sandbox, mas podem ser aplicadas manualmente aos ambientes em seu programa de sandbox.<br>· Uma atualização manual só pode ser executada quando o ambiente de destino tem um pipeline configurado corretamente.<br>· Uma atualização manual em um ambiente de produção ou de preparo atualiza automaticamente o outro. O conjunto de ambientes de Produção+Preparo deve ter a mesma versão do AEM.<br>Consulte [atualizações de versão do AEM](/help/implementing/deploying/aem-version-updates.md) para obter mais detalhes.<br>Consulte [Atualizando o Ambiente](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment) para saber como atualizar um ambiente. |
| Sem suporte técnico | Como um programa de sandbox é normalmente criado para fins de treinamento, execução de demonstrações, capacitação ou POCs (prova de conceitos), o suporte técnico não está disponível para problemas enfrentados em um programa de sandbox.<br>Se tiver problemas ao criar e gerenciar seus programas de sandbox, esses problemas estarão dentro do escopo do suporte técnico. |
| Hibernação e exclusão | Os ambientes em um programa de sandbox são hibernados automaticamente após oito horas de inatividade. Os ambientes de sandbox são excluídos após seis meses contínuos de hibernação.<br>Consulte [Hibernação e cancelamento da hibernação de ambientes de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md) para obter mais detalhes sobre como cancelar a hibernação de ambientes e a exclusão automática da sandbox. |
