# SQL_SW_CASE


    SELECT   ProductNumber, Category =  
          CASE ProductLine  
             WHEN 'R' THEN 'Road'  
             WHEN 'M' THEN 'Mountain'  
             WHEN 'T' THEN 'Touring'  
             WHEN 'S' THEN 'Other sale items'  
             ELSE 'Not for sale'  
          END,  
       Name  
    FROM Production.Product  
    GO  
