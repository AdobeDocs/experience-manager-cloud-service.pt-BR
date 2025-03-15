---
title: APIs de comunicação do AEM Forms as a Cloud Service
description: Gerar, manipular e proteger documentos com APIs de comunicação da AEM Forms na nuvem
Keywords: document generation, PDF manipulation, document security, batch processing, document conversion, PDF/A compliance
feature: Adaptive Forms, APIs & Integrations, Document Services
role: Admin, Developer, User
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: a9eed5b6219163e721d81c9d77a31604666a2ac5
workflow-type: tm+mt
source-wordcount: '1432'
ht-degree: 3%

---


# APIs de comunicação do AEM Forms as a Cloud Service {#communications-apis-overview}

> **Disponibilidade de Versão**
>
> * **AEM 6.5**: [Visão Geral dos Serviços de Documento da AEM](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/overview-aem-document-services.html)
> * **AEM as a Cloud Service**: Este artigo

## Introdução

As APIs de comunicação no AEM Forms as a Cloud Service ajudam você a criar documentos aprovados pela marca, personalizados e padronizados para as necessidades de sua empresa. Essas APIs avançadas permitem gerar, manipular e proteger documentos programaticamente, seja sob demanda ou em processos em lote de alto volume.


### Principais benefícios

* **Geração de documentos simplificada** - Crie documentos personalizados mesclando modelos com dados do cliente
* **Manipulação poderosa de documentos** - Combine, reorganize e valide documentos do PDF de forma programática
* **Opções de implantação flexíveis** - Use APIs sob demanda para necessidades de baixa latência ou APIs em lote para operações de alta taxa de transferência
* **Segurança avançada** - Aplique assinaturas digitais, certificação e criptografia para proteger documentos confidenciais
* **Arquitetura nativa em nuvem** - Aproveite a infraestrutura de nuvem escalável e segura sem sobrecarga de manutenção

## Principais recursos

As APIs de comunicação fornecem um conjunto abrangente de recursos de processamento de documentos organizados nas seguintes áreas funcionais:


| Geração de documentos | Manipulação de documentos | Extração de documento | Conversão de documentos | Assurance do documento |
|---------------------|----------------------|---------------------|---------------------|-------------------|
| Gerar documentos personalizados mesclando modelos com dados em vários formatos, incluindo formatos de PDF e impressão. | Combine, reorganize e valide documentos do PDF de forma programática para criar novos pacotes de documentos. | Extraia propriedades, metadados e conteúdo dos documentos do PDF para processamento adicional. | Converter documentos entre formatos, incluindo validação de conformidade PDF/A para necessidades de arquivamento. | Aplique assinaturas digitais, certificação e criptografia para proteger documentos. |

## Geração de documentos

As APIs de geração de documentos de comunicação combinam modelos (XFA ou PDF) com dados do cliente (XML) para criar documentos personalizados no PDF e em vários formatos de impressão (PS, PCL, DPL, IPL, ZPL).

### Como funciona a geração de documentos

O fluxo de trabalho típico envolve:

1. Criando um modelo usando o [Designer](use-forms-designer.md)
2. Preparando dados XML para preencher o modelo
3. Utilização de APIs de comunicações para mesclar o modelo com os dados
4. Gerar documentos de saída no formato desejado

![Fluxo de trabalho de geração de documentos de comunicações](assets/communicaions-workflow.png)

### Criar documentos do PDF

As APIs de geração de documentos permitem criar documentos não interativos do PDF mesclando dados XML com modelos de formulário:

![Criar documentos do PDF](assets/outPutPDF_popup.png)

Você pode entregar os PDFs gerados aos usuários por meio de downloads, armazená-los em um repositório ou, opcionalmente, carregá-los no Armazenamento de blobs do Azure.

<span class="preview">O carregamento de PDFs gerados para o Armazenamento Azure Blob está disponível por meio do [Programa Early Adoter](/help/forms/early-access-ea-features.md). Entre em contato com aem-forms-ea@adobe.com pelo seu email oficial para participar.</span>

### Criar Documentos de Formato de Impressão

Gerar documentos em formatos de impressão incluindo:
* PostScript (PS)
* PCL (Idioma de Comando da Impressora)
* Linguagem de impressão de zebra (ZPL)

Esses formatos são ideais para operações de impressão de alto volume e necessidades de impressão especializadas.

### Processamento em lote para vários documentos

Processar grandes volumes de documentos com eficiência usando APIs em lote:

![Fluxo de Trabalho de Processamento em Lote](assets/ou_OutputBatchMany_popup.png)

O processamento em lote permite:

* Gerar documentos separados para cada registro em uma fonte de dados XML
* Processar documentos de forma assíncrona para melhorar o desempenho
* Configurar vários parâmetros de conversão para o processo em lote

## Manipulação de documentos

As APIs de manipulação de documentos ajudam a combinar, reorganizar e transformar documentos do PDF de forma programática.

### Montagem do documento

Combine vários documentos PDF ou XDP em um único documento coeso:

![Montando um documento PDF simples a partir de vários documentos PDF](assets/as_document_assembly.png)

Os recursos de montagem de documento incluem:
* Criação de documentos simples do PDF a partir de várias fontes
* Criação de portfólios do PDF
* Montagem de documentos criptografados
* Adição de numeração de Bates para documentos legais
* Nivelamento e montagem de formulários interativos

### Desmontagem do documento

Divida documentos grandes do PDF em componentes menores e mais gerenciáveis:

![Dividindo um documento de origem com base em marcadores em vários documentos](assets/as_intro_pdfsfrombookmarks.png)

A desmontagem de documento permite:
* Extrair páginas específicas dos documentos de origem
* Dividir documentos com base em marcadores
* Criar conjuntos de documentos lógicos a partir de compilações maiores

>[!NOTE]
>
> O AEM Forms inclui muitas fontes integradas que se integram perfeitamente aos arquivos PDF. Para obter uma lista completa das fontes com suporte, [clique aqui](/help/forms/supported-out-of-the-box-fonts.md).

## Extração de documento

A <span class="preview">Extração de documentos está disponível por meio do [Early Adoter Program](/help/forms/early-access-ea-features.md). Entre em contato com aem-forms-ea@adobe.com pelo seu email oficial para participar.</span>

As APIs de extração de documentos permitem recuperar informações de documentos do PDF, incluindo:

* Propriedades do documento (é um formulário preenchível, tem anexos etc.)
* Direitos e permissões de uso
* Informações de metadados usando a Adobe Extensible Metadata Platform (XMP)

Esse recurso é particularmente útil para sistemas de gerenciamento de documentos, soluções de arquivamento e automação de fluxo de trabalho.

## Conversão de documentos

### Conversão e validação do PDF/A

Converta documentos padrão do PDF em formato PDF/A para fins de arquivamento de longo prazo:

* Suporte para padrões de conformidade PDF/A-1a, 1b, 2a, 2b, 3a e 3b
* Validação da conformidade com o PDF/A
* Preservação da integridade do documento com fontes incorporadas e conteúdo descompactado

### Conversão do PDF em XDP

A <span class="preview">conversão de PDF em XDP está disponível por meio do [Early Adoter Program](/help/forms/early-access-ea-features.md). Entre em contato com aem-forms-ea@adobe.com pelo seu email oficial para participar.</span>

Converta documentos do PDF que contêm fluxos XFA em formato XDP para edição e reutilização de modelos.

## Assurance do documento {#doc-assurance}

O Document Assurance inclui APIs de assinatura e criptografia para proteger seus documentos durante todo o ciclo de vida.

### APIs de assinatura

Proteja documentos do PDF com assinaturas digitais e certificação:

* Adicionar campos de assinatura visíveis ou invisíveis
* Assinar digitalmente campos de assinatura
* Certificar documentos para integridade
* Remover assinaturas de documentos
* Excluir campos de assinatura de documentos

<span class="preview">A remoção da assinatura e a exclusão do campo de assinatura estão disponíveis por meio do [Programa Early Adoter](/help/forms/early-access-ea-features.md). Entre em contato com aem-forms-ea@adobe.com pelo seu email oficial para participar.</span>

### APIs de criptografia

Proteger o conteúdo de documentos com criptografia:

* Criptografar documentos do PDF com senhas
* Remover criptografia baseada em senha
* Determinar os tipos de segurança aplicados aos documentos
* Recuperar informações de segurança de documentos protegidos

### Utilitários de documento {#doc-utility}

Os utilitários de documento fornecem funcionalidade adicional para trabalhar com documentos do PDF:

#### APIs de direitos de uso (extensão do Reader)

<span class="preview">Direitos de Uso (Extensão do Reader) estão disponíveis por meio do [Programa de Primeiros Adotores](/help/forms/early-access-ea-features.md). Entre em contato com aem-forms-ea@adobe.com pelo seu email oficial para participar.</span>

Estender a funcionalidade do Adobe Reader adicionando direitos de uso a documentos do PDF, habilitando recursos como:

* Preenchimento e salvamento de formulário
* Adição de comentários e anotações
* Assinatura digital
* Anexos de arquivo
* Importação/exportação de dados do formulário
* Acesso a serviços da Web e bancos de dados

Os direitos de uso disponíveis incluem:

* **Interação De Formulário**: Preenchimento De Formulário, Importação/Exportação De Dados De Formulário, Campos/Páginas De Formulário Dinâmico
* **Anotações**: Comentários (online e offline), Assinaturas digitais
* **Manuseio De Documentos**: Arquivos Inseridos, Enviar Autônomo, Decodificação De Códigos De Barras
* **Serviços Online**: Forms Online, acesso a serviços Web

## Tipos de APIs de comunicações {#types}

As comunicações fornecem dois tipos de APIs para atender a casos de uso diferentes:

### APIs síncronas

**Recomendado para**: geração de documentos únicos sob demanda, de baixa latência
**Casos de uso**: geração de documentos acionada pelo usuário, aplicativos interativos
**Documentação**: [Referência de API síncrona](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)

### APIs em lote (assíncrono)

**Recomendado para**: geração agendada de vários documentos com alta taxa de transferência
**Casos de uso**: extratos mensais, contas, avisos, relatórios agendados
**Documentação**: [Referência da API de lote](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)

## Introdução às APIs de comunicações

### Processo de integração

A comunicação está disponível como um módulo independente ou complemento para os usuários do Forms as a Cloud Service:

1. Entre em contato com o setor de Vendas da Adobe ou com seu representante da Adobe para solicitar acesso
2. A Adobe habilitará o acesso para sua organização e concederá privilégios de administrador
3. Seu administrador pode conceder acesso aos desenvolvedores em sua organização

### Habilitando comunicações no seu ambiente

Siga estas etapas para habilitar as Comunicações para o seu ambiente do Forms as a Cloud Service:

1. Faça logon no Cloud Manager e abra sua instância do AEM Forms as a Cloud Service
2. Abra a opção Editar programa e acesse a guia Soluções e complementos
3. Selecione a opção **[!UICONTROL Forms - Comunicações]**

   ![Comunicações](assets/communications.png)

   Se você já tiver habilitado o **[!UICONTROL Forms - Inscrição Digital]**, selecione a opção **[!UICONTROL Forms - Complemento de Comunicações]**.

   ![Complementos](assets/add-on.png)

4. Clique em **[!UICONTROL Atualizar]**
5. Executar o pipeline de compilação - As APIs de comunicações serão habilitadas após a conclusão bem-sucedida

>[!NOTE]
>
> Para habilitar APIs de manipulação de documentos, adicione a seguinte regra à sua [configuração do Dispatcher](setup-local-development-environment.md#forms-specific-rules-to-dispatcher):
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

## Documentação de referência da API {#api-reference}

As APIs de comunicações são organizadas em várias categorias funcionais, cada uma com documentação de referência detalhada. Essas referências de API fornecem informações abrangentes sobre endpoints, parâmetros, formatos de solicitação/resposta e requisitos de autenticação.

### APIs de geração de documento

| API | Descrição | Link de referência |
|-----|-------------|----------------|
| Geração de documentos - Síncrona | Gerar documentos sob demanda com baixa latência para cenários interativos | [Referência da API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/) |
| Geração de documento - Lote | Processar grandes volumes de documentos de forma assíncrona para operações programadas | [Referência da API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/) |

### APIs de manipulação de documentos

| API | Descrição | Link de referência |
|-----|-------------|----------------|
| Manipulação de documentos - Síncrona | Combinar, dividir e transformar documentos do PDF usando instruções DDX | [Referência da API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/) |

### Documentar APIs do Assurance

| API | Descrição | Link de referência |
|-----|-------------|----------------|
| DocAssurance - Síncrono | Aplicar assinaturas digitais, certificação, criptografia e extensões de leitores | [Referência da API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/docassurance/) |

### Parâmetros comuns da API

Cada categoria de API tem parâmetros específicos, mas alguns parâmetros comuns incluem:

#### Parâmetros de geração de documento

| Parâmetro | Tipo | Obrigatório | Descrição |
|-----------|------|----------|-------------|
| `template` | String | Sim | Caminho para o arquivo de modelo XDP ou PDF |
| `data` | String | Não | Dados XML a serem mesclados com o modelo |
| `outputOptions` | Objeto | Não | Opções de configuração para o documento de saída |

#### Parâmetros de manipulação de documentos

| Parâmetro | Tipo | Obrigatório | Descrição |
|-----------|------|----------|-------------|
| `ddx` | String | Sim | Instruções do DDX para montagem ou desmontagem de documentos |
| `inputDocuments` | Objeto | Sim | Mapa de documentos de entrada a serem processados |
| `outputOptions` | Objeto | Não | Opções de configuração para o documento de saída |

#### Parâmetros do Assurance do documento

| Parâmetro | Tipo | Obrigatório | Descrição |
|-----------|------|----------|-------------|
| `inputPDF` | String | Sim | Documento PDF de entrada a ser protegido ou assinado |
| `certificateAlias` | String | Condicional | Alias do certificado para operações de assinatura |
| `credentialPassword` | String | Condicional | Senha da credencial usada na assinatura |

Para obter detalhes completos sobre os parâmetros, requisitos de autenticação e exemplos de solicitações/respostas, consulte a documentação de referência da API específica vinculada às tabelas acima.

## Recursos adicionais {#see-also}

* [Processamento de comunicação - APIs síncronas](/help/forms/aem-forms-cloud-service-communications.md)
* [Processamento de comunicação - APIs em lote](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
* [Arquitetura do AEM Forms as a Cloud Service](/help/forms/aem-forms-cloud-service-architecture.md)
* [Documentação de referência da API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)
* [Recursos anteriores do programa do adotante](/help/forms/early-access-ea-features.md)
