## E-Commerce Platform

An online store sells products from multiple vendors. Customers place orders containing multiple products. Vendors supply products. This scenario introduces weak entities and complex multi-attribute relationships.


### Requirements

- Each customer has a Customer ID, name, email, and multiple shipping addresses.
- Each order has an Order ID, order date, and status. An order belongs to one customer.
- Each order contains one or more products with a quantity and unit price at time of purchase.
- Each product has a Product ID, name, description, and current price.
- Each vendor has a Vendor ID, name, and contact email.
- A product is supplied by one or more vendors; each vendor supplies many products.
- ORDER_ITEM is a weak entity that depends on ORDER — its key is (OrderID + ProductID).


<details>
  <summary>💡 Show Hints (attempt first!)</summary>

- 💡 ORDER_ITEM is a weak entity — its existence depends on ORDER
- 💡 Customer has a multi-valued attribute: ShippingAddress (multiple addresses)
- 💡 The supply relationship SUPPLIES between VENDOR and PRODUCT is M:N
- 💡 Unit price at time of purchase goes on ORDER_ITEM, not PRODUCT (price may change)
- 💡 Order status (Pending, Shipped, Delivered) is a single-valued attribute of ORDER
</details>

<details>
    <summary>Reveal Answer & Diagram</summary>

<details>
<summary>ER Diagram</summary>
           
- [ER diagram](https://github.com/PankajKumarAgrawal1729/ER-Models-Practice/blob/main/E-Commerce%20Platform/ERDiagram.png)
    </details>
 <details>
        <summary>Entities & Rels</summary>

- Entities
    - CUSTOMER
    - ORDER
    - ORDER_ITEM (weak)
    - PRODUCT
    - VENDOR
- Relationships
    - PLACES CUSTOMER ↔ ORDER (1:N)
    - CONTAINS (identifying) ORDER ↔ ORDER_ITEM (1:N)
    - REFERENCES ORDER_ITEM ↔ PRODUCT (N:1)
    - SUPPLIES VENDOR ↔ PRODUCT (M:N)
    </details>

    <details>
        <summary>Analysis</summary>

#### ✦ Key Concepts in This Exercise

##### Weak Entity: ORDER_ITEM
- ORDER_ITEM cannot exist without ORDER. Its partial key is ProductID — combined with the owning entity's PK (OrderID), it forms a composite key. Use double rectangle for the weak entity and double diamond for the identifying relationship.

##### Why Unit Price is on ORDER_ITEM
- Product prices change over time. If you store price on PRODUCT, you lose the historical price at order time. Storing UnitPrice on ORDER_ITEM captures the price at the moment of purchase — this is a critical business requirement.

##### Multi-valued Attribute
- ShippingAddress on CUSTOMER should be a double oval (multi-valued attribute) since a customer can have multiple shipping addresses. In SQL, this would become a separate table.

- ⚠️ Don't make ORDER_ITEM a regular entity — it has no meaning outside of an ORDER
- ⚠️ Don't put the current product price on ORDER_ITEM — it should be UnitPriceAtPurchase
- ⚠️ SUPPLIES between VENDOR and PRODUCT is M:N because a product can come from multiple vendors
- ⚠️ Don't forget: weak entities use double rectangles AND double diamonds for their identifying relationship
    </details>
</details>
