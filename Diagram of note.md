sequenceDiagram
    participant browser
    participant server

    Note right of browser: The user submits the form

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
    Note right of browser: The form data is sent in the request body
    activate server
    Note right of server: The server accesses the data through req.body
    Note right of server: The server creates a new note object with content and date fields
    Note right of server: The new note is added to the notes array
    server-->>browser: HTTP 302 Found
    deactivate server

    Note right of browser: The browser redirects to the URL specified in the Location header

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: The CSS file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: The JavaScript file
    deactivate server

    Note right of browser: The browser executes the JavaScript code that fetches the notes data

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: JSON data containing the notes
    deactivate server

    Note right of browser: The browser executes the callback function that renders the notes

    Note over server: Notes are stored in memory, not in a database. All notes are lost when the server restarts
