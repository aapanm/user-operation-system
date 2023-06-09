# Parent Child Api

## Introduction

Provide a brief introduction to the API, including its purpose and any relevant background information.

## Base URL

Specify the base URL for the API endpoints. For example: `https://localhost:8000/`.

## Endpoints

### Get Parent List

- **URL**: `/parent`
- **Method**: `GET`
- **Description**: when triggered it shows all exisiting parents data from parent table.
- **Response**:
  - ```json
    [
      {
        "id": 1,
        "parentId": 301,
        "firstName": "aapan",
        "lastName": "mutsuddy",
        "street": "2",
        "city": "CTG",
        "state": "CTG",
        "zip": "4000",
        "createdAt": "2023-06-03T15:30:02.755Z",
        "updatedAt": "2023-06-03T15:30:02.755Z"
      },
      {
        "id": 2,
        "parentId": 302,
        "firstName": "aapan",
        "lastName": "mutsuddy",
        "street": "2",
        "city": "CTG",
        "state": "CTG",
        "zip": "4000",
        "createdAt": "2023-06-03T15:34:02.193Z",
        "updatedAt": "2023-06-03T15:34:02.193Z"
      }
    ]
    ```

### Get Parent With ID

- **URL**: `/parent/:parentID`
- **Method**: `GET`
- **Description**: When triggered it fethces a single parent data associated with parent id provided in the parameter.
- **Parameters**:
  - `parentID`: This is the parentId stored in the parent table which is used to fetch a particular row from the db.
- **Response**:
  - ```json
    [
      {
        "id": 1,
        "parentId": 301,
        "firstName": "aapan",
        "lastName": "mutsuddy",
        "street": "2",
        "city": "CTG",
        "state": "CTG",
        "zip": "4000",
        "createdAt": "2023-06-05T13:51:18.576Z",
        "updatedAt": "2023-06-05T13:51:18.576Z"
      }
    ]
    ```

### Create Parent

- **URL**: `/createParent`
- **Method**: `POST`
- **Description**: When triggered it creates a row in the parent table with given data.
- **Request Body**:

  - ```json
    {
      "parentId": 301,
      "firstName": "aapan",
      "lastName": "mutsuddy",
      "address": {
        "street": "2",
        "city": "CTG",
        "state": "CTG",
        "zip": "4000"
      }
    }
    ```

- **Response**:

  - ```json
    {
      "id": 304,
      "parentId": 301,
      "firstName": "aapan",
      "lastName": "mutsuddy",
      "street": "2",
      "city": "CTG",
      "state": "CTG",
      "zip": "4000",
      "createdAt": "2023-06-05T13:51:18.576Z",
      "updatedAt": "2023-06-05T13:51:18.576Z"
    }
    ```

- **Error Codes**:
  - 403 error can be returned if there are missing fields in the request body with a json code as following
  ```json
  { "error": "One or more than one requried fields missing!" }
  ```
  - 409 conflict error can be returned if parent already exists with a json code as following
  ```json
  {
    "error": "Record with the same ID already exists."
  }
  ```

### Update Parent

- **URL**: `/updateParent`
- **Method**: `PATCH`
- **Description**: When triggered dynamically updates given fields in the request body.
- **Request Body**:
  - ```json
    {
      "parentID": 301,
      "data": {
        "lastName": "Chowdhury",
        "address": {
          "city": "dhaka",
          "state": "dhaka",
          "zip": "1000"
        }
      }
    }
    ```
- **Response**:
  - ```json
    {
      "id": 1,
      "parentId": 301,
      "firstName": "aapan",
      "lastName": "Chowdhury",
      "street": "2",
      "city": "dhaka",
      "state": "dhaka",
      "zip": "1000",
      "createdAt": "2023-06-05T13:51:18.576Z",
      "updatedAt": "2023-06-05T14:11:44.090Z"
    }
    ```
- **Error Codes**:

  - 404 error can be displayed if the provided parent id is not found in the database with following json code

  ```json
  { "error": "parent not found!" }
  ```

  ### Delete Parent

- **URL**: `/parent`
- **Method**: `DELETE`
- **Description**: When triggered it deletes a single parent data associated with parent id provided in the request body.
- **Request Body**:
  - ```json
    {
      "parentID": 301
    }
    ```
- **Response**:
  - ```json
    [
      {
        "id": 1,
        "parentId": 301,
        "firstName": "aapan",
        "lastName": "mutsuddy",
        "street": "2",
        "city": "CTG",
        "state": "CTG",
        "zip": "4000",
        "createdAt": "2023-06-05T13:51:18.576Z",
        "updatedAt": "2023-06-05T13:51:18.576Z"
      }
    ]
    ```

### Create Child

- **URL**: `/createChildren`
- **Method**: `POST`
- **Description**: When triggered it creates a row in the children table with given data.
- **Request Body**:

  - ```json
    {
      "parentIdx": 301,
      "childId": 501,
      "firstName": "Johny",
      "lastName": "Depp"
    }
    ```

- **Response**:

  - ```json
    {
      "id": 3,
      "childId": 501,
      "firstName": "Johny",
      "lastName": "Depp",
      "parentIdx": 301,
      "createdAt": "2023-06-04T07:16:04.142Z",
      "updatedAt": "2023-06-04T07:16:04.142Z"
    }
    ```

- **Error Codes**:
  - 404 error can be returned if parent is not found with provided parent id with a json code as following
  ```json
  { "error": "parent not found!" }
  ```

### Get Children List

- **URL**: `/children`
- **Method**: `GET`
- **Description**: when triggered it shows all exisiting children data from children table along with associated parent information.
- **Response**:
  - ```json
    [
      {
        "id": 1,
        "childId": 501,
        "firstName": "Johny",
        "lastName": "Depp",
        "parentIdx": 301,
        "createdAt": "2023-06-04T06:06:24.280Z",
        "updatedAt": "2023-06-04T06:06:24.280Z",
        "parentInfo": {
          "id": 1,
          "parentId": 301,
          "firstName": "aapan",
          "lastName": "mutsuddy",
          "street": "2",
          "city": "CTG",
          "state": "CTG",
          "zip": "1000",
          "createdAt": "2023-06-03T15:30:02.755Z",
          "updatedAt": "2023-06-03T19:01:05.116Z"
        }
      }
    ]
    ```

### Get Children List With Parent Id

- **URL**: `/childrenWithParent/:parentID`
- **Method**: `GET`
- **Description**: when triggered it shows all exisiting children data from children table along with associated with provided parent id.
- **Parameters**:
  - `parentID`: This is the parentIdx stored in the child table which is used to fetch a child data from the db.
- **Response**:
  - ```json
    [
      {
        "id": 129,
        "childId": 501,
        "firstName": "Johny",
        "lastName": "Depp",
        "parentIdx": 301,
        "createdAt": "2023-06-06T11:09:05.508Z",
        "updatedAt": "2023-06-06T11:09:05.508Z",
        "parentInfo": {
          "id": 524,
          "parentId": 301,
          "firstName": "aapan",
          "lastName": "mutsuddy",
          "street": "2",
          "city": "CTG",
          "state": "CTG",
          "zip": "4000",
          "createdAt": "2023-06-06T11:08:53.094Z",
          "updatedAt": "2023-06-06T11:08:53.094Z"
        }
      },
      {
        "id": 130,
        "childId": 502,
        "firstName": "Johny",
        "lastName": "Depp",
        "parentIdx": 301,
        "createdAt": "2023-06-06T11:09:11.562Z",
        "updatedAt": "2023-06-06T11:09:11.562Z",
        "parentInfo": {
          "id": 524,
          "parentId": 301,
          "firstName": "aapan",
          "lastName": "mutsuddy",
          "street": "2",
          "city": "CTG",
          "state": "CTG",
          "zip": "4000",
          "createdAt": "2023-06-06T11:08:53.094Z",
          "updatedAt": "2023-06-06T11:08:53.094Z"
        }
      }
    ]
    ```

### Get Children With ID

- **URL**: `/children/:childrenID`
- **Method**: `GET`
- **Description**: When triggered it fethces a single children data associated with children id provided in the parameter along with parent information.
- **Parameters**:
  - `childrenID`: This is the childrenID stored in the children table which is used to fetch a particular row from the db.
- **Response**:
  - ```json
    {
      "firstName": "Johny",
      "lastName": "Depp",
      "parentInfo": {
        "firstName": "aapan",
        "lastName": "mutsuddy",
        "address": "2,CTG,CTG,4000"
      }
    }
    ```

### Update Children

- **URL**: `/updateChildren`
- **Method**: `PATCH`
- **Description**: When triggered dynamically updates given fields in the request body.
- **Request Body**:
  - ```json
    {
      "childID": 501,
      "data": {
        "lastName": "Chowdhury"
      }
    }
    ```
- **Response**:

  - ```json
    {
      "id": 3,
      "childId": 501,
      "firstName": "Johny",
      "lastName": "Chowdhury",
      "parentIdx": 301,
      "createdAt": "2023-06-04T07:16:04.142Z",
      "updatedAt": "2023-06-04T07:34:53.080Z"
    }
    ```

### Delete Children

- **URL**: `/children`
- **Method**: `DELETE`
- **Description**: When triggered it deletes a single children data associated with children id provided in the request body.
- **Request Body**:
  - ```json
    {
      "childrenID": 501
    }
    ```
- **Response**:
  - ```json
    {
      "id": 2,
      "childId": 501,
      "firstName": "Johny",
      "lastName": "Depp",
      "parentIdx": 301,
      "createdAt": "2023-06-04T07:12:48.847Z",
      "updatedAt": "2023-06-04T07:12:48.847Z"
    }
    ```

# Middleware Validation - validateJSON

The `validateJSON` middleware function is responsible for validating the JSON data received in the request body. It checks if all the required fields exist and sends an error response if any required field is missing.

-**Error Response**:
If any required fields are missing in the request body, the middleware will send the following error response with status code 403:

```json
{
  "error": "One or more required fields missing!"
}
```

## Conclusion

In conclusion, this API documentation provides a comprehensive guide on how to interact with the 'Parent Child Api'. It has covered the authentication mechanism, base URL, and detailed information about each endpoint, including their purpose, parameters, request/response structures, and possible error scenarios.

[Test Documentation](unit.md)
