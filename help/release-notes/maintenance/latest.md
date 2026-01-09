---
title: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas da versão de manutenção mais recentes do [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: b4df0abb43d69f629d2c643c408cb77af697b942
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 9%

---


# Notas da versão de manutenção {#maintenance-release-notes}

A seção a seguir descreve as notas de versão técnicas para a versão de manutenção atual do Experience Manager as a Cloud Service.

## Versão 23862 {#23862}

>[!CAUTION]
>
> A versão 23862 foi tornada privada. Uma nova versão de manutenção será fornecida em breve.

Veja abaixo um resumo das melhorias contínuas da versão de manutenção 23862, lançada publicamente em quarta-feira, 23 de dezembro de 2025. A versão de manutenção anterior era 23482.

A ativação de recursos do 2026.1.0 fornecerá o conjunto completo de recursos para esta versão de manutenção. Consulte o [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obter mais informações.

### Aprimoramentos {#enhancements-23862}

* CQ-4361812: adição de suporte para param folderPath opcional na api rest. Descrição: Um novo projeto de tradução é criado pela API e será colocado dentro do caminho especificado pelo parâmetro `folderPath` opcional, caso contrário, assumirá como padrão o caminho do projeto raiz `/content/projects`.
* FORMS-21960: adição de suporte para edição de tela no local para Comunicações interativas, semelhante a forms-spa.
* FORMS-22001: adição de orientação para reduzir o alto volume de `/etc.clientlibs/toggles.json` solicitações no AEM Forms as a Cloud Service.
* FORMS-22496: Expor ResponseBody Bruto no Serviço de Chamada.
* FORMS-22495: adicionar a propriedade placeholder na regra SetProperty.
* FORMS-21925: Formatação de notas de rodapé UBS: Exibir todas as notas de rodapé no formulário durante o carregamento do formulário.
* FORMS-20536: Exponha uma opção de resposta completa em eventPayload no editor de regras sem mapeamento.
* SITES-37199: o recurso de anotação aciona a passagem do repositório pela chamada `authorizables.json` não validada, causando degradação de desempenho.
* SITES-37118: Suporte do Commerce Optimizer na ferramenta Cockpit do produto.
* SITES-38029: adicione logs para rastrear eventos de modificação de push do MSM.
* SITES-37050: suporte para &quot;forçar o cancelamento da publicação&quot;, permitindo desfazer a publicação de fragmentos de conteúdo referenciados por outros recursos publicados.
* SITES-37142: adição do recurso para fazer check-in/check-out de um fragmento de conteúdo por meio do fragmento de conteúdo PATCH.
* SITES-37613: No ponto de acesso de permissões da API do CF, retorne o check-in se o usuário puder fazer check-in de um fragmento de conteúdo ou o check-out se o usuário puder fazer check-out de um fragmento de conteúdo.
* SITES-37835: ao tentar criar vários fragmentos de conteúdo com o mesmo título, mas sem nome fornecido, gere automaticamente um novo nome em vez de falhar devido a um conflito.
* SITES-36823: Edge Delivery com Universal Editor: remova a necessidade de mapeamentos reversos para índices.
* SITES-34751: Edge Delivery com Universal Editor: falha para tipos de arquivos não compatíveis e caminhos fora dos limites ao publicar (Acesso antecipado).
* SITES-37888: Edge Delivery com editor universal: use o sufixo Alt como sinônimo de Texto para links.
* SITES-19850: Edge Delivery com Universal Editor: adicionar suporte para várias planilhas em planilhas.
* SITES-32490: Edge Delivery com Universal Editor: adicionar suporte para data-aue-component e data-aue-label definido pelo usuário para blocos e conteúdo padrão.
* SITES-37794: Edge Delivery com Universal Editor: assistente de criação de página simplificada.
* SITES-36963: Migrar endpoint de público-alvo/segmento para a API v3 do Target para suporte do Workspace.

### Problemas corrigidos {#fixed-issues-23862}

* CQ-4361831: o problema corrigido que causava genai_dropdown_span não está definido.
* CQ-4360895: correção da contagem de status de trabalho de tradução imprecisa no projeto durante atualizações simultâneas.
* CQ-4361599: correção de ignorar Fragmentos de conteúdo de Trabalhos de tradução após a atualização de 2025.7.
* CQ-4360747: trabalhos de tradução repetíveis corrigidos criam cargas vazias e acionam com muita frequência (NullPointerException em ScheduleRepeatTranslationProject).
* CQ-4359994: correção de inconsistência de tipo de campo destinationLanguage para projeto único e multilíngue.
* SITES-38153: corrija o provedor de referência de publicação cf para referências baseadas em uuid.
* SITES-37594: melhorias de desempenho para a funcionalidade de modelo por tags.
* SITES-37337: FragmentCreateProcessor: forneça detalhes adicionais do erro nos logs.
* SITES-33666: mensagem de erro &quot;Não é possível imprimir o Json do fragmento&quot; deslocalizada no Editor de fragmento de conteúdo.
* SITES-33675: sequência de caracteres &quot;indefinida&quot; codificada no Editor de fragmentos de conteúdo > Conteúdo associado.
* SITES-30715: cadeia de caracteres &quot;Geral&quot; não localizada no Editor de fragmento de conteúdo.
* SITES-28592: cadeias de caracteres não localizadas no Editor de modelo de fragmento de conteúdo > Caixa de diálogo &quot;O modelo está bloqueado&quot;.
* SITES-977: as cadeias de caracteres &quot;Tags&quot; e &quot;coleções&quot; não são localizadas na página Editar fragmento de conteúdo.
* SITES-29699: tipos não localizados de ativos permitidos no Editor de fragmento de conteúdo.
* SITES-25240: os campos do Call to action no modal do teaser não têm um rótulo visível.
* SITES-24869: Dica de ferramenta truncada no Editor de modelo > Separador > Política.
* SITES-19313: o erro é deslocalizado ao arrastar e soltar um componente para o modelo excluído no Editor de modelo.
* SITES-18103: strings não localizadas no Editor de páginas > Fluxo de trabalho.
* SITES-17501: cadeias de caracteres não localizadas no Editor de modelos > Editor de política de componentes.
* SITES-15091: as cadeias de caracteres são deslocalizadas nas propriedades do componente de texto do Fragmento de experiência.
* SITES-8113: A cadeia de caracteres &#39;Assets&#39; não está localizada na caixa de diálogo &#39;Selecionar imagem&#39; para &#39;Modelos&#39; no menu Ferramentas.
* SITES-37587: a criação da Live Copy ainda falha no PROD com NPE em RolloutManagerImpl.
* SITES-37335: propriedades de página da Live Copy mostrando erro no console relacionado às tags cq.
* SITES-36972: O botão &quot;Implantação&quot; não aparece na barra de ferramentas editável.
* SITES-36570: a criação de Live Copies falha depois que o botão Criar Live Copy fragmentado é ativado.
* SITES-36158: falha na implantação com o trabalho devido a uma exceção.
* SITES-35655: o novo editor de CF mostra a herança ativa após sua quebra.
* SITES-31425: Mensagem de erro não localizada `Error: {} field is required` exibida no fluxo de trabalho Iniciar em sites.
* SITES-19802: as dicas de ferramentas são deslocalizadas em Site dos componentes principais > Índice.
* SITES-36543: correção de um problema que permitia ao administrador editar fragmentos de conteúdo com check-out.
* SITES-36967: NullPointerExceptions corrigidas que ocorrem ao tentar gerar dados de miniatura para fragmentos de conteúdo corrompidos.
* SITES-37791: correção de um problema em que a chamada de FindAndReplace para cadeias de caracteres contendo `$` falhava.
* SITES-37018: Pop-up de erro vazio ao copiar a página com o caminho de modelo não permitido.
* SITES-36243: Edge Delivery com Universal Editor: corrigir 404s ao publicar `sling:OrderedFolder`.
* SITES-37684: Edge Delivery com Universal Editor: corrija a degradação do desempenho em ambientes com muitos sites.
* SITES-37840: Edge Delivery com Universal Editor: corrija falhas de publicação devido a token de acesso desatualizado do Edge Delivery.
* SITES-37933: Edge Delivery com Universal Editor: corrigir (des)falhas de publicação de recursos excluídos em inicializações.
* SITES-37870: Edge Delivery com Universal Editor: corrija a renderização corrompida de metadados de página personalizados com suporte a vários campos ativado.
* SITES-37349: Edge Delivery com Universal Editor: renderiza vários campos com entradas únicas como uma lista com um único item de lista.
* SITES-36148: Edge Delivery com editor universal: corrija o rótulo de uso de dados para vários campos compostos.

### Problemas conhecidos {#known-issues-23862}

Nenhum.

### Recursos e APIs obsoletos {#deprecated-23862}

Os recursos e APIs obsoletos e removidos do AEM as a Cloud Service estão detalhados no documento [Recursos e APIs obsoletos e removidos](/help/release-notes/deprecated-removed-features.md).

### Correções de segurança {#security-23862}

A AEM as a Cloud Service dedica-se a otimizar a segurança e o desempenho da sua plataforma. Esta versão de manutenção aborda 23 vulnerabilidades identificadas, reforçando nosso compromisso com a proteção robusta do sistema.

### Tecnologias integradas {#embedded-tech-23862}

| Tecnologia | Versão | Link |
|---|---|---|
| AEM Oak | 1.88.0 | [API do Oak 1.88.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.88.0/index.html) |
| API DO SLING DO AEM | 2.27.6 | [API Apache Sling API 2.27.6](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| HTL do AEM | 1.4.28-1.4.0 | [Especificação da linguagem de modelo HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principais do AEM | 2.30.2 | [Componentes principais de WCM do AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (padrão) | [Versões Node.js com suporte](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
