# Use ReserveInventory setting to disable committed inventory computation

## Merchants can configure whether HotWax should consider committed inventory while calculating online ATP if Shopify is the inventory source.

Retailers can now use the ReserveInventory setting on their Product Store to configure if the OMS should consider order queues as committed inventory. If the OMS is not the source of sellable inventory, retailers can disable ReserveInventory which will stop accounting for order queues such as the Brokering Queue, Pre-order Queue and more when computing valid inventory counts.

When the OMS is reading inventory levels from systems, like Shopify, that commit inventory for open orders before publishing inventory to external systems, deducting order queues leads to double inventory reservations in the OMS. Lower inventory levels in OMS lead to further ramifications for merchants that use the OMS for pre-orders. Products end up being listed for pre-order even though they have physical inventory available that is simply being held by open order queues. Inaccurately accepting regular orders as pre-orders reduces the upcoming PO’s inventory, leading to lost sales when the product actually enters pre-order because PO ATP has been promised to normal orders.

Using Reserve Inventory to toggle if order queues are accounted for when computing valid inventory, prevents retailers from underselling pre-orders when HotWax is not responsible for computing sellable inventory.

Merchants using HotWax Commerce OMS can toggle the product store setting “ReserveInventory” and configure if HotWax should reduce committed inventory again.

*Internal quote* 

*Customer quote*
