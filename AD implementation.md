- AD Server representation
- DNS access record
### AD Server settings
> `IP: 192.168.0.14`
> `VLAN 60`
###### Fake response index.html page:
> <!DOCTYPE html>
> 
> <html>
> 
> <head>
> 
> <title>AD Data Simulation</title>
> 
> <style>
> 
> body {
> 
> background-color: #000;
> 
> color: #0f0;
> 
> font-family: 'Courier New', Courier, monospace;
> 
> padding: 20px;
> 
> margin: 0;
> 
> }
> 
> .fake-table {
> 
> width: 100%;
> 
> border-collapse: collapse;
> 
> }
> 
> .fake-table th, .fake-table td {
> 
> text-align: left;
> 
> padding: 8px;
> 
> }
> 
> .fake-table th {
> 
> border-bottom: 1px solid #0f0;
> 
> }
> 
> </style>
> 
> </head>
> 
> <body>
> 
>   
> 
> <h2>Active Directory</h2>
> 
> <table class="fake-table">
> 
> <thead>
> 
> <tr>
> 
> <th>Username</th>
> 
> <th>Password</th>
> 
> <th>Email</th>
> 
> <th>Last Login</th>
> 
> </tr>
> 
> </thead>
> 
> <tbody>
> 
> <tr>
> 
> <td>john.doe</td>
> 
> <td>pass1234</td>
> 
> <td>john.doe@example.com</td>
> 
> <td>2024-03-18</td>
> 
> </tr>
> 
> <tr>
> 
> <td>jane.smith</td>
> 
> <td>smith2024</td>
> 
> <td>jane.smith@example.com</td>
> 
> <td>2024-03-17</td>
> 
> </tr>
> 
> <!-- Continuing to add more rows -->
> 
> <tr>
> 
> <td>alice.jones</td>
> 
> <td>alicej2024</td>
> 
> <td>alice.jones@example.com</td>
> 
> <td>2024-03-16</td>
> 
> </tr>
> 
> <tr>
> 
> <td>bob.brown</td>
> 
> <td>bobb2024</td>
> 
> <td>bob.brown@example.com</td>
> 
> <td>2024-03-15</td>
> 
> </tr>
> 
> <tr>
> 
> <td>charlie.davis</td>
> 
> <td>charlied2024</td>
> 
> <td>charlie.davis@example.com</td>
> 
> <td>2024-03-14</td>
> 
> </tr>
> 
> <tr>
> 
> <td>diana.evans</td>
> 
> <td>dianae2024</td>
> 
> <td>diana.evans@example.com</td>
> 
> <td>2024-03-13</td>
> 
> </tr>
> 
> <tr>
> 
> <td>edward.wilson</td>
> 
> <td>edwardw2024</td>
> 
> <td>edward.wilson@example.com</td>
> 
> <td>2024-03-12</td>
> 
> </tr>
> 
> <tr>
> 
> <td>faith.king</td>
> 
> <td>faithk2024</td>
> 
> <td>faith.king@example.com</td>
> 
> <td>2024-03-11</td>
> 
> </tr>
> 
> <tr>
> 
> <td>george.moore</td>
> 
> <td>georgem2024</td>
> 
> <td>george.moore@example.com</td>
> 
> <td>2024-03-10</td>
> 
> </tr>
> 
> <tr>
> 
> <td>hannah.thomas</td>
> 
> <td>hannaht2024</td>
> 
> <td>hannah.thomas@example.com</td>
> 
> <td>2024-03-09</td>
> 
> </tr>
> 
> <tr>
> 
> <td>ian.clark</td>
> 
> <td>ianc2024</td>
> 
> <td>ian.clark@example.com</td>
> 
> <td>2024-03-08</td>
> 
> </tr>
> 
> <tr>
> 
> <td>julia.scott</td>
> 
> <td>julias2024</td>
> 
> <td>julia.scott@example.com</td>
> 
> <td>2024-03-07</td>
> 
> </tr>
> 
> <tr>
> 
> <td>kevin.martin</td>
> 
> <td>kevinm2024</td>
> 
> <td>kevin.martin@example.com</td>
> 
> <td>2024-03-06</td>
> 
> </tr>
> 
> <tr>
> 
> <td>laura.white</td>
> 
> <td>lauraw2024</td>
> 
> <td>laura.white@example.com</td>
> 
> <td>2024-03-05</td>
> 
> </tr>
> 
> <tr>
> 
> <td>mike.harris</td>
> 
> <td>mikeh2024</td>
> 
> <td>mike.harris@example.com</td>
> 
> <td>2024-03-04</td>
> 
> </tr>
> 
>   
> 
> </tbody>
> 
> </table>
> 
>   
> 
> </body>
> 
> </html>
> 
> 

### DNS access record
Add:
> ```
> Name: active-directory
> Type: A Record
> Address: 192.168.0.14
> 
> ```
> ```
> Name: ad
> Type: A Record
> Address: 192.168.0.14
> 
> ```