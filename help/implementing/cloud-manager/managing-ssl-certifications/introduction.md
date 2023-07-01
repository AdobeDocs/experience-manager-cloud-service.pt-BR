---
title: Introdução ao gerenciamento de certificados SSL
description: Saiba como o Cloud Manager fornece ferramentas de autoatendimento para instalar certificados SSL.
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 81%

---


# Introdução ao gerenciamento de certificados SSL{#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="Gerenciar certificados SSL"
>abstract="Saiba como o Cloud Manager fornece ferramentas de autoatendimento para instalar e gerenciar certificados SSL a fim de proteger seu site para os usuários. O Cloud Manager usa um serviço TLS para gerenciar certificados SSL e chaves privadas de propriedade de clientes e obtidas de autoridades de certificação terceirizadas."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html?lang=pt-BR" text="Visualização, atualização e substituição de um certificado SSL"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html?lang=pt-BR" text="Verificar o status de um certificado SSL"

O Cloud Manager fornece ferramentas de autoatendimento para instalar e gerenciar certificados SSL a fim de proteger seu site para os usuários. O Cloud Manager usa um serviço TLS para gerenciar certificados SSL e chaves privadas de propriedade de clientes e obtidas de autoridades de certificação terceirizadas, como Let&#39;s Encrypt.

## Introdução aos certificados {#certificates}

As empresas usam certificados SSL para proteger seus sites e permitir que os clientes confiem neles. Para usar o protocolo SSL, um servidor da Web exige o uso de um certificado SSL.

Quando uma entidade solicita um certificado de uma autoridade de certificação, esta realiza um processo de verificação. Isso pode variar desde a verificação do controle do nome de domínio até a coleta de documentos de registro da empresa e contratos de assinante. Uma vez verificadas as informações de uma entidade, a CA assinará a chave pública usando sua chave privada. Como todas as principais autoridades de certificação têm certificados raiz em navegadores da Web, o certificado da entidade é vinculado por meio de um *cadeia de confiança* e o navegador da web o reconhecerá como um certificado confiável.

>[!IMPORTANT]
>
>O Cloud Manager não fornece certificados SSL ou chaves privadas. Estas devem ser obtidas junto às autoridades de certificação (CA).

## Recursos de gerenciamento de SSL do Cloud Manager {#features}

O Cloud Manager oferece suporte às opções de uso do certificado SSL do cliente descritas a seguir.

* Um certificado SSL pode ser usado por vários ambientes. Ou seja, pode ser adicionado uma vez e usado várias vezes.
* Cada ambiente do Cloud Manager pode usar vários certificados.
* Uma chave privada pode emitir vários certificados SSL.
* Cada certificado normalmente contém vários domínios.
* O serviço TLS da plataforma encaminha solicitações para o serviço de CDN do cliente, com base no certificado SSL usado para encerramento, e para o serviço de CDN que hospeda esse domínio.
* O AEM as a Cloud Service aceita certificados SSL curinga para um domínio.

## Recomendações {#recommendations}

O AEM as a Cloud Service somente oferece suporte seguro a sites `https`.

* Os clientes com vários domínios personalizados não querem ter que carregar um certificado sempre que adicionam um domínio.
* Esses clientes se beneficiam obtendo um certificado com vários domínios.

## Requisitos {#requirements}

* O AEM as a Cloud Service somente aceitará certificados que estejam em conformidade com a política OV (Validação da organização) ou EV (Validação estendida).
* Todos os certificados devem ser certificados TLS X.509 emitidos por uma autoridade de certificação (CA) confiável e incluir uma chave privada RSA de 2048 bits correspondente.
* A política DV (Validação de domínio) não é aceita.
* Certificados autoassinados não são aceitos.

Os certificados OV e EV fornecem aos usuários informações adicionais validadas pela CA que podem ser usadas para decidir se o proprietário de um site, remetente de um email ou signatário digital de código executável ou de documentos PDF é confiável. Os certificados DV não permitem essa verificação de propriedade.

## Limitações {#limitations}

A qualquer momento, o Cloud Manager permitirá a instalação de no máximo 50 certificados SSL. Eles podem ser associados a um ou mais ambientes em todo o programa e também incluir certificados expirados.

Se tiver atingido o limite, revise os certificados e considere:

* Excluir os certificados expirados.
* Agrupar vários domínios no mesmo certificado, pois um certificado pode abranger vários domínios (até 100 SANs).

## Saiba mais {#learn-more}

Um usuário com as permissões necessárias pode usar o Cloud Manager para gerenciar certificados SSL para um programa. Consulte os documentos a seguir para obter mais detalhes sobre o uso desses recursos.

* [Adicionar um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [Visualização, atualização e substituição de um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
* [Exclusão de um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
