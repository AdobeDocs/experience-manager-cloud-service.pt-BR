---
title: Visão geral do AEM Forms Edge Delivery Services
description: O AEM Forms Edge Delivery Services foi criado para desempenho máximo, permitindo que você visualize o futuro da coleta de dados simplificada e do engajamento do usuário.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 0%

---

# AEM Forms Edge Delivery Services

Simplifique a criação de formulários e impulsione taxas de conclusão mais altas com o Adobe AEM Forms Edge Delivery Services. Esse serviço potente e combinável permite que você crie formulários de nível empresarial com desempenho e apelo visual excepcionais. O AEM prioriza a experiência do usuário e seus objetivos comerciais, garantindo tempos de carregamento extremamente rápidos e conversões de formulários mais altas.

Você pode usar o serviço para:

* **Crie experiências de inscrição excepcionais**: crie experiências de inscrição que são carregadas e renderizadas rapidamente, mesmo em conexões de Internet lentas. Carregamentos mais rápidos e experiência otimizada do usuário contribuem para taxas mais altas de preenchimento de formulários e taxas de conversão aprimoradas.

* **Crie experiências de inscrição com as ferramentas de sua escolha**: aumente a eficiência da criação ao dissociar as fontes de conteúdo. Pronto para uso, você pode usar ambos **criação baseada em documento** (Microsoft SharePoint ou Google Drive) e **Criação no AEM** (Editores AEM). Dessa forma, você pode trabalhar com várias fontes de conteúdo no mesmo formulário e usar suas ferramentas de criação preferidas, como o Microsoft Excel, o Google Sheets ou o Adaptive Forms Editor.

* **Usar conjunto de ferramentas para desenvolvedores:** O AEM Forms usa o HTML simples, o CSS moderno e o JavaScript padrão para criar experiências excepcionais sem a sobrecarga normal. Qualquer desenvolvedor com conhecimento básico de HTML, CSS e JS deve ser capaz de criar seus próprios componentes e não precisa aprender nenhuma linguagem ou estrutura específica. Não há necessidade de pipeline ou espera, faça o check-in do código no Github e suas alterações estarão ativas. Além disso, não há necessidade de pipeline ou espera, faça o check-in do código no Github e suas alterações estarão ativas.


## Criação de uma experiência de inscrição digital

O AEM Forms oferece ambos **criação baseada em documento** (Microsoft SharePoint ou Google Drive) e **Criação no AEM** (Editores AEM). Você pode usar o [Bloco Forms adaptável](/help/edge/docs/forms/create-forms.md) para adicionar um formulário ao site do Edge Delivery Services.


>[!BEGINTABS]

>[!TAB Criação baseada em documento]

A criação baseada em documentos é uma opção versátil, adequada para criar formulários simples com funcionalidades essenciais. Ele permite integrar vários tipos de entrada, como campos de texto, menus suspensos e botões de opção, permitindo coletar dados do usuário com eficiência. Ela oferece uma versão básica de regras para adicionar comportamento dinâmico a formulários. Os principais recursos da criação baseada em documentos são:

* **[Componentes de campo de formulário baseados em HTML](/help/edge/docs/forms/form-components.md)**: o AEM Forms Edge Delivery Services permite criar formulários amigáveis e interativos usando componentes de formulário baseados no HTML5 [tipos de entrada](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">selecionar</a>, e <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a>  elementos. Esses componentes atendem a diferentes tipos de coleção de dados e podem ser facilmente personalizados para atender às suas necessidades específicas.

* **Acessibilidade**: os campos no bloco de formulário são acessíveis. Cada rótulo é vinculado ao respectivo elemento de entrada, e as IDs são geradas automaticamente para vinculação. As descrições associadas a campos são vinculadas por meio do atributo aria-descripbedby. A navegação pelo teclado usando as teclas Tab/Shift + Tab padrão é suportada.

* **[Estilo](/help/edge/docs/forms/style-theme-forms.md)**: cada campo de formulário tem uma estrutura de HTML fixa que pode ser facilmente decorada usando arquivos CSS ou JavaScript personalizados. Os seletores para campos de direcionamento em CSS e JS são fornecidos com base no tipo e no nome. Você pode criar facilmente novos seletores devido à estrutura padronizada e ao estilo do seu formulário.

* **Regras básicas**: crie facilmente uma lógica que ajuste a visibilidade, a validação e o comportamento do campo com base na entrada do usuário ou em condições predefinidas. As regras oferecem uma maneira flexível e intuitiva de adicionar inteligência aos seus formulários, garantindo que eles se adaptem perfeitamente com base nas entradas do usuário.

* **Validações**: Antes do envio, o formulário é validado e os campos inválidos são marcados apropriadamente com mensagens de erro exibidas para o usuário. Os blocos adaptáveis do Forms são compatíveis com toda a validação de formulários de HTML, com o suporte de navegadores modernos, e fornecem mecanismo de validação adicional, como script de validação, tamanho de arquivo, tipo de arquivo, tamanho geral do arquivo e muito mais.

* **Uploads de arquivo**: Você pode adicionar recursos de anexo de arquivo aos formulários. Não importa se você precisa coletar documentos, imagens ou outros arquivos de seus usuários, a funcionalidade de upload de arquivos atende você sem esforço. Com as opções de manuseio personalizado disponíveis, você pode adaptar o processo de upload de arquivo para atender aos seus requisitos específicos.

* **reCAPTCHA**: aproveite a integração perfeita do Google reCAPTCHA em seus formulários com nosso suporte pronto para uso (OOTB). Proteja seus formulários contra atividades fraudulentas, spam e abuso, mantendo ao mesmo tempo uma experiência perfeita e ininterrupta do usuário. O bloco Forms adaptável é compatível com reCaptcha V3 e reCaptcha Enterprise.

* **Enviar notificação por e-mail no envio do formulário**: elimine o incômodo causado pelos acompanhamentos manuais e garanta a comunicação oportuna com nossa automação de email integrada para envios de formulários. Essa solução integrada permite que você notifique facilmente as partes relevantes, incluindo o envio de dados de formulário, sempre que alguém preencher um formulário em seu site. Sem necessidade de configurações complexas ou ferramentas adicionais, ele está pronto para uso imediato.

>[!TAB Criação no AEM]

A criação no AEM desbloqueia recursos adicionais além da criação baseada em documentos, permitindo que você crie formulários mais complexos e interativos. Além dos recursos da criação baseada em documentos, a criação por AEM oferece os seguintes recursos adicionais:

* Regras avançadas: defina ações baseadas em lógica nos seus formulários. Você pode usar regras para mostrar ou ocultar condicionalmente seções de formulário, preencher previamente campos com base na entrada do usuário e executar várias validações para garantir a integridade dos dados.

* Extensibilidade do lado do servidor: estenda as funcionalidades de seus formulários integrando-os à lógica do lado do servidor. Isso permite executar cálculos complexos, interagir com sistemas externos e automatizar tarefas específicas com base nas ações do usuário no formulário.
* Simplifique os fluxos de trabalho e o gerenciamento de dados: aproveite o poder do AEM para:
   * Crie formulários amigáveis usando editores AEM.
   * Gerar um &quot;Documento de registro&quot; para arquivamento seguro e à prova de adulteração dos dados enviados.
   * Facilite a assinatura eletrônica com o Adobe Sign para obter uma experiência de assinatura perfeita e segura.
   * Automatize processos comerciais por meio de fluxos de trabalho de AEM, acionando ações com base em envios de formulários.
   * Integre-se facilmente a várias fontes de dados, permitindo um fluxo e troca de dados perfeitos.

>[!ENDTABS]








## Começar a criar formulários

<div>

<style>
    .card-container {
        width: calc(33.33% - 10px);;
        margin: 5px;
        border: 1px solid #ccc;
        border-radius: 5px;
        padding: 5px;
        box-sizing: border-box;
        transition: background-color 0.3s ease; /* Adding transition effect */
    }
    .card-container:hover {
        background-color: #f0f0f0; /* Changing background color on hover */
    }
</style>

<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: -5px;">
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md">
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Criar um formulário usando o eds forms" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Criar um formulário usando o Google Sheets ou o Microsoft Excel</b>
        </a>
        <p>Crie formulários que são carregados e renderizados de forma rápida e automática em dispositivos móveis.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Enviar formulário" alt="Usar fragmentos de formulário em um formulário EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Enviar formulário para planilha</b>
        </a>
        <p>Envie formulários diretamente para o Microsoft Excel ou o Google Sheets.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Aplicar estilos ou temas a um formulário eds" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Personalizar um tema</b>
        </a>
        <p>Crie uma imagem de marca consistente aplicando o mesmo tema em vários formulários.</p>
    </div>
      <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Adicionar validações a campos de formulário" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Aplicar validações de campo</b>
        </a>
        <p>Reduza erros e frustrações verificando as entradas do formulário para obter a formatação adequada.</p>
    </div> 
            <div class="card-container">
        <a href="/help/edge/docs/forms/rules-forms.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Usar regras para adicionar comportamento dinâmico a um formulário" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Usar regras para adicionar comportamento dinâmico a um formulário</b>
        </a>
        <p>Reutilizar fragmentos pré-configurados em vários formulários.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Traduzir um formulário EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Traduzir um formulário</b>
        </a>
        <p>Estenda o alcance de seus formulários mantendo os custos sob controle.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Adicionar seções que podem ser repetidas a um Formulário EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Adicionar seções repetíveis</b>
        </a>
        <p>Crie e adicione facilmente seções repetíveis a um formulário.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="Criar componentes de formulários personalizados usando JavaScript e CSS padrão"  style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Criar componentes personalizados</b>
        </a>
        <p>Use JavaScript e CSS padrão para criar componentes e temas.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Usar reCAPTCHA em um formulário EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Usar reCAPTCHA</b>
        </a>
        <p>Use a integração OTB reCAPTCHA para uma proteção robusta contra spam e bot.</p>
    </div>


</div>


</br>
