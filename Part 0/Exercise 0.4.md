# EXERCISE 0.4
Below is a depiction of what happens when a user creates a new note on the [notes page](https://studies.cs.helsinki.fi/exampleapp/notes), by writing something into the text field and clicking the Save button.

```mermaid
sequenceDiagram
    participant browser
    participant server

    Note over browser: User enters note content and clicks Save

    browser->>server: POST /new_note (form data: note="user input")
    activate server
    
    Note right of server: Server receives POST data,\nadds new note in memory
    
    server-->>browser: HTTP 302 Redirect /notes
    deactivate server

    browser->>server: GET /notes
    activate server
    
    server-->>browser: HTML document with updated notes data
    deactivate server

    browser->>server: GET /main.css
    activate server
    server-->>browser: CSS file
    deactivate server

    browser->>server: GET /main.js
    activate server
    server-->>browser: JavaScript file
    deactivate server

    Note right of browser: JS fetches updated notes JSON via GET /data.json

    browser->>server: GET /data.json
    activate server
    server-->>browser: JSON notes array including new note
    deactivate server

    Note right of browser: Browser executes JS to render updated notes on page

```
