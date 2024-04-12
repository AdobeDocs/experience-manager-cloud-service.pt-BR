---
title: Introdução a nomes de domínio personalizados
description: A interface do Cloud Manager permite adicionar um domínio personalizado para identificar seu site com um nome exclusivo e de marca por meio de autoatendimento.
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
source-git-commit: d9cd10772252d80487f578ee73f40ec334600029
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 82%

---


# Introdução a nomes de domínio personalizados {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="Gerenciar nomes de domínio personalizados"
>abstract="A interface do Cloud Manager permite adicionar um domínio personalizado para identificar seu site com um nome exclusivo e de marca por meio de autoatendimento."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name" text="Adicionar um nome de domínio personalizado"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/managing-custom-domain-names" text="Exibir e atualizar o nome de domínio personalizado"

A interface do usuário do Cloud Manager permite adicionar um domínio personalizado para identificar seu site com um nome exclusivo e de marca, de maneira automatizada. O Adobe Experience Manager as a Cloud Service é provisionado com um nome de domínio padrão, terminando em `*.adobeaemcloud.com`. Esse nome de domínio padrão permanece, mesmo depois de associar nomes de domínio personalizados ao site.

## O que são nomes de domínio personalizados? {#what-are-custom-domain-names}

Cada site tem um endereço numérico exclusivo, legível por máquina, associado a ele, como `184.33.123.64`. O Domain Name System (DNS) é o que permite ter domínios personalizados e de marca anexados aos sites, traduzindo endereços numéricos em endereços possíveis de memorizar, como `wknd.com`.

É recomendado ter um nome de domínio para seu site que possa ser memorizado pelos seus clientes e reflita a sua marca.

Você pode comprar um nome de domínio de um registrador de nomes de domínio, de uma empresa ou organização que gerencia e vende nomes de domínio. Registros de nomes de domínio gerenciam nomes de domínio em servidores DNS.

>[!IMPORTANT]
>
>O Cloud Manager não é um registrador de nomes de domínio e não fornece serviços DNS.

## Nomes de domínio personalizados e CDNs BYO {#byo-cdn}

O AEM as a Cloud Service oferece um serviço de rede de entrega de conteúdo (CDN) integrado, mas também permite que você traga seu próprio CDN (BYO) para usar com o AEM. Os domínios personalizados podem ser instalados ou na CDN gerenciada pelo AEM ou em uma CDN gerenciada por você.

* Os nomes de domínio personalizados (e certificados) que são instalados na CDN gerenciada pelo AEM são gerenciados através do Cloud Manager.
* Os nomes de domínio personalizados (e certificados) que são instalados em sua própria CDN são gerenciados nessa CDN específica.

Os domínios gerenciados em sua própria CDN não precisam ser instalados via Cloud Manager. Eles são disponibilizados no AEM por meio do X-Forwarded-Host e correspondem aos vhosts definidos no Dispatcher. Consulte a [documentação da CDN](/help/implementing/dispatcher/cdn.md).

Em um ambiente, é possível ter ambos os domínios instalados na CDN gerenciada pela AEM e instalados em sua própria CDN.

## Fluxo de trabalho {#workflow}

A adição de um nome de domínio personalizado exige interação entre o serviço DNS e o Cloud Manager. Por causa disso, há várias etapas necessárias para instalar, configurar e verificar nomes de domínio personalizados. A tabela a seguir fornece uma visão geral das etapas necessárias, incluindo o que fazer quando ocorrerem erros comuns.

| Etapa | Descrição | Responsabilidade | Saiba mais |
|--- |--- |--- |---|
| 1 | Adicionar certificado SSL ao Cloud Manager | Cliente | [Adicionar um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | Adicionar registro TXT para verificar o domínio | Cliente | [Adicionar um registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) |
| 3 | Revisar o status de verificação de domínio | Cliente | [Verificação de status do nome de domínio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3a | Se a verificação de domínio falhar com o status `Domain Verification Failure` | Cliente | [Verificação de status do nome de domínio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3b | Se a verificação de domínio falhar com o status `Verified, Deployment Failed`, entre em contato com a Adobe | Atendimento ao cliente da Adobe | [Verificação de status do nome de domínio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 4 | Definir as configurações de DNS adicionando registros CNAME ou Apex de DNS que apontem para o AEM as a Cloud Service | Cliente | [Definição das configurações de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) |
| 5 | Verificar o status do registro DNS | Cliente | [Verificação de status do registro DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5a | Se o status do registro DNS falhar com `DNS status not detected` | Cliente | [Verificação de status do registro DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5b | Se o status do registro DNS falhar com `DNS resolves incorrectly` | Cliente | [Verificação de status do registro DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |

>[!TIP]
>
>Geralmente, a configuração de nomes de domínio personalizados com o AEM as a Cloud Service é um processo simples. No entanto, ocasionalmente, podem ocorrer problemas de delegação de domínio, que podem levar de 1 a 2 dias úteis para serem resolvidos. Por esse motivo, é altamente recomendável instalar os domínios bem antes de sua data de ativação. Consulte o documento [Verificando o status do nome de domínio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obter mais informações.

## Limitações {#limitations}

Há várias limitações no uso de nomes de domínio personalizados com o AEMaaCS.

* Os nomes de domínio personalizados são compatíveis com o Cloud Manager para serviços de publicação e de visualização para os programas do Sites. Não há suporte para domínios personalizados para serviços de autor.
* Cada ambiente do Cloud Manager pode hospedar até 500 domínios personalizados por ambiente.
* Os nomes de domínio não podem ser adicionados aos ambientes enquanto houver um pipeline em execução anexado a eles.
* O mesmo nome de domínio não pode ser usado em mais de um ambiente.
* Somente um nome de domínio pode ser adicionado por vez.
* O AEM as a Cloud Service não oferece suporte a domínios curinga, como o `*.example.com`.
* Antes de adicionar um nome de domínio personalizado, um certificado SSL válido contendo o nome de domínio personalizado (certificados curinga são válidos) deve ser instalado para o seu programa. Consulte [Adicionar um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) para saber mais.
