---
title: Avaliação de integridade para ambientes de produção e preparo
description: Saiba como usar a Avaliação de integridade da Cloud Manager. É possível digitalizar ambientes do AEM, executar e revisar relatórios, exibir detalhes de problemas, exportar PDFs e gerenciar execuções anteriores.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1406'
ht-degree: 7%

---


# Avaliação de integridade {#about-health-assessment}

A Avaliação de integridade é uma verificação automatizada e não invasiva para ambientes de produção e preparo no Cloud Manager dentro do AEM as a Cloud Service. Ele avalia o conteúdo, o código e as configurações para encontrar padrões alternativos e desvios das práticas recomendadas, melhorando a segurança e o desempenho.

O serviço de avaliação de integridade faz o seguinte:

* Verifica ambientes e expõe gargalos de desempenho, ineficiências e riscos.
* Analisa estruturas de conteúdo, como blueprints, live copies e configurações de clientes.
* Detecta dependências desatualizadas, incluindo AEM SDK e bibliotecas de terceiros.
* Sinaliza problemas de qualidade de código, como anotações incorretas e padrões ineficientes.
* Fornece orientação acionável em painéis (por exemplo, Centro de ações).
* Promove a correção proativa para melhorar o desempenho do sistema.

Cada execução lista problemas por gravidade, links para orientação e correções recomendadas e oferece suporte a uma exportação do relatório pelo PDF. Você pode usar o modo de exibição **Relatório Mais Recente** para o estado atual e **Relatórios Anteriores** para comparar execuções.

Consulte também [padrões de Avaliação de Integridade](#ha-patterns) para obter detalhes sobre definições de regras e correção.

## Acessar a página Avaliação de integridade {#access-health-assessment}

1. Entre no Cloud Manager em [experience.adobe.com](https://experience.adobe.com).
1. Na seção **Acesso rápido**, clique em **Experience Manager**.
1. No painel lateral esquerdo, clique em **Cloud Manager**.
1. Selecione a organização desejada. A imagem abaixo serve de ilustração. Selecione o nome da sua própria organização.

   ![Selecionar uma organização no Cloud Manager](/help/implementing/cloud-manager/reports/assets/ha-org.png)

1. No console **Meus Programas**, clique no programa para o qual deseja exibir seu relatório.

1. Siga um destes procedimentos:
   * No cartão **Ambientes**, à direita do nome de um ambiente, clique no ícone ![Reticências ou no ícone Mais](https://spectrum.adobe.com/static/icons/ui_18/More.svg) e escolha **Avaliação de Integridade** no menu.

     ![Selecionando a Avaliação de Integridade no menu de reticências do cartão Ambientes](/help/implementing/cloud-manager/reports/assets/ha-myprograms-environments-card.png)

   * No menu do lado esquerdo, em **Serviços**, clique em ![Ícone de dados](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Ambientes**. Na página Ambientes, à direita do nome de um ambiente, clique no ícone ![Reticências ou no ícone Mais](https://spectrum.adobe.com/static/icons/ui_18/More.svg) e escolha **Avaliação de Integridade** no menu.

     ![Selecionando a Avaliação de Integridade no menu de reticências na página Ambientes](/help/implementing/cloud-manager/reports/assets/ha-environments-page.png)

## Executar um novo relatório para um ambiente selecionado {#run-report}

1. [Acesse a página Avaliação de Integridade](#access-health-assessment).
1. No canto superior direito da página **Avaliação de integridade**, confirme o ambiente de destino que você está prestes a avaliar.

   Se o ambiente estiver incorreto, clique em ![Divisa no menu suspenso para selecionar um ambiente diferente](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) para escolher o ambiente correto na lista.

1. Clique em **Executar relatório**.

   ![Clique no botão Gerar novo relatório na página Avaliação de Integridade](/help/implementing/cloud-manager/reports/assets/ha-run-report.png)

   Enquanto um relatório é executado para o ambiente selecionado, o **Executar Relatório** permanece desabilitado até a conclusão.

   ![Relatório no meio da execução](/help/implementing/cloud-manager/reports/assets/ha-running-report.png)

   Quando o relatório for concluído, ele aparecerá na página **Avaliação de Integridade**, na seção **Relatório Mais Recente**.

## Exibir o relatório mais recente {#view-latest-report}

* Na página **Avaliação de Integridade**, verifique a seção **Último relatório** para obter as seguintes informações:

   * Resultados da execução mais recente.
   * Data e hora de execução.
   * Total de problemas.
   * Destaques das principais questões críticas.
   * Ações: **[Exibir detalhes](#view-report-details)** ou **[Baixar o PDF](#download-pdf-report)** de todos os problemas.

  ![A página Última Avaliação após a geração de um novo relatório para um ambiente selecionado](/help/implementing/cloud-manager/reports/assets/ha-latest-report-page.png)

### Exibir os detalhes mais recentes do relatório {#view-report-details}

* Na página **Avaliação de Integridade**, à direita do título **Último Relatório**, clique no ícone ![Reticências ou Mais](https://spectrum.adobe.com/static/icons/ui_18/More.svg) e em **Exibir detalhes** ou **Download**.

  A opção **Exibir detalhes** mostra o seguinte:

   * Uma lista abrangente de problemas.
   * Capacidade de exibir descobertas e descrições de problemas.
   * Capacidade de exibir a documentação com possíveis correções.

     ![Descrições e descobertas de problemas](/help/implementing/cloud-manager/reports/assets/ha-issue-descriptions-and-findings.png)

   * A opção **Baixar** oferece a capacidade de baixar relatórios de problemas individuais no PDF.

     ![Baixar o PDF de relatórios de problemas individuais](/help/implementing/cloud-manager/reports/assets/ha-details-page-doc-links.png)


### Baixar o PDF de todo o relatório {#download-pdf-report}

* Próximo ao canto superior direito da página do relatório, clique em **Baixar**.

  É gerado um arquivo ZIP que contém PDFs para todos os problemas detectados nesse relatório.

  ![Baixar o PDF de todos os problemas encontrados em um relatório](/help/implementing/cloud-manager/reports/assets/ha-download-pdf.png)


## Revisar relatórios anteriores {#review-past-reports}

Na página **Avaliação de Integridade**, analise a seção **Relatórios Anteriores** para obter as seguintes informações:

* Exibir detalhes de qualquer relatório anterior.
* Exibir a data de cada execução.
* Baixe uma PDF para qualquer relatório.
* Classificar por data, contagem de problemas ou ambiente.

![Revisar relatórios anteriores](/help/implementing/cloud-manager/reports/assets/ha-past-reports.png)

* À direita do cabeçalho **Relatórios Anteriores**, clique na ![Divisa do menu suspenso ou no menu suspenso para selecionar um ambiente diferente](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) para classificar os relatórios anteriores por data.
* Na extremidade direita de um relatório, clique em ![Ícone de reticências ou em Mais ícones](https://spectrum.adobe.com/static/icons/ui_18/More.svg) e em **Exibir detalhes** ou **Baixar**.


## Padrões de avaliação de integridade {#ha-patterns}

Esta é a lista completa de antipadrões e problemas que a Avaliação de integridade detecta no AEM as a Cloud Service. A tabela agrupa itens em três tipos: análise de conteúdo, análise de código e antipadrões do Cloud Service Otimizer, com uma explicação para cada um.

| Nome do padrão | Categoria | Tipo | Descrição | Impacto | Corrigido automaticamente? |
| --- | --- | --- | --- | --- | --- |
| Grupos personalizados do AEM com adições diretas do usuário | Segurança | Análise de conteúdo | Os usuários adicionavam diretamente aos grupos do AEM em vez de adicionar grupos IMS como membros. | O gerenciamento de permissões e a governança de segurança podem se tornar complicados. [Suporte IMS](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/security/ims-support) | Não |
| Nó de conteúdo JCR ausente em páginas | Estrutura do repositório | Análise de conteúdo | Nó `jcr:content` ausente na página. | Limitações funcionais no Experience Manager as a Cloud Service. [Detecção de padrão - ACV](https://experienceleague.adobe.com/pt-br/docs/experience-manager-pattern-detection/table-of-contents/acv) | Não |
| Tipo de recurso Sling ausente em páginas | Estrutura do repositório | Análise de conteúdo | `sling:resourceType` ausente na página. | Limitações funcionais no Experience Manager as a Cloud Service. [Detecção de padrão - ACV](https://experienceleague.adobe.com/pt-br/docs/experience-manager-pattern-detection/table-of-contents/acv) | Não |
| Páginas com contagem excessiva de nós | Desempenho | Análise de conteúdo | As páginas contêm um grande número de nós em sua estrutura. | Tempo de carregamento de página lento e experiência do usuário ruim. [Detecção de padrão - PCX](https://experienceleague.adobe.com/pt-br/docs/experience-manager-pattern-detection/table-of-contents/pcx) | Não |
| Excesso de instâncias de fluxo de trabalho em execução | Desempenho | Análise de conteúdo | Muitas instâncias de fluxo de trabalho estão em execução. | Degradação geral do desempenho do sistema. [Tarefas de manutenção](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/operations/maintenance) | Não |
| Instâncias de fluxo de trabalho concluídas e não removidas | Desempenho | Análise de conteúdo | As instâncias de fluxo de trabalho concluídas mais antigas não estão sendo removidas. | Redução da eficiência do sistema e aumento dos custos de armazenamento. [Tarefas de manutenção](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/operations/maintenance) | Não |
| Estatísticas de uso de fragmentos de conteúdo | Estatísticas | Análise de conteúdo | Rastreia o número de fragmentos de conteúdo em uso. | N/A | N/A |
| Estatísticas de uso do modelo de fragmento de conteúdo | Estatísticas | Análise de conteúdo | Rastreia o número de modelos de fragmento de conteúdo em uso. | N/A | N/A |
| Grande número de blueprints do MSM | Estatísticas | Análise de conteúdo | Rastreia o número de blueprints. | Isso pode aumentar a complexidade do gerenciamento e dificultar o controle de conteúdo. | N/A |
| Páginas MSM por blueprint | Estatísticas | Análise de conteúdo | Rastreia o número de páginas por blueprint. | Isso pode aumentar a complexidade do gerenciamento e dificultar o controle de conteúdo. | N/A |
| Excesso de Live Copies do MSM | Estatísticas | Análise de conteúdo | Rastreia o número de live copies. | Isso pode levar a problemas de desempenho durante implantações e complicar a sincronização do conteúdo. | N/A |
| Live Copies excessivas do MSM por blueprint | Estatísticas | Análise de conteúdo | Rastreia o número de cópias dinâmicas por blueprint. | Isso pode levar a problemas de desempenho durante implantações e complicar a sincronização do conteúdo. | N/A |
| Número de Assets | Estatísticas | Análise de conteúdo | Rastreia o número de ativos. | N/A | N/A |
| Número de sites | Estatísticas | Análise de conteúdo | Rastreia o número de sites. | N/A | N/A |
| Número de Forms | Estatísticas | Análise de conteúdo | Rastreia o número de formulários. | N/A | N/A |
| Fragmentos de formulários | Estatísticas | Análise de conteúdo | Rastreia o número de fragmentos de formulário. | N/A | N/A |
| Comunicações de interação | Estatísticas | Análise de conteúdo | Rastreia o número de interações de comunicação de formulário. | N/A | N/A |
| FDMs | Estatísticas | Análise de conteúdo | Rastreia o número de modelos de dados de formulário. | N/A | N/A |
| Dependências desatualizadas | Dependências | Análise de código | Destaca dependências desatualizadas no repositório do cliente. | Incompatibilidade com versões mais recentes do AEM; possíveis vulnerabilidades de segurança. | Não |
| Incompatibilidade de versão do AEM SDK | Dependências | Análise de código | Versões anteriores a (n-2) em comparação à versão do ambiente do Cloud Manager. | Ele pode causar erros de criação no Cloud Manager e problemas em ambientes de desenvolvimento locais. | Não |
| Dependência do Mockito Core desatualizada | Dependências | Análise de código | As versões anteriores à 4.x.x são consideradas desatualizadas para o AEM as a Cloud Service. | Ele pode causar erros de criação no Cloud Manager e problemas em ambientes de desenvolvimento locais. | Não |
| Anotações não suportadas | Dependências | Análise de código | Anotações incompatíveis no repositório do Cloud Manager do cliente. | Possíveis falhas de aplicativos e desempenho reduzido. | Não |
| Anotação @Inject em modelos Sling | Dependências | Análise de código | Anotação `@Inject` obsoleta. | Desempenho de aplicativo reduzido devido à sobrecarga na resolução de injeção. | Não |
| Solicitações HTTP de saída | Desempenho | Padrões do Cloud Service Otimizer | Uso problemático no contexto da solicitação, tempos limite altos ou conexões não sendo fechadas. | Redução geral do desempenho do sistema e possíveis paralisações. | Sim |
| Consultas lentas | Desempenho | Padrões do Cloud Service Otimizer | Consultas lentas no código do cliente. | Degradação do desempenho do sistema e possíveis tempos limite. | Sim |

### Categorias {#ha-patterns-categories}

| Categoria | Descrição |
| --- | --- |
| Segurança | Padrões relacionados a práticas de segurança, gerenciamento de usuários e controle de acesso. |
| Desempenho | Padrões que afetam o desempenho do aplicativo e do sistema. |
| Estrutura do repositório | Padrões relacionados à organização e estrutura do repositório JCR. |
| Dependências | Padrões relacionados a dependências de código e gerenciamento de versões. |
| Estatísticas | Padrões que representam estatísticas e métricas de uso. |



