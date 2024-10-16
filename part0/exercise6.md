sequenceDiagram
    participant browser
    participant server

    Note over browser: El usuario escribe una nueva nota y hace clic en el botón Save
    browser->>browser: El JavaScript de la SPA captura el evento de clic
    Note right of browser: El navegador crea un objeto con el contenido de la nueva nota y la fecha actual

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
    activate server
    Note right of server: El servidor recibe la nueva nota en formato JSON
    server-->>browser: 201 Created (confirmación de nota guardada)
    deactivate server

    Note right of browser: El navegador actualiza la lista de notas en la interfaz sin recargar la página
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: JSON actualizado con la nueva nota
    deactivate server

    Note right of browser: El navegador renderiza la nueva nota en la lista visible
