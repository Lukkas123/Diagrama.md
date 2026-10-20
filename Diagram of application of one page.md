ahora crees una nueva nota, notaras que el navegador envía solo una solicitud al servidor.
La solicitud POST a la dirección new_note_spa contiene la nueva nota como datos JSON que contienen tanto el contenido de la nota (content) como la marca de tiempo (date):
La cabecera Content-Type de la solicitud le dice al servidor que los datos incluidos están representados en formato JSON.
El servidor responde con el código de estado 201 Created. Esta vez, el servidor no solicita una redirección, el navegador permanece en la misma página y no envía más solicitudes HTTP.La versión SPA de la aplicación no envía los datos del formulario de la forma tradicional, sino que utiliza el código JavaScript que obtuvo del servidor
var form = document.getElementById('notes_form')

form.onsubmit = function(e) {
  e.preventDefault()

  var note = {
    content: e.target.elements[0].value,
    date: new Date(),
  }

  notes.push(note)
  e.target.elements[0].value = ''
  redrawNotes()
  sendToServer(note)
}copy
El comando document.getElementById('notes_form') le indica al código que obtenga el elemento form de la página y que registre un event handler para manejar el evento de envío del formulario. El controlador de eventos llama inmediatamente al método e.preventDefault() para evitar el manejo por defecto del envío de formularios. El método por defecto enviaría los datos al servidor y causaría una nueva solicitud GET, lo cual no queremos que suceda.
Luego el controlador de eventos crea una nueva nota, la agrega a la lista de notas con el comando notes.push(note), vuelve a renderizar la lista de notas en la página y envía la nueva nota al servidor.

El código para enviar la nota al servidor es el siguiente:

var sendToServer = function(note) {
  var xhttpForPost = new XMLHttpRequest()
  // ...

  xhttpForPost.open('POST', '/new_note_spa', true)
  xhttpForPost.setRequestHeader('Content-type', 'application/json')
  xhttpForPost.send(JSON.stringify(note))
}copy
El código determina que los datos se enviarán con una solicitud HTTP POST y el tipo de datos será JSON. El tipo de datos se determina con una cabecera Content-type. Luego los datos se envían como una cadena JSON.
