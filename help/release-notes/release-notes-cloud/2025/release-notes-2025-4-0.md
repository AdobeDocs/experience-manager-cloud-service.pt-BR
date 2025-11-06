---
title: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2025.4.0.
description: Notas de versão do  [!DNL Adobe Experience Manager]  as a Cloud Service 2025.4.0.
feature: Release Information
role: Admin
exl-id: 48e09824-5c67-49d8-8896-358d679649fc
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1828'
ht-degree: 11%

---

# Notas de versão do [!DNL Adobe Experience Manager] as a Cloud Service 2025.4.0 {#release-notes}

A seção a seguir descreve as notas da versão de recursos do [!DNL Experience Manager] as a Cloud Service 2025.4.0.

>[!NOTE]
>
>A partir desta seção, você pode navegar até as notas das versões anteriores, como as de 2023 ou 2024.
>
>Dê uma olhada no [Roteiro de versões do Experience Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para saber mais sobre as próximas ativações de recursos do [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para receber uma notificação por email mensal sobre atualizações nas notas de versão do Experience Cloud, assine a [Atualização prioritária de produto da Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Data de lançamento {#release-date}

A data de lançamento da versão atual (2025.4.0) do [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] é sexta-feira, 24 de abril de 2025. O próximo lançamento de recursos (2025.5.0) está planejado para sexta-feira, 5 de junho de 2025.

## Notas da versão de manutenção {#maintenance}

Encontre as notas de versão de manutenção mais recentes [aqui](/help/release-notes/maintenance/latest.md).

## Vídeo da versão {#release-video}

Assista ao vídeo Visão geral da versão de abril de 2025 que exibe um resumo dos recursos adicionados na versão 2025.4.0:

>[!VIDEO](https://video.tv.adobe.com/v/3463991?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novos recursos no Experience Manager Sites {#enhancements-sites}

**Nova interface do Administrador do modelo de fragmento de conteúdo**

Completando ainda mais a lista de novas interfaces de usuário do lado do cliente ao trabalhar com Fragmentos de conteúdo do AEM, uma nova interface de administrador agora está disponível para modelos de fragmento de conteúdo. A nova interface do usuário fornece uma exibição de lista limpa e moderna que permite pesquisar modelos com filtros e que mostra as tags de modelo e quais fragmentos de conteúdo existem com base em um determinado modelo. A documentação pode ser encontrada [aqui](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md).

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Dynamic Media (Scene7) {#dynamic-media-scene7}

**Não há suporte para Dynamic Media (Scene7) em ambientes de Segurança aprimorada**

O Dynamic Media (Scene7) no AEM as a Cloud Service não está pronto para HIPAA e não pode ser usado em ambientes AEM onde a Segurança aprimorada esteja ativada.

A partir da versão de abril de 2025 do AEM as a Cloud Service, uma restrição técnica impede que o Dynamic Media (Scene7) seja configurado em ambientes com Segurança aprimorada. Como resultado, o cartão **Configuração do Dynamic Media** em **Ferramentas** > **Serviços em nuvem** não está mais visível nesses ambientes.

Além disso, os clientes que usam o AEM 6.5 devem estar cientes de que a pilha do Dynamic Media (Scene7) não está pronta para HIPAA.

### Dynamic Media Classic {#dynamic-media-classic}

**Relatório**

A guia Largura de banda no painel de relatórios do Dynamic Media Classic não é mais compatível desde abril de 2025.

Consulte [Largura de Banda e Armazenamento, Tipos de relatórios](https://experienceleague.adobe.com/pt-br/docs/dynamic-media-classic/using/setup/administration-setup#types-of-reports).

## Novos recursos no Assets View {#new-features-assets-view}

**Relações do ativo**

A Exibição do Assets agora permite visualizar e editar relações de ativos em um painel de Detalhes de ativos simplificado. Adicione facilmente relacionamentos como Source e Derivação ao conteúdo para que os usuários possam encontrar de forma mais eficaz o conteúdo principal relevante.

![Exemplo de relação do Assets](/help/assets/assets/asset-relations-example.png)

**Comparar versões de um ativo**

Agora é possível selecionar e comparar rapidamente qualquer versão de um ativo com a versão mais recente usando a visualização do Assets.

![comparar versões do ativo](/help/assets/assets/version-compare2.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Recursos de pré-lançamento

* [Editor Universal para Forms Forms Adaptável e Fragmentos de Formulário](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md): o Editor Universal agora oferece suporte à criação de Fragmentos de Formulário Adaptáveis e Reutilizáveis. Os autores podem criar formulários visualmente, configurar ações de envio e adicionar a validação do reCAPTCHA, tudo em um ambiente de criação simplificado do WYSIWYG. Esse recurso acelera a criação de formulários, melhora a consistência e melhora a proteção contra spam e abuso automatizado.

* [Biblioteca de documentos do SharePoint - Salvar anexos com nomes de arquivo originais](/help/forms/connect-forms-to-sharepoint-document-library.md#connect-an-adaptive-form-to-microsoft-sharepoint-document-library): agora há a opção de salvar anexos de formulário usando seus nomes de arquivo originais ao armazená-los em uma Biblioteca de Documentos do SharePoint. Esse aprimoramento simplifica a identificação e o gerenciamento de arquivos carregados.

* **Editor de regras**:
   * [Condição Binária com Evento de Clique na Cláusula &quot;When&quot;](/help/forms/rule-editor-core-components-events-operators.md#available-operator-types-and-events-in-rule-editor): o Editor de Regras agora permite combinar um evento de clique de botão (_É Clicado_) com outras condições na cláusula &quot;When&quot;. Isso permite um controle mais preciso sobre a execução da regra com base na interação do usuário e outros fatores. Observação: ao usar várias condições, o evento de clique deve ser a primeira condição listada.
   * [Condições de Validação para Campos e Painéis](/help/forms/rule-editor-core-components-usecases.md): o Editor de Regras agora inclui condições _IsValid_ e _IsNotValid_. Isso permite verificar o status de validação de campos específicos ou painéis inteiros (incluindo layouts como Guias horizontais, Guias verticais, Acordeões e Assistentes), facilitando a navegação aprimorada do formulário e a experiência do usuário com base nos resultados da validação.
* [Gerenciamento de Escopo aprimorado para Listas do SharePoint](/help/forms/connect-forms-to-sharepoint-list.md): os sites do SharePoint agora oferecem suporte a todos os caminhos gerenciados, por exemplo, /sites e /team. Esse aprimoramento permite uma integração mais ampla em várias estruturas de site do SharePoint, oferecendo maior flexibilidade na conexão com o conteúdo organizacional.
* [Suporte para Salvar Documento de Registro na Lista do SharePoint](/help/forms/generate-document-of-record-core-components.md#bind-adaptive-form-components-with-template-fields): o Forms criado usando um Modelo de Dados de Formulário (FDM) baseado em Lista do SharePoint agora pode salvar o Documento de Registro (DoR) nas Listas do SharePoint configurando a propriedade do campo Documento de Referência de Associação de Registro. Esse aprimoramento permite a integração perfeita de dados e documentos de formulário compatíveis com o armazenamento da SharePoint.
* [Suporte a Mapeamento Automático para Fragmentos de Formulário Adaptáveis](/help/forms/adaptive-form-fragments-core-components.md#auto-mapping-support-for-fragments-in-an-adaptive-form): o Adaptive Forms agora oferece suporte à inserção automática de fragmentos correspondentes quando os objetos de esquema se alinham com uma estrutura de fragmento definida, simplificando a criação de formulários e promovendo a reutilização.

### Recursos de acesso antecipado no AEM Forms {#forms-new-early-access-features}

O programa de acesso antecipado da AEM Forms oferece uma oportunidade única para você obter acesso exclusivo a inovações de última geração e ajudar a moldar seu desenvolvimento.

Estas notas de versão listam as inovações fornecidas na versão atual. Para obter a lista completa de inovações disponíveis no Programa de Acesso Antecipado, consulte a [documentação do Programa de Acesso Antecipado do AEM Forms](/help/forms/early-access-ea-features.md).

#### Integração do Adobe Experience Platform (AEP) com o Forms

* [Integração do AEM Forms com o Adobe Experience Platform](/help/forms/aem-forms-aep-connector.md): o AEM Forms ao Adobe Experience Platform Connector permite a integração perfeita entre o Adaptive Forms e o Adobe Experience Platform. Esse recurso permite que os dados do formulário sejam mapeados para esquemas XDM e enviados diretamente para a AEP em tempo real. Ele simplifica a captura de dados para casos de uso de personalização e ativação em soluções da Adobe Experience Cloud.

## Complemento CIF {#cloud-services-cif}

### Aprimoramentos {#enhancements-cif}

* Adição da seleção de variante de produto para o tipo de dados de referência de produto CIF
* **Experimental**: [JSON+LD em Componentes Principais do CIF em PDPs](/help/commerce-cloud/cif-storefront/customizing/json-ld.md)
* **Experimental**: [a capacidade do CIF de limpar o cache](/help/commerce-cloud/cif-storefront/configuring/clear-cache.md)

### Correções de erros {#bug-fixes-cif}

* Corrigir problema de pesquisa no campo do produto
* O formato de URL do produto não está funcionando como esperado para #variant_sku
* Não é possível adicionar mais de 20 SKUs ao componente de lista de produtos

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### APIs baseadas em OpenAPI {#open-apis}

Os desenvolvedores podem integrar profundamente os recursos do AEM as Cloud Service em seus próprios aplicativos e ferramentas. As novas APIs do AEM as a Cloud Service seguem a especificação OpenAPI, com o objetivo de serem consistentes, bem documentadas e fáceis de usar. As credenciais para endpoints que exigem autenticação são geradas pela criação de projetos do Adobe Developer Console e oferecem suporte a OAuth de servidor para servidor, aplicativo da Web e aplicativo de página única (SPA).

[Consulte a lista completa](https://developer.adobe.com/experience-cloud/experience-manager-apis/#openapi-based-apis) de APIs baseadas em OpenAPI, [saiba mais](/help/implementing/developing/open-api-based-apis.md) e experimente um [tutorial completo](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/cloud-service/aem-apis/openapis/invoke-api-using-oauth-s2s) que ilustre a configuração e o uso.

Assista a este vídeo para saber como configurar uma API autenticada para uso posterior:

>[!VIDEO](https://video.tv.adobe.com/v/3457510?quality=12&learn=on)

### Aprimoramentos relacionados à configuração do CDN {#cdn-enhancements}

A CDN gerenciada pela Adobe oferece opções de configuração flexíveis, conforme descrito no [artigo sobre Pipeline de configuração](/help/operations/config-pipeline.md#configurations). Estes são alguns recursos recentes:

#### Incluir propriedades adicionais em logs CDN {#props-in-cdnlogs}

Útil para cenários que incluem depuração e análise de dados, você pode incluir mais informações nos logs de CDN, além das propriedades padrão, definindo a ação `logProperty` nas [transformações de solicitação e resposta](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations).

#### Propriedades da Região, Continente e Organização como Condições de Correspondência {#matching-conditions}

Agora, as regras de CDN podem corresponder com base na região, no continente e na organização para casos de uso, incluindo o bloqueio de tráfego e redirecionamentos. `clientRegion` e `clientContinent` aumentam a correspondência dos `clientCountry` já suportados com base na geografia, enquanto `clientAsName` e `clientAsNumber` correspondem aos Sistemas Autônomos para identificar grandes ISPs, empresas ou provedores de nuvem. Saiba mais sobre estas [propriedades de solicitação recém-expostas](/help/security/traffic-filter-rules-including-waf.md#condition-structure).

#### Definir valor do cookie {#cookie-attributes}

Você pode definir atributos de cookie em [transformações de resposta](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations).

### Suporte a Java 21 {#java21}

A partir da versão de janeiro, você pode criar código com o Java 21 e Java 17. Você obtém acesso a novos recursos, como correspondência de padrões, classes lacradas e várias melhorias de desempenho. Para obter as etapas de configuração, incluindo a atualização das versões do projeto e da biblioteca Maven, consulte o artigo [Ambiente de compilação](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support).

O Java 21 **runtime** de maior desempenho é implantado automaticamente quando uma compilação Java 17 ou 21 é detectada. No entanto, a Adobe também recomenda aceitar o tempo de execução do Java 21 para ambientes criados com o Java 11, enviando um email para [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com). Saiba mais sobre [requisitos de tempo de execução do Java 21](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

>[!IMPORTANT]
>
> O Java 21 **runtime** foi implantado em seus ambientes dev/RDE em fevereiro; ele será aplicado em seus ambientes de preparo/produção em **28 e 29**. Observe que o **código de construção** com Java 21 (ou Java 17) é independente do tempo de execução do Java 21 — você deve tomar etapas explicitamente para criar o código com Java 21 (ou Java 17).

### Imposição da política de configuração de log do AEM {#logconfig-policy}

Para garantir o monitoramento eficaz dos ambientes do cliente, os registros Java da AEM devem manter um formato consistente e não devem ser substituídos por configurações personalizadas. A saída do registro deve permanecer direcionada aos arquivos padrão. Para o código de produto do AEM, os níveis de log padrão devem ser preservados. No entanto, é aceitável ajustar os níveis de log para o código desenvolvido pelo cliente.

Para esse fim, as alterações não devem ser feitas às seguintes propriedades OSGi:

* **Configuração do Log do Apache Sling** (PID: `org.apache.sling.commons.log.LogManager`) — *todas as propriedades*
* **Configuração do Agente de Log do Apache Sling** (PID de Fábrica: `org.apache.sling.commons.log.LogManager.factory.config`):
   * `org.apache.sling.commons.log.file`
   * `org.apache.sling.commons.log.pattern`

Em meados de maio, a AEM aplicará uma política em que qualquer modificação personalizada nessas propriedades será ignorada. Revise e ajuste seus processos downstream de acordo. Por exemplo, se você usar o recurso de encaminhamento de logs:

* Se o destino de registro esperar um formato de registro personalizado (não padrão), talvez seja necessário atualizar as regras de assimilação.
* Se as alterações nos níveis de log reduzirem a verbosidade do log, esteja ciente de que os níveis de log padrão podem resultar em um aumento significativo no volume de log.

### Encaminhamento de logs do AEM para mais destinos - programa Beta {#log-forwarding-earlyadopter}

Agora na versão beta, você pode encaminhar logs do AEM para o New Relic (usando HTTPS), Amazon S3 e Sumo Logic. Observe que os logs do AEM (incluindo o Apache/Dispatcher) são compatíveis, mas não os logs CDN. Email [aemcs-logforwarding-beta@adobe.com](mailto:aemcs-logforwarding-beta@adobe.com) para acesso.

Embora os logs possam ser baixados da Cloud Manager, muitas organizações acham útil transmitir esses logs para um destino de registro preferencial. O AEM já oferece suporte ao (GA) encaminhamento de logs do AEM e do CDN para o Armazenamento de blobs do Azure, Datadog, HTTPS, Elasticsearch (e OpenSearch) e Splunk. Esse recurso é configurado de maneira automatizada e implantado usando o Pipeline de configuração.

Saiba mais na [documentação sobre encaminhamento de logs](/help/implementing/developing/introduction/log-forwarding.md).

### Computação Edge - Solicitação de feedback! {#edge-computing-feedback}

A computação Edge aproxima o processamento de dados do navegador, o que traz benefícios, inclusive latência reduzida. A Adobe gostaria de saber se você acha que essa tecnologia é útil para o AEM Publish Delivery e para projetos Edge Delivery Services. Além disso, informe-nos sobre o que você planeja usar como entrada no roteiro de produtos.

Alguns casos de uso possíveis:

* Autenticação com um IdP para portar o acesso ao conteúdo
* O Personalization renderiza conteúdo dinâmico com base na geolocalização, tipo de dispositivo, atributos do usuário etc.
* Manipulação avançada de imagem
* Middleware entre a CDN e uma origem
* Uma camada entre o navegador e uma API de terceiros, talvez para reformatar a resposta da API
* Agregar dados de várias origens para facilitar a renderização pelo navegador do cliente

Email [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) com perguntas e comentários!

## Guias do [!DNL Experience Manager] {#guides}

Você pode encontrar uma lista completa de recursos novos e aprimorados da versão mais recente do Adobe Experience Manager Guides [aqui](https://experienceleague.adobe.com/pt-br/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

Você pode encontrar uma lista completa de versões mensais do Cloud Manager [aqui](/help/implementing/cloud-manager/release-notes/current.md).

## Ferramentas de migração {#migration-tools}

Você pode encontrar uma lista completa de versões das ferramentas de migração [aqui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Editor universal {#universal-editor}

Você pode encontrar uma lista completa de versões do Universal Editor [aqui](/help/release-notes/universal-editor/current.md).

## Gerar variações {#generate-variations}

Você pode encontrar uma lista completa de versões de Gerar Variações [aqui](/help/generative-ai/release-notes-generate-variations.md).

## Notas de versão da Experience Cloud {#experience-cloud}

Você pode encontrar informações sobre versões de outros aplicativos da Experience Cloud [aqui](https://experienceleague.adobe.com/pt-br/docs/release-notes/experience-cloud/current).
