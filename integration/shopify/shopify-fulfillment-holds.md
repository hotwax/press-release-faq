# Respecting Shopify Fulfillment Holds
## HotWax Commerce automatically pauses order brokering and fulfillment when a fulfillment hold is applied in Shopify.

Many retailers use third-party apps for fraud analysis, address validation, or "cooling off" periods, which can apply a temporary fulfillment hold on an order in Shopify. If an Order Management System ignores these holds and imports the order for immediate processing, it could lead to the fulfillment of fraudulent orders or orders with invalid addresses.

HotWax Commerce natively respects Shopify fulfillment holds to prevent premature fulfillment. When importing orders, HotWax checks the hold status. If an order is placed on hold in Shopify, HotWax imports the order but sets its status to "Hold," excluding it from the brokering and routing engine. 

Furthermore, HotWax Commerce listens to Shopify's `fulfillment_holds/added` and `fulfillment_holds/released` webhooks to keep the order status synchronized in real time. Once the hold is resolved in Shopify (e.g., the fraud check passes), HotWax automatically updates the order status to "Approved," making it instantly eligible for order routing and fulfillment.

### FAQs

**Question 1: What happens if an order is already in the brokering queue when a fulfillment hold is added in Shopify?**

Answer: HotWax Commerce consumes the `fulfillment_holds/added` webhook and immediately places the order on "Hold." If the order hasn't been fulfilled yet, the system will suspend any further processing or allocation until the hold is released.

**Question 2: Does HotWax Commerce sync the reason for the fulfillment hold?**

Answer: Yes, the hold reason provided by Shopify is mapped to the order notes in HotWax Commerce, giving customer service representatives clear visibility into why an order's fulfillment is paused.

### Internal FAQs

**Question 1: How does HotWax OMS detect fulfillment holds during the initial order import?**

Answer: During the `orders/create` or `orders/updated` webhook ingestion, the OMS checks the Shopify payload for active fulfillment holds. If a hold exists, the order is created with an `ORDER_HOLD` status instead of the standard `ORDER_APPROVED` status.

**Question 2: How is the order released from hold in HotWax Commerce?**

Answer: When the hold is removed in Shopify, a `fulfillment_holds/released` webhook is triggered (or an `orders/updated` webhook with the hold removed). HotWax processes this event and transitions the order status from `ORDER_HOLD` to `ORDER_APPROVED`, releasing it to the brokering engine.
