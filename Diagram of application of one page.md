sequenceDiagram
    participant browser
    participant server

    Note right of browser: The user submits the form

    Note right of browser: JavaScript intercepts the form submission using the onsubmit event handler
    Note right of browser: e.preventDefault() prevents the default form submission behavior
    Note right of browser: The browser creates a new note object containing content and date
    Note right of browser: The new note is added to the notes array using notes.push(note)
    Note right of browser: The browser clears the input field and redraws the notes list

    browser->>server: POST /new_note_spa
    Note right of browser: The request body contains the note as JSON
    Note right of browser: Content-Type: application/json
    activate server
    Note right of server: The server receives and processes the JSON data
    server-->>browser: HTTP 201 Created
    deactivate server

    Note right of browser: The browser remains on the same page without a redirect or additional HTTP requests
