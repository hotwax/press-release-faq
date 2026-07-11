# Managing Third-Party Fulfillment Services
## How HotWax Commerce harmonizes orders routed by Shopify and orders brokered by the OMS while respecting fulfillment holds.

Retailers often use a mix of fulfillment strategies: in-house warehouses and third-party logistics (3PLs). Friction arises when an OMS attempts to route orders that Shopify has already committed to a specific 3PL, or when marketplace integrations import orders with mandatory "cooling periods" (fulfillment holds) that should not be processed instantly.

HotWax Commerce natively supports a hybrid fulfillment architecture, seamlessly handling different routing flows without conflict by aligning with Shopify's Fulfillment Orders API:

1. **Shopify-Assigned Fulfillment Services (Shopify Routing):** 
When a retailer uses a 3PL or Print on Demand (POD) app installed directly on Shopify (e.g., Printful, Quickbox, Amazon MCF), Shopify assigns a specific `fulfillment_service` to the line items and naturally separates them into dedicated Fulfillment Orders. During order import, HotWax detects this `fulfillment_service` string, maps it to a corresponding Facility ID in HotWax, and allocates the item directly to that facility. HotWax intentionally bypasses its own brokering engine for these items, perfectly respecting Shopify's routing decision. When the external application fulfills the order in Shopify, HotWax consumes the fulfillment webhook to mark the item as Completed internally, maintaining financial synchronization without interfering with the 3PL's workflow.

2. **OMS-Assigned 3PL Fulfillment (HotWax Routing):** 
When a retailer uses HotWax as the central decision engine, Shopify acts strictly as the storefront. HotWax ingests the unassigned orders, evaluates them in the routing engine, and assigns them to a 3PL warehouse based on inventory availability and proximity. To keep systems aligned, HotWax executes the Shopify GraphQL `fulfillmentOrderMove` mutation to transfer the Shopify Fulfillment Order to the mapped Shopify Location. Once the 3PL packs and ships the order, HotWax calls the Shopify GraphQL `fulfillmentCreate` mutation to finalize the fulfillment and publish the tracking information to the storefront.

### Respecting Fulfillment Orders and Holds
To prevent premature processing of marketplace orders (or orders requiring a cooling period), HotWax actively monitors Shopify's Fulfillment Orders API and webhook events (`fulfillment_holds/added` and `fulfillment_holds/released`). If a merchant's workflow places an order on hold, HotWax honors the `fulfillment_holds` payload, placing the order in an internal `ORDER_HOLD` status. This guarantees that held orders are never picked up by downstream 3PL routing processes until the hold is explicitly released in Shopify.

### FAQs

**Question 1: Does the current Shopify `fulfillment_service` logic fit into this architecture?**

Answer: Yes. HotWax natively looks for the `fulfillment_service` attribute on imported line items. If it exists, HotWax uses a system mapping (`SHOP_FULL_SRVC_ALLOC`) to translate the Shopify fulfillment service name into a specific HotWax Facility ID, ensuring the order goes exactly where Shopify intended.

**Question 2: What happens if a single order contains some items for a Shopify 3PL and other items that require HotWax routing?**

Answer: HotWax Commerce supports split fulfillments natively. It will split the order into multiple "Ship Groups." The items tagged with a Shopify `fulfillment_service` are assigned to the mapped 3PL facility and bypassed by the broker, while the remaining items are sent through the HotWax brokering engine for dynamic allocation.

### Internal FAQs

**Question 1: How does HotWax map Shopify fulfillment services to internal facilities?**

Answer: HotWax uses the `ShopifyShopTypeMapping` entity in the database. It filters for the `SHOP_FULL_SRVC_ALLOC` mapping type, comparing the incoming `fulfillment_service` string (e.g., "amazon_mcf") to the `mappedKey`, and assigns the item to the corresponding `mappedValue` (the HotWax FacilityId).

**Question 2: How does HotWax determine whether to run brokering or skip it for an imported line item?**

Answer: During order ingestion, HotWax checks each line item for a `fulfillment_service` attribute in the Shopify payload. If the value matches a configured `SHOP_FULL_SRVC_ALLOC` mapping, the item is pre-allocated to the mapped facility and the brokering engine skips it entirely. Items without a matching `fulfillment_service` enter the standard brokering queue.
