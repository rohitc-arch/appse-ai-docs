---
slug: /platform/key-concepts/nodes/built-in/code
title: Code Node
---

The **Code Node** allows you to run custom code to transform data, perform complex logic, or aggregate information that standard nodes can't handle. It provides a secure, sandboxed environment for data manipulation.

This might be helpful in situations such as:
*   Transforming JSON structures (e.g., renaming fields, restructuring objects)
*   Filtering items based on complex conditions
*   Aggregating data (e.g., summing up order totals)
*   Merging data from multiple previous nodes

## Configuration

<img src="\img\platform\key-concepts\nodes\built-in\code\configuration.png" alt="Code Node Configuration" width="700"/>

### Modes of Execution


The Code Node operates in two modes, which determine how input data is processed:

1.  **Run Once for All Items** (Default):
    *   **Input**: Receives an **Array** of all items from the previous node.
    *   **Output**: Must return an **Array** of object.
    *   **Ideal for**: Aggregation, sorting, filtering, or merging data.
    
    ```javascript
    // Input ($payload): [
    //  { "product": "A", "price": 10 },
    //  { "product": "B", "price": 25 },
    //  { "product": "C", "price": 5 }
    // ]

    // Filter items over $15 and sort by price descending
    const filtered = $payload
      .filter(item => item.price > 5)
      .sort((a, b) => b.price - a.price);

    return [{ result: filtered }];
    // Output: [
    //  { "result": [
    //      { "product": "B", "price": 25 }, 
    //      { "product": "A", "price": 10 }
    //    ] 
    //  }
    // ]
    ```

2.  **Run for Each Item**:
    *   **Input**: Receives a **Single Object** for each item. The code runs multiple times (once per item).
    *   **Output**: Must return a **Single Object**.
    *   **Ideal for**: Mapping fields, formatting values, or adding new properties to each item independently.

    ```javascript
    // Input ($payload): { 
    // "firstName": "John", 
    // "lastName": "Doe", 
    // "price": 100 
    // }

    const taxRate = 0.18;
    return {
      fullName: `${$payload.firstName} ${$payload.lastName}`,
      originalPrice: $payload.price,
      finalPrice: parseFloat(($payload.price * (1 + taxRate)).toFixed(2))
    };
    // Output: { 
    // "fullName": "John Doe", 
    // "originalPrice": 100, 
    // "finalPrice": 118 
    // }
    ```

### Language


Currently, the Code Node supports **JavaScript** only. You can write standard ES6+ JavaScript to manipulate your data.

### Code


This is where you write your custom code for data transformation. 

*   The code must return a valid JSON output (Array or Object depending on the [mode](#modes-of-execution)).

## Code Editor Features

The built-in code editor provides several tools to help you write and debug your logic:

*   **Autocomplete**: Type `$` to see suggestions for `$payload`, previous nodes (e.g., `$('Get Users')`), or start typing a variable name or method name to see suggestions for standard JavaScript methods. Suggestions from previous nodes are available once those nodes have been executed. Use `Ctrl` + `Space` for toggling the suggestion tooltip on or off.
*   **Real-time Linting**: Flags errors immediately, such as syntax issues or attempts to modify read-only data. Warnings will appear if data from previous nodes is not available — this typically means those nodes have not been executed yet.
*   **Console Output**: Use `console.log()` to print messages to your browser's developer console for debugging.
*   **Syntax Highlighting**: Colors your code for better readability.

## Accessing Data

<img src="\img\platform\key-concepts\nodes\built-in\code\autocomplete.png" alt="Code Node Autocomplete" width="700"/>

### `$payload`

<img src="\img\platform\key-concepts\nodes\built-in\code\immediate-parent.png" alt="Code Node Payload" width="700"/>

This is the main variable containing your input data.

*   **In "Run Once for All Items" mode**:
    `$payload` is an **Array** containing **all items** returned by the previous node. You have access to the entire dataset at once.
    *   *Example:* `[ { "id": 1, "name": "Ali" }, { "id": 2, "name": "Bob" } ]`

*   **In "Run for Each Item" mode**:
    `$payload` is a **Single Object** representing **one item** from the list. The code runs individually for each item in the dataset.
    *   *Example:* `{ "id": 1, "name": "Ali" }` (First execution) -> `{ "id": 2, "name": "Bob" }` (Second execution)

### `$('Node Name')`

<img src="\img\platform\key-concepts\nodes\built-in\code\descendants.png" alt="Code Node Previous Node" width="700"/>

Access output from any previous node by name. In the figure above, **Shopify** is the node name.

*   **Syntax**: `$('Node Name').payload`
*   The `$('Node Name')` function returns a wrapper object. You usually need to access the `.payload` property to get the actual data array.

**Example:**
```javascript
// Access data from a previous "Get Users" node
const users = $('Get Users').payload;
const matchingUser = users.find(u => u.id === $payload.userId);
```

| Library | Usage | Example |
| :--- | :--- | :--- |
| **moment** | Date & Time manipulation | `moment().add(7, 'days').format('YYYY-MM-DD')` |
| **crypto** | Cryptographic functions | `crypto.randomUUID()` |
| **Math** | Mathematical operations | `Math.round(10.5)` | 
| **JSON** | Parsing and stringifying JSON | `JSON.parse('{"a":1}')` |

## Steps to Use the Code Node

1.  Select the **Code Node** from the node selection screen.
<img src="\img\platform\key-concepts\nodes\built-in\code\selection.png" alt="Code Node Selection" width="700"/>

---

2.  Connect it to a node that provides data (e.g., an HTTP Request Node or App Node).
<img src="\img\platform\key-concepts\nodes\built-in\code\connection.png" alt="Code Node Connection" width="700"/>

---

3.  Open the **Configuration** tab and select your **Mode** (Run Once or Run Each).

---

4.  Write your JavaScript logic in the **Code** section. Utilize `$payload` to access input data.
<img src="\img\platform\key-concepts\nodes\built-in\code\js-code.png" alt="Code Node JS Code" width="700"/>

---

5.  Use `console.log()` to debug if needed.

---

6.  Click **Run** to test your code and see the output.

---

### Example: Calculate Total with Tax

**Scenario**: You have a list of orders and want to format the date and calculate the total price including tax.

**Mode**: Run for Each Item

```javascript
// Input: { "price": 100, "date": "2023-10-01" }

const taxRate = 0.2;
const total = $payload.price * (1 + taxRate);

return {
  originalPrice: $payload.price,
  finalPrice: parseFloat(total.toFixed(2)),
  processedAt: moment().toISOString(),
  status: "Processed"
};
```

## Output Behavior

*   **Success**: The Output panel will show the transformed data (Array or Object depending on mode).
*   **Errors**: If your code has syntax errors or runtime exceptions, they will be shown in the output section. You may also find additional error details in your browser's developer console.
*   **Important**: Input data is **Read-Only**. Always return a **new** object or array. Do not directly modify `$payload` or `$('Node Name').payload`.

## Supported & Restricted Features

### Supported ✅

| Category | Details |
| :--- | :--- |
| **Standard Objects** | `Math`, `Date`, `JSON`, `RegExp`, `String`, `Number`, `Boolean`, `Array`, `Object`, `Error`, `TypeError` |
| **Collections** | `Map`, `Set` |
| **Utilities** | `structuredClone()`, `atob()`, `btoa()`, `parseInt()`, `parseFloat()`, `isNaN()`, `isFinite()` |
| **URI Encoding** | `encodeURIComponent()`, `decodeURIComponent()`, `encodeURI()`, `decodeURI()` |
| **Console** | `console.log()`, `console.warn()`, `console.error()`, `console.info()`, `console.debug()`, `console.table()` |
| **Libraries** | `moment` (date/time manipulation), `crypto` (`randomUUID()`, `getRandomValues()`) |
| **Syntax** | ES6+ features: arrow functions, destructuring, spread operator, template literals, optional chaining (`?.`), nullish coalescing (`??`), `for...of` loops |

### Not Supported / Restricted ❌

| Category | Details | Alternative |
| :--- | :--- | :--- |
| **Network Requests** | `fetch`, `XMLHttpRequest`, `http`, `https` | Use the **HTTP Request Node** |
| **Async Operations** | `async/await`, `Promise`, `setTimeout`, `setInterval` | Code runs synchronously |
| **Browser APIs** | `window`, `document`, DOM access | Not applicable |
| **File System** | `fs`, file read/write | Use dedicated nodes |
| **Modules** | `import`, `require`, `module.exports` | Use built-in libraries only |
| **Data Mutation** | Direct modification of `$payload` or node data `$('Node name').payload` | Return a new object using the spread operator (`...`) |

#### These will cause errors ❌: 
```javascript
$payload.status = "Active";          // Cannot assign to read-only property
$payload.push({ id: 3 });            // Cannot use mutating methods
delete $payload.name;                // Cannot delete properties
$('Get Users').payload[0].age = 30;  // Cannot modify referenced node data
```

#### Instead, return new objects ✅:
```javascript
// Spread into a new object
return { ...$payload, status: "Active" };

// Use non-mutating array methods
const filtered = $payload.filter(item => item.active);
const mapped = $payload.map(item => ({ ...item, seen: true }));
```
## Real Integration Use Cases

Select the appropriate tab below based on your desired **Mode** (Run Once for All Item or Run Once for Each item) :

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

<Tabs>

<TabItem value="run-all" label="Run Once for All Items">

### Use Case: Daily SAP SL Order Summary

**Scenario**:  
All SAP SL orders created in a day are received as an array.  
We generate a **daily sales summary report** and notify in Microsoft Teams with:

- Total revenue  
- Total number of orders  
- International order count  
- Order IDs  
- Top-selling product  

<img src="\img\platform\key-concepts\nodes\built-in\code\orderSummaryFlow.png" alt="connect html source" width="700"/>

---

### Why Run Once for All Items?

- `$payload` is an **Array of all orders**
- The code runs **only once**
- Since aggregation is required (summing totals, counting, finding max product), we must manually loop through all records.

> Aggregation requires iterating through the entire dataset.

---

### Example Code

```javascript
let totalRevenue = 0;
let internationalCount = 0;
let orderIds = [];
let productSales = {};
let currency = "$";

// Single loop to handle everything
for (let order of $payload) {
    if (!order) continue;

    // 1. Revenue & Currency
    if (order.DocTotal) {
      const docTotal = order.DocTotal; 
      if(order.DocCurrency="$"){
        totalRevenue +=  Math.round(docTotal) || 0;
      }
      else{
        totalRevenue +=  Math.round(docTotal)/82 || 0
      }
  }

    // 2. Order IDs
    if (order.DocNum !== undefined) {
        orderIds.push(order.DocNum);
    }

    // 3. International Check
    // Using optional chaining to prevent errors if TaxExtension is missing
    let country = order.TaxExtension?.CountryS || "";
    if(country == null || country == ""){
      country = "US";
    }
  
    if (country !== "US") {
        internationalCount++;
    }

    // 4. Product Sales
    if (order.DocumentLines) {
        for (let line of order.DocumentLines) {
            let productName = line.ItemDescription || line.ItemCode || "Unknown";
            let qty = line.Quantity || 0;
            productSales[productName] = (productSales[productName] || 0) + qty;
        }
    }
    else{
      continue
    }
}

// Find Top Product
let topProduct = "";
let maxQty = 0;
for (let [name, qty] of Object.entries(productSales)) {
    if (qty > maxQty) {
        maxQty = qty;
        topProduct = name;
    }
}

// ... rest of your message and return logic
 
var message =
    "<b>Daily Report:</b>

" +
    "We processed " + $payload.length +
    " orders today for a total of " + currency + totalRevenue + ".
" +
    "International orders: " + internationalCount + ".
" +
    "Order IDs Processed: " + orderIds.join(", ") + ".
" +
    "Top Product: " + topProduct + " (" + maxQty + " units).";
;

return [{
        json: {
            total_orders: $payload.length,
            total_revenue: totalRevenue,
            international_orders: internationalCount,
            order_ids: orderIds,
            top_selling_product: topProduct,
            top_product_quantity: maxQty,
            message: message
        }
    }];

```

**Output**
```JSON
[
  {
    "_pair_index": 0,
    "json": {
      "total_orders": 10,
      "total_revenue": 3947397,
      "international_orders": 0,
      "order_ids": [
        2103,
        2159,
        2160,
        2199,
        2200,
        2201,
        2202,
        2203,
        2204,
        2205
      ],
      "top_selling_product": "Biker Jacket",
      "top_product_quantity": 100,
      "message": "<b>Daily Report:</b>

We processed 10 orders today for a total of $3947397.
International orders: 0.
Order IDs Processed: 2103, 2159, 2160, 2199, 2200, 2201, 2202, 2203, 2204, 2205.
Top Product: Biker Jacket (100 units)."
    }
  }
]
```

</TabItem>

<TabItem value="run-each" label="Run Once for Each Item">

### Use Case: Convert Currency Symbols to ISO Codes

**Scenario 1**:  
SAP Service Layer sends Item prices using currency symbols (`$`, `€`, `£`, `₹`).  
Pipedrive requires ISO currency codes (`USD`, `EUR`, `GBP`, `INR`).  

We transform each item individually before sending to Pipedrive.

<img src="\img\platform\key-concepts\nodes\built-in\code\convertCurrencySymbolWorkflow.png" alt="connect html source" width="700"/>

---

### Why Run Once for Each Item?

- `$payload` is a **Single Object**
- The engine automatically runs the code once per item
- No manual loop over all items is required
- Ideal for record-level transformation

> This mode is best when modifying one record independently of others.

---

### Example Code

```javascript
const item = $payload;
if (Array.isArray(item.ItemPrices)) {
  item.ItemPrices = item.ItemPrices.map(price => {
    if (price.Currency) {
      switch (price.Currency.trim()) {
        case "$":
          price.Currency = "USD";
          break;
        case "€":
          price.Currency = "EUR";
          break;
        case "£":
          price.Currency = "GBP";
          break;
        case "₹":
          price.Currency = "INR";
          break;
        default:
          // keep original currency
          break;
      }
    }
    return price;
  });
}
return item;

```
**Output**

```JSON
  "ItemPrices": [
      {
        "PriceList": 1,
        "Price": 4544.45,
        "Currency": "USD",
        "AdditionalPrice1": 0,
        "AdditionalCurrency1": "",
        "AdditionalPrice2": 0,
        "AdditionalCurrency2": "",
        "BasePriceList": 1,
        "Factor": 1,
        "UoMPrices": []
      }
  ]
```
 ---

 ### Use Case: ShipStation Order Processing

**Scenario 2**:  
Order data is received in the workflow. Before creating an order in ShipStation, the data must be enriched and transformed to meet ShipStation's requirements.

The transformation includes:

- Converting item weight from kilograms to grams  
- Identifying whether the shipment is Domestic or International  
- Calculating an international shipping surcharge  

<img src="\img\platform\key-concepts\nodes\built-in\code\shipstationWorkflow.png" alt="connect html source" width="700"/>

---

### Why Run Once for Each Item?

- `$payload` represents **one order**
- The code runs once per order
- No aggregation across multiple orders is required
- Each order is processed independently

> This mode is ideal when enriching or formatting a single record before sending it to another system.

---

### Example Code

```javascript
const data = $payload;

if (!Array.isArray(data.items) || data.items.length === 0) {
  return {};
}

const order = data.items[0];
const country = order.shippingAddress?.country || "";

if (!Array.isArray(order.lineItems?.nodes)) {
  return {};
}

const processedLineItems = order.lineItems.nodes.map(item => {

  const weightKg = item.weight || 0;
  const weightGrams = Math.round(weightKg * 1000);

  let shipping_category = "Domestic";
  let international_surcharge = 0;

  if (country !== "USA") {
    shipping_category = "International";
    international_surcharge = 20 + (5 * weightKg);
  }

  return {
    ...item,
    weight_grams: weightGrams,
    shipping_category,
    international_surcharge,
    shipping_country: country
  };
});

return { processedLineItems };
```
**Output**
```JSON
[
  {
    "_pair_index": 0,
    "processedLineItems": [
      {
        "id": "gid://shopify/LineItem/17761653424437",
        "sku": "AB5353",
        "weight": 3.55,
        "quantity": 1,
        "title": "Armani Boots",
        "name": "Armani Boots",
        "originalUnitPriceSet": {
          "presentmentMoney": {
            "amount": "34343.43"
          }
        },
        "taxLines": [
          {
            "title": "CGST",
            "rate": 0.1,
            "priceSet": {
              "presentmentMoney": {
                "amount": "3434.35"
              }
            }
          },
          {
            "title": "IGSTKA",
            "rate": 0.091,
            "priceSet": {
              "presentmentMoney": {
                "amount": "3125.25"
              }
            }
          }
        ],
        "weight_grams": 3550,
        "shipping_category": "International",
        "international_surcharge": 37.75,
        "shipping_country": "India"
      },
      {
        "id": "gid://shopify/LineItem/17761653457205",
        "sku": "LB343",
        "weight": 4.44,
        "quantity": 1,
        "title": "Leather Boots",
        "name": "Leather Boots",
        "originalUnitPriceSet": {
          "presentmentMoney": {
            "amount": "343.43"
          }
        },
        "taxLines": [
          {
            "title": "CGST",
            "rate": 0.1,
            "priceSet": {
              "presentmentMoney": {
                "amount": "34.34"
              }
            }
          },
          {
            "title": "IGSTKA",
            "rate": 0.091,
            "priceSet": {
              "presentmentMoney": {
                "amount": "31.25"
              }
            }
          }
        ],
        "weight_grams": 4440,
        "shipping_category": "International",
        "international_surcharge": 42.2,
        "shipping_country": "India"
      }
    ]
  }
]
```
</TabItem>

</Tabs>
 
