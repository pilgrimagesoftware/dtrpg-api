# Login

1. POST https://www.drivethrurpg.com/validate_login_credentials.php
   * Headers: 
     - Content-type: multipart/form-data;·boundary=<boundary-string>
   * Request Body:
     ```
     --<boundary-string>
     Content-Disposition: form-data; name="email_address"
     
     <email_address>
     --<boundary-string>
     Content-Disposition: form-data; name="password"
     
     <password>
     --<boundary-string>--
     ```
   * Response:
     * Headers:
       - Content-type: text/html; charset=UTF-8
     * Body:
       ```
       ["password",true,"Locked",true]
       ```

2. POST https://www.drivethrurpg.com/create_account_app.php
   * Same headers and body as #1
   * Response:
     * Headers:
       - Content-type: application/json
     * Body:
       ```json
       {
         "status": "success",
         "message": {
           "key": "<application-key>"
         }
       }
       ```
