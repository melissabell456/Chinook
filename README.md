# Chinook

## This is an exercise to practice SQL statements using the chinook db. To download the db, visit the repository (link below) and download locally. Then open in db browser and test my statements below. 

#### https://github.com/lerocha/chinook-database/blob/master/ChinookDatabase/DataSources/Chinook_Sqlite.sqlite

1. Provide a query showing Customers (just their full names, customer ID and country) who are not in the US.
  ```
  SELECT (Customer.FirstName || " " || Customer.LastName) as CustName, Customer.CustomerId, Customer.Country
  FROM Customer
  WHERE Customer.Country != "USA"
  ```

2. Provide a query only showing the Customers from Brazil.
  ```
  SELECT customer.*
  FROM customer
  WHERE customer.country = "Brazil"
  ```

3. Provide a query showing the Invoices of customers who are from Brazil. The resultant table should show the customer's full name, Invoice ID, Date of the invoice and billing country.
  ```
  SELECT (Customer.firstName || " " || Customer.lastName) AS CustomerName, Invoice.InvoiceId, Invoice.InvoiceDate, Invoice.BillingCountry
  FROM Customer
  JOIN Invoice ON Customer.CustomerId = Invoice.CustomerId
  WHERE Customer.Country = "Brazil"
  ```


4. Provide a query showing only the Employees who are Sales Agents.
  ```
  SELECT *
  FROM Employee
  WHERE Employee.Title = "Sales Support Agent"
  ```

5. Provide a query showing a unique list of billing countries from the Invoice table.
  ```
  SELECT Invoice.BillingCountry 
  FROM Invoice
  GROUP BY Invoice.BillingCountry
  ```

6. Provide a query that shows the invoices associated with each sales agent. The resultant table should include the Sales Agent's full name.
  ```
  SELECT (Employee.FirstName || " " || Employee.lastName) as SalesAgentName, Invoice.InvoiceId as AssociatedInvoice
  FROM Invoice
  JOIN Customer ON Invoice.CustomerId = Customer.CustomerId
  JOIN Employee ON Employee.EmployeeId = Customer.SupportRepId
  ```

7. Provide a query that shows the Invoice Total, Customer name, Country and Sale Agent name for all invoices and customers.
  ```
  SELECT (Customer.FirstName || " " || Customer.LastName) AS CustomerName, Customer.Country,
  Invoice.Total AS InvoiceTotal, (Employee.FirstName || " " || Employee.LastName) AS SalesAgent
  FROM Customer
  JOIN Invoice ON Invoice.CustomerId = Customer.CustomerId
  JOIN Employee ON Employee.EmployeeId = Customer.SupportRepId
  ```

8. How many Invoices were there in 2009 and 2011? What are the respective total sales for each of those years?
  ```
  SELECT COUNT(Invoice.InvoiceId) AS InvoiceCount, SUM(Invoice.Total) as TotalSales, strftime('%Y', Invoice.InvoiceDate) AS InvoiceYear
  FROM Invoice
  WHERE strftime('%Y', Invoice.InvoiceDate) = "2009" OR strftime('%Y', Invoice.InvoiceDate) = "2011"
  GROUP BY InvoiceYear
  ```

9. Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for Invoice ID 37.
  ```
  SELECT Invoice.InvoiceId, COUNT(InvoiceLine.InvoiceLineId) AS LineCount
  FROM Invoice
  JOIN InvoiceLine ON InvoiceLine.InvoiceId = Invoice.InvoiceId
  WHERE Invoice.InvoiceId = 37
  ```

10. Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for each Invoice. HINT: GROUP BY
  ```
  SELECT Invoice.InvoiceId, COUNT(InvoiceLine.InvoiceLineId) AS LineCount
  FROM Invoice
  JOIN InvoiceLine ON InvoiceLine.InvoiceId = Invoice.InvoiceId
  GROUP BY Invoice.InvoiceId
  ```

11. Provide a query that includes the track name with each invoice line item.
  ```
  SELECT InvoiceLine.*, Track.Name AS TrackName
  FROM InvoiceLine
  JOIN Track ON InvoiceLine.TrackId = Track.TrackId
  ```

12. Provide a query that includes the purchased track name AND artist name with each invoice line item.
  ```
  SELECT Track.Name AS TrackName, Artist.Name AS ArtistName, InvoiceLine.InvoiceLineId AS AssociatedInvoiceLine
  FROM Track
  JOIN Album ON Album.AlbumId = Track.AlbumId
  JOIN Artist ON Album.ArtistId = Artist.ArtistId
  JOIN InvoiceLine ON InvoiceLine.TrackId = Track.TrackId
  ```

13. Provide a query that shows the # of invoices per country. HINT: GROUP BY
  ```
  SELECT Invoice.BillingCountry, COUNT(Invoice.InvoiceId) AS InvoiceCount
  FROM Invoice
  GROUP BY Invoice.BillingCountry
  ```

14. Provide a query that shows the total number of tracks in each playlist. The Playlist name should be included on the resultant table.
  ```
  SELECT Playlist.Name AS Playlist, COUNT(Track.TrackID) AS NumOfSongs
  FROM Playlist
  JOIN PlaylistTrack ON PlaylistTrack.PlaylistId = Playlist.PlaylistId
  JOIN Track ON PlaylistTrack.TrackId = Track.TrackId
  GROUP BY Playlist.Name
  ```

15. Provide a query that shows all the Tracks, but displays no IDs. The resultant table should include the Album name, Media type and Genre.
  ```
  SELECT Track.Name AS SongName, Album.Title AS AlbumName, MediaType.Name AS MediaTypeName, Genre.Name AS Genre
  FROM Track
  JOIN Album ON Album.AlbumId = Track.AlbumId
  JOIN MediaType ON MediaType.MediaTypeId = Track.MediaTypeId
  JOIN Genre ON Genre.GenreId = Track.GenreId
  ```

16. Provide a query that shows all Invoices but includes the # of invoice line items.
  ```
  SELECT Invoice.InvoiceId AS Invoice, COUNT(InvoiceLine.InvoiceLineId) AS LineCount
  FROM Invoice
  JOIN InvoiceLine ON Invoice.InvoiceId = InvoiceLine.InvoiceId
  GROUP BY Invoice.InvoiceId
  ```

17. Provide a query that shows total sales made by each sales agent.
  ```
  SELECT (Employee.FirstName || " " || Employee.LastName) AS SalesRep, ROUND(SUM(Invoice.Total), 2) AS TotalSales
  FROM Employee
  JOIN Customer ON Customer.SupportRepId = Employee.EmployeeId
  JOIN Invoice ON Invoice.CustomerId = Customer.CustomerId
  GROUP BY Employee.FirstName
  ```

18. Which sales agent made the most in sales in 2009? Steve Johnson - $164.34
  ```
  SELECT (Employee.FirstName || " " || Employee.LastName) AS SalesRep, ROUND(SUM(Invoice.Total), 2) AS TotalSales
  FROM Employee
  JOIN Customer ON Customer.SupportRepId = Employee.EmployeeId
  JOIN Invoice ON Invoice.CustomerId = Customer.CustomerId WHERE strftime('%Y', Invoice.InvoiceDate) = "2009"
  GROUP BY Employee.FirstName
  ORDER BY TotalSales desc
  ```

19. Which sales agent made the most in sales in 2010? Jane Peacock - 221.92
  ```
  SELECT (Employee.FirstName || " " || Employee.LastName) AS SalesRep, ROUND(SUM(Invoice.Total), 2) AS TotalSales
  FROM Employee
  JOIN Customer ON Customer.SupportRepId = Employee.EmployeeId
  JOIN Invoice ON Invoice.CustomerId = Customer.CustomerId WHERE strftime('%Y', Invoice.InvoiceDate) = "2010"
  GROUP BY Employee.FirstName
  ORDER BY TotalSales desc
  ```

20. Which sales agent made the most in sales over all? Jane Peacock -	833.04
  ```
  SELECT (Employee.FirstName || " " || Employee.LastName) AS SalesRep, ROUND(SUM(Invoice.Total), 2) AS TotalSales
  FROM Employee
  JOIN Customer ON Customer.SupportRepId = Employee.EmployeeId
  JOIN Invoice ON Invoice.CustomerId = Customer.CustomerId
  GROUP BY Employee.FirstName
  ORDER BY TotalSales desc
  ```

21. Provide a query that shows the # of customers assigned to each sales agent.
  ```
  SELECT (Employee.FirstName ||" "|| Employee.LastName) AS SalesAgent, COUNT(Customer.CustomerId) AS TotalCustomers
  FROM Employee
  JOIN Customer ON Customer.SupportRepId = Employee.EmployeeId
  GROUP BY SalesAgent
  ```

22. Provide a query that shows the total sales per country. Which country's customers spent the most? USA
  ```
  SELECT Invoice.BillingCountry AS Country, ROUND(SUM(Invoice.Total), 2) as TotalSales
  FROM Invoice
  GROUP BY Country
  ORDER BY TotalSales desc
  ```

23. Provide a query that shows the most purchased track of 2013.
  ```
  SELECT TrackName, MAX(Sales)
  FROM
    (SELECT Track.Name as TrackName, SUM(InvoiceLine.Quantity) as Sales
    FROM Track
    JOIN InvoiceLine ON InvoiceLine.TrackId = Track.TrackId
    JOIN Invoice ON Invoice.InvoiceId = InvoiceLine.InvoiceId WHERE strftime('%Y', Invoice.InvoiceDate) = "2013"
    GROUP BY TrackName
    ORDER BY Sales desc)
  ```

24. Provide a query that shows the top 5 most purchased tracks over all.
  ```
  SELECT Track.Name AS TrackName, COUNT(InvoiceLine.Quantity) as Sales
  FROM Track
  JOIN InvoiceLine ON InvoiceLine.TrackId = Track.TrackId
  GROUP BY TrackName
  ORDER BY Sales desc 
  LIMIT 5
  ```

25. Provide a query that shows the top 3 best selling artists.
  ```
  SELECT Artist.Name AS ArtistName, COUNT(InvoiceLine.Quantity) AS TracksSold
  FROM Artist
  JOIN Album ON Album.ArtistId = Artist.ArtistId
  JOIN Track ON Track.AlbumId = Album.AlbumId
  JOIN InvoiceLine ON InvoiceLine.TrackId = Track.TrackId
  GROUP BY ArtistName 
  ORDER BY TracksSold desc 
  LIMIT 3
  ```

26. Provide a query that shows the most purchased Media Type.
  ```
  SELECT MediaTypeName, MAX(TotalSales)
  FROM
    (SELECT MediaType.Name AS MediaTypeName, COUNT(InvoiceLine.Quantity) AS TotalSales
    FROM MediaType
    JOIN Track ON Track.MediaTypeId = MediaType.MediaTypeId
    JOIN InvoiceLine ON InvoiceLine.TrackId = Track.TrackId
    GROUP BY MediaTypeName)
  ```

27. Provide a query that shows the number tracks purchased in all invoices that contain more than one genre.
 ```
 SELECT Invoice.InvoiceId AS InvoiceNumber, SUM(InvoiceLine.Quantity) AS TrackCount, group_concat(DISTINCT Genre.Name) AS Genres, COUNT(DISTINCT Genre.Name) AS TotalGenres
  FROM Invoice
  JOIN InvoiceLine ON InvoiceLine.InvoiceId = Invoice.InvoiceId
  JOIN Track ON Track.TrackId = InvoiceLine.TrackId
  JOIN Genre ON Genre.GenreId = Track.GenreId
  GROUP BY InvoiceNumber
  HAVING TotalGenres > 1
 ```