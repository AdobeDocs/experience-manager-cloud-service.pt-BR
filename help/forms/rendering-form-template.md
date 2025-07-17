---
title: Modelo de formulário de renderização para formulários HTML5
description: Os perfis de formulários do HTML5 estão associados às renderizações de perfil. Os Renderizadores de perfil são páginas JSP responsáveis por gerar a representação HTML do formulário chamando o serviço OSGi da Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: HTML5 Forms,Mobile Forms
exl-id: 022b9953-2d64-473f-87b7-aac1602f6a7e
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 1%

---

# Modelo de formulário de renderização para formulários HTML5 {#rendering-form-template-for-html-forms}

<span class="preview"> O recurso HTML5 Forms é oferecido como parte do Programa de acesso antecipado. Para solicitar acesso, envie um email de sua ID de email oficial (comercial) para aem-forms-ea@adobe.com.
</span>

## Renderizar Ponto de Extremidade {#render-endpoint}

Os formulários HTML5 têm a noção de **Perfis** que são expostos como pontos de extremidade REST para habilitar a Renderização Móvel de Modelos de Formulário. Estes perfis associaram o **Renderizador de Perfil**. Elas são páginas JSP responsáveis por gerar a representação do formulário no HTML, chamando o serviço OSGi do Forms. O caminho JCR do nó de Perfil determina o URL do ponto final de renderização. O ponto final de renderização padrão do formulário apontando para o perfil &#39;padrão&#39; é semelhante a:

https://&lt;*host*>:&lt;*porta*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*caminho da pasta que contém o formulário xdp*>&amp;modelo=&lt;*nome do xdp*>

Por exemplo, `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Para um perfil personalizado, o endpoint é alterado de acordo. Por exemplo, o ponto final do perfil personalizado com o nome hrforms é:

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Se o modelo residir no repositório do AEM em um aplicativo chamado FormSubmission, o URI será:

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## Parâmetros de renderização {#render-parameters}

Os parâmetros de solicitação compatíveis ao renderizar o formulário como HTML são:

<table>
 <tbody>
  <tr>
   <th><strong>Parâmetro </strong></th>
   <th><strong>Descrição</strong></th>
  </tr>
  <tr>
   <td>modelo<br /> </td>
   <td>Este parâmetro especifica o nome do arquivo de modelo.<br /> </td>
  </tr>
  <tr>
   <td>contentRoot<br /> </td>
   <td>Esse parâmetro especifica o caminho onde o modelo e os recursos associados residem. Este caminho pode ser o caminho do sistema de arquivos do servidor ou um caminho de repositório ou um caminho http ou ftp.<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>Esse parâmetro especifica a url para a qual o xml de dados de formulário é postado.<br /> </td>
  </tr>
 </tbody>
</table>

### Mesclar dados com o modelo de formulário {#merge-data-with-form-template}

| Parâmetro | Descrição |
|---|---|
| dataRef | Este parâmetro especifica o **caminho absoluto** do arquivo de dados mesclado com o modelo. Esse parâmetro pode ser um URL para um serviço rest que retorna os dados no formato xml. |
| dados | Esse parâmetro especifica os bytes de dados codificados em UTF-8 que são mesclados com o modelo. Se esse parâmetro for especificado, o formulário HTML5 ignorará o parâmetro dataRef. |

### Passagem do parâmetro de renderização {#passing-the-render-parameter}

Os formulários HTML5 suportam três métodos para transmitir os parâmetros de renderização. Você pode enviar parâmetros por meio de URLs, pares de valores chave e nó de perfil. No parâmetro de renderização, o par de valor-chave tem a precedência mais alta seguida pelo nó do perfil. O parâmetro de solicitação de URL tem menos precedência.

* **Parâmetros de solicitação de URL**: você pode especificar os parâmetros de renderização na URL. Nos parâmetros de solicitação de URL, os parâmetros estão visíveis para o usuário final. Por exemplo, a URL de envio a seguir contém um parâmetro de modelo na URL: `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **Parâmetros de solicitação SetAttribute**: você pode especificar os parâmetros de renderização como um par de valores chave. Nos parâmetros de solicitação SetAttribute, os parâmetros não estão visíveis para o usuário final. Você pode encaminhar uma solicitação de qualquer outro JSP para o JSP do renderizador de perfil de formulário do HTML5 e usar *setAttribute* no objeto de solicitação para passar todos os parâmetros de renderização. Esse método tem a maior precedência.

* **Parâmetros de solicitação de nó de perfil:** Você pode especificar os parâmetros de renderização como propriedades de nó de um nó de perfil. Nos parâmetros de solicitação do nó de perfil, os parâmetros não estão visíveis para o usuário final. O nó de perfil é o nó para onde a solicitação é enviada. Para especificar parâmetros como propriedades de nó, use o CRXDE lite.

### Enviar parâmetros {#submit-parameters}

Os formulários HTML5 enviam dados; executam scripts do lado do servidor e serviços da Web nos servidores da AEM. Para obter informações detalhadas sobre os parâmetros usados para executar scripts do lado do servidor e serviços da Web em servidores AEM, consulte [Proxy do HTML5 Forms Service](/help/forms/service-proxy.md).
