# Shopping App Schema Design

## User Story

As a shopper, I want to be able to browse a catalog of products and add items to my shopping cart. I also want to be able to view the contents of my cart and adjust the quantity of items in my cart. Finally, I want to be able to place an order and receive confirmation of my order.

## Requirement Analysis

### Entities:

Products: A catalogue has a list of products, each with a name, quantity and price.
Cart: 
Customers: A customer has a unique identifier, name, email, and password.
Orders: An order has a unique identifier, the customer who placed it, a list of items, and the total amount.

### Relationships:
A customer can view the Products catalogue and place an order.
An order can contain multiple items.

## NoSQL Schema Design

Based on the requirements analysis, the following schema can be designed:

### Product Collection:

```
{
   _id: ObjectId,
   name: string,
   quantity: number,
   price: number
}

```

### Customers Collection:

```
{
   _id: ObjectId,
   name: string,
   email: string,
   password: string
}

```

### Items Collection:
```
{
   _id: ObjectId,
   productId: ObjectId,
   quantity: number,
   price: number
}

```

### Cart Collection:
```
{
   _id: ObjectId,
   items: [
     {
        itemId: ObjectId,
        quantity: number
     }
   ],
   totalQuantity: number,
   totalPrice: number
}

```

### Orders Collection:

```
{
   _id: ObjectId,
   customerId: ObjectId,
   items: [
     {
        itemId: ObjectId,
        quantity: number
     }
   ],
   totalAmount: number,
   status: string,
   orderDate: date,
   deliveryAddress: string
}

```

## API Endpoints

```
-   GET /products - Get a list of all products in the catalogue.
-   GET /products/:{productsId} - Get details of a specific products.
-   GET /custormers/:{customerId}/cart - Get the list of items added to cart by a customer.
-   PUT /custormers/:{customerId}/cart - Update the list of items and their quantities added to cart by a customer.
-   POST /custormers/:{customerId}/orders - Place an order for the items selected by the customer.
-   GET /custormers/:{customerId}/orders/ordersId - Get the details of a specific order(confirmation of order).
```