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


* Other Example

            CREATE PROCEDURE `uspLogInMember`(
            Id int,
            SearchId int /* this param eqals to column called account in table called memeber*/
        )
        BEGIN

            declare checkKey varchar(20);
            set checkKey = member.Level;

            select checkKey =
                case member.Level
                    when 0 then 'down'
                    when 1 then 'downMiddleLevel'
                    when 2 then 'midMiddleLevel'
                    when 3 then 'upMiddleLevel'
                    Else 'top'
                End, 
                m.Id, m.account
            from member as m
            where m.Id = Id and m.account = SearchId;

            if checkKey = 'down' then 

                select *
                from gmember as m 
                where m.Id = Id and gm.account = SearchId;

            if checkKey = 'downMiddleLevel' then

                    select *
                    from(select * from member as m where m.Id = Id) as tampTable
                    where tampTable.Level = 0 or tampTable.agentLevel = 1;

            elseif checkKey = 'midMiddleLevel' then

                select *
                from(select * from member as m where m.Id = Id) as tampTable
                where tampTable.Level = 0 or tampTable.Level = 1 or  tampTable.Level = 2; 

            elseif checkKey = 'upMiddleLevel' then

                select *
                from(select * from member as m where m.Id = Id) as tampTable
                where tampTable.Level = 0 or tampTable.Level = 1 or tampTable.Level = 2 or tampTable.Level = 3;


            elseif checkKey = 'top' then 

                select * from member as m where gm.Id = Id;

            end if;

        END
    
    
    
