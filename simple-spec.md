# First Pass at Spec
At a high level, how could this system work, and what further digging needs to be done?

## Requirements
For ecommerce data, brands are the source of truth.  Only brands should be allowed to create or change data.

- Requirement: Verified brand signatures
- Requirement: Brands can join network
- Requirement: Brands IRL can join the network and remove imposters

Brands can create, update, and delete products from the system.  Anyone can read products.  Brands can also categorize products to align with their marketing initiatives

- Requirement: System can issue new ids for products
- Requirement: Only registered brands can create products
- Requirement: System can store product data for a given product id
- Requirement: System will process updates issued by the product's brand owner

## Sample implementation

- Trusted contract owner whitelists brands (new brand whitelisting could be further decentralized in steady-state, but trusted system to bootstrap)
- Brands generate JSON data and store on IPFS
  - Tech savvy brands could do this themselves, otherwise work with a tech partner
  - ( How to store the top-level hash per brand?  Where do the keepers look for content? )
- Chainlink Keepers contract tracks product content via IPFS hash
  - Contract would index by product id at least
  - Possibly add more complex indices like a brand's "fall line", or tags
- An update to a product would be triggred if the brand changes the ipfs hash
- A brand can exit voluntrily by unpinning any ipfs content, or the trusted owner can force-exit a brand