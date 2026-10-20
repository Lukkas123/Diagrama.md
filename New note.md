sequenceDiagram
    participant browser
    participant server

    Note right of browser: The user types "Viva Argentina" into the text field and clicks Save

    Note right of browser: JavaScript intercepts the form submission using e.preventDefault()
    Note right of browser: A new note object is created with content "Viva Argentina" and the current timestamp
    Note right of browser: The note is added to the local notes array using notes.push(note)
    Note right of browser: The input field is cleared and the notes list is redrawn

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
    Note right of browser: The request body contains the note as JSON
    Note right of browser: Content-Type: application/json
    activate server
    Note right of server: The server processes the JSON data
    server-->>browser: HTTP 201 Created
    deactivate server

    Note right of browser: The browser remains on the same page without a redirect or additional HTTP requests
