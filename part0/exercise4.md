sequenceDiagram
    participant browser
    participant server

    Note over browser: El usuario escribe una nueva nota en el campo de texto
    browser->>browser: El JavaScript detecta el evento de clic en el botón Save
    Note right of browser: El navegador crea un objeto con el contenido de la nueva nota y la fecha actual

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
    activate server
    Note right of server: El servidor recibe la nueva nota en formato JSON
    server-->>browser: 302 Found (redirección a /notes)
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document (nueva página de notas)
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, {"content": "Nueva nota", "date": "2024-10-16"}, ...]
    deactivate server

    Note right of browser: El navegador actualiza la lista de notas con la nueva nota
