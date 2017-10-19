This example was created by websystique.com.

Link [http://websystique.com/spring-security/secure-spring-rest-api-using-oauth2/]

## Testing in Postman

### 1. Request a token
```shell
curl -H "Authorization:Basic bXktdHJ1c3RlZC1jbGllbnQ6c2VjcmV0" \
-H "Accept:application/json" \
-X POST "http://localhost:8080/SpringSecurityOAuth2Example/oauth/token\
?grant_type=password&username=bill&password=abc123"

```
Credential for basic authentication: Username: my-trusted-client; Password: secret

Response should be something like:
```
{
    "access_token": "363cb911-b63c-4f29-83f3-a59d9ac5470f",
    "token_type": "bearer",
    "refresh_token": "c0780381-3481-4b3a-9b0c-56ffe3687d79",
    "expires_in": 119,
    "scope": "read write trust"
}
```

### 2. Call Rest service
```shell
curl -H "Accept:application/json" \
-X GET "http://localhost:8080/SpringSecurityOAuth2Example/user/\
?access_token=6e956e92-4246-4bf4-8807-a7f79adc91ed"
```

Response:
```
[
    {
        "id": 1,
        "name": "Sam",
        "age": 30,
        "salary": 70000
    },
    {
        "id": 2,
        "name": "Tom",
        "age": 40,
        "salary": 50000
    },
    {
        "id": 3,
        "name": "Jerome",
        "age": 45,
        "salary": 30000
    },
    {
        "id": 4,
        "name": "Silvia",
        "age": 50,
        "salary": 40000
    }
]
```

### 3. HTTP Get Response when token expires
```shell
curl -H "Accept:application/json" \
-X GET "http://localhost:8080/SpringSecurityOAuth2Example/user/\
?access_token=390d255e-c109-4995-9f4b-1e07c7adede2"
```

Response:
```
{
    "error": "invalid_token",
    "error_description": "Invalid access token: dacd32c7-d8da-4136-b05c-2212dceafa2c"
}
```

### 4. Request a token using refresh token
``` shell
curl -H "Authorization:Basic bXktdHJ1c3RlZC1jbGllbnQ6c2VjcmV0" \
-H "Accept:application/json" \
-X POST "http://localhost:8080/SpringSecurityOAuth2Example/oauth/token\
?grant_type=refresh_token&refresh_token=033c5691-4c28-4131-b91f-edb58fc84a34"
```

Response
```
{
    "access_token": "d5337e4a-7dcc-4f47-9569-6867b7e78677",
    "token_type": "bearer",
    "refresh_token": "e77b0081-5881-4978-8d03-f8d0af33fdf6",
    "expires_in": 119,
    "scope": "read write trust"
}
```
