---
title: Registrar uma transação para implementações personalizadas
description: Usar a API TransactionRecorder para registrar ações que não são contabilizadas como transações automaticamente
feature: Adaptive Forms, Foundation Components
exl-id: cb584f78-30af-4a58-be99-843352e8249c
source-git-commit: 539f4bf86f0e32057b2228dc44c86120d6e8457b
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 10%

---

# Registrar uma transação para implementações personalizadas {#record-a-transaction-for-custom-implementations}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/transaction-reports/transaction-reports-osgi/record-transaction-custom-implementation) |
| AEM as a Cloud Service | Este artigo |

Use a API TransactionRecorder para registrar ações que não são contabilizadas como transações automaticamente.

Você pode usar o código personalizado para enviar um Formulário PDF. Ou você envia um formulário usando métodos personalizados em vez de usar os métodos de envio fornecidos com o AEM Forms. Todas as ações mencionadas anteriormente e implementações personalizadas de APIs do AEM Forms não são contabilizadas como transações. O AEM Forms fornece uma API, [TransactionRecorder](https://javadoc.io/doc/com.adobe.aem/aem-forms-sdk-api/latest/com/adobe/aem/transaction/core/ITransactionRecorder.html), para registrar essas ações como transações.

Para registrar uma transação, escreva o [servlet sling padrão](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/store-and-retrieve-af-with-2fa/create-servlet.html?lang=en) e chamar o servlet de um cliente para registrar uma transação. Você pode chamar o servlet usando AJAX ou qualquer outro método padrão.

## Código de exemplo do lado do servidor {#sample-server-sided-code}

Você pode usar o código de amostra abaixo para executar a API TransactionRecorder a partir de uma classe Java™ usando um pacote OSGi personalizado.

```java
import com.adobe.aem.transaction.core.ITransactionRecorder;
import com.adobe.aem.transaction.core.model.TransactionRecord;
import com.adobe.aem.transaction.core.exception.TransactionException;
import com.adobe.aem.transaction.core.FormsTransactionConstants;

@Reference
private ITransactionRecorder transactionRecorder;

doPost (SlingHttpServletRequest request, SlingHttpServletResponse response) {
    transactionRecorder.startContext();
    TransactionRecord txRecord = extractTxRecordFromRequest(request); //extract transaction relevant data from request
    try {
        bool success = doBillableWork();
        if (success) {
            transactionRecorder.recordTransaction(txRecord);
        }
    } catch (Exception e) {
        //exception handling
    } finally {
        transactionRecorder.endContext();
    }
}

//Here, it is assumed that txInfo is passed in Stringified json form in the ajax call (in data parameter). You can pass txInfo from client in any way that you find suitable.
private TransactionRecord extractTxRecordFromRequest(SlingHttpServletRequest request) {
    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(request.getInputStream()));
    Map<String, Object> txDataMap = new HashMap<String, Object>();
    String txData = bufferedReader.readLine();
    JSONObject txInfo= new JSONObject(txData );
    try {
        String resourceType= txInfo.getString("resourceType");
        String transactionType = txInfo.getString("transactionType");
        Integer transactionCount = (Integer)txInfo.get("transactionCount");
        //Extract all the relevant tx record attributes similarly and pass them in Transaction Record constructor as per the java doc}
        return new TransactionRecord(transactionCount, transactionType, resourceType, ..);
    } catch (JSONException e) {
        //exception handling
    } finally {
        bufferedReader.close();
    }
}
```

## Código de exemplo do lado do cliente {#sample-client-side-code}

Você pode usar o código de amostra abaixo para chamar o servlet que tem o `TransactionRecorder`API.

```javascript
$.ajax({
   type: 'POST',
   url: url, //servlet url
   contentType: 'application/json; UTF-8',
   data: JSON.stringify({transactionCount : 1,
                        transactionType: "SUBMIT",
                        resourceType: "FORM",
                        resourceSubType: "ADAPTIVE-FORM"}),
   success: successHandler,
   error: faultHandler
})
```

## Artigos relacionados {#related-articles}

* [APIs faturáveis de relatórios de transação](/help/forms/transaction-reports-billable-apis.md)
