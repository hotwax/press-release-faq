# Webhook based Shopify GraphQL file processing speed 

## GraphQL files should automatically be processed as soon as Shopify finishes processing an operation.

Shopify’s file processing status webhook lets HotWax Commerce know when Shopify has finished an operation so that the next GraphQL file can be requested for processing. Automatically picking the latest file that is ready to process ensures optimized execution time while respecting Shopify rate limits. 

Shopify usually processes GraphQL files within a minute or two but when a request to process a new file is submitted at the default interval of 15 minutes, the integration process is unnecessarily delayed. If HotWax reduces the interval between pushing pending files to expedite the file processing speed, it often results in exceeding Shopify rate limits, overlapping multiple files, and failed operations.

HotWax uses the GraphQL file processing status webhook to make sure that the next file is pushed for processing in Shopify immediately after it finishes an operation. Switching to the next GraphQL file only after an ongoing operation is completed also helps to work around Shopify rate limits. Not waiting for a timer to run down to pick a file ensures more files are processed in the least amount of time.

Merchants using HotWax Commerce will automatically be switched to using webhook based Shopify GraphQL file processing procedure.

*Internal quote* 

*Customer quote* 
