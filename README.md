# User swagger for api docs

### Installation -> 
✅ Step 1: Install Required Packages:
  ```bash
  npm install swagger-ui-express swagger-jsdoc
  ```
✅ Step 2: Setup Swagger in Your Express App
```bash
const express = require('express');
const swaggerUi = require('swagger-ui-express');
const swaggerJsdoc = require('swagger-jsdoc');

const app = express();
app.use(express.json());

```
✅ Step 3: Define Swagger Options
```bash
const swaggerJsdoc = require('swagger-jsdoc');

const options = {
  definition: {
    openapi: '3.0.0',
    info: {
      title: 'My API Documentation',
      version: '1.0.0',
      description: 'Documentation for my Express API',
    },
    servers: [
      {
        url: 'http://localhost:5000', // Change based on your server port
      },
    ],
  },
  apis: ['./routes/*.js'], // Path to your route files with Swagger comments
};

const swaggerSpec = swaggerJsdoc(options);

module.exports = swaggerSpec;

```
Then import and use in your main file:
  ```bash
  const swaggerSpec = require('./swaggerOptions');
  app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerSpec));
  ```

✅ Step 4: Add Swagger Comments in Your Route Files
- For example, in `routes/user.js`:

  ```bash
    /**
   * @swagger
   * /user:
   *   get:
   *     summary: Get all users
   *     responses:
   *       200:
   *         description: A list of users
   */
  router.get('/user', (req, res) => {
    res.json([{ name: 'John Doe' }]);
  });


   ```


### Swagger Comment Demo:

```bash
/**
 * @swagger
 * /api/auth/login:
 *   post:
 *     summary: Login a user
 *     tags: [Auth]
 *     requestBody:
 *       required: true
 *       content:
 *         application/json:
 *           schema:
 *             type: object
 *             required:
 *               - email
 *               - password
 *             properties:
 *               email:
 *                 type: string
 *               password:
 *                 type: string
 *     responses:
 *       200:
 *         description: User logged in successfully
 *       401:
 *         description: Invalid credentials
 */


```
