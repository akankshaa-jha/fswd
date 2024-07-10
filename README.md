If the headers option is not showing in Postman, you can follow these steps to manually add the necessary headers:

1. **Create a New Request**:
   - Click "New" -> "Request".

2. **Enter the URL**:
   - Set the URL to the appropriate endpoint (e.g., `http://localhost:3000/register`).

3. **Select the Method**:
   - Choose the HTTP method (e.g., `POST`).

4. **Add Headers Manually**:
   - Click on the "Headers" tab.
   - Add a new header:
     - Key: `Content-Type`
     - Value: `application/json`

5. **Set the Body**:
   - Click on the "Body" tab.
   - Select "raw" and then select "JSON" from the dropdown.
   - Enter the JSON data. For example:
     ```json
     {
       "name": "jyotsna",
       "work": "Assistant Professor",
       "password": "abc"
     }
     ```

6. **Send the Request**:
   - Click "Send".

Repeat these steps for each endpoint you want to test. Here is the detailed process for each endpoint:

### Register a User
- **URL**: `http://localhost:3000/register`
- **Method**: `POST`
- **Headers**:
  - `Content-Type`: `application/json`
- **Body**:
  ```json
  {
    "name": "jyotsna",
    "work": "Assistant Professor",
    "password": "abc"
  }
  ```

### Log In a User
- **URL**: `http://localhost:3000/auth`
- **Method**: `POST`
- **Headers**:
  - `Content-Type`: `application/json`
- **Body**:
  ```json
  {
    "name": "jyotsna",
    "password": "abc"
  }
  ```

### Verify Token
- **URL**: `http://localhost:3000/verifyToken`
- **Method**: `POST`
- **Headers**:
  - `Content-Type`: `application/json`
- **Body**:
  ```json
  {
    "token": "your_received_token"
  }
  ```

By following these steps, you should be able to manually set the headers and validate your API endpoints using Postman.
# fswd
