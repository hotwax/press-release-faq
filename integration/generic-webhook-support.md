# Generic webhook support 
 
## Parameterized webhook endpoint URLs allow users to connect their OMS to webhook topics with clear actions and integration definitions.

Generic webhook support allows setting parameterized and logically built naming conventions across all webhook integrated systems. Standardized webhook URLs ensure accurate mappings for multiple systems and also help developers easily run a transformation or scale operations without any unpredictable URL variation.

Systems, like Shopify, broadcasts order or inventory updates to OMS at hardcoded webhook URLs. Developers end-up creating URLs based on their preferences when integrating new systems with OMS. Inconsistent naming often results in difficulty to manage integrations across multiple systems.

Clearly defining URL naming conventions will ensure uniform webhook URLs for all the systems connected with OMS. System generated webhook URLs will allow developers to work around multiple systems systematically and independently extend operations. Deriving consistent URL parameters for the integrated systems will also help in deploying new transformations without restructuring the existing URL framework.

To start using standardized naming conventions users will need to re-subscribe their existing webhooks to the new URLs. For initial set-up, developers will need to feed the operation/action, configuration and transformation ID. When establishing a new integration with OMS, only the configuration ID will be swapped, keeping the standard format unchanged.

*Internal quote*

*Customer quote* 
