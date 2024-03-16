# Shopping Site 

## Entities 

### User
- id 
- created_at
- updated_at
- type (vendor, customer)

### Product 
- id                    // sku 
- group_id      
- created_at            
- updated_at
- vendor_id             reference(user.id) && user.type == vendor
- quantity
- variant
  - eg1: {size: XL, color: red}
  - eg2: {size: L, color: white}  
- marked_price          // in INR, paise
- sale_price            // in INR, paise 

### Cart
- id
- created_at
- updated_at
- user_id               // reference(user.id)
  -                     // if global cart => set field unique

### Order 
- id 
- created_at
- updated_at
- user_id
- status           (created, processing, shipped, delivered, cancelled)
- billing_address_id
- shipping_address_id

### Payment 
- id 
- created_at
- updated_at
- method            (credit_card, debit_card, net_banking, wallet, cash_on_delivery)
- status            (pending, success, failed)

### Address
- id
- created_at
- updated_at
- user_id
- type             (home, office, other)
- line1
- line2
- city
- state
- country
- pincode

### Mapping Entities 

#### Cart Product 
- cart_id
- product_id
- quantity

#### Order Product 
- order_id
- product_id
- quantity

#### Order Payment
- order_id
- payment_id


## Functional Requirements 

### User 
- Guest can register as user (self-choice vendor vs customer)
- Guest can login as user (if they have registered already)
- User can logout 
- User can update their profile details 
  - customer -> vendor allowed (vice-versa not allowed) 
- Addresses
  - Users can add addresses 
  - Users can edit addresses
  - Users can delete addresses

### Product 
- Vendor can add product
- Vendor can update product
- Guests can list all products 
  - filter by vendor
  - search by name
  - filter by price
- Guests can list details of a single product

### Cart 
- User can add product to cart
  - User can change quantity of product in cart
- User can remove product from cart

### Order
- User can place order
  - User can select address for billing
  - User can select address for shipping
- User can fetch all orders
  - sort by created 
- User can fetch order by order_id 
- User can cancel order
  - order status should be `created` or `processing`

### Payment
- User can pay for order
  - User can select payment method
- User can see payment status