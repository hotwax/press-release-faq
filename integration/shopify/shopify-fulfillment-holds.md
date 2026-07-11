# Respecting Shopify Fulfillment Holds
## HotWax Commerce automatically pauses order brokering and fulfillment when a fulfillment hold is applied in Shopify, supporting Fulfillment Orders, hybrid routing, and post-shipment events.

Many retailers use third-party apps, marketplace integrations, or custom flows for fraud analysis, address validation, or "cooling off" periods, which can apply a temporary fulfillment hold on an order in Shopify. If an Order Management System (OMS) ignores these holds and imports the order for immediate processing, it could lead to the fulfillment of fraudulent orders or orders with invalid details.

HotWax Commerce natively respects Shopify fulfillment holds to prevent premature fulfillment. Under the hood, HotWax integrates with Shopify's **Fulfillment Orders API**. This allows Shopify to split an order into multiple `FulfillmentOrder` records based on the fulfillment locations or services assigned (e.g., separating merchant-managed warehouse items from Print-on-Demand (POD) or dropship items). HotWax only imports and manages the Fulfillment Orders assigned to locations it is configured to control.

### How the Ingestion Flow Works
- **Order Download**: When an order is created or updated, the OMS fetches complete order details via Shopify's GraphQL API (`get#ShopifyOrderDetails`). This query retrieves the status of the order's Fulfillment Orders, including any active fulfillment holds.
- **Auto-Approval**: All downloaded orders are initially created in `ORDER_CREATED` status. Real-time Service Condition Actions (SECAs) evaluate the order. If an active fulfillment hold is detected on any of the Fulfillment Orders, the OMS defers approval, keeping the order in `ORDER_CREATED` status so it is excluded from brokering and routing.
- **Fulfillment Holds Added**: If a hold is added in Shopify *after* an order has already been approved in HotWax, the OMS consumes the `fulfillment_holds/added` webhook and immediately transitions the order status from `ORDER_APPROVED` to `ORDER_HOLD`.
- **Fulfillment Holds Released**: When all holds are released in Shopify, the `fulfillment_holds/released` webhook triggers HotWax to update the order. The auto-approval SECA re-evaluates the order and transitions it to `ORDER_APPROVED` status.
- **Hybrid Routing Mapping**: For items assigned to unmapped third-party locations (like Print-on-Demand or dropshippers), HotWax automatically ignores and excludes them from downstream OMS allocation. When HotWax determines the optimal warehouse for the remaining items, it uses the `fulfillmentOrderMove` GraphQL mutation to update the assignment in Shopify.
- **Post-Shipment Progress Tracking**: In addition to updating the status, HotWax Commerce (or its integrated shipping aggregator) tracks shipment delivery milestones (e.g., in transit, out for delivery, delivered) and updates Shopify in real time using the `fulfillmentEventCreate` mutation.

### FAQs

**Question 1: What happens if an order is already in the brokering queue when a fulfillment hold is added in Shopify?**

Answer: HotWax Commerce consumes the `fulfillment_holds/added` webhook and immediately transitions the order status from `ORDER_APPROVED` to `ORDER_HOLD` in the OMS. If the order has not been fulfilled yet, the system will suspend any further processing or allocation until the hold is released.

**Question 2: Does HotWax Commerce sync the reason for the fulfillment hold?**

Answer: Yes, the hold reason provided by Shopify is mapped to the order notes in HotWax Commerce, giving customer service representatives clear visibility into why an order's fulfillment is paused.

**Question 3: What happens if a Shopify order contains a mix of warehouse items and POD/third-party items?**

Answer: Shopify splits the order into separate Fulfillment Orders. HotWax Commerce only imports and brokers the Fulfillment Orders assigned to locations it manages. The POD/third-party Fulfillment Order remains untouched in Shopify and is processed independently, preventing duplicate fulfillment.

### Internal FAQs

**Question 1: How does HotWax OMS detect fulfillment holds during the initial order import?**

Answer: During order download (via webhooks or scheduled sync), the OMS queries Shopify's GraphQL API (`get#ShopifyOrderDetails`) to retrieve complete order details, which includes the status of the order's Fulfillment Orders. If an active hold is found on any of the Fulfillment Orders, the OMS defers approval, leaving the order in the `ORDER_CREATED` status.

**Question 2: How is the order released from hold in HotWax Commerce?**

Answer: When all holds are removed from the fulfillment order in Shopify, a `fulfillment_holds/released` webhook is triggered. HotWax processes this event, updating the order information. This update triggers the auto-approval SECA, which re-evaluates the order and transitions it to `ORDER_APPROVED` status.

**Question 3: Does HotWax generate manual CS tasks (like `RESOLVE_ONHOLD_ORDER`) for Shopify fulfillment holds?**

Answer: No. Since Shopify fulfillment holds are resolved directly on Shopify (either automatically by risk/fraud apps or manually by CSRs) and HotWax automatically syncs the release status, creating manual CS tasks in the OMS is not required. This prevents duplicate work for CSRs across multiple systems.
