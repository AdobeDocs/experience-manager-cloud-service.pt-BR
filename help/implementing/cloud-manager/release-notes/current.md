---
title: Notas de versão do Cloud Manager 2024.11.0 no Adobe Experience Manager as a Cloud Service
description: Saiba mais sobre o lançamento do Cloud Manager 2024.11.0 no AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 87293526ca9c10a142bc1d1d3a35562b171da385
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 27%

---

# Notas de versão do Cloud Manager 2024.11.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Saiba mais sobre o lançamento do Cloud Manager 2024.11.0 no AEM (Adobe Experience Manager) as a Cloud Service.

>[!NOTE]
>
>Consulte as [notas de versão atuais do Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Datas de lançamento {#release-date}

A data de lançamento do Cloud Manager 2024.11.0 no AEM as a Cloud Service é 7 de novembro de 2024.

A próxima versão planejada é 5 de dezembro de 2024.

## Novidades {#what-is-new}

* Experimente a mais recente inovação em Edge Delivery Services com o AEM Cloud Service - agora disponível para explorar em seu programa de sandbox. [Saiba mais](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md#auto-creation) <!-- (CMGR-62319) -->
* A página Configurações de domínio no AEM Cloud Manager agora inclui um recurso de pesquisa que permite localizar rapidamente os domínios por nome. Você pode inserir palavras-chave no campo de pesquisa para filtrar e exibir domínios correspondentes, facilitando o gerenciamento de vários domínios com eficiência. Além disso, a página oferece filtros de status, como **Verificado** e **Não Verificado**, para refinar ainda mais os resultados da pesquisa. <!-- (CMGR-62615) -->

![Campo de pesquisa nas Configurações de Domínio](/help/implementing/cloud-manager/assets/domain-settings-search.png)

## Programa de adoção antecipada {#early-adoption}

Faça parte do programa de adoção antecipada do Cloud Manager e aproveite a oportunidade de testar alguns dos próximos recursos.

### Página inicial do AEM {#aem-home}

A página inicial do AEM apresenta um ponto de partida centralizado para gerenciar conteúdo, ativos e sites no Adobe Experience Manager. Projetado para proporcionar uma experiência personalizada, o AEM Home permite navegar pelo ecossistema AEM sem interrupções de acordo com suas funções e metas. Atuando como guia, ele fornece insights importantes e ações recomendadas para ajudar você a atingir seus objetivos com eficiência. Com um layout claro e personalizado, o AEM Home garante acesso rápido a ferramentas essenciais, oferecendo suporte a uma experiência simplificada e eficaz em todos os recursos do AEM.

Disponível para os primeiros usuários, a AEM Home oferece uma experiência otimizada focada na melhoria dos fluxos de trabalho, na priorização de metas e na entrega de resultados. A aceitação permite influenciar o desenvolvimento da AEM Home, fornecendo feedback que ajuda a moldar seu futuro e aumenta seu valor para toda a comunidade AEM.

Se você estiver interessado em testar este novo recurso e compartilhar seus comentários, envie um email para [Grp-AemHome@adobe.com](mailto:Grp-AemHome@adobe.com) a partir do seu endereço de email associado à sua Adobe ID. Certifique-se de incluir as seguintes informações:

* A função que melhor se adapta ao seu perfil: Autor de conteúdo, Desenvolvedor, Proprietário da empresa, Administrador ou Outro (forneça uma descrição).
* Sua superfície de acesso primária ao AEM: AEM Sites, AEM Assets, AEM Forms, Cloud Manager ou Outro (forneça uma descrição).

### Traga seu próprio Git: agora com suporte para GitLab e Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

O recurso **Traga seu próprio Git** foi expandido para incluir suporte para repositórios externos, como GitLab e Bitbucket. Esse novo suporte é uma adição ao suporte já existente para repositórios GitHub privados e empresariais. Ao adicionar esses novos repositórios, também é possível vinculá-los diretamente aos seus pipelines. Você pode hospedar esses repositórios em plataformas de nuvem pública ou em sua infraestrutura ou nuvem privada. Essa integração também elimina a necessidade de sincronização constante do código com o repositório da Adobe e oferece a capacidade de validar solicitações de pull antes de mesclá-las em uma ramificação principal.

Consulte [Adicionar repositórios externos no Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Caixa de diálogo Adicionar repositório](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>Atualmente, as verificações de qualidade do código de solicitação de pull prontas para uso são exclusivas de repositórios hospedados no GitHub, mas uma atualização para estender essa funcionalidade a outros fornecedores Git está em andamento.

Se tiver interesse em testar esse novo recurso e compartilhar o seu feedback, envie um email para [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) do seu endereço de email associado à sua Adobe ID. Certifique-se de incluir qual plataforma Git deseja usar e se você está em uma estrutura de repositório privado/público ou corporativo. —>


## Correções de erros

* Uma atualização recente abordou um problema no SonarQube em que senhas codificadas não eram detectadas em determinados casos. A correção agora inclui uma verificação de padrão expandida e se alinha aos padrões de detecção padrão no SonarQube. <!-- CMGR-62682 -->
* Ao tentar atualizar um certificado SSL no Cloud Manager, um erro desconhecido apareceria ao clicar em **[!UICONTROL Atualizar]** na caixa de diálogo **[!UICONTROL Exibir e atualizar certificado SSL]**. <!-- CMGR-62848 -->
* No Cloud Manager, as atualizações do certificado SSL falhavam com o erro &quot;O novo certificado não corresponde aos domínios existentes&quot;, mesmo quando os domínios eram idênticos, mas tinham diferenças na caixa de correio (maiúsculas ou minúsculas). A atualização agora reconhece domínios como não diferencia maiúsculas de minúsculas, alinhando-se aos padrões RFC. <!-- CMGR-62844 -->
* No Cloud Manager, os vínculos de Inclui na lista de permissões de IP permaneceram presos em um estado de execução porque os links de chave estrangeira para configurações de domínio estavam ausentes. A correção agora garante que as associações de Inclui na lista de permissões de IP estejam vinculadas corretamente às configurações de domínio associadas. <!-- CMGR-62838 -->
* O Cloud Manager valida o status OCSP (Online Certificate Status Protocol) de um certificado SSL. A Adobe recomenda que você também valide a integridade do certificado localmente usando uma ferramenta como o `openssl verify -untrusted intermediate.pem certificate.pem` antes de instalá-lo pelo Cloud Manager. Para obter mais detalhes, consulte a [documentação de requisitos do certificado SSL](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/introduction-to-ssl-certificates#requirements). <!-- CMGR-62341  -->



<!-- ## Known issues {#known-issues} -->