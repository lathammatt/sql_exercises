#  Provide a query showing Customers (just their full names, customer ID and country) who are not in the US.

SELECT FirstName || " " || LastName AS "FullName", CustomerId, Country FROM Customer
Where Country <> "USA"

#  Provide a query only showing the Customers from Brazil.

SELECT FirstName || " " || LastName AS "FullName", CustomerId, Country FROM Customer
Where Country = "Brazil"

#  Provide a query showing the Invoices of customers who are from Brazil. The resultant table should show the customer's full name, Invoice ID, Date of the invoice and billing country.

SELECT Invoiceid, InvoiceDate, BillingCountry, Customer.FirstName || " " || Customer.LastName AS "FullName" FROM Invoice
JOIN Customer On Invoice.CustomerID = Customer.CustomerId
Where Customer.Country = "Brazil" 

#  Provide a query showing only the Employees who are Sales Agents.

SELECT FirstName || " " || LastName AS "FullName" FROM Employee
Where Title = "Sales Support Agent" 

#  Provide a query showing a unique list of billing countries from the Invoice table.

SELECT BillingCountry FROM Invoice
GROUP BY BillingCountry

#  Provide a query showing the invoices of customers who are from Brazil.

SELECT Invoiceid FROM Invoice
JOIN Customer On Invoice.CustomerID = Customer.CustomerId
Where Customer.Country = "Brazil" 

#  Provide a query that shows the invoices associated with each sales agent. The resultant table should include the Sales Agent's full name.

SELECT Invoiceid, Employee.FirstName || " " || Employee.LastName AS "FullName" FROM Invoice
JOIN Customer ON Invoice.CustomerID = Customer.CustomerId
JOIN Employee ON Customer.SupportRepId = Employee.EmployeeId
WHERE Employee.Title = "Sales Support Agent" 

#  Provide a query that shows the Invoice Total, Customer name, Country and Sale Agent name for all invoices and customers.

SELECT Total, Customer.FirstName || " " || Customer.LastName AS "Customer FullName", Customer.Country, Employee.FirstName || " " || Employee.LastName AS "Sales Agent" FROM Invoice
JOIN Customer ON Invoice.CustomerID = Customer.CustomerId
JOIN Employee ON Customer.SupportRepId = Employee.EmployeeId

#  How many Invoices were there in 2009 and 2011? What are the respective total sales for each of those years?

