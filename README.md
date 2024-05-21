### **Rest Booking API Testing with Postman Newman**

This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API.

### **Features**

- Tests for GET, POST, PUT, DELETE requests
- Collection of tests covering different API endpoints
- Environment setup for easy switching between environments
- Pre-request scripts for data setup
- Test scripts for assertions and validations

## API Documentation:

- https://documenter.getpostman.com/view/34581549/2sA3JNaLGF

### **Technology used:**

- Postman
- Newman

### **Prerequisite:**

- Node Js
- Newman
- Newman Html Report Library

### **Installation**

1. Postman: If you haven't already, [download and install Postman.](https://www.postman.com/downloads/)
2. Clone the repository:

```console
git clone https://github.com/ifoysalahmmed/Automated-Testing-of-Rest-Booking-API-with-Newman-Report.git
```

3. Import the Postman collection:
   - Open Postman.
   - Click on the Import button.
   - Select the file from the repository.
4. Import the Postman environment:
   - In Postman, click on the gear icon in the top right corner.
   - Select **Import** and choose the file.
5. Newman and Report Installation Process:
   - Newman Install Command:
   ```console
   npm install -g newman
   ```
   - Newman Html Report Install Command:
   ```console
   npm install -g newman-reporter-htmlextra
   ```

### **Usage**

1. Select Environment:
   - In Postman, select the appropriate environment (e.g., Development, Production) from the top-right dropdown.
2. Run Collection:
   - Select the imported collection from the Collections sidebar.
   - Click on the Runner button to open the collection runner.
   - Select the desired environment.
   - Click Start Test to run the collection.
3. View Results:
   - Once the tests are complete, view the results in the Runner tab.
   - Detailed test results can be viewed for each request.

## **Testing**

## Test Case Scenarios:

## _**1. Create A Token For Authentication.**_

### Request URL: https://restful-booker.herokuapp.com/auth

### Request Method: POST

### Request Body:

```console
{
    "username": "admin",
    "password": "password123"
}
```

### Response Body:

```console
{
    "token": "4144e08a1549e38"
}
```

## _**2. Create New Booking**_

### Request URL: https://restful-booker.herokuapp.com/booking/

### Request Method: POST

### Pre-request Script:

```console
var firstName = pm.variables.replaceIn('{{$randomFirstName}}');
pm.environment.set("FirstName", firstName);

var lastName = pm.variables.replaceIn('{{$randomLastName}}');
pm.environment.set("LastName", lastName);

var totalPrice = pm.variables.replaceIn("{{$randomInt}}");
pm.environment.set("TotalPrice", totalPrice);

var depositPaid = pm.variables.replaceIn("{{$randomBoolean}}");
pm.environment.set("DepositPaid", depositPaid);

const moment = require('moment');
const today = moment();

pm.environment.set("CheckIn", today.add(1, 'd').format("YYYY-MM-DD"));

pm.environment.set("CheckOut", today.add(5, 'd').format("YYYY-MM-DD"));

var additionalNeeds = pm.variables.replaceIn("{{$randomNoun}}");
pm.environment.set("AdditionalNeeds", additionalNeeds);
```

### Request Body:

```console
{
    "firstname" : "{{FirstName}}",
    "lastname" : "{{LastName}}",
    "totalprice" : {{TotalPrice}},
    "depositpaid" : {{DepositPaid}},
    "bookingdates" : {
        "checkin" : "{{CheckIn}}",
        "checkout" : "{{CheckOut}}"
    },
    "additionalneeds" : "{{AdditionalNeeds}}"
}
```

### Response Body:

```console
{
    "bookingid": 3737,
    "booking": {
        "firstname": "Johnpaul",
        "lastname": "Mayert",
        "totalprice": 649,
        "depositpaid": false,
        "bookingdates": {
            "checkin": "2024-05-14",
            "checkout": "2024-05-19"
        },
        "additionalneeds": "application"
    }
}
```

## _**3. Get Booking Details By ID**_

### Request URL: https://restful-booker.herokuapp.com/booking/BookingID

### Request Method: GET

### Response Body:

```console
{
    "firstname": "Johnpaul",
    "lastname": "Mayert",
    "totalprice": 649,
    "depositpaid": false,
    "bookingdates": {
        "checkin": "2024-05-14",
        "checkout": "2024-05-19"
    },
    "additionalneeds": "application"
}
```

## _**4. Update the Booking Details**_

### Request URL: https://restful-booker.herokuapp.com/booking/BookingID

### Request Method: PUT

### Pre-request Script:

```console
var firstName = pm.variables.replaceIn('{{$randomFirstName}}');
pm.environment.set("FirstName", firstName);

var lastName = pm.variables.replaceIn('{{$randomLastName}}');
pm.environment.set("LastName", lastName);

var totalPrice = pm.variables.replaceIn("{{$randomInt}}");
pm.environment.set("TotalPrice", totalPrice);

var depositPaid = pm.variables.replaceIn("{{$randomBoolean}}");
pm.environment.set("DepositPaid", depositPaid);

const moment = require('moment');
const today = moment();

pm.environment.set("CheckIn", today.add(1, 'd').format("YYYY-MM-DD"));

pm.environment.set("CheckOut", today.add(5, 'd').format("YYYY-MM-DD"));

var additionalNeeds = pm.variables.replaceIn("{{$randomNoun}}");
pm.environment.set("AdditionalNeeds", additionalNeeds);
```

### Request Body:

```console
{
    "firstname" : "{{FirstName}}",
    "lastname" : "{{LastName}}",
    "totalprice" : {{TotalPrice}},
    "depositpaid" : {{DepositPaid}},
    "bookingdates" : {
        "checkin" : "{{CheckIn}}",
        "checkout" : "{{CheckOut}}"
    },
    "additionalneeds" : "{{AdditionalNeeds}}"
}
```

### Response Body:

```console
{
    "firstname": "Cale",
    "lastname": "Haley",
    "totalprice": 488,
    "depositpaid": false,
    "bookingdates": {
        "checkin": "2024-05-14",
        "checkout": "2024-05-19"
    },
    "additionalneeds": "feed"
}
```

## _**5. Check After The Update**_

### Request URL: https://restful-booker.herokuapp.com/booking/BookingID

### Request Method: GET

### Response Body:

```console
{
    "firstname": "Freddy",
    "lastname": "Wolf",
    "totalprice": 781,
    "depositpaid": false,
    "bookingdates": {
        "checkin": "2024-05-23",
        "checkout": "2024-05-28"
    },
    "additionalneeds": "port"
}
```

## _**6. Delete Booking Record**_

### Request URL: https://restful-booker.herokuapp.com/booking/BookingID

### Request Method: DELETE

### Response Body:

```console
Created
```

## _**7. Check After The Delete**_

### Request URL: https://restful-booker.herokuapp.com/booking/BookingID

### Request Method: DELETE

### Response Body:

```console
Not Found
```

## Run Command:

- Run Command for Console:

```console
newman run Rest_Booking_API.postman_collection.json -e Rest_Booking_API.postman_environment.json
```

- Run Command for Report:

```console
newman run Rest_Booking_API.postman_collection.json -e Rest_Booking_API.postman_environment.json -r cli,htmlextra
```

## Newman Report Summary:

![Newman Report Summary](https://github.com/ifoysalahmmed/Automated-Testing-of-Rest-Booking-API-with-Newman-Report/assets/68318362/66f82c47-abea-403c-ac60-3c1e0cdbf7dc)
![Newman Report Summary](https://github.com/ifoysalahmmed/Automated-Testing-of-Rest-Booking-API-with-Newman-Report/assets/68318362/9349fd97-8bd2-467f-bf10-97fbd7048e34)
![Newman Report Summary](https://github.com/ifoysalahmmed/Automated-Testing-of-Rest-Booking-API-with-Newman-Report/assets/68318362/d8bb4ef9-bfb1-4112-8abe-4d899848d68a)
![Newman Report Summary](https://github.com/ifoysalahmmed/Automated-Testing-of-Rest-Booking-API-with-Newman-Report/assets/68318362/6c5cca52-b886-44c3-973a-28791cc2c081)
