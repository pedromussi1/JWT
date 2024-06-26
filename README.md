
<h1 align="center">JWT with PERN</h1>





<a href="https://www.youtube.com/watch?v=lOLUN-cHrbg">
<kbd><img src="https://i.imgur.com/ZTNjSuP.png?1" alt="JWT Website"></kbd>
</a>

<h2>Description</h2>

<p>This website was created to showcase my skills as a PERN developer along with using JSON Web Tokens to provide authentication and authorization for user logins. I designed and implemented the database schemas using PostgreSQL. JWT was used to secure web APIs. When a user logs in, the server verifies the user's credentials. If they are valid, the server generates a JWT containing a set of claims and signs it using a secret key. The server sends this JWT back to the client. The client stores this token in the browser's local storage. For further requests to protected resources, the client sends the JWT in the request header. The server verifies the JWT's signature to ensure it hasn't been tampered with. If the verification is successful, the server processes the request. The server checks the claims in the JWT to determine whether the user is authorized to access the requested resource. The server sends back the requested data or performs the requested action.</p>

<h2>Languages and Utilities Used</h2>

<ul>
  <li><b>PostgreSQL</b></li>
  <li><b>Express.js</b></li>
  <li><b>React</b></li>
  <li><b>Node.js</b></li>
  <li><b>JWT</b></li>
</ul>

<h2>Environments Used</h2>

<ul>
  <li><b>Windows 11</b></li>
  <li><b>Visual Studio Code</b></li>
</ul>

<h2>
<a href="https://github.com/pedromussi1/JWT/blob/main/READCODE.md">Code Breakdown Here!</a>
</h2>


<h2>Project Walk-through</h2>

<h3>Logging into the Website</h3>

<p align="center">
  <kbd><img src="https://i.imgur.com/9p4H4wO.png?1" alt="AddingItem"></kbd>
</p>

<p>The user can write their email and password credentials in order to log into the website. Doing so will take the user to their Dashboard that displays their username. The user will only be able to log into an account that has already been registered on the website.</p>

<p align="center">
  <kbd><img src="https://i.imgur.com/wtCjc3x.png?1" alt="AddingItem1"></kbd>
</p>

<p align="center">
  <kbd><img src="https://i.imgur.com/ILhG1lD.png?1" alt="Level 2"></kbd>
</p>

<h3>Registering new User on the Website</h3>

<p align="center">
  <kbd><img src="https://i.imgur.com/RhRDuUr.png?1" alt="DeletingItem"></kbd>
</p>

<p>The user here can register a new account on the website by providing email, password and username credentials. After registering, the user will access their dashboard that displays their username.</p>

<p align="center">
  <kbd><img src="https://i.imgur.com/LZuuvNn.png?3" alt="DeletingItem"></kbd>
</p>
