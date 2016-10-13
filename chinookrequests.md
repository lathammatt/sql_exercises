####  Provide a query showing Customers (just their full names, customer ID and country) who are not in the US.

SELECT FirstName || " " || LastName AS "FullName", CustomerId, Country FROM Customer  
WHERE Country <> "USA"  

####  Provide a query only showing the Customers from Brazil.

SELECT FirstName || " " || LastName AS "FullName", CustomerId, Country FROM Customer  
WHERE Country = "Brazil"  

####  Provide a query showing the Invoices of customers who are from Brazil. The resultant table should show the customer's full name, Invoice ID, Date of the invoice and billing country.

SELECT InvoiceId, InvoiceDate, BillingCountry, Customer.FirstName || " " || Customer.LastName AS "FullName" FROM Invoice  
JOIN Customer On Invoice.CustomerID = Customer.CustomerId  
WHERE Customer.Country = "Brazil"   

####  Provide a query showing only the Employees who are Sales Agents.

SELECT FirstName || " " || LastName AS "FullName" FROM Employee  
WHERE Title = "Sales Support Agent"  

####  Provide a query showing a unique list of billing countries from the Invoice table.

SELECT BillingCountry FROM Invoice  
GROUP BY BillingCountry  

####  Provide a query showing the invoices of customers who are from Brazil.

SELECT \* FROM Invoice  
JOIN Customer On Invoice.CustomerID = Customer.CustomerId  
WHERE Customer.Country = "Brazil"  

####  Provide a query that shows the invoices associated with each sales agent. The resultant table should include the Sales Agent's full name.

SELECT InvoiceId, Employee.FirstName || " " || Employee.LastName AS "FullName" FROM Invoice  
JOIN Customer ON Invoice.CustomerID = Customer.CustomerId  
JOIN Employee ON Customer.SupportRepId = Employee.EmployeeId  
WHERE Employee.Title = "Sales Support Agent"  

####  Provide a query that shows the Invoice Total, Customer name, Country and Sale Agent name for all invoices and customers.

SELECT Total, Customer.FirstName || " " || Customer.LastName AS "Customer FullName", Customer.Country, Employee.FirstName || " " || Employee.LastName AS "Sales Agent" FROM Invoice  
JOIN Customer ON Invoice.CustomerID = Customer.CustomerId  
JOIN Employee ON Customer.SupportRepId = Employee.EmployeeId  

####  How many Invoices were there in 2009 and 2011? What are the respective total sales for each of those years?

SELECT COUNT(Total) FROM Invoice  
WHERE InvoiceDate LIKE "2009%"  

SELECT COUNT(Total) FROM Invoice  
WHERE InvoiceDate LIKE "2011%"  

SELECT SUM(Total) FROM Invoice  
WHERE InvoiceDate LIKE "2009%"  

SELECT SUM(Total) FROM Invoice  
WHERE InvoiceDate LIKE "2011%"  

#### Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for Invoice ID 37.

SELECT COUNT(InvoiceId) FROM InvoiceLine  
WHERE InvoiceID = "37"  

#### Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for each Invoice.

SELECT COUNT(InvoiceId) FROM InvoiceLine  
GROUP BY InvoiceId  

#### Provide a query that includes the track name with each invoice line item.

SELECT InvoiceLine.\*, Track.Name FROM InvoiceLine  
JOIN Track ON InvoiceLine.TrackId = Track.TrackId  

#### Provide a query that includes the purchased track name AND artist name with each invoice line item.

SELECT InvoiceLine.\*, Track.Name AS "Song", Artist.Name AS "Artist" FROM InvoiceLine  
JOIN Track ON InvoiceLine.TrackId = Track.TrackId  
JOIN Album ON Track.AlbumId = Album.AlbumId  
JOIN Artist ON Album.ArtistId = Artist.ArtistId  

#### Provide a query that shows the # of invoices per country.

SELECT COUNT(InvoiceId) As "Invoice Total", Customer.Country FROM Invoice  
JOIN Customer ON Invoice.CustomerId = Customer.CustomerId  
GROUP BY Customer.Country  

#### Provide a query that shows the total number of tracks in each playlist. The Playlist name should be include on the resultant table.

SELECT COUNT(PlaylistTrack.PlaylistId) AS "Number of Tracks", Playlist.Name AS "Playlist Name" FROM PlaylistTrack  
JOIN Playlist ON PlaylistTrack.PlaylistId = Playlist.PlaylistId  
GROUP BY Playlist.Name  

#### Provide a query that shows all the Tracks, but displays no IDs. The resultant table should include the Album name, Media type and Genre.

SELECT Track.Name AS "Song Name", Album.Title AS "Album", MediaType.Name AS "Media Type", Genre.Name AS "Genre" FROM Track  
JOIN Album ON Track.AlbumId = Album.AlbumId  
JOIN MediaType ON Track.MediaTypeId = MediaType.MediaTypeId  
JOIN Genre ON Track.GenreId = Genre.GenreId  

#### Provide a query that shows all Invoices but includes the # of invoice line items.

SELECT Invoice.\*, COUNT(InvoiceLine.InvoiceId) AS "Count" FROM Invoice  
JOIN InvoiceLine ON Invoice.InvoiceId = InvoiceLine.InvoiceId  
GROUP BY Invoice.InvoiceId  


#### Provide a query that shows total sales made by each sales agent.

SELECT ROUND(SUM(Invoice.Total)) AS "Total", Employee.FirstName || " " || Employee.LastName AS "Employee Full Name" FROM Invoice  
JOIN Customer ON Invoice.CustomerId = Customer.CustomerId  
JOIN Employee ON Customer.SupportRepId = Employee.EmployeeId  
WHERE Employee.Title = "Sales Support Agent"  
GROUP BY Employee.EmployeeId  

#### Which sales agent made the most in sales in 2009?

SELECT ROUND(SUM(Invoice.Total)) AS "Total", Employee.FirstName || " " || Employee.LastName AS "Employee Full Name" FROM Invoice  
JOIN Customer ON Invoice.CustomerId = Customer.CustomerId  
JOIN Employee ON Customer.SupportRepId = Employee.EmployeeId  
WHERE Invoice.InvoiceDate LIKE "2009%"  
GROUP BY Employee.EmployeeId  
ORDER BY Invoice.Total DESC  
LIMIT 1  

#### Which sales agent made the most in sales in 2010?

SELECT ROUND(SUM(Invoice.Total)) AS "Total", Employee.FirstName || " " || Employee.LastName AS "Employee Full Name" FROM Invoice  
JOIN Customer ON Invoice.CustomerId = Customer.CustomerId  
JOIN Employee ON Customer.SupportRepId = Employee.EmployeeId  
WHERE Invoice.InvoiceDate LIKE "2010%"  
GROUP BY Employee.EmployeeId  
ORDER BY Invoice.Total DESC  
LIMIT 1  

#### Which sales agent made the most in sales over all?

SELECT ROUND(SUM(Invoice.Total)) AS "Total", Employee.FirstName || " " || Employee.LastName AS "Employee Full Name" FROM Invoice  
JOIN Customer ON Invoice.CustomerId = Customer.CustomerId  
JOIN Employee ON Customer.SupportRepId = Employee.EmployeeId  
GROUP BY Employee.EmployeeId  
ORDER BY Invoice.Total ASC  
LIMIT 1  

#### Provide a query that shows the # of customers assigned to each sales agent.

SELECT COUNT(Customer.CustomerId) AS "Number of Customers", Employee.FirstName || " " || Employee.LastName AS "Employee Full Name" FROM Customer  
JOIN Employee ON Customer.SupportRepId = Employee.EmployeeId  
GROUP BY Employee.FirstName  

#### Provide a query that shows the total sales per country. Which country's customers spent the most?

SELECT COUNT(Invoice.Total) AS "Total Sales", Customer.Country AS "Country" FROM Invoice  
JOIN Customer ON Invoice.CustomerId = Customer.CustomerId  
GROUP BY Customer.Country  

#### Provide a query that shows the most purchased track of 2013.

SELECT COUNT(Invoice.Total) AS "Total Sales", Track.Name AS "Song" FROM Invoice  
JOIN InvoiceLine ON Invoice.InvoiceId = InvoiceLine.InvoiceId  
JOIN Track ON InvoiceLine.TrackId = Track.TrackId  
WHERE Invoice.InvoiceDate LIKE "2013%"  
GROUP BY Track.Name  
ORDER BY COUNT(Invoice.Total) DESC  

#### Provide a query that shows the top 5 most purchased tracks over all

SELECT COUNT(Invoice.Total) AS "Total Sales", Track.Name AS "Song" FROM Invoice  
JOIN InvoiceLine ON Invoice.InvoiceId = InvoiceLine.InvoiceId  
JOIN Track ON InvoiceLine.TrackId = Track.TrackId  
GROUP BY Track.Name  
ORDER BY COUNT(Invoice.Total) DESC  
Limit 5  

#### Provide a query that shows the top 3 best selling artists.

SELECT COUNT(Invoice.Total) AS "Total Sales", Artist.Name AS "Artist" FROM Invoice  
JOIN InvoiceLine ON Invoice.InvoiceId = InvoiceLine.InvoiceId  
JOIN Track ON InvoiceLine.TrackId = Track.TrackId  
JOIN Album ON Track.AlbumId = Album.AlbumId  
JOIN Artist ON Album.ArtistId = Artist.ArtistId  
GROUP BY Artist.Name  
ORDER BY COUNT(Invoice.Total) DESC  
Limit 3  

#### Provide a query that shows the most purchased Media Type.

SELECT COUNT(Invoice.Total) AS "Total Sales", MediaType.Name AS "Media Type" FROM Invoice  
JOIN InvoiceLine ON Invoice.InvoiceId = InvoiceLine.InvoiceId  
JOIN Track ON InvoiceLine.TrackId = Track.TrackId  
JOIN MediaType ON Track.MediaTypeId = MediaType.MediaTypeId  
GROUP BY Mediatype.Name  
ORDER BY COUNT(Invoice.Total) DESC  
Limit 1  

