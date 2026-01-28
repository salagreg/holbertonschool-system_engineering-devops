
<img width="398" height="444" alt="Capture d’écran 2026-01-28 à 11 02 29" src="https://github.com/user-attachments/assets/0f3d57d5-c5f9-48ec-8faa-34e44f813905" />


Explanation of the diagram:

- A user wants to access the website and enters www.foobar.com in their browser.

- The DNS translates the domain name and returns the IP address 8.8.8.8 using an A record.

- The user's browser then sends an HTTP or HTTPS request to the server at this IP address.

- The web server (Nginx) receives the request and forwards it to the application server.

- The application server executes the business logic using the application's codebase.

- If necessary, the application server reads from or writes data to the MySQL database.

- The response is sent back to the user via the web server.


Problems with this diagram:

- Only one server.

- Restarting the web or application server is required for maintenance.

- It cannot handle high traffic volumes.
