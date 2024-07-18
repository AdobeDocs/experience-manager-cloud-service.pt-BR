---
title: Regiões de publicação adicionais
description: Saiba como o AEM as a Cloud Service permite regiões de publicação adicionais para aumentar a disponibilidade e reduzir a latência.
exl-id: b9ac3c6a-eb8b-461d-8f1d-a0356046a3f9
feature: Operations
role: Admin
source-git-commit: c7362a77fd929d812db3cd40bf01763ed3bef02c
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 71%

---


# Regiões de publicação adicionais {#additional-publish-regions}

É possível licenciar e habilitar regiões de publicação adicionais em programas configurados com o AEM Sites. Uma vez configuradas, o tráfego nos ambientes de preparo e produção é roteado para vários farms de publicação, o que oferece as seguintes vantagens:

* Latência reduzida: as solicitações que partem da CDN para as instâncias de publicação do AEM são direcionadas para a região de publicação mais próxima, o que é vantajoso para sites e aplicativos visitados por pessoas em várias regiões geográficas.
* Maior disponibilidade: se uma região não estiver disponível, a CDN direciona o tráfego para as outras regiões disponíveis.

As organizações podem licenciar até três regiões de publicação adicionais.

>[!NOTE]
>
>* Esse recurso está disponível para as soluções Sites e Forms.
>* Este recurso não pode ser aplicado a [programas de sandbox.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)
>* Este recurso requer que seu programa seja atualizado para AEM versão 12142 ou superior.

## Casos de uso {#use-cases}

Veja a seguir alguns casos de uso em que as organizações podem se beneficiar do licenciamento de regiões de publicação adicionais.

1. Para organizações que recebem tráfego significativo ou fundamental de visitantes distantes da região principal, as regiões de publicação adicionais podem reduzir a latência para esses visitantes.
1. Para organizações que podem sofrer danos financeiros ou reputacionais significativos pela indisponibilidade de um site, é possível mitigar esses riscos usando regiões de publicação adicionais para tornar o nível de publicação do AEM mais resistente a falhas regionais.
1. Para organizações cujos autores de conteúdo estão numa localização geográfica distante da maioria dos visitantes do nível de publicação, a região principal escolhida pode estar próxima à localização dos autores de conteúdo, enquanto as regiões de publicação adicionais podem ser configuradas para uma localização próxima ao tráfego do lado da publicação, para que ambos os públicos se beneficiem de uma experiência otimizada.

## Habilitar e configurar {#enabling-and-configuring}

Depois de licenciar uma região de publicação adicional, as regiões são configuradas usando o Cloud Manager. Consulte a [Documentação do Cloud Manager](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) para obter instruções detalhadas.

Regiões de publicação adicionais são aplicadas a ambientes de preparo e produção, mas não a ambientes de RDE ou desenvolvimento.

Caso uma região se torne indisponível, os clientes não precisarão gerenciar o roteamento de tráfego para regiões disponíveis, pois ele é gerenciado pela CDN do Adobe.

Conforme descrito abaixo na seção Considerações avançadas sobre rede, é recomendável que os clientes que usam rede avançada a configurem para cada região de publicação adicional para que a disponibilidade seja mantida se uma região ficar indisponível.


## Considerações sobre redes avançadas {#advanced-networking-considerations}

Quando uma região de publicação adicional é habilitada em um programa com uma rede avançada já configurada, o tráfego na região de publicação adicional que corresponde às regras de redes avançadas será roteado por padrão pela região principal. Para aproveitar o aumento da disponibilidade, é recomendável habilitar a rede avançada nas regiões adicionais.

Consulte a seção [Configuração de rede avançada para regiões de publicação adicionais](/help/security/configuring-advanced-networking.md#advanced-networking-configuration-for-additional-publish-regions) na documentação de Redes avançadas para obter mais detalhes, incluindo como adicionar configurações de rede avançada a regiões adicionais sem incorrer em perda de conectividade.

## Logs {#logging}

Se regiões de publicação adicionais estiverem ativadas, logs separados para cada região serão disponibilizados por meio do Cloud Manager. Para obter mais informações, consulte [Acesso e gerenciamento de logs](/help/implementing/cloud-manager/manage-logs.md) e [Logs para regiões adicionais do Publish](/help/implementing/developing/introduction/logging.md#logs-for-additional-publish-regions).

## Limitações {#limitations}

Lembre-se das limitações a seguir ao considerar o uso de regiões de publicação adicionais.

* Regiões de publicação adicionais só podem ser adicionadas ao AEM Sites ou AEM Forms.
   * Regiões de publicação adicionais não se estendem a outras soluções de AEM ou funcionalidades relacionadas implantadas no mesmo programa (por exemplo, AEM Assets ou Adobe Learning Manager).
   * No entanto, essas soluções podem ser adicionadas a um programa, desde que ele tenha pelo menos uma solução do Sites ou do Forms aplicável.
* Regiões adicionais só podem ser adicionadas se os direitos associados estiverem disponíveis e sem uso no locatário.
* É possível adicionar no máximo três regiões de publicação adicionais a qualquer ambiente individual.
* Regiões adicionais estão disponíveis somente em programas de produção. O recurso não está disponível em programas de sandbox.
* Regiões de publicação adicionais são aplicadas apenas a ambientes de preparo e produção, não a ambientes de RDE ou desenvolvimento.
* Regiões de publicação adicionais exigem que seu programa esteja atualizado com a versão 12142 (ou superior) do AEM.
