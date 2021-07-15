---
title: Introdução - Gerenciar certificados SSL
description: Introdução - Gerenciar certificados SSL
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: d457d76d56a729a2e6eb729ad91a6e7877fd6a0c
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# Introdução {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="Gerenciar certificados SSL"
>abstract="O Cloud Manager fornece aos clientes o recurso de autoatendimento para instalar certificados SSL por meio da interface do usuário do Cloud Manager. O Cloud Manager usa um serviço TLS da Platform para gerenciar certificados SSL e chaves privadas de propriedade de clientes e normalmente obtidas de autoridades de certificação de terceiros."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/view-update-replace-ssl-certificate.html" text="Exibir, atualizar e substituir um certificado SSL"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/check-status-ssl-certificate.html" text="Verificar o status de um certificado SSL"


O Cloud Manager fornece aos clientes o recurso de autoatendimento para instalar certificados SSL por meio da interface do usuário do Cloud Manager. O Cloud Manager usa um serviço TLS da plataforma para gerenciar certificados SSL e chaves privadas de propriedade de clientes e normalmente obtidas de autoridades de certificação de terceiros, por exemplo, *Let&#39;s Encrypt*.

## Considerações importantes {#important-considerations}

* O Cloud Manager não fornece certificados SSL ou chaves privadas. Estes devem ser obtidos junto de autoridades certificadoras de terceiros. Consulte [Obter um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md) para saber mais.

* O AEM como Cloud Service só oferece suporte a sites `https` seguros. Os clientes com vários domínios personalizados não desejarão carregar um certificado sempre que adicionarem um domínio. Portanto, esses clientes se beneficiarão ao obter um certificado com vários domínios.

* AEM como Cloud Service só aceitará certificados OV (Validação da Organização) ou EV (Validação Estendida). Certificados DV (Validação de Domínio) não serão aceitos. Além disso, qualquer certificado deve ser um certificado TLS X.509 de uma autoridade de certificação (CA) confiável com uma chave privada RSA de 2048 bits correspondente.

* AEM como Cloud Service aceitará certificados SSL curinga para um domínio.

* A qualquer momento, o Cloud Manager permitirá um máximo de 20 certificados SSL que podem ser associados a um ou mais ambientes em todo o Programa, mesmo que um certificado tenha expirado. No entanto, a interface do usuário do Cloud Manager permitirá que até 50 certificados SSL sejam instalados no programa com essa restrição. Normalmente, um certificado pode abranger vários domínios (até 100 SANs), portanto, considere agrupar vários domínios no mesmo certificado para permanecer abaixo desse limite.

O Cloud Manager é compatível com os seguintes requisitos de certificado SSL do cliente:

* Um certificado SSL pode ser usado por vários ambientes, ou seja, adicionar uma vez e usar várias vezes.
* Cada Ambiente do Cloud Manager pode usar vários certificados.
* Uma Chave privada pode emitir vários certificados SSL.
* Cada certificado normalmente conterá vários domínios.
* O serviço TLS da plataforma encaminha solicitações para o Serviço CDN do cliente com base no certificado SSL usado para encerrar e no Serviço CDN que hospeda esse domínio.

Usando a página Certificados SSL de interface do usuário do Cloud Manager , um usuário com permissões pode executar várias tarefas para gerenciar certificados SSL para um programa:

* [Adicionar um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [Exibição, atualização ou substituição de um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/view-update-replace-ssl-certificate.md)
   >[!NOTE]
   >Essas ações permitem exibir detalhes ou substituir um certificado que está prestes a expirar.
* [Excluindo um certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/delete-ssl-certificate.md)
