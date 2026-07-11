# Real-Time Post-Shipment Event Tracking
## HotWax Commerce offers a flexible, tiered architecture to sync granular post-shipment delivery events back to Shopify, ensuring accurate tracking updates for every retailer's unique ecosystem.

Once an order is fulfilled and handed off to a carrier, the customer's anxiety about delivery begins. Traditionally, OMS and ERP systems only send the initial tracking number and carrier name back to Shopify. This forces customers to leave the retailer's ecosystem and visit the carrier's website to check the delivery progress, reducing post-purchase engagement and increasing "Where is my order?" (WISMO) support tickets.

Because HotWax Commerce acts as the central OMS for multiple retailers—each with different carrier networks and tracking tools—we solve this by offering a flexible, three-tiered tracking architecture:

1. **Native Tracking Sync (The Fallback):** For retailers not requiring granular tracking, HotWax pushes the standard initial fulfillment payload (Carrier Name, Tracking Number, Tracking URL) to Shopify.
2. **Platform-Level Aggregator Integration (Recommended):** HotWax seamlessly integrates with third-party tracking aggregators. By consuming unified webhooks from the aggregator, HotWax pushes granular delivery updates—such as "In Transit," "Out for Delivery," and "Delivered"—directly back to Shopify using the `fulfillmentEventCreate` GraphQL API mutation.
3. **Direct Major Carrier Integrations:** For retailers relying exclusively on the big carriers (like FedEx and UPS), HotWax can natively consume direct carrier webhooks and translate them into Shopify GraphQL mutations, removing the need for a middleman.

This tiered integration ensures that the Shopify Order Status Page is always up-to-date with the latest delivery milestones, significantly reducing customer service inquiries and improving post-purchase satisfaction, regardless of the retailer's technical stack.

### FAQs

**Question 1: What types of post-shipment statuses are synced to Shopify?**

Answer: When using the aggregator or direct carrier tiers, HotWax Commerce maps tracking statuses to Shopify's standard fulfillment events, including `in_transit`, `out_for_delivery`, `delivered`, `attempted_delivery`, and `failure`.

**Question 2: Do customers get notified when these tracking events occur?**

Answer: Yes, depending on the retailer's Shopify notification settings, syncing these events via the `fulfillmentEventCreate` API can trigger automated Shopify emails or SMS updates (e.g., an "Out for Delivery" notification) without requiring additional marketing apps on Shopify.

### Internal FAQs

**Question 1: Which Shopify API is used to update the tracking events?**

Answer: HotWax Commerce uses the Shopify GraphQL Admin API, specifically the `fulfillmentEventCreate` mutation. This mutation requires the `fulfillmentId` and the specific `status` of the event.

**Question 2: Why does HotWax Commerce use a tiered architecture for post-shipment tracking instead of a single integration method?**

Answer: Because HotWax acts as a central OMS for multiple retailers, it must support highly diverse technical ecosystems. Some retailers utilize third-party tracking apps, some rely exclusively on major carriers, and others use niche regional networks. A tiered architecture ensures HotWax can seamlessly push granular updates for advanced setups (via aggregators or direct major carrier hooks), while still providing a reliable fallback (Native Tracking Sync) for retailers who do not use tracking apps, all without forcing unnecessary engineering constraints.

**Question 2: How does HotWax Commerce normalize tracking statuses from different sources before pushing them to Shopify?**

Answer: HotWax maps incoming carrier or aggregator statuses to Shopify's standardized `FulfillmentEventStatus` enum values (e.g., `IN_TRANSIT`, `OUT_FOR_DELIVERY`, `DELIVERED`). This normalization layer ensures consistent status updates regardless of whether the source is a direct carrier webhook or an aggregator.
