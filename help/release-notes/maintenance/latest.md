---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9a653fbe13b29fa60af7410fff178cbac6ca554d
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 13%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 18598 {#18598}

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 18598, lançada publicamente em quinta-feira, 13 de novembro de 2024. A versão de manutenção anterior era a versão 18311. A versão 18459 foi tornada privada devido a um problema.

A ativação de recursos do 2024.11.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-18598}

* CQ-4357471: adição de suporte para tradução de dicionários i18n no AEMaaCS.
* FORMS-11646: Definição de variáveis globaisContext para páginas relevantes do AEM Forms.
* FORMS-14833: o AEM Forms agora tem a capacidade de incluir fragmentos de formulário adaptável no Documento de registro final (DoR).
* FORMS-14255: os usuários agora podem se beneficiar de um recurso de salvamento automático que salva automaticamente um formulário parcialmente concluído como rascunho. Eles podem retornar mais tarde para terminar de preenchê-lo no mesmo dispositivo ou em outro.
* SITES-23591: Fragmentos de conteúdo: atualização de fragmento de conteúdo para suporte a UUID.
* SITES-25440: Fragmentos de conteúdo: API de pesquisa CFM para mostrar o status de replicação.
* SITES-24369: Fragmentos de conteúdo: melhorias na documentação da OpenAPI.
* SITES-25478: fragmentos de conteúdo: adicione suporte de back-end para referências de ativos externos.
* SITES-26119: Fragmentos de conteúdo: adicione suporte a referências de ativos externos no tipo de referência.
* SITES-21199: Edge Delivery com Universal Editor: adicionar suporte para modelos criados a partir de páginas.
* SITES-20311: Edge Delivery com editor universal: adicione suporte para importar CSVs para planilhas.
* SITES-24821: Edge Delivery com Universal Editor: torne aem.page / aem.live o padrão para integrar com o Edge Delivery.

### Problemas corrigidos {#fixed-issues-18598}

* CQ-4358730: CQPagePreviewGenerator falha quando há mais de 10 chaves a serem traduzidas.
* CQ-4358028: a criação do projeto AEM falha quando um usuário com apenas um grupo de administradores de projeto carrega uma nova miniatura na página de criação do projeto.
* FORMS-14978: Ativação do carregamento de página para um formulário baseado em Componente principal para o editor de tema.
* FORMS-15682: o problema envolve a integração do AEM Forms e do Dynamics FDM. Quando um usuário envia um formulário, o Documento de registro (DOR) não é enviado como um anexo de PDF para o campo de entidade especificado.
* FORMS-15799: a página Assinatura do Adobe Sign GovCloud não é renderizada no iframe.
* FORMS-16113: Quando um usuário, que é um administrador da conta do Adobe Sign, tenta acessar um documento enviado por outro usuário (também um administrador), a API de obtenção de contrato pode retornar uma ID de contrato diferente da gerada inicialmente quando o contrato foi criado.
* FORMS-16596: Problema de acessibilidade: botões desativados não reconhecidos pelo Reader de tela.
* GRANITE-53907: não é possível identificar o usuário do serviço como superusuário do workflow.
* SKYOPS-90560: A versão mais recente do Modelo Sling afeta o desempenho da exportação do Modelo Sling.
* SITES-10575: MSM: O carregador de bloomfilter de blueprint tenta carregar >100.000 linhas.
* SITES-20755: Fragmentos de conteúdo: a referência de ativo com atualização de UUID não mostra a miniatura.
* SITES-26253: Fragmentos de conteúdo: Migração de UUID: alterar o tópico de trabalho do sling para genérico.
* SITES-21338: Fragmentos de conteúdo: o endpoint referencedBy não retorna a referência de página correta.
* SITES-24421: Fragmentos de conteúdo: editar o ponto de extremidade do CF não funciona para o CF recuperado via GET CF.
* SITES-25461: Fragmentos de conteúdo: filtre por modelo na pesquisa de CFs não deve diferenciar maiúsculas de minúsculas.
* SITES-25471: Fragmentos de conteúdo: corrigir a validação de modelos globais no ModelValidatorServlet.
* SITES-25795: Fragmentos de conteúdo: a API do modelo CF falha quando não há data de cq definida.
* SITES-25817: Fragmentos de conteúdo: aprimorar promoteLaunch: atualizar última promoção para Lançamentos de CF.
* SITES-26030: Fragmentos de conteúdo: Endpoint /referencesTree não retorna o cabeçalho necessário.
* SITES-26031: Fragmentos de conteúdo: status de replicação não retornado no endpoint de pesquisa CFM.
* SITES-26213: fragmentos de conteúdo: desfazer a publicação de fragmentos de conteúdo deve validar somente as referências publicadas.
* SITES-26226: Fragmentos de conteúdo: inicia um problema de fluxo de trabalho quando nenhum dos caminhos fornecidos é utilizável.
* SITES-26238: Fragmentos de conteúdo: as referências de ativos retornadas pela API têm uma ordem diferente da ordem do JCR.
* SITES-25456: eventos: ao mover uma página, um evento de exclusão de página é gerado além do evento de movimentação de página.
* SITES-25658: Eventos: a camada e sourceUrl não são preenchidas nos eventos de estado de conteúdo da página.
* SITES-6497: Inicializações: a página Criar na inicialização não funciona.
* SITES-25938: inicializações: exclusão inesperada após o projeto de tradução.
* SITES-25393: Edge Delivery com Universal Editor: nós de texto perdidos ao renderizar richtext formatado com parágrafo único.
* SITES-24643: Edge Delivery com Universal Editor: os atributos de metadados OpenGraph e twitter não funcionam no modelo de metadados da página.
* SITES-25401: Fragmentos de experiência: atualização lenta da referência XF.

### Problemas conhecidos {#known-issues-18598}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-18598}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-18598}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda 21 vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-18598}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.70.0 | [API Oak API 1.70.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.24-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Componentes principais do AEM | 2.27.0 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
