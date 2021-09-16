# Advanced-Task--SSRS

1. Given suburb and city, display median rental value, median yearly income, and value changes of the property within 1 km radius  

        SELECT G.Suburb + '/' + G.City as Selected_Location,  
               R.Suburb + '/' + R.City as Location_of_Property,  
               ROUND(
                        (geography::Point(G.Latitude,G.Longitude, 4326).STDistance(geography::Point(R.Latitude,R.Longitude, 4326))/1000
                        ),
                    3) as Distance_Radius,  
               R.Property_type,  
               R.Median_rental_value,  
               R.Latitude,  
               R.Longitude  
        INTO Task15RentalMedian  
        FROM DimRMV R  
        CROSS JOIN DimGeography G  
        WHERE (geography::Point(G.Latitude,G.Longitude, 4326).STDistance(geography::Point(R.Latitude,R.Longitude, 4326))/1000) <= 1  
        AND R.Suburb <> G.Suburb AND R.Suburb IS NOT NULL  
        
![image](https://github.com/Zihan-Luo/Property-Analysis-Standard-Sprint--Advanced-Task--SSRS/blob/23ea28f5a6c241342bcb17124c10ce53225e3ffa/images/9-1.png)

![image](https://github.com/Zihan-Luo/Property-Analysis-Standard-Sprint--Advanced-Task--SSRS/blob/23ea28f5a6c241342bcb17124c10ce53225e3ffa/images/9-2.png)

2. Given suburb and city, display local public transport within 1km radius - update data sets  

        SELECT G.Suburb + '/' + G.City as Selected_Location,  
               T.StopName as Stop_Name,  
               ROUND(
                        (geography::Point(G.Latitude,G.Longitude, 4326).STDistance(geography::Point(T.Latitude,T.Longitude, 4326))/1000
                        ),
                    3) as Distance_Radius,  
               T.Mode,  
               T.Latitude,  
               T.Longitude  
        INTO Task16Transport  
        FROM DimTransport T  
        CROSS JOIN DimGeography G  
        WHERE (geography::Point(G.Latitude,G.Longitude, 4326).STDistance(geography::Point(T.Latitude,T.Longitude, 4326))/1000) <= 1  
        AND T.Suburb <> G.Suburb AND T.Suburb IS NOT NULL  
        
![image](https://github.com/Zihan-Luo/Property-Analysis-Standard-Sprint--Advanced-Task--SSRS/blob/23ea28f5a6c241342bcb17124c10ce53225e3ffa/images/10-1.png)

![image](https://github.com/Zihan-Luo/Property-Analysis-Standard-Sprint--Advanced-Task--SSRS/blob/23ea28f5a6c241342bcb17124c10ce53225e3ffa/images/10-2.png)

3. Given suburb and city, display local schools within 1km radius  

        SELECT G.Suburb + '/' + G.City AS Selected_Location,  
               S.SchoolType AS School_Type,  
               S.SchoolName AS School_Name,  
               S.Address,  
               S.Suburb,  
               ROUND(
                        (geography::Point(G.Latitude,G.Longitude, 4326).STDistance(geography::Point(S.Latitude,S.Longitude, 4326))/1000
                        ),
                    3) as Distance_Radius,  
               S.Latitude,  
               S.Longitude  
        INTO Task17School  
        FROM DimAuLocalSchool17 S  
        CROSS JOIN DimGeography G  
        WHERE (geography::Point(G.Latitude,G.Longitude, 4326).STDistance(geography::Point(S.Latitude,S.Longitude, 4326))/1000) <= 1  
        AND S.Suburb <> G.Suburb AND S.Suburb IS NOT NULL  
        
![image](https://github.com/Zihan-Luo/Property-Analysis-Standard-Sprint--Advanced-Task--SSRS/blob/23ea28f5a6c241342bcb17124c10ce53225e3ffa/images/11-1.png)

![image](https://github.com/Zihan-Luo/Property-Analysis-Standard-Sprint--Advanced-Task--SSRS/blob/23ea28f5a6c241342bcb17124c10ce53225e3ffa/images/11-2.png)

4. Given suburb and city, display crime rate within 1 km radius  

        SELECT G.Suburb + '/' + G.City AS Selected_Location,  
               G.Latitude,  
               G.Longitude,  
               C.OffenceCategory AS Offence_Category,  
               C.OffenceSubcategory AS Offence_Subcategory,  
               C.RecordedIncidents AS Recorded_Incidents,  
               C.Suburb,  
               '0KM' as Distance_Radius,  
               C.UpdateYr AS Update_Year  
        INTO Task18Crime  
        FROM DimCrime C  
        CROSS JOIN DimGeography G  
        WHERE C.Suburb = G.Suburb AND C.Suburb IS NOT NULL 
                
![image](https://github.com/Zihan-Luo/Property-Analysis-Standard-Sprint--Advanced-Task--SSRS/blob/23ea28f5a6c241342bcb17124c10ce53225e3ffa/images/12-1.png)

![image](https://github.com/Zihan-Luo/Property-Analysis-Standard-Sprint--Advanced-Task--SSRS/blob/23ea28f5a6c241342bcb17124c10ce53225e3ffa/images/12-2.png)

5. Given suburb and city, display property value of the area in Column chart and line chart of 1 year, 5 years and 10 years value  

        SELECT G.Suburb + '/' + G.City AS Selected_Location,  
               G.City,  
               G.Latitude,  
               G.Longitude,  
               Median_Value_2018,  
               Annual_Growth_Rate,  
               Median_Value_in_1Y,  
               Median_Value_in_5Y,  
               Median_Value_in_10Y
        INTO Task19PMV  
        FROM DimPMV19 P  
        INNER JOIN DimGeography G ON P.Suburb = G.Suburb 
                
![image](https://github.com/Zihan-Luo/Property-Analysis-Standard-Sprint--Advanced-Task--SSRS/blob/23ea28f5a6c241342bcb17124c10ce53225e3ffa/images/13-1.png)

![image](https://github.com/Zihan-Luo/Property-Analysis-Standard-Sprint--Advanced-Task--SSRS/blob/23ea28f5a6c241342bcb17124c10ce53225e3ffa/images/13-2.png)
