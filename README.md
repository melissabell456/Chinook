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
  SELECT SUM(Invoice.Total) as TotalSales, strftime('%Y', Invoice.InvoiceDate) AS InvoiceYear
  FROM Invoice
  WHERE strftime('%Y', Invoice.InvoiceDate) = "2009" OR strftime('%Y', Invoice.InvoiceDate) = "2011"
  GROUP BY strftime('%Y', Invoice.InvoiceDate)
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
  ```

12. Provide a query that includes the purchased track name AND artist name with each invoice line item.
  ```
  ```

13. Provide a query that shows the # of invoices per country. HINT: GROUP BY
  ```
  ```

14. Provide a query that shows the total number of tracks in each playlist. The Playlist name should be included on the resultant table.
  ```
  ```

15. Provide a query that shows all the Tracks, but displays no IDs. The resultant table should include the Album name, Media type and Genre.
  ```
  ```

16. Provide a query that shows all Invoices but includes the # of invoice line items.
  ```
  ```

17. Provide a query that shows total sales made by each sales agent.
  ```
  ```

18. Which sales agent made the most in sales in 2009?
  ```
  ```

19. Which sales agent made the most in sales in 2010?
  ```
  ```

20. Which sales agent made the most in sales over all?
  ```
  ```

21. Provide a query that shows the # of customers assigned to each sales agent.
  ```
  ```

22. Provide a query that shows the total sales per country. Which country's customers spent the most?
  ```
  ```

23. Provide a query that shows the most purchased track of 2013.
  ```
  ```

24. Provide a query that shows the top 5 most purchased tracks over all.
  ```
  ```

25. Provide a query that shows the top 3 best selling artists.
  ```
  ```

26. Provide a query that shows the most purchased Media Type.
  ```
  ```

27. Provide a query that shows the number tracks purchased in all invoices that contain more than one genre.