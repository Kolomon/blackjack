# BlackJack REST service

### BlackJack API:

#### Objects:
- ##### User:

- ##### Table:

#### Urls:
- ##### Account:

    ```json
    
        URL: /account
        TYPE: POST
        BODY: JSON
            {
                "login": "your_login",
                "nickName": "your_nickname",
                "password": "pass"
            }
        EFFECT: Create new user with start balance $10_000 in database
        RESPONSE: JSON
            {   
                "status": 0 or -1,     
                "message": "status message"
            }
            
    ```

    ```json

        URL: /account/{login}
        TYPE: GET
        BODY: NONE
        EFFECT: User info like login, nickname, balance
        RESPONSE: JSON
            {
                "login": "your_login",
                "nickName": "your_nickname",
                "balance": 10000
            }
            
    ```

    ```json

        URL: /account/{login}
        TYPE: DELETE
        BODY: NONE
        EFFECT: Delete user from database
        RESPONSE:  JSON
            {
                "status": 0 or -1,     
                "message": "status message"
            }
       
    ```

- ##### Table:

    ```json
        URL: /account/{login}/select-table
        TYPE: GET
        BODY: NONE
        EFFECT: Gets the available tables types
        RESPONSE:  JSON
            {
                "tabletypes": [
                   {
                       "id": 1
                       "minBet": 1,
                       "maxBet": 100
                   },
                   ...
                   ]
            }
       
    ```

    ```json

        URL: /account/{login}/table
        TYPE: POST
        BODY: 
            {
                "tabletype": 1
            }
        EFFECT: Create new table by tabletype for user by login
        RESPONSE:  JSON
            {
                "status": 0 or -1,     
                "message": "status message",
                "tableID": 4623
            }
       
    ```

    ```json

        URL: /account/{login}/table/{tableID}
        TYPE: GET
        BODY: NONE
        EFFECT: Gets available commands for this state of game or error message if the game not started.
        RESPONSE:  JSON
            {
                "comands": [
                    {
                        "name": "HIT",
                        "available": false 
                    },
                    {
                        "name": "BET",
                        "available": true 
                    }
                    ...
                ]                
            }
       
    ```

    - Commands:

        ```json
    
            URL: /account/{login}/table/{tableID}
            TYPE: POST
            BODY: Command in JSON format. See command types
            EFFECT: Sends command to server
            RESPONSE:  JSON
                
           
        ```
    
        - Command types:
    
            ```json 
                HIT:
                    {
                        "command": "HIT"
                    }
                
                BET:
                    {
                        "command": "BET",
                        "amount": 25
                    }
                
                STAND:
                    {
                        "command": "STAND"
                    }
                
                EXIT:
                    {
                        "command": "EXIT"
                    }
            ```

