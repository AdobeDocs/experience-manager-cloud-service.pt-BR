---
title: Introdução a nomes de domínio personalizados
description: A interface do Cloud Manager permite adicionar um domínio personalizado para identificar seu site com um nome exclusivo e de marca por meio de autoatendimento.
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 37%

---


# Introdução a nomes de domínio personalizados {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="Gerenciar nomes de domínio personalizados"
>abstract="A interface do Cloud Manager permite adicionar um domínio personalizado para identificar seu site com um nome exclusivo e de marca por meio de autoatendimento."
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name" text="Adicionar um nome de domínio personalizado"
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/managing-custom-domain-names" text="Exibir e atualizar o nome de domínio personalizado"

O Adobe Experience Manager as a Cloud Service é provisionado com um nome de domínio padrão, terminando em `*.adobeaemcloud.com`. Usando a interface do usuário da Cloud Manager, você pode adicionar um domínio personalizado para identificar seu site com um nome exclusivo e de marca, de maneira automatizada. O nome de domínio padrão `*.adobeaemcloud.com` permanece, mesmo depois de associar nomes de domínio personalizados ao site.

## O que são nomes de domínio personalizados? {#what-are-custom-domain-names}

Cada site tem um endereço numérico exclusivo, legível por máquina, associado a ele, como `184.33.123.64`. O Sistema de Nomes de Domínio (DNS) é o que permite ter domínios personalizados e de marca anexados aos sites, traduzindo endereços numéricos em endereços possíveis de memorizar, como `wknd.com`.

É uma boa prática ter um nome de domínio para seu site que possa ser memorizado pelos seus clientes e reflita a sua marca.

Você pode comprar um nome de domínio de um registrador de nomes de domínio, de uma empresa ou organização que gerencia e vende nomes de domínio. Registros de nomes de domínio gerenciam nomes de domínio em servidores DNS.

>[!IMPORTANT]
>
>O Cloud Manager não é um registrador de nomes de domínio e não fornece serviços DNS.

## Nomes de domínio personalizados e Traga seus próprios CDNs {#byo-cdn}

O AEM as a Cloud Service oferece um serviço CDN (Content Delivery Network) integrado, mas também permite que você use a CDN BYO (Bring Your Own, Traga sua própria) com o AEM. Os domínios personalizados podem ser instalados ou na CDN gerenciada pelo AEM ou em uma CDN gerenciada por você.

* O Cloud Manager gerencia nomes de domínio personalizados e certificados instalados na CDN gerenciada pela AEM.
* Os nomes de domínio e certificados personalizados instalados em um CDN BYO são gerenciados diretamente nesse CDN.

**Os domínios gerenciados na sua própria CDN não exigem instalação por meio do Cloud Manager**. Eles são disponibilizados para o AEM por meio do X-Forwarded-Host e correspondem aos vhosts definidos no Dispatcher. Consulte a [documentação da CDN](/help/implementing/dispatcher/cdn.md).

Em um ambiente, você pode ter ambos os domínios instalados na CDN gerenciada pela AEM e em uma CDN BYO.

## Fluxo de trabalho {#workflow}

A adição de um nome de domínio personalizado exige interação entre o serviço DNS e o Cloud Manager. Devido a esse fluxo de trabalho, há várias etapas necessárias para instalar, configurar e verificar nomes de domínio personalizados. A tabela a seguir descreve as etapas necessárias, com links para os recursos da documentação para concluí-las.

>[!WARNING]
>
>Execute a Etapa 4 (Configurar DNS) *somente após a Etapa 3* (Adicionar mapeamento de domínio) ser concluída com êxito. Seguindo essa ordem, registra o domínio com o CDN da Adobe e configura o roteamento correto, protegendo seu site contra aquisições de domínio.

| Etapa | Descrição |
| --- | --- |
| 1 | [Adicionar certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | [Adicionar um domínio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) |
| 3 | [Adicionar mapeamento de domínio](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) |
| 4 | [Configurar DNS](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#config-dns) |
| 5 | [Verificar status do DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |

>[!TIP]
>
>Geralmente, a configuração de nomes de domínio personalizados com o AEM as a Cloud Service é um processo simples. No entanto, ocasionalmente, podem ocorrer problemas de delegação de domínio, que podem levar de 1 a 2 dias úteis para serem resolvidos. Por esse motivo, é recomendável instalar os domínios bem antes de suas datas de ativação. Consulte o documento [Verificar o status do nome de domínio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obter mais informações.

## Notas de uso {#usage-notes}

* Os nomes de domínio personalizados são suportados no Cloud Manager somente para serviços de publicação e visualização de programas do Sites.
   * Não há suporte para domínios personalizados para serviços de autor.
* Cada ambiente do Cloud Manager pode hospedar até 500 domínios personalizados por ambiente.
* Os nomes de domínio não podem ser adicionados aos ambientes enquanto houver um pipeline em execução anexado a eles.
* O mesmo nome de domínio não pode ser usado em mais de um ambiente.
* Somente um nome de domínio pode ser adicionado por vez.
* O AEM as a Cloud Service não oferece suporte a domínios curinga, como o `*.example.com`.
* Antes de adicionar um nome de domínio personalizado, um certificado SSL válido contendo o nome de domínio personalizado (certificados curingas são válidos) deve ser instalado para o seu programa.
* Etapas de configuração adicionais são necessárias para usar um nome de domínio personalizado com [o recurso Pipeline de Front-End](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md#custom-domains).

## Introdução {#get-started}

* Comece a configurar um novo nome de domínio personalizado para seu projeto [adicionando um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).
* Gerencie seus nomes de domínio existentes revisando o documento [Gerenciar nomes de domínio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md).
