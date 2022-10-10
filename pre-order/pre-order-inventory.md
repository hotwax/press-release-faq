# Pre-order inventory on Shopify

## Merchants want to make sure they don't oversell when taking pre-orders because of gaps in scheduled jobs.

Calculating pre-orderable inventory directly in Shopify as pre-orders are captured on eCommerce helps retailers ensure that they oversell as little as possible. Customers that order multiple quantities of the same SKU can also be stopped from over ordering right from the product detail page, which often helps with B2B sellers.

HotWax Commerce maintains a pre-order catalog to ascertain qualified pre-orderable items. The algorithm ensures items that can be pre-ordered are added and items that should be removed are delisted every 15 minutes. HotWax Commerce doesn’t push actual on-order ATP to Shopify, instead it just syncs valid and invalid pre-order items using independent operations. While a merchant waits for exhausted pre-order items to be delisted, they may be overselling a sold out pre-order item because of the time lag in publishing the latest pre-order catalog to Shopify. Syncing the actual pre-orderable quantity is especially crucial in cases when order velocity is high. Overselling also dramatically increases workload on CSRs that have to find a way to appease customers when they cancel pre-orders.

HotWax Commerce will push actual on-order inventory levels to Shopify for every pre-order item allowing Shopify to stop accepting pre-orders when the pre-order inventory will exhaust. The functionality will make sure that customers may only order the exact amount that is available and not more.

Merchants already upload purchase orders to HotWax Commerce, so they will automatically receive this feature to push pre-orderable quantity from purchase orders and to Shopify.
