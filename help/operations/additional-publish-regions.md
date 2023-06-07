---
title: Regiões de publicação adicionais
description: Saiba como o AEM as a Cloud Service suporta regiões de publicação adicionais para aumentar a disponibilidade e reduzir a latência.
source-git-commit: 9fccc1672aad243b648115e657396be1ce4ed614
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---


# Regiões de publicação adicionais {#additional-publish-regions}

Regiões de publicação adicionais podem ser licenciadas e ativadas em programas configurados com o AEM Sites. Quando configurado, o tráfego nos ambientes de preparo e produção é roteado para vários farms de publicação, que têm os seguintes benefícios:

* Latência reduzida - As solicitações que roteiam do CDN para as instâncias de publicação do AEM são direcionadas para a região de publicação mais próxima, o que é vantajoso para sites e aplicativos visitados por usuários em várias regiões geográficas.
* Maior disponibilidade - Se uma região não estiver disponível, o CDN direcionará o tráfego para as outras regiões disponíveis.

As organizações podem licenciar até três regiões de publicação adicionais.

>[!NOTE]
>
>No momento, esse recurso está disponível apenas para o AEM Sites. Também não pode ser aplicado a programas de sandbox. Além disso, esteja ciente de que os recursos adicionais de regiões de publicação exigem que seu programa seja atualizado para o AEM versão 12142 ou superior.

## Casos de uso {#use-cases}

Veja a seguir alguns casos de uso em que as organizações podem se beneficiar do licenciamento de regiões de publicação adicionais.

1. Para organizações que recebem tráfego significativo ou crítico de negócios de usuários distantes da região principal, regiões de publicação adicionais podem reduzir a latência vivida por esses visitantes.
1. Para organizações que podem sofrer danos significativos monetários ou de reputação quando um site não está disponível, isso pode ser atenuado usando regiões de publicação adicionais para tornar o nível de publicação do AEM mais resiliente à falha regional.
1. Para organizações cujos autores de conteúdo estão localizados em uma localização geográfica distante da maioria dos visitantes do nível de publicação, a região primária pode ser escolhida próximo ao local dos autores de conteúdo, enquanto regiões de publicação adicionais podem ser configuradas próximo ao tráfego do lado da publicação, com ambos os públicos-alvo se beneficiando de uma experiência otimizada.

## Ativar e configurar {#enabling-and-configuring}

Depois de licenciar uma região de publicação adicional, as regiões são configuradas usando o Cloud Manager. Consulte a [Documentação do Cloud Manager](/help/implementing/cloud-manager/manage-environments.md#multiple-regions) para obter instruções detalhadas.

Regiões de publicação adicionais são aplicadas a ambientes de preparo e produção, mas não a ambientes de RDE ou desenvolvimento.

## Considerações sobre redes avançadas {#advanced-networking-considerations}

Quando uma região de publicação adicional é ativada em um programa com rede avançada já configurada, o tráfego na região de publicação adicional que corresponde às regras de rede avançadas será roteado por padrão pela região primária. Para aproveitar o aumento da disponibilidade, é recomendável habilitar a rede avançada nas regiões adicionais.

Consulte a [Configuração avançada de rede para regiões de publicação adicionais](/help/security/configuring-advanced-networking.md#advanced-networking-configuration-for-additional-publish-regions) seção na documentação de Rede avançada para obter detalhes, incluindo como adicionar configurações avançadas de rede a regiões adicionais sem incorrer em perda de conectividade.

## Limitações {#limitations}

Lembre-se dessas limitações ao considerar o uso de regiões de publicação adicionais.

* Regiões de publicação adicionais só podem ser adicionadas à AEM Sites. Regiões de publicação adicionais não se estendem a outras soluções de AEM ou funcionalidades relacionadas implantadas no mesmo programa (por exemplo, AEM Forms ou Adobe Learning Manager).
* Regiões adicionais só podem ser adicionadas se os direitos associados estiverem disponíveis e não forem usados no locatário.
* No máximo três regiões de publicação adicionais podem ser adicionadas a qualquer ambiente individual.
* Regiões adicionais estão disponíveis somente em programas de produção. O recurso não está disponível em programas de sandbox.
* Regiões de publicação adicionais são aplicadas apenas a ambientes de preparo e produção, não a ambientes de RDE ou desenvolvimento.
* Regiões de publicação adicionais exigem que seu programa seja atualizado para o AEM versão 12142 ou superior.
