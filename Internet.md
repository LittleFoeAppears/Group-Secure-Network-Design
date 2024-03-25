### Google Router:
Switch port (Fa0/0)
> - `IP: 192.169.1.1/24`
> ```bash
> en
> conf t
> int fa0/0 
> ip address 192.169.1.1 255.255.255.0 
> no shutdown 
> exit
> ```

---
### Switch:
nothing

---
### PC Google:
- `IP Address: 192.169.1.3`
- `Subnet Mask: 255.255.255.0`
- `Default Gateway: 192.168.1.1`

---
### Google Server:
- `IP Address: 192.169.1.2`
- `Subnet Mask: 255.255.255.0`
- `Default Gateway: 192.168.1.1`
###### Fake Google index.html:
> <!DOCTYPE html>
> 
> <html lang="en">
> 
> <head>
> 
> <meta charset="UTF-8">
> 
> <meta name="viewport" content="width=device-width, initial-scale=1.0">
> 
> <title>Simple Search</title>
> 
> <style>
> 
> body {
> 
> font-family: Arial, sans-serif;
> 
> text-align: center;
> 
> margin-top: 100px;
> 
> }
> 
> #googleLogo {
> 
> font-size: 72px;
> 
> font-weight: bold;
> 
> }
> 
> .G { color: #4285F4; } /* Blue */
> 
> .O1 { color: #EA4335; } /* Red */
> 
> .O2 { color: #FBBC05; } /* Yellow */
> 
> .G2 { color: #4285F4; } /* Blue */
> 
> .L { color: #34A853; } /* Green */
> 
> .E { color: #EA4335; } /* Red */
> 
> #searchBox {
> 
> margin-top: 20px;
> 
> width: 50%;
> 
> padding: 10px;
> 
> font-size: 18px;
> 
> border: 1px solid #DDD;
> 
> border-radius: 20px;
> 
> outline: none;
> 
> }
> 
> #searchButton {
> 
> margin-top: 20px;
> 
> padding: 10px 20px;
> 
> font-size: 18px;
> 
> border: none;
> 
> border-radius: 5px;
> 
> background-color: #F8F9FA;
> 
> cursor: pointer;
> 
> }
> 
> </style>
> 
> </head>
> 
> <body>
> 
> <div id="googleLogo">
> 
> <span class="G">G</span>
> 
> <span class="O1">o</span>
> 
> <span class="O2">o</span>
> 
> <span class="G2">g</span>
> 
> <span class="L">l</span>
> 
> <span class="E">e</span>
> 
> </div>
> 
> <input type="text" id="searchBox" placeholder="Search the web">
> 
> <br>
> 
> <button id="searchButton">Simple Search</button>
> 
> </body>
> 
> </html>
>---




---


---
## Inter Network config:
### Internal Router:
- route for Google
> ```
> en
> conf t
> 
> ip route 192.169.1.0 255.255.255.0 10.1.1.2
> ```

---
### External Router:
- `IP: 10.1.1.1`
- route for Google
> ```
> en
> conf t
> 
> int Se2/0
> ip address 10.1.1.1 255.255.255.252
> exit
> 
> ip route 192.169.1.0 255.255.255.0 10.1.1.2
> exit
> ```

---
### Google Router:
- `IP: 10.1.1.2`
- route for Network 
> ```
> en
> conf t
> 
> int Se2/0
> ip address 10.1.1.2 255.255.255.252
> exit
> 
> ip route 192.168.0.0 255.255.0.0 10.1.1.1
> ```
