---
title: Perguntas frequentes sobre o DHTML Viewer End-of-Life
description: A partir de 31 de janeiro de 2014, a plataforma do visualizador DHTML do Scene7 será oficialmente encerrada. Esta notificação fornece respostas para perguntas frequentes para que você possa se preparar para essa transição para a nova plataforma do visualizador HTML5.
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# Perguntas frequentes sobre o DHTML Viewer End-of-Life{#dhtml-viewer-end-of-life-faqs}

A partir de 31 de janeiro de 2014, a plataforma do visualizador DHTML do Scene7 será oficialmente encerrada. Esta notificação fornece respostas para perguntas frequentes para que você possa se preparar para essa transição para a nova plataforma do visualizador HTML5.

**Qual é a mudança?**

A partir de 31 de janeiro de 2014, o Scene7 oferecerá suporte oficial ao fim da vida útil da plataforma do visualizador DHTML.

**O que significa o fim da vida?**

Fim da vida útil significa que o Scene7 (1) não adicionará mais nenhum aprimoramento de recurso à plataforma do visualizador DHTML (2) não mais endereçará nem lançará nenhuma correção de erros na plataforma do visualizador DHTML e (3) o atendimento ao cliente não estará mais solucionando problemas ou fornecendo suporte para quaisquer problemas ou perguntas do visualizador relacionados ao DHTML.

**Por que o Scene7 está fazendo essa mudança?**

Os padrões da Web estão em constante evolução e o DHTML é uma tecnologia de desenvolvimento da Web mais antiga que está sendo rapidamente substituída pelo HTML5. A maior limitação para o DHTML como plataforma é que ele não é capaz de criar a riqueza da experiência que o HTML5 agora pode suportar de forma consistente e mais fácil entre navegadores. Por exemplo, essas limitações incluem falta de suporte entre navegadores para:

* Cursores personalizados
* Cantos arredondados
* Animações (como girar a página, diminuir o zoom)
* Efeitos (como sombras, brilho)
* Suporte completo para fontes
* Reprodução de vídeo sem plug-in

Específico à plataforma do visualizador Scene7 DHTML, a solução baseada em JSP e as APIs do Javascript não foram otimizadas para dispositivos móveis para aproveitar os recursos de multitoque e gesto. E mesmo que os visualizadores DHTML lançados em 2011/início de 2012 fossem otimizados para dispositivos móveis, eles eram difíceis de personalizar e manter devido à falta de uma estrutura de desenvolvimento flexível baseada em componentes do SDK.

Orientado por essas limitações no DHTML e pela rápida tração do setor com o HTML5 como um padrão emergente no desktop e no dispositivo móvel, o Scene7 decidiu investir em uma plataforma de visualizador baseada em HTML5. Esse investimento oferecerá aos nossos clientes uma plataforma robusta contra a qual eles podem criar visualizadores interativos mais ricos e mais envolventes, que podem chegar aos usuários em várias telas, incluindo dispositivos desktop, iOS e Android.

**Como faço para saber se meu visualizador está usando a plataforma DHTML?**

Para determinar se o visualizador que sua empresa está usando é DHTML e, portanto, é afetado por essa alteração, verifique se:

1. Sua empresa está usando um visualizador Scene7 pronto para uso listado nesta tabela onde a &quot;Tecnologia de visualizador&quot; é designada como &quot;DHTML&quot;:

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. Sua empresa está usando um visualizador que foi criado como uma nova predefinição com base em um visualizador Scene7 pronto para uso nesta tabela onde a &quot;Tecnologia de visualizador&quot; é designada como &quot;DHTML&quot;:

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. Sua empresa está usando um visualizador personalizado criado a partir da solução DHTML baseada em JSP:

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference)

1. Sua empresa está usando um visualizador personalizado criado a partir da API Javascript:

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference)

1. Sua empresa está usando um visualizador personalizado criado com a API de flyout multitela DHTML:

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer)

1. Sua empresa está usando um visualizador personalizado criado com a API de flyout de desktop DHTML:

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer)

1. Sua empresa está usando uma biblioteca de detecção de dispositivos que faz parte do pacote de visualizadores DHTML:

   Procure por JS incluindo &quot;sj_deviceDetect.js&quot; no código.

   Este foi substituído pelo novo código de detecção de dispositivo JS aqui: [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers) .

**O que é a plataforma de visualização substituta?**

A substituição para DHTML é a plataforma do visualizador Scene7 HTML5, que consiste em:

* Visualizadores HTML5 prontos para uso com interações móveis otimizadas em vários tipos de visualizadores, incluindo zoom básico, zoom de deslocamento, conjuntos de imagens, conjuntos de amostras, rotação multidimensional e mídia mista. Para obter exemplos atualizados desses visualizadores, consulte: [https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
* O SDK do visualizador HTML5, que permite a personalização abrangente dos visualizadores do Adobe Scene7 para sites e dispositivos compatíveis com HTML5 (como iOS e Android), proporcionando a máxima flexibilidade e criatividade para marcar a aparência e a interatividade do visualizador. A vantagem dos componentes reutilizáveis otimizados para desempenho reduz o custo geral do desenvolvimento do visualizador e acelera o desenvolvimento personalizado.

**Quando a plataforma do visualizador HTML5 terá os recursos necessários para fazer a transição da plataforma do visualizador DHTML?**

O Scene7 lançou o primeiro SDK do visualizador HTML5 no último trimestre de 2011 com o lançamento da versão 5.5. Desde então, adicionamos vários recursos à plataforma e suporte estendido para mais e mais tipos de visualizadores. Para os requisitos mais comuns do visualizador, a plataforma do visualizador HTML5 provavelmente já tem os recursos que você precisa migrar agora. E continuamos a investir agressivamente nesta plataforma de espectadores com lançamentos a cada trimestre.

Para determinar se os requisitos do visualizador podem ser atendidos hoje com a plataforma do visualizador HTML5, consulte a seguinte documentação:

[https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers) (para recursos e recursos de personalização de visualizadores prontos para uso)

[https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html) (para acessar a documentação da API do SDK)

Se ainda não tiver certeza se o SDK do visualizador HTML5 atende aos seus requisitos, consulte nossa equipe de serviços profissionais.

**Como transfiro meus visualizadores para a plataforma HTML5?**

Para transferir seus visualizadores para a plataforma HTML5, o Scene7 oferece as seguintes opções:

1. Use um dos visualizadores HTML5 prontos para uso do Scene7, cujos exemplos podem ser encontrados aqui: [https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
1. Configure um dos visualizadores HTML5 prontos para uso do Scene7 na configuração do aplicativo SPS. Isso permitirá que você personalize determinados comportamentos, como tamanho do visualizador, transições, comportamento de zoom etc.: [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html)
1. Personalize a aparência dos visualizadores HTML5 prontos para uso do Scene7 modificando o CSS para alterar o design visual, como arte-final de botão, posicionamento, transparência, cores de fundo, etc: [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers)
1. Crie um visualizador HTML5 personalizado do zero usando o SDK que pode ser baixado aqui: [https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html). Você pode se envolver com serviços profissionais para criar o visualizador personalizado ou ter sua própria equipe de desenvolvimento da Web para criá-lo.

**E os navegadores que não suportam HTML5?**

O HTML5 é compatível com vários dispositivos móveis e navegadores da Web e continua a ganhar força. Atualmente, mesmo que o HTML5 não seja suportado no Internet Explorer 8 ou abaixo, o Scene7 inovou nossa plataforma de visualizador HTML5 para estender o suporte até mesmo ao IE 7 e IE 8. Com a plataforma do visualizador Scene7 HTML5 , você pode alcançar a grande maioria dos usuários de desktop e de dispositivos móveis com uma única plataforma de desenvolvimento.

Os requisitos de sistema atuais a partir do SDK HTML5 versão 2.2.1 são:

* Microsoft® Windows® XP ou posterior, Macintosh® OS X 10.6 ou posterior
* Firefox 17, Safari 5.1, Chrome 23, Internet Explorer 7 ou posterior
* iOS 3.2.2 ou posterior
* Certificado no iPhone3 ou posterior e no iPad1 ou posterior (navegadores nativos)
* Android OS 2.2 ou posterior

Para verificar se o navegador é compatível com a plataforma do visualizador HTML5, inicie o visualizador de exemplo a seguir:

[https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image](https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image)

Se você vir a imagem ampliada passando o mouse ou arrastando o dedo sobre a imagem principal, então é um navegador/dispositivo suportado.

**Quais opções tenho se eu quiser permanecer em produção com meu visualizador DHTML existente?**

Embora você ainda possa estar em produção com visualizadores baseados em DHTML, é importante observar que não haverá aprimoramentos, correções de bugs nem atendimento ao cliente após 31 de janeiro de 2014. Dessa forma, recomendamos que todos os clientes migrem para nossa plataforma de visualizador HTML5 mais robusta. . No entanto, se sua situação comercial impedir essa migração até a data final de vida útil, você terá a opção de contrair com serviços profissionais para estender o período de tempo de manutenção suportado. Para obter mais informações, entre em contato com seu gerente de conta.

**Com quem posso entrar em contato para obter mais informações?**

Se essas perguntas frequentes não responderem a todas as suas perguntas, entre em contato com o suporte ([s7support@adobe.com](mailto:s7support@adobe.com)) ou com o gerente de conta da Adobe.
