---
title: Introdução aos programas de sandbox
description: Saiba quais programas de sandbox são diferentes dos programas de produção.
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: 05cba12cdd14c2e29f6a471047ce95fcf720abc4
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 2%

---


# Introdução aos programas de sandbox {#sandbox-programs}

Saiba quais programas de sandbox são diferentes dos programas de produção.

## Introdução {#introduction}

Geralmente, um programa de sandbox é criado para servir aos propósitos de treinamento, execução de demonstrações, ativação ou prova de conceitos (POCs) e, portanto, não é destinado a transportar tráfego ao vivo.

Um programa de sandbox é um dos dois tipos de programas disponíveis no AEM Cloud Service, sendo o outro um [programa de produção.](introduction-production-programs.md) Consulte o documento [Noções básicas sobre programas e tipos de programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) para saber mais sobre tipos de programas.

## Criação automática {#auto-creation}

Os programas de sandbox apresentam criação automática. Sempre que você cria um novo programa de sandbox, o Cloud Manager automaticamente:

* Adiciona AEM Sites e AEM Assets como soluções em seu programa.
* Configura um repositório Git de projeto com um projeto de amostra baseado no [AEM Arquétipo de projeto.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt_BR)
* Cria um ambiente de desenvolvimento.
* Cria um pipeline de não produção que é implantado no ambiente de desenvolvimento.

Um programa de sandbox terá apenas um ambiente de desenvolvimento.

## Limitações e condições {#limitations}

Como não se destinam ao tráfego ao vivo, os programas sandbox têm determinadas limitações e condições de uso, que os diferenciam dos programas de produção.

### Sem tráfego ao vivo {#live-traffic}

Os programas de sandbox não se destinam a transportar tráfego ao vivo e, por conseguinte, não estão sujeitos [AEM compromissos as a Cloud Service.](https://www.adobe.com/legal/service-commitments.html)

### Sem dimensionamento automático {#auto-scaling}

Os ambientes criados em um programa sandbox não são configurados para dimensionamento automático. Portanto, esses ambientes não são adequados para teste de desempenho ou carga.

### Nenhum domínio personalizado ou Listas de permissões de IP {#ip-allow}

Domínios personalizados e listas de permissões IP não estão disponíveis em programas sandbox.

### Sem rede avançada {#advanced-networking}

[Recursos avançados de rede](/help/security/configuring-advanced-networking.md) (por exemplo, provisionamento de autoatendimento de VPN, portas não padrão, endereços IP de saída dedicados, etc.) não estão disponíveis em programas sandbox.

### Atualizações Manuais de AEM {#updates}

AEM atualizações não são automaticamente enviadas para programas sandbox, mas podem ser aplicadas manualmente aos ambientes em seu programa sandbox.

* Uma atualização manual só pode ser executada quando o ambiente de destino tiver um pipeline configurado corretamente.
* Uma atualização manual para um ambiente de produção ou de preparo atualizará automaticamente o outro. O conjunto de ambientes Production+Stage deve estar na mesma versão de AEM.

Consulte o documento [Atualizações da versão de AEM](/help/implementing/deploying/aem-version-updates.md) para obter mais detalhes.

Consulte o documento [Atualização do ambiente](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment) para saber como atualizar um ambiente.

### Hibernação e exclusão {#hibernation}

Os ambientes em um programa sandbox hibernam automaticamente após 8 horas de inatividade. Uma vez hibernados, eles podem ser removidos da hibernação manualmente.

Os programas de sandbox são excluídos depois de 6 meses em modo de hibernação contínua, e depois disso podem ser recriados.

Consulte [Hibernar e desibernar ambientes de sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md) para obter mais detalhes.
