---
title: Introdução ao Gerenciamento de certificados SSL
description: Saiba como o Cloud Manager oferece ferramentas de autoatendimento para instalar certificados SSL.
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: f69a26c6156c1f9038d612a00b16cac0e51e17ca
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 2%

---


# Introdução ao Gerenciamento de certificados SSL{#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="Gerenciar certificados SSL"
>abstract="Saiba como o Cloud Manager fornece ferramentas de autoatendimento para instalar e gerenciar certificados SSL para proteger seu site para seus usuários. O Cloud Manager usa um serviço TLS de plataforma para gerenciar certificados SSL e chaves privadas de propriedade de clientes e obtidas de autoridades de certificação de terceiros."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html" text="Exibir, atualizar e substituir um certificado SSL"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html" text="Verificar o status de um certificado SSL"

O Cloud Manager fornece ferramentas de autoatendimento para instalar e gerenciar certificados SSL para proteger seu site para seus usuários. O Cloud Manager usa um serviço TLS de plataforma para gerenciar certificados SSL e chaves privadas de propriedade de clientes e obtidas de autoridades de certificação de terceiros, como Let&#39;s Encrypt.

## Introdução aos certificados {#certificates}

As empresas usam certificados SSL para proteger seus sites e permitir que seus clientes confiem neles. Para usar o protocolo SSL, um servidor da Web requer o uso de um certificado SSL.

Quando uma entidade solicita um certificado de uma autoridade de certificação, a autoridade de certificação conclui um processo de verificação. Isso pode variar desde verificar o controle do nome de domínio até coletar documentos de registro da empresa e contratos de assinante. Depois que as informações de uma entidade forem verificadas, a CA assinará sua chave pública usando a chave privada da CA. Como todas as principais autoridades de certificados têm certificados raiz em navegadores da Web, o certificado da entidade será vinculado por meio de um *cadeia de confiança* e o navegador da Web o reconhecerá como um certificado confiável.

>[!IMPORTANT]
>
>O Cloud Manager não fornece certificados SSL ou chaves privadas. Estas devem ser obtidas junto das autoridades de certificação (AC).

## Recursos de gerenciamento SSL do Cloud Manager {#features}

O Cloud Manager oferece suporte às seguintes opções de uso do certificado SSL do cliente.

* Um certificado SSL pode ser usado por vários ambientes. Ou seja, pode ser adicionado uma vez e usado várias vezes.
* Cada ambiente do Cloud Manager pode usar vários certificados.
* Uma chave privada pode emitir vários certificados SSL.
* Cada certificado normalmente contém vários domínios.
* O serviço TLS da plataforma encaminha solicitações para o serviço CDN do cliente com base no certificado SSL usado para encerrar e no serviço CDN que hospeda esse domínio.
* AEM as a Cloud Service aceita certificados SSL curinga para um domínio.

## Recomendações {#recommendations}

AEM as a Cloud Service só oferece suporte seguro `https` sites.

* Os clientes com vários domínios personalizados não desejarão carregar um certificado sempre que adicionarem um domínio.
* Esses clientes se beneficiarão ao obter um certificado com vários domínios.

## Requisitos {#requirements}

* AEM as a Cloud Service só aceitará certificados que estejam em conformidade com a política OV (Validação da Organização) ou EV (Validação Estendida).
* Qualquer certificado deve ser um certificado TLS X.509 de uma autoridade de certificação (CA) confiável com uma chave privada RSA de 2048 bits correspondente.
* A política DV (Validação de Domínio) não é aceita.
* Certificados autoassinados não são aceitos.

Os certificados OV e EV fornecem aos usuários informações extras validadas por CA que podem ser usadas para decidir se o proprietário de um site, remetente de um email ou signatário digital de código executável ou documentos PDF é confiável. Os certificados DV não permitem essa verificação da propriedade.

## Limitações           {#limitations}

A qualquer momento, o Cloud Manager permitirá a instalação de no máximo 50 certificados SSL. Eles podem ser associados a um ou mais ambientes em todo o programa e também incluir quaisquer certificados expirados.

Se tiver atingido o limite, revise os certificados e considere:

* Exclusão de certificados expirados.
* Agrupar vários domínios no mesmo certificado, pois um certificado pode abranger vários domínios (até 100 SANs).

## Saiba mais {#learn-more}

Um usuário com as permissões necessárias pode usar o Cloud Manager para gerenciar certificados SSL para um programa. Consulte os seguintes documentos para obter mais detalhes sobre o uso desses recursos.

* [Adicionar um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [Exibição, atualização ou substituição de um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
* [Excluir um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
