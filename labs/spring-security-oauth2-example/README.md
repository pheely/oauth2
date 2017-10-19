This example was created by websystique.com.

Link [http://websystique.com/spring-security/secure-spring-rest-api-using-oauth2/]

## Testing in Postman

### 1. Request a token
```shell
curl -H "Authorization:Basic bXktdHJ1c3RlZC1jbGllbnQ6c2VjcmV0" \
-H "Accept:application/json" \
-X POST "http://localhost:8080/SpringSecurityOAuth2Example/oauth/token?grant_type=password&username=bill&password=abc123"

```
Credential for basic authentication

Username: my-trusted-client
Password: secret

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
curl -X GET "http://localhost:8080/SpringSecurityOAuth2Example/user/?access_token=6e956e92-4246-4bf4-8807-a7f79adc91ed"
```

Response:
```
<List xmlns="">
    <item>
        <id>1</id>
        <name>Sam</name>
        <age>30</age>
        <salary>70000.0</salary>
    </item>
    <item>
        <id>2</id>
        <name>Tom</name>
        <age>40</age>
        <salary>50000.0</salary>
    </item>
    <item>
        <id>3</id>
        <name>Jerome</name>
        <age>45</age>
        <salary>30000.0</salary>
    </item>
    <item>
        <id>4</id>
        <name>Silvia</name>
        <age>50</age>
        <salary>40000.0</salary>
    </item>
</List>
```

### 3. HTTP Get Response when token expires
```shell
curl -X GET "http://localhost:8080/SpringSecurityOAuth2Example/user/?access_token=390d255e-c109-4995-9f4b-1e07c7adede2"
```

Response:
```
<InvalidTokenException xmlns="">
    <error>invalid_token</error>
    <error_description>Access token expired: 390d255e-c109-4995-9f4b-1e07c7adede2</error_description>
</InvalidTokenException>
```

### 4. Request a token using refresh token
``` shell
curl -H "Authorization:Basic bXktdHJ1c3RlZC1jbGllbnQ6c2VjcmV0" -X POST "http://localhost:8080/SpringSecurityOAuth2Example/oauth/token?grant_type=refresh_token&refresh_token=033c5691-4c28-4131-b91f-edb58fc84a34"
```

Response
```
<DefaultOAuth2AccessToken xmlns="">
    <access_token>9e8d3eb1-89d8-4120-b1c3-fec60f05adb5</access_token>
    <token_type>bearer</token_type>
    <refresh_token>033c5691-4c28-4131-b91f-edb58fc84a34</refresh_token>
    <expires_in>119</expires_in>
    <scope>read write trust</scope>
</DefaultOAuth2AccessToken>
```
