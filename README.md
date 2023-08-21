# Encriptador-de-texto
Encriptador de texto creado con HTML, CSS Y JavaScript.

#HTML.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="Enc.css">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@200;400&display=swap" rel="stylesheet">
    <title>Encriptador.</title> 
</head>
<body>
    <header>
        <h1 class="titulo">Encriptador de texto.</h1>
    </header>
    <main>
        <section>
            <textarea class="text-area" cols="30" rows="10" placeholder="Ingrese el texto aqui"></textarea>
            <div>
                <h6 class="informacion">Solo letras minúsculas y sin acentos.</h6>
            </div>
            <div class="botones">
                <button class="btn-encriptar" onclick="btnEncriptar()">Encriptar.</button>
                <button class="btn-desencriptar" onclick="btnDesencriptar()">Desencriptar.</button>
            </div>
        </section>
        
        <section>
            <textarea class="mensaje" cols="20" rows="10"></textarea>
            <div>
                <button class="copiar" onclick="copiar()">Copiar.</button>
            </div>
        </section>
    </main>
<script src="Enc.js"></script>
</body>
</html>

#CSS.
*{
    background-color: grey;
}

.titulo{
    text-align: left;
    color: #0A3871;
    text-align: center;
}

main{
    display: flex;
    margin-bottom: 10px;
    margin-left: 100px;
    
}

.text-area {
    height: 400px;
    background-color: white;
    color: #0A3871;
    margin-top: 30px;
    padding: 2px;
    text-transform: lowercase;
}
::placeholder { color: #0A3871; }

.text-area:focus {
      outline: none;
}

.informacion {
        color:#0A3871;
        font-size:18px;
}

.mensaje{
    height: 400px;
    background: white;
    background-repeat: no-repeat;
    background-position: center;
    border-radius: 24px;
    color: #0A3871;
    margin-left: 98px;
    margin-top: 20px;
    padding-left: 20px;
}
.mensaje:focus {
    outline: none;
}

.botones{
    display: inline-block;
}

.btn-encriptar {
    background-color: #0A3871;
    border: 1px solid #0A3871;
    border-radius: 24px;
    color: white;
    cursor: pointer;
    height: 67px;
    width: 250px;
}

.btn-desencriptar {
    background: #D8DFE8;
    border: 1px solid #0A3871;
    border-radius: 24px;
    color: #0A3871;
    cursor: pointer;
    height: 67px;
    margin-left: 30px;
    width: 250px; 
}

.copiar {
    background-color: blue;
    border: 1px solid black;
    border-radius: 24px;
    color: white;
    cursor: pointer;
    height: 67px;
    padding-left: 30px;
    width: 250px;
    margin: 115px 0 200px 90px;
}

#JS.
const textArea = document.querySelector(".text-area");
const mensaje = document.querySelector(".mensaje");
const copia = document.querySelector(".copiar");

copia.style.display = "none"

function validarTexto(){
    let textoEscrito = document.querySelector(".text-area").value;
    let validador = textoEscrito.match(/^[a-z]*$/);

    if(!validador || validador === 0) {
        alert("Solo son permitidas letras minúsculas y sin acentos")
        location.reload();
        return true; 
    }
}

function btnEncriptar(){
    if(!validarTexto()) {
        const textoEncriptado = encriptar(textArea.value)
        mensaje.value = textoEncriptado
        mensaje.style.backgroundImage = "none"
        textArea.value = "";
        copia.style.display = "block"
    
    }
}

function encriptar(stringEncriptada){
    let matrizCodigo = [["e", "enter"], ["i", "imes"], ["a", "ai"], ["o", "ober"], ["u", "ufat"]];
    stringEncriptada = stringEncriptada.toLowerCase()

    for(let i = 0; i < matrizCodigo.length; i++){
        if(stringEncriptada.includes(matrizCodigo[i][0])){
            stringEncriptada = stringEncriptada.replaceAll(matrizCodigo[i][0], matrizCodigo[i][1])

        }

    }
    return stringEncriptada
}

function btnDesencriptar(){
    const textoEncriptado = desencriptar(textArea.value)
    mensaje.value = textoEncriptado
    textArea.value = "";
    
}

function desencriptar(stringDesencriptada){
    let matrizCodigo = [["e", "enter"], ["i", "imes"], ["a", "ai"], ["o", "ober"], ["u", "ufat"]];
    stringDesencriptada = stringDesencriptada.toLowerCase()

    for(let i = 0; i < matrizCodigo.length; i++){
        if(stringDesencriptada.includes(matrizCodigo[i][1])){
            stringDesencriptada = stringDesencriptada.replaceAll(matrizCodigo[i][1] , matrizCodigo[i][0])

        }

    }
    return stringDesencriptada
}

function copiar(){
    mensaje.select();
    navigator.clipboard.writeText(mensaje.value)
    mensaje.value = "";
    alert("Texto Copiado")
}
