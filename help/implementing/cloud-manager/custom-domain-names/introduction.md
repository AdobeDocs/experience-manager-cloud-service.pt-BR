---
title: Introdução a nomes de domínio personalizados
description: A interface do usuário do Cloud Manager permite que você adicione um domínio personalizado para identificar seu site com um nome exclusivo e de marca, de maneira automatizada.
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
source-git-commit: cc1b0d653706150c616ceafd002dc7594b6c7072
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 7%

---


# Introdução a nomes de domínio personalizados {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="Gerenciar nomes de domínio personalizados"
>abstract="A interface do usuário do Cloud Manager permite que você adicione um domínio personalizado para identificar seu site com um nome exclusivo e de marca, de maneira automatizada."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name.html" text="Adicionar um nome de domínio personalizado"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.html" text="Exibir e atualizar o nome de domínio personalizado"

A interface do usuário do Cloud Manager permite que você adicione um domínio personalizado para identificar seu site com um nome exclusivo e de marca, de maneira automatizada. O Adobe Experience Manager as a Cloud Service é provisionado com um nome de domínio padrão, terminando em `*.adobeaemcloud.com`. Esse nome de domínio padrão permanece, mesmo depois de associar nomes de domínio personalizados ao site.

## O que são nomes de domínio personalizados? {#what-are-custom-domain-names}

Cada site tem um endereço numérico exclusivo, legível por máquina, associado a ele, como `184.33.123.64`. O Sistema de nomes de domínio (DNS) é o que permite ter domínios personalizados e de marca anexados a sites, traduzindo endereços numéricos em endereços memoráveis, como `wknd.com`.

É recomendável ter um nome de domínio para seu site que seja memorável para seus clientes e reflita sua marca.

Você pode comprar um nome de domínio de um registrador de nomes de domínio, de uma empresa ou organização que gerencia e vende nomes de domínio. Registros de nomes de domínio gerenciam nomes de domínio em servidores DNS.

>[!IMPORTANT]
>
>O Cloud Manager não é um registrador de nome de domínio e não fornece serviços DNS.

## Limitações           {#limitations}

Há várias limitações no uso de nomes de domínio personalizados com o AEMaaCS.

* Os nomes de domínio personalizados são suportados no Cloud Manager para programas de publicação e de visualização de Serviços para sites. Domínios personalizados no lado do autor não são compatíveis.
* Cada Ambiente do Cloud Manager pode hospedar até 500 domínios personalizados por ambiente.
* AEM as a Cloud Service não oferece suporte a domínios curingas.
* Antes de adicionar um nome de domínio personalizado, um certificado SSL válido que contenha o nome de domínio personalizado deve ser instalado para o seu programa. Consulte Adicionar um certificado SSL para saber mais.
* Os nomes de domínio não podem ser adicionados a ambientes enquanto houver um pipeline de execução atual anexado a esses ambientes.
* Somente um nome de domínio pode ser adicionado por vez.
* O mesmo nome de domínio não pode ser usado em mais de um ambiente.

## Fluxo de trabalho {#workflow}

A adição de um nome de domínio personalizado requer interação entre o serviço DNS e o Cloud Manager. Por causa disso, há várias etapas necessárias para instalar, configurar e verificar nomes de domínio personalizados. A tabela a seguir fornece uma visão geral das etapas necessárias, incluindo o que fazer quando ocorrerem erros comuns.

| Etapa | Descrição | Responsabilidade | Saiba mais |
|--- |--- |--- |---|
| 1 | Adicionar certificado SLL ao Cloud Manager | Cliente | [Adicionar um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | Adicionar registro TXT para verificar o domínio | Cliente | [Adicionar um registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) |
| 3 | Verificar Status de Verificação de Domínio | Cliente | [Verificando o status do nome de domínio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3 bis | Se a verificação de domínio falhar com o status `Domain Verification Failure` | Cliente | [Verificando o status do nome de domínio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3b | Se a verificação de domínio falhar com o status `Verified, Deployment Failed`, entre em contato com o Adobe | Atendimento ao cliente do Adobe | [Verificando o status do nome de domínio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 4 | Defina as configurações de DNS adicionando registros DNS CNAME ou APEX que apontem para AEM as a Cloud Service | Cliente | [Definição das configurações de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) |
| 5 | Verificar status do registro DNS | Cliente | [Verificação de status do registro DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5 bis | Se o status do registro DNS falhar com `DNS status not detected` | Cliente | [Verificação de status do registro DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5b | Se o status do registro DNS falhar com `DNS resolves incorrectly` | Cliente | [Verificação de status do registro DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
