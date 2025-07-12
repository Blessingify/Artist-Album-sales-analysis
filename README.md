# Artist-Album-sales-analysis

ANALYSIS OF ARTISTS, ALBUMS, MUSIC SALES, REVENUE GENERATED AND CUSTOMER BEHAVIOUR USING SQL

##INTRODUCTION

With the growing digitization of music, understanding consumer preferences and sales performance has become crucial for music businesses. This database simulates real-world sales and customer data for Geng Music Label in different countries. By analyzing it through SQL, we can evaluate both customer trends, artist and album performance globally.
### Problem Statement
- Which artists and albums generate the most revenue.
- Where top customers are located.
- Which genres or tracks are most popular.
- How spending varies across selected countries and orders.

### OBJECTIVES
- Analyze customer distribution and purchasing power across countries.
- Identify top-performing tracks, albums, and artists.
- Evaluate the genre spread and track volume.
- Provide business recommendation to optimize marketing, promotions and investments.

To find all artist and their album, the subquery below was excuted:
````sql
select *,(select name from artist) Artist from album
````
