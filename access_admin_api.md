# Accessing Admin Login and API Keys

## 1. [Install Postman Here](https://www.postman.com/downloads/)

## 2. Create Admin Account
 1. Click the `Collections` menu on the left sidebar.
 2. Navigate to `PhotoServer/Auth/Create Admin Account`.
 3. You should see a `POST` request to `http://localhost:5000/auth/create_admin_account`.
 4. Click `Send`.
 5. In the bottom section, under `Body`, you should see the following:
 ```
 {
    "status": "success",
    "detail": "Admin account has been created.",
    "account": "Username: \"admin\", Password: \"password\""
}
```

You have created the admin account! You can now login directly in the web-app client, or follow the steps below to create an API key.

## 3. Log In
 1. Click the `Collections` menu on the left sidebar.
 2. Navigate to `PhotoServer/Auth/Login`.
 3. You should see a `POST` request to `localhost:5000/auth/login` which may or may not have text following this.
 4. Just under that, click `Body` to edit the Body of the Post Request.
 5. Replace `jdoe1` with `admin`.
 6. Replace `secret` with `password`.
 7. Click `Send`.
 8. In the bottom section, under `Body`, you should see the following, with `<some_token>` replaced with an alphanumeric string.
 ```
{
    "status": "success",
    "detail": "Successfully Logged In.",
    "access_token": "<some_token>",
    "token_type": "bearer"
}
```
You have successfully logged in! Keep the response for step 4 below.

## 4. Setting the auth_token for the API Keys
1. After logging in, highlight the alphanumeric string `<some_token>` in the `Body` of your response.
2. Right click the highlighted token so a menu appears.
3. In the menu, click on `Set: Globals > auth_token`.

You have set the `auth_token` global variable! You can now create api keys for the train and predict microservices.

## 5. Creating an API Key for Predict or Train
*You can choose between predict or train in step 6*
1. Click the `Collections` menu on the left sidebar
 2. Navigate to `PhotoServer/API/Create API Key`
 3. You should see a `POST` request to `localhost:5000/auth/key` which may or may not have text following this.
 4. Just under that, stay on `Params` to edit the Params of the Post Request
 5. Replace `jdoe1` with `admin`
 6. Replace `dataset_microservice` with **`predict_microservice` or `train_microservice`** to specify the value of the `service` key.
 7. Replace `Testing Dataset Key` with any text you would like to provide detail. 
 7. Click `Send`.
 8. In the bottom section, under `Body`, you should see the following, with `<api_key>` replaced with an alphanumeric string.
 ```
{
    "status": "success",
    "key": "<api_key>",
    "type": "train_microservice",
    "user": "admin",
    "detail": "Testing Dataset Key",
    "enabled": true
}
```
You have successfully accessed the predict or train api key! Copy `<api_key>` to paste wherever it is needed in the app.
