


CREATE TABLE ProductDetails_1NF (
  OrderID INT,
  CustomerName VARCHAR(255),
  Product VARCHAR(255)
);

INSERT INTO ProductDetails_1NF (OrderID, CustomerName, Product)
SELECT OrderID, CustomerName, value
FROM (
  SELECT OrderID, CustomerName, Products,
    STRING_SPLIT(Products, ',') AS value
  FROM ProductDetail
) AS ProductDetails;




CREATE TABLE Orders (
  OrderID INT PRIMARY KEY,
  CustomerName VARCHAR(255)
);

CREATE TABLE OrderDetails (
  OrderID INT,
  Product VARCHAR(255),
  Quantity INT,
  FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);

INSERT INTO Orders (OrderID, CustomerName)
SELECT DISTINCT OrderID, CustomerName
FROM OrderDetails;

INSERT INTO OrderDetails (OrderID, Product, Quantity)
SELECT OrderID, Product, Quantity
FROM OrderDetails;
