---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: f0dc0e0ccd196ab748e2bfcdb4ce404c1c91c213
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 20%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 12441 {#release-12441}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 12441, lançada publicamente em 27 de junho de 2023. Esta versão de manutenção é uma atualização da versão de manutenção anterior a 12255.

A Ativação de recursos 2023.7.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte a [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para obter mais informações.

### Aprimoramentos {#enhancements-12441}

- SITES-8769: Melhorar chamadas StyleImpl em ResponsiveGrid
- FORMS-5054: adição de suporte para todos os [estátuas](https://opensource.adobe.com/acrobat-sign/acrobat_sign_events/webhookeventsagreements.html) com suporte da Adobe Sign.

### Problemas corrigidos {#fixed-issues-12441}

- Várias atualizações relacionadas à acessibilidade
- SITES-12688: Editor de páginas: operador lógico OU que não está funcionando corretamente na pesquisa do Localizador de ativos
- SITES-4951: Editor de páginas: a pesquisa de tags no editor de páginas não encontra subtags
- SITES-12465: Fragmentos de experiência: as teclas de seta não funcionam na caixa de diálogo do componente de Fragmento de experiência
- SITES-12893: Fragmentos de experiência: aplicar validação de referência circular para Fragmentos de experiência
- SITES-12715: Fragmentos de experiência: as configurações do serviço em nuvem aplicadas à pasta Fragmentos de experiência não persistem
- SITES-13097: Fragmentos de experiência: não é possível adicionar fragmentos de experiência a um projeto de tradução
- SITES-13165: GraphQL: restaura o comportamento padrão para a filtragem de valores nulos
- SITES-12577: Verificador de links: transformador não reescreve links intermitentemente
- SITES-13559: MSM: exceção &quot;Não é modificável&quot; lançada ao implantar o componente
- SITES-11757: MSM: herdar a configuração de implantação do Pai não é revertido para páginas filhas
- SITES-14073: Administrador de sites: o relatório CSV falha com 500 ao selecionar nenhuma propriedade para exportar
- FORMS-7648: a validação do campo Número máximo de dígitos não funciona para o componente de Caixa numérica.
- FORMS-8177: quando o serviço do Forms está ativo, o erro &quot;com.adobe.aem.formsndocuments.publish.AssetReferenceProvider falhou ao recuperar dependências de ativos&quot; encontra.
- FORMS-8300: quando um usuário tenta delegar uma tarefa após abri-la, a resposta do delegado recarrega a tarefa, em vez de abrir a interface de entrada AEM do usuário.
- FORMS-8500: No navegador Microsoft® Edge com a opção Modo IE ativada, o HTML5 Forms não abre.
- FORMS-8541: Ao renderizar um Forms adaptável, ocorre uma exceção de ponteiro nulo.
- FORMS-8964: quando um formulário é aberto em um dispositivo Android™ no Google Chrome ou Mozilla Firefox, o texto inserido no componente Caixa de texto não pode ser removido.
- FORMS-9026: Quando um usuário cria um Formulário adaptável com base em um esquema JSON complexo e válido, arrasta os campos de esquema JSON relacionados para o Editor Forms adaptável para criar campos do Forms adaptável e atualiza a janela Editor Forms adaptável, todos os campos são excluídos e o editor Forms adaptável aparece em branco.
- FORMS-9263: quando o texto de exibição de uma opção de caixa de seleção contém um caractere especial, os usuários não podem marcar essas caixas de seleção.
- FORMS-8668: ao renderizar uma Visualização de PDF de um formulário, alguns despejos de pilha do Java™ não necessários são exibidos nos logs de erro. No entanto, não há problemas ao renderizar o formulário.
- FORMS-8116: quando as regras são aplicadas ao componente de Contêiner adaptável do Forms, as regras aplicadas não são salvas.
- FORMS-7906: quando um Formulário adaptável é adicionado a um componente de Contêiner do AEM Sites, o editor de regras não é aberto.
- FORMS-8846: a propriedade de referência Vincular não funciona para o componente de anexos adaptáveis do Forms.
- FORMS-9072: Ao pesquisar um Esquema ao criar um fragmento de formulário, o resultado da pesquisa não retorna nenhum esquema para seleção.
- FORMS: correção de vários bugs relacionados à acessibilidade para melhorar a acessibilidade dos recursos do AEM Forms.


### Problemas conhecidos {#known-issues-12441}

Nenhum.

### Tecnologias integradas {#embedded-tech-12441}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.50-T20230405052634-f9df4aa | [API Oak 1.50.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.50.0/index.html) |
| API do Sling do AEM | Versão 2.27.0 | [API do Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.23.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
