# Unify pre-order backorder listing-delisting

## Listing-delisting operations for pre-order and backorder products should be synchronized.

HotWax now lists and delists pre-order and backorder products in a single API call, ensuring that a product is removed only if it is not on pre-order or backorder. Unified listing-delisting operations helps in correctly amending products transitioning from pre-order to backorder on Shopify.

When a product exits pre-order and enters the backorder category, HotWax may first list it for backorder on Shopify before delisting it from pre-order. Because of the pre-order delisting operation the inventory policy for the product gets disabled even though the product should be available for backorder. When a product is incorrectly delisted on Shopify, backorder products appear “out of stock” on the eCommerce PDP, which costs retailers potential sales.

Running listing-delisting from a unified API call will ensure the products are added and removed from pre-order or backorder accurately when transitioning from one category to the other. Synchronized operations also help in displaying up to date pre-order and backorder products on the eCommerce PDP.

To unify pre-order and backorder listing-delisting, retailers will need to disable their existing pre-order and backorder jobs and switch to the new jobs from the Job Manager App.

## Testimony

*Internal quote*: Running independent jobs for pre-order and backorder listing-delisting results in incorrectly modifying inventory policy for products in Shopify. A unified API call will help ensure that pre-order and backorder products on Shopify are updated correctly.
