# AngularExample

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 9.1.5.

## Development server
Run `npm run server` for mocking REST API server, which is utilizing `json-server` from npm,, and we set it up in `server` folder in this project.

Run `ng serve` for a dev server, which is consuming `json-server` above. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.
## How to mock a REST API
Go to a new command-line interface and start by installing  `json-server`  from npm in your project:

```
$ cd ~/angular-example
$ npm install --save json-server 
```
Next, create a  server  folder in the root folder of your Angular project:
```
$ mkdir server
$ cd server
```
In the  `server`  folder, create a  `database.json`  file and add the following JSON object:
```
{
    "products": []
}
```
This JSON file will act as a database for your REST API server. You can simply add some data to be served by your REST API or use Faker.js for automatically generating massive amounts of realistic fake data.

Go back to your command-line, navigate back from the  `server`  folder, and install `Faker.js`  from npm using the following command:
```
$ cd ..
$ npm install faker --save
```
At the time of creating this example, `faker v4.1.0` will be installed.

Now, create a  `generate.js`  file and add the following code:
```
var faker = require('faker');

var database = { products: []};

for (var i = 1; i<= 300; i++) {
  database.products.push({
    id: i,
    name: faker.commerce.productName(),
    description: faker.lorem.sentences(),
    price: faker.commerce.price(),
    imageUrl: "https://source.unsplash.com/1600x900/?product",
    quantity: faker.random.number()
  });
}

console.log(JSON.stringify(database));
```
We first imported `faker`, and next we defined an object with one empty array for products. Next, we entered a for loop to create 300 fake entries using faker methods like  faker.commerce.productName()  for generating product names. Check all the available methods. Finally we converted the database object to a string and logged it to standard output.

Next, add the  generate  and  server  scripts to the  `package.json`  file:
```
  "scripts": {
    "ng": "ng",
    "start": "ng serve",
    "build": "ng build",
    "test": "ng test",
    "lint": "ng lint",
    "e2e": "ng e2e",
    "generate": "node ./server/generate.js > ./server/database.json",
    "server": "json-server -p 900 --watch ./server/database.json"
  },
```
Next, head back to your command-line interface and run the generate script using the following command:
```
$ npm run generate
```
Finally, run the REST API server by executing the following command:
```
$ npm run server
```
You can now send HTTP requests to the server just like any typical REST API server. Your server will be available from the  http://localhost:900/products  address.

These are the API endpoints we'll be able to use via our JSON REST API server:

GET /products  for getting the products
GET /products/<id>  for getting a single product by id
POST /products  for creating a new product
PUT /products/<id>  for updating a product by id
PATCH /products/<id>  for partially updating a product by id
DELETE /products/<id>  for deleting a product by id
You can use  _page  and  _limit  parameters to get paginated data. In the  Link header you'll get  first,  prev,  next  and  last  links.

Leave the JSON REST API server running 
p.s. Windows or Linux, for some reasons, does NOT allow this service run on http://localhost:3000, and that's why we change the port to 900.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.
