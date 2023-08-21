---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: e78410a1ce229db0dd3529bf544f694e97bfff46
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 15%

---

# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 13206 {#release-13206}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 13206, lançada publicamente em 21 de agosto de 2023. Esta versão de manutenção substitui as versões 13173 e 13099 para corrigir um problema que afeta a funcionalidade da Caixa de entrada.

A Ativação de recursos 2023.8.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte a [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=pt-BR) para obter mais informações.

### Aprimoramentos {#enhancements-13206}

- SITES-13906: GraphQL - Atualização para graphql-java 20.1.
- SITES-8972: GraphQL - Adicione o rótulo de opção no JSON para o tipo de dados Enumeration.
- SITES-9689: GraphQL - Adicione o título e a descrição no JSON para o tipo de dados Referência de conteúdo.
- SITES-13052: Fragmentos de conteúdo - Exporte fragmentos de conteúdo para o Adobe Target.

### Problemas corrigidos {#fixed-issues-13206}

- SITES-14937: MSM - herdar configurações de implantação do valor principal é alternado ao clicar em Salvar e fechar nas cópias online.
- SITES-14847: Fragmentos de conteúdo - Os links de fragmento de conteúdo não são realçados.
- SITES-11620: Fragmentos de conteúdo - O caminho de referências é ligeiramente cortado na interface.
- SITES-14171: GraphQL - Em alguns casos, as referências circulares não são quebradas para dados em cache.
- SITES-14577: Fragmentos de experiência - A publicação em massa não funciona para cópias online.
- SITES-14341: Interface do usuário do administrador - Comportamento inconsistente do botão &quot;Propriedades&quot; quando as permissões de exclusão são removidas.
- SITES-11000: Interface do administrador - Referências: links de entrada ausentes em algumas páginas.
- SITES-11559: interface do administrador - Referências: os links recebidos mostram páginas incorretas.
- SITES-14337: Interface do administrador - A abertura da página do editor produz um erro em casos específicos.
- SITES-13425: ContextHub - a barra de menus não é exibida ao clicar no botão ContextHub.
- CQ-4354266: não é possível abrir itens da caixa de entrada.
- CQ-4354279: não é possível ver o relatório de atividades na guia Personalização.
- FORMS-9971: quando um Formulário adaptável é renderizado em um local diferente, a visibilidade dos componentes é interpretada e aplicada de forma imprecisa.
- FORMS-9888: quando um Formulário adaptável é definido para redirecionar para um URL externo (página de agradecimento) no envio do formulário, ele não é redirecionado para o URL externo.
- FORMS-9845: depois de limpar uma lista suspensa usando o editor de regras, os valores fornecidos anteriormente persistem, apesar da suposta limpeza.
- FORMS-9263: quando o rótulo de uma caixa de seleção contém caracteres especiais e um usuário clica na caixa de seleção, a respectiva caixa de seleção não é selecionada.
- FORMS-9254: À medida que o usuário navega pelo texto do componente de Termos e condições, a caixa de seleção no componente é automaticamente ativada mesmo antes de o usuário rolar pelo texto inteiro.
- FORMS-9045: a tag de script não resolve referências de fragmento externo no XDP base.
- FORMS-9026: ao tentar criar um Formulário adaptável usando um esquema JSON que tem Enums com cadeias de caracteres vazias e valida sem erros, o processo resulta em uma falha. Em seguida, após atualizar a página, ocorre uma falha no carregamento correto do formulário, exibindo um formulário em branco juntamente com um erro nos logs.
- FORMS-8964: no Android™ Chrome/Firefox, o texto se torna não editável no componente Caixa de texto se o limite máximo de caracteres for atingido.
- FORMS-8668: Despejos excessivos de pilha do Java™ em logs de erro, apesar da renderização funcional do formulário, causando aumento do arquivo de log.
- FORMS-8554: O Forms adaptável com carregamento lento ativado não funciona no modo de visualização da instância do autor.
- FORMS-8177: quando o serviço de formulários está ativo, uma exceção &quot;com.adobe.aem.formsndocuments.publish.AssetReferenceProvider falhou ao recuperar dependências de ativos.&quot; ocorre. O erro desaparece ao desabilitar o serviço de formulário.
- FORMS-3691: O escopo IIFE (Expressão de Função Imediatamente Invocada) está ausente em alguns objetos. O principal objetivo de usar um IIFE é criar um escopo para variáveis dentro da função, evitando que essas variáveis poluam o escopo global.
- SITES-15463: Modelos de sites - Modelos não podem ser publicados.

### Problemas conhecidos {#known-issues-13206}

- SITES-15359: Fragmentos de conteúdo - O padrão de nome de variação não corresponde corretamente às variações que têm ```'_'``` em seus nomes de recursos.
- FORMS-10444: Modelos adaptáveis do Forms - Os modelos não podem ser publicados (solução alternativa: use o Console de distribuição).
- CQ-4354191: workflows - O iniciador personalizado pode ser acionado muitas vezes devido a metadados de replicação presentes em nós nt:unstructured (solução alternativa: atualize os iniciadores para excluir propriedades de metadados de replicação para evitar sobreposição).

### Tecnologias integradas {#embedded-tech-13206}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM OAK | 1.52-T20230629133256-25c01b8 | [API Oak 1.52.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| API do Sling do AEM | Versão 2.27.2 | [API do Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | Versão 1.4.20-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | Versão 2.23.2 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
