# EXERCISE 0.6
Below is a depiction of what happens when a user creates a new note using the [single-page app version of the notes app](https://studies.cs.helsinki.fi/exampleapp/spa) by writing something into the text field and clicking the Save button.

```mermaid
sequenceDiagram
    participant browser
    participant server

    Note over browser: User enters note content and clicks Save

    browser->>browser: Prevent default form submission\nHandle note locally (add to memory and redraw UI)
    
    browser->>server: POST /new_note_spa (JSON data with note content and date)
    activate server
    
    Note right of server: Server receives JSON data,\nadds new note in memory
    
    server-->>browser: HTTP 201 Created (no redirect)
    deactivate server

    Note right of browser: Browser stays on the same page,\nno further HTTP requests sent.
```

Explanation:
- The SPA intercepts the form submission to prevent a full page reload.
- The browser adds the new note locally and updates the UI immediately.
- The browser sends a POST request with the new note JSON to the server.
- The server stores the note and responds with a 201 status.
- Unlike traditional apps, the page does not reload and no further HTTP requests occur after submission.

This reflects the core SPA behavior of handling data and UI updates client-side while syncing with the backend asynchronously.