### **Rest Booking API Testing with Postman Newman**

This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API.

### **Features**

- Tests for GET, POST, PUT, PATCH, DELETE requests
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

## _**2. Create A New Booking**_

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
    "bookingid": 2032,
    "booking": {
        "firstname": "Newton",
        "lastname": "Bailey",
        "totalprice": 196,
        "depositpaid": true,
        "bookingdates": {
        "checkin": "2024-05-24",
        "checkout": "2024-05-29"
        },
        "additionalneeds": "protocol"
    }
}
```

## _**3. Get The Booking Details By ID**_

### Request URL: https://restful-booker.herokuapp.com/booking/BookingID

### Request Method: GET

### Response Body:

```console
{
    "firstname": "Newton",
    "lastname": "Bailey",
    "totalprice": 196,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2024-05-24",
        "checkout": "2024-05-29"
    },
    "additionalneeds": "protocol"
}
```

## _**4. Update The Booking Details**_

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
    "firstname": "Sandy",
    "lastname": "Schamberger",
    "totalprice": 946,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2024-05-24",
        "checkout": "2024-05-29"
    },
    "additionalneeds": "hard drive"
}
```

## _**5. Check After The Update**_

### Request URL: https://restful-booker.herokuapp.com/booking/BookingID

### Request Method: GET

### Response Body:

```console
{
    "firstname": "Sandy",
    "lastname": "Schamberger",
    "totalprice": 946,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2024-05-24",
        "checkout": "2024-05-29"
    },
    "additionalneeds": "hard drive"
}
```

## _**6. Update The First Name of The Booking Details**_

### Request URL: https://restful-booker.herokuapp.com/booking/BookingID

### Request Method: PATCH

### Pre-request Script:

```console
var firstName = pm.variables.replaceIn('{{$randomFirstName}}');
pm.environment.set("FirstName", firstName);
```

### Request Body:

```console
{
    "firstname" : "{{FirstName}}",
}
```

### Response Body:

```console
{
    "firstname": "Dashawn",
    "lastname": "Schamberger",
    "totalprice": 946,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2024-05-24",
        "checkout": "2024-05-29"
    },
    "additionalneeds": "hard drive"
}
```

## _**7. Check After The First Name Update**_

### Request URL: https://restful-booker.herokuapp.com/booking/BookingID

### Request Method: GET

### Response Body:

```console
{
    "firstname": "Dashawn",
    "lastname": "Schamberger",
    "totalprice": 946,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2024-05-24",
        "checkout": "2024-05-29"
    },
    "additionalneeds": "hard drive"
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

![Newman Report Summary](https://github.com/ifoysalahmmed/Automated-Testing-of-Rest-Booking-API-with-Newman-Report/assets/68318362/8711a454-9305-470b-b3e7-980f4235a023)
![Newman Report Summary](https://github.com/ifoysalahmmed/Automated-Testing-of-Rest-Booking-API-with-Newman-Report/assets/68318362/4a4e16a0-634c-4524-ae58-ec51ce7c6725)
![Newman Report Summary](https://github.com/ifoysalahmmed/Automated-Testing-of-Rest-Booking-API-with-Newman-Report/assets/68318362/2585795b-3946-475a-8835-81db0b22f3e5)
![Newman Report Summary](https://github.com/ifoysalahmmed/Automated-Testing-of-Rest-Booking-API-with-Newman-Report/assets/68318362/0178df65-1b09-41a7-9dbb-67863ec4a765)
