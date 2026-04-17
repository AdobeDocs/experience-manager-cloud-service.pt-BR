---
title: Desenvolvimento local com ferramentas de IA
description: Saiba como configurar ferramentas de codificação de IA com contexto de projeto, habilidades de agente e servidores MCP para acelerar o desenvolvimento do AEM as a Cloud Service.
feature: Developing
role: Developer
exl-id: 09d6257d-36ad-49e5-831f-c44b356f1800
source-git-commit: f7a46a5b8c5bbe30ab5d6828ba99b2435b88dbeb
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 0%

---

# Desenvolvimento local com ferramentas de IA {#local-development-with-ai-tools}

>[!IMPORTANT]
>
>Os recursos descritos neste artigo são **beta**. Obter acesso antecipado aos recursos que a Adobe está desenvolvendo permite que clientes e parceiros forneçam feedback (ao enviar um email para [aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)) e aperfeiçoem o produto. Também os ajuda a se preparar para adotar novos recursos antes da disponibilidade geral.
>
>As versões do Beta podem conter defeitos e são fornecidas &quot;NO ESTADO EM QUE SE ENCONTRAM&quot; sem garantias de nenhum tipo. A Adobe não tem nenhuma obrigação de manter, corrigir, atualizar, alterar, modificar ou oferecer suporte (por meio dos Serviços de suporte da Adobe ou de outra forma) às versões beta. A Adobe recomenda que os clientes tenham cuidado e não dependam do funcionamento ou do desempenho correto das versões beta, nem de qualquer documentação ou material que as acompanhe. Os recursos e as APIs na versão beta estão sujeitos a alterações sem aviso prévio. Portanto, qualquer uso das versões beta é de inteira responsabilidade do cliente.

>[!NOTE]
>
>Este artigo se concentra no Desenvolvimento local com ferramentas de IA para o **desenvolvimento de pilha Java do AEM**. Para o Edge Delivery Services, consulte [Desenvolvimento com Ferramentas de IA](https://www.aem.live/developer/ai-coding-agents).

Os agentes de codificação de IA (Claude Code, Cursor, GitHub Copilot e ferramentas semelhantes) têm amplo conhecimento das tecnologias subjacentes da AEM (Java, OSGi, Sling, JCR, HTL), mas não conhecem necessariamente as práticas recomendadas para gerar código e configuração ou como depurar problemas comuns de desenvolvimento do AEM.

Quatro componentes complementares abordam esta questão:

| Componente | Propósito |
|---|---|
| **AGENTS.md** | Um arquivo de contexto específico do projeto que baseia a IA no projeto do AEM Cloud Service para cada sessão |
| **Habilidades do agente** | Conjuntos de instruções reutilizáveis para tarefas de desenvolvimento recorrentes, como criação de componentes e configuração do Dispatcher |
| **Servidor MCP local do AEM Quickstart** | Expõe dados em tempo de execução em tempo real de uma instância local do AEM SDK para oferecer suporte à solução de problemas |
| **Servidor MCP local do Dispatcher** | Habilita a validação e a inspeção em tempo de execução de uma instância local do Dispatcher |

>[!NOTE]
>
> Também úteis para o desenvolvimento local, mas não abordados neste artigo, são os servidores MCP remotos do AEM Cloud Service. Saiba mais sobre eles no [artigo Uso do MCP com o Cloud Service](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md).

## AGENTS.md {#agentsmd}

`AGENTS.md` é um arquivo do Markdown na raiz do seu projeto do AEM que as ferramentas de codificação de IA carregam automaticamente no início de cada sessão para serem baseadas no conhecimento essencial de domínio da pilha de Java do AEM Cloud Service (e não em outras soluções da AEM, como o AEM 6.5 ou Edge Delivery Services).

`AGENTS.md` não é um arquivo estático copiado — ele é gerado pela habilidade `ensure-agents-md` descrita na próxima seção. A habilidade lê o `pom.xml` para resolver o nome do projeto, descobrir módulos e detectar complementos instalados, produzindo um arquivo adaptado ao seu projeto específico.

>[!NOTE]
>
>Quando `AGENTS.md` existir na raiz do projeto, a habilidade `ensure-agents-md` não será mais executada. Edite o arquivo diretamente se a estrutura do projeto mudar.

## Habilidades do agente {#agent-skills}

Habilidades são conjuntos de instruções que codificam fluxos de trabalho de desenvolvimento de várias etapas. Quando invocada, a IA segue o procedimento da habilidade, em vez de depender apenas do conhecimento geral, produzindo resultados consistentes e compatíveis com a convenção.

O Adobe publica habilidades do AEM as a Cloud Service no repositório **[adobe/skills](https://github.com/adobe/skills/tree/beta/skills/aem/cloud-service/skills)** na ramificação `beta`, pois esse recurso ainda não está disponível:

| Habilidade | Propósito |
|---|---|
| `ensure-agents-md` | Inicializações `AGENTS.md` e `CLAUDE.md` ajustadas à estrutura do módulo real do projeto |
| `create-component` | Os scaffolds são um componente completo do AEM: definição de componentes, XML da caixa de diálogo, modelo HTL, modelo Sling, testes de unidade e clientlibs |
| `dispatcher` | Assistente de configuração Dispatcher e Apache HTTPD alimentado por IA, que abrange criação de configuração, consultoria técnica, resposta a incidentes, ajuste de desempenho e fortalecimento de segurança |
| `workflow` | Ponto de entrada único para todas as habilidades do AEM as a Cloud Service Workflow. Abrange o design do modelo de fluxo de trabalho, a etapa de processo personalizada e o desenvolvimento do seletor de participantes, a configuração do iniciador, o acionamento do fluxo de trabalho e o suporte à produção, incluindo a depuração de fluxos de trabalho travados/com falha, a triagem de incidentes com logs do Cloud Manager, a análise do pool de threads e o diagnóstico de Sling Job para o Mecanismo de fluxo de trabalho do Granite. |

### Instalar habilidades {#install-skills}

Escolha o método que corresponde à ferramenta de codificação de IA. Instalar as habilidades uma vez as disponibiliza para todos os projetos nessa máquina.

#### código Claude {#claude-code}

```bash
# Add the Adobe Skills marketplace (one-time setup)
/plugin marketplace add adobe/skills

# Install all available skills
/plugin install aem-cloud-service@adobe-skills
```

#### Habilidades Npx {#npx-skills}

```bash
# Install all available skills
npx skills add https://github.com/adobe/skills/tree/main/skills/aem/cloud-service --all
```

#### Aprimoramento (extensão CLI do GitHub) {#upskill-github-cli-extension}

```bash
# Install the gh-upskill extension (one-time setup)
gh extension install ai-ecoverse/gh-upskill

# Install all available skills
gh upskill adobe/skills --path skills/aem/cloud-service --all
```

### Usar a habilidade sure-agents-md {#use-the-ensure-agents-md-skill}

Após instalar a habilidade, abra o assistente de IA em qualquer projeto do AEM Cloud Service que ainda não tenha um `AGENTS.md`. A habilidade é executada automaticamente antes do processamento da primeira solicitação, criando ambos os arquivos na raiz do projeto sem a necessidade de chamada explícita.

### Usar a habilidade create-component {#use-the-create-component-skill}

Na primeira utilização, a habilidade detecta automaticamente `project`, `package` e `group` de `pom.xml` e componentes existentes, solicita sua confirmação dos valores detectados e cria `.aem-skills-config.yaml` na raiz do projeto. Nenhuma configuração manual é necessária antes da primeira utilização.

Se preferir pré-criar o arquivo, coloque `.aem-skills-config.yaml` na raiz do projeto com a seguinte estrutura:

```yaml
configured: true

project: "wknd"                                    # Check /apps/{project}/ or pom.xml
package: "com.adobe.aem.guides.wknd.core"          # Check core/pom.xml
group: "WKND Components"                           # Check existing component .content.xml files
```

O arquivo fica fora do diretório de habilidades e nunca é substituído quando a habilidade é atualizada.

Descreva o componente no bate-papo de IA:

```
Create an AEM component called "Hero Banner"

Dialog specification:
Title (title) - Textfield, mandatory
Subtitle (subtitle) - Textfield
Background Image (backgroundImage) - Fileupload
CTA Text (ctaText) - Textfield
CTA Link (ctaLink) - Pathfield
```

O agente ecoa a especificação do campo para confirmação e, em seguida, gera todos os arquivos de componente. Os padrões compatíveis incluem vários campos com itens aninhados compostos, lógica condicional de mostrar/ocultar, extensão do Componente principal por meio do Sling Resource Merger e testes JUnit 5 usando AEM Mocks.

### Usar a habilidade do Dispatcher {#use-the-dispatcher-skill}

Chame a habilidade do dispatcher para qualquer trabalho de configuração HTTPD do Dispatcher ou Apache. As solicitações de rotas de habilidades para uma das seis sub-habilidades especializadas, dependendo da natureza da solicitação:

| Sub-habilidade | Propósito |
|---|---|
| `workflow-orchestrator` | Trabalho completo abrangendo design, alterações de configuração, validação e acompanhamento |
| `config-authoring` | Alterações de configuração concretas: filtros, regras de cache, regravações, vhosts, cabeçalhos e farms |
| `technical-advisory` | Orientação conceitual, explicação de políticas e recomendações baseadas em citações |
| `incident-response` | Falhas de tempo de execução, anomalias de cache e regressões |
| `performance-tuning` | Eficiência de cache, latência e otimização de throughput |
| `security-hardening` | Análise da exposição e fortalecimento da produção |

Para solicitações amplas ou iniciadas, comece com a subhabilidade `workflow-orchestrator`. Para trabalho direcionado, descreva a preocupação específica e as rotas de habilidades para o especialista apropriado.

A habilidade do dispatcher lida com orquestração e orientação de consultoria. O servidor MCP do Dispatcher, descrito abaixo, fornece as sete ferramentas de validação e tempo de execução que a habilidade usa quando precisa de evidências locais.

## AEM Quickstart MCP Server {#aem-quickstart-mcp-server}

O Protocolo de contexto de modelo (MCP) é um padrão aberto que permite que as ferramentas de codificação de IA se conectem a fontes de dados e serviços externos. O servidor MCP AEM Quickstart é um pacote de conteúdo que, uma vez instalado em uma instância local do AEM SDK, expõe os dados de tempo de execução diretamente às ferramentas de IA conectadas, permitindo que os agentes recuperem registros, diagnostiquem falhas de OSGi e inspecionem o processamento de solicitações sem sair do IDE.

### Instalar o pacote de conteúdo {#install-the-content-package}

Baixe o pacote de conteúdo do [Portal de Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=mcp*&1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=software-type%3Atooling&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=3) e instale o `com.adobe.aem:com.adobe.aem.mcp-server-contribs-content` no Quickstart local usando o Gerenciador de Pacotes em `/crx/packmgr`.

**Compatibilidade:** validada com AEM SDK `2026.2.24678.20260226T154829Z-260200` e mais recente.

### Ferramentas disponíveis {#available-tools}

| Ferramenta  | Descrição |
|---|---|
| `aem-logs` | Recupera entradas de log do AEM e do OSGi, filtráveis por padrão regex, nível de log e contagem de entradas |
| `diagnose-osgi-bundle` | Diagnostica por que um pacote ou componente DS não está sendo iniciado; relata pacotes ausentes, referências não satisfeitas e problemas de configuração |
| `recent-requests` | Retorna solicitações HTTP recentes com o rastreamento de processamento interno completo do Sling (resolução de recursos, resolução de scripts, cadeia de filtros), filtrável por regex de caminho |

### Configurar o IDE {#configure-your-ide}

#### Cursor {#cursor}

Em Configurações do Cursor, adicione um novo servidor MCP personalizado:

```json
"aem-cs-sdk": {
  "type": "streamable-http",
  "url": "http://localhost:4502/bin/mcp",
  "headers": {
    "Authorization": "Basic YWRtaW46YWRtaW4="
  }
}
```

#### GitHub Copilot com IntelliJ IDEA {#github-copilot-with-ihtellij-idea}

Navegue até **Ferramentas > GitHub Copilot > Protocolo de Contexto de Modelo (MCP)** e clique em **Configurar**. Adicionar:

```json
"aem-cs-sdk": {
  "url": "http://localhost:4502/bin/mcp",
  "requestInit": {
    "headers": {
      "Authorization": "Basic YWRtaW46YWRtaW4="
    }
  }
}
```

#### Outras IDEs {#other-ides}

Qualquer cliente MCP pode se conectar apontando para `http://localhost:4502/bin/mcp` com um cabeçalho `Authorization: Basic YWRtaW46YWRtaW4=`. Configure cabeçalhos personalizados usando as configurações de MCP do IDE.

>[!NOTE]
>
>O valor `Basic YWRtaW46YWRtaW4=` é a codificação Base64 de `admin:admin`, a credencial padrão para um Quickstart local. Não use com ambientes não locais.

## Dispatcher MCP Server {#dispatcher-mcp-server}

O servidor Dispatcher MCP é fornecido com o AEM Dispatcher SDK. Ela permite que as ferramentas de IA validem a configuração HTTPD do Dispatcher e do Apache, rastreiem a manipulação de solicitações e inspecionem o comportamento do cache em relação a uma instância do Dispatcher executada localmente no Docker.

Ao contrário da habilidade do dispatcher, o servidor MCP do Dispatcher expõe apenas ferramentas: sete ferramentas MCP e nenhum prompt ou recurso.

### Pré-requisitos {#prerequisites}

- Docker Desktop 4.x ou posterior, instalado e em execução
- AEM Dispatcher SDK baixado do [Portal de distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=mcp*&1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=software-type%3Atooling&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=3)

>[!NOTE]
>
>Se você vir `client version 1.43 is too new`, defina `DOCKER_API_VERSION=1.41` em seu shell ou em `mcp.json`.

### Instalar o Dispatcher SDK {#install-the-dispatcher-sdk}

**macOS e Linux:**

```bash
chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
./aem-sdk-dispatcher-tools-<version>-unix.sh
cd dispatcher-sdk-<version>
chmod +x ./bin/docker_run_mcp.sh
./bin/docker_run_mcp.sh test
```

**Janelas:**

```powershell
Expand-Archive aem-sdk-dispatcher-tools-<version>-windows.zip
```

Execute `./bin/docker_run_mcp.sh help` para recuperar a configuração do IDE de copiar e colar e `./bin/docker_run_mcp.sh version` para confirmar a versão do MCP e do SDK agrupados. Use `./bin/docker_run_mcp.sh diagnose` para investigar problemas de conectividade.

### Configurar o cursor {#configure-cursor}

Adicionar uma entrada `aem-dispatcher-mcp` a `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "aem-dispatcher-mcp": {
      "command": "<path_to_dispatcher_sdk>/bin/docker_run_mcp.sh",
      "env": {
        "DOCKER_API_VERSION": "1.43",
        "AEM_DEPLOYMENT_MODE": "cloud",
        "MCP_LOG_LEVEL": "trace",
        "MCP_LOG_FILE": "/tmp/dispatcher-mcp.log",
        "DISPATCHER_CONFIG_PATH": "<path_to_dispatcher_src>"
      }
    }
  }
}
```

Substitua `<path_to_dispatcher_sdk>` pelo local extraído do Dispatcher SDK e `<path_to_dispatcher_src>` pelo diretório `src` do Dispatcher do projeto. Defina `DISPATCHER_CONFIG_PATH` para a raiz de configuração que inclui os arquivos em que `/docroot` está definido. `MCP_LOG_LEVEL` e `MCP_LOG_FILE` são configurações opcionais de depuração. Se você vir `client version 1.43 is too new`, defina `DOCKER_API_VERSION` como `1.41`. Se outros servidores MCP já estiverem configurados, adicione a entrada `aem-dispatcher-mcp` sem substituí-los. Reiniciar o cursor após salvar.

Outros IDEs podem ser configurados de maneira semelhante. O `docs/DispatcherMCP.md` do SDK inclui exemplos completos para Claude Desktop e o Código VS.

### Ferramentas disponíveis {#available-tools-dispatcher}

| Ferramenta  | Descrição |
|---|---|
| `validate` | Valida as configurações HTTPD do Dispatcher e Apache |
| `lint` | Executa verificações estáticas com reconhecimento de modo e análise de práticas recomendadas |
| `sdk` | Executa fluxos de trabalho do Dispatcher SDK: `validate`, `validate-full`, `three-phase-validate`, `docker-test`, `check-files`, `diff-baseline` |
| `trace_request` | Rastreia o comportamento da solicitação com evidência de tempo de execução |
| `inspect_cache` | Inspeciona o comportamento do cache e do docroot para um URL de destino |
| `monitor_metrics` | Lê métricas de tempo de execução de logs Dispatcher e HTTPD |
| `tail_logs` | Rastreia logs relevantes de tempo de execução do Dispatcher e HTTPD |

A superfície MCP expõe intencionalmente apenas essas sete ferramentas; as instruções e os recursos permanecem na camada de habilidade. A documentação de referência completa está disponível em `docs/DispatcherMCP.md` dentro do SDK extraído do Dispatcher.
