# Chinook

## This is an exercise to practice SQL statements using the chinook db. To download the db, visit the repository (link below) and download locally. Then open in db browser and test my statements below. 

#### https://github.com/lerocha/chinook-database/blob/master/ChinookDatabase/DataSources/Chinook_Sqlite.sqlite

1. Provide a query showing Customers (just their full names, customer ID and country) who are not in the US.
```
SELECT (customer.firstName || " " || customer.lastName) as custName, customer.customerId, customer.country
FROM customer
WHERE customer.country != "USA"
```

1. Provide a query only showing the Customers from Brazil.
1. Provide a query showing the Invoices of customers who are from Brazil. The resultant table should show the 
1. customer's full name, Invoice ID, Date of the invoice and billing country.
1. Provide a query showing only the Employees who are Sales Agents.
1. Provide a query showing a unique list of billing countries from the Invoice table.
1. Provide a query that shows the invoices associated with each sales agent. The resultant table should include the Sales Agent's full name.
1. Provide a query that shows the Invoice Total, Customer name, Country and Sale Agent name for all invoices and customers.
1. How many Invoices were there in 2009 and 2011? What are the respective total sales for each of those years?
1. Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for Invoice ID 37.
1. Looking at the InvoiceLine table, provide a query that COUNTs the number of line items for each Invoice. HINT: GROUP BY
1. Provide a query that includes the track name with each invoice line item.
1. Provide a query that includes the purchased track name AND artist name with each invoice line item.
1. Provide a query that shows the # of invoices per country. HINT: GROUP BY
1. Provide a query that shows the total number of tracks in each playlist. The Playlist name should be included on the resultant table.
1. Provide a query that shows all the Tracks, but displays no IDs. The resultant table should include the Album name, Media type and Genre.
1. Provide a query that shows all Invoices but includes the # of invoice line items.
1. Provide a query that shows total sales made by each sales agent.
1. Which sales agent made the most in sales in 2009?
1. Which sales agent made the most in sales in 2010?
1. Which sales agent made the most in sales over all?
1. Provide a query that shows the # of customers assigned to each sales agent.
1. Provide a query that shows the total sales per country. Which country's customers spent the most?
1. Provide a query that shows the most purchased track of 2013.
1. Provide a query that shows the top 5 most purchased tracks over all.
1. Provide a query that shows the top 3 best selling artists.
1. Provide a query that shows the most purchased Media Type.
1. Provide a query that shows the number tracks purchased in all invoices that contain more than one genre.