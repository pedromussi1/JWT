
<h1 align="center">PernTodo</h1>




<kbd><img src="https://i.imgur.com/o33BFMI.png?1" alt="PernTodo Website"></kbd>


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
  <kbd><img src="https://i.imgur.com/6yWAVK2.png" alt="AddingItem"></kbd>
</p>

<p>The user can write the name of a new item they want to add to the list and click on "add" to add that item. In this example I chose to add "Need to buy groceries" to the list. You can see on the second image below that the item has been added to the list.</p>

<p align="center">
  <kbd><img src="https://i.imgur.com/EffXnKy.png" alt="AddingItem1"></kbd>
</p>

<h3>Registering as a User on the Website</h3>

<p align="center">
  <kbd><img src="https://i.imgur.com/Kuhy6Hr.png" alt="DeletingItem"></kbd>
</p>

<p>In case the user wants to delete an item for the list, they can simply click on the button "delete" next to the item they want to delete. In this example, I chose to delete the item "wash the dishes".</p>

<h3>Editing an item on the list</h3>

<p align="center">
  <kbd><img src="https://i.imgur.com/NEnmtvj.png" alt="Level 2"></kbd>
</p>

<p>In case the user wants to edit an item on the list, they can press the button "edit" next to the item they want to edit. In this example I chose to edit the "I need to clean my car" item on the list and change it to "I need to buy toothpaste".</p>

<p align="center">
  <kbd><img src="https://i.imgur.com/8orPkgC.png" alt="Level 3"></kbd>
</p>

<p align="center">
  <kbd><img src="https://i.imgur.com/ULVNaP3.png" alt="Level 4"></kbd>
</p>

<p>You can see now that the item has been changed and it is displayed correctly on the list.</p>
