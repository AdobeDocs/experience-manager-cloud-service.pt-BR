---
title: Introdução - Gerenciamento de certificados SSL
description: Introdução - Gerenciamento de certificados SSL
translation-type: tm+mt
source-git-commit: 74cc587874c4d0a0ef9b542549801198d4f2d7a5
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# Introdução {#introduction}

O Cloud Manager fornece aos clientes o recurso de autoatendimento para instalar certificados SSL por meio da interface do usuário do Cloud Manager. O Cloud Manager usa um serviço TLS da plataforma para gerenciar certificados SSL e chaves privadas de propriedade de clientes e normalmente obtidas de autoridades de certificação de terceiros, por exemplo, Let&#39;s Encrypt.

>[!IMPORTANT]
>O Cloud Manager não fornece certificados SSL nem chaves privadas. Estes devem ser obtidos junto de autoridades certificadoras de terceiros. Consulte Como obter um certificado SSL para saber mais. INSERIR LINK

>[!NOTE]
>AEM como Cloud Service só suporta sites https seguros. Os clientes com vários domínios personalizados não desejarão carregar um certificado sempre que adicionarem um domínio. Assim, esses clientes se beneficiarão ao obter um certificado com vários domínios.

O Cloud Manager oferece suporte aos seguintes requisitos de certificado SSL do cliente:

* Um certificado SSL pode ser usado por vários Ambientes - Adicione uma vez e use várias vezes.
* Cada Ambiente do Cloud Manager pode usar vários certificados.
* Uma Chave privada pode emitir vários certificados SSL.
* Em geral, cada certificado conterá vários domínios.
* O serviço TLS da plataforma encaminha solicitações ao Serviço CDN do cliente com base no certificado SSL usado para encerrar e no Serviço CDN que hospeda esse domínio.

Usando a página Certificados SSL de interface do usuário do Cloud Manager, um usuário com permissões pode executar várias tarefas para gerenciar certificados SSL para um programa:

* Adicionando um certificado SSL.
* Visualização, atualização ou substituição de um certificado SSL. Essas ações permitem que você visualização detalhes ou substitua um certificado que está prestes a expirar.
* Excluindo um certificado SSL.