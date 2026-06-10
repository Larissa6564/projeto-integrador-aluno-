# projeto-integrador-aluno-
<!DOCTYPE html>
<html lang="pt-Br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Crud Comentários</title>
</head>
<body>
    <div>
        <h1>CRUD de comentários</h1>

        <input type="text" id="buscaTexto" placeholder="buscar...">
        <input type="text" id="comentario" placeholder="Digite um comentario">

        <button type="submit" onclick="salvar()">Salvar comentário</button>

        <ul id="lista">
        </ul>
    </div>

    <script>
        let comentarios = []

        let editando = null

        let input = document.getElementById("comentario")

        let getStorage = localStorage.getItem("comentarios")
        

        if(getStorage != null){
            comentarios = JSON.parse(getStorage)

            renderizar()
        }

        function renderizar(listaRecebida = comentarios){
            let lista = document.querySelector("#lista")

            lista.innerHTML = ""

            for(let i = 0; i < listaRecebida.length; i++){
                
                const iOrignal = comentarios.indexOf(listaRecebida[i])
         
                lista.innerHTML += `
                    <li>
                        <p id="a${i}">${listaRecebida[i]}</p>

                        <div>
                            <button onclick="editar(${i})">📝</button>
                            <button onclick="deletar(${i})"> 🗑️</button>
                        </div>
                    </li>
                `
                      
    
                 
            }
            
        }
        
        function salvar(){
            

            let comentario = input.value


            comentarios.push(comentario)
            
           
            input.value = ""
            
            salvarStorage()
            renderizar()
        }
        
        function editar(indice){
            const btnEditar = document.querySelector(button[onclick='editar(${indice})'])
            btnEditar.onclick = salvarEdicao
            btnEditar.textContent = "✅"

            document.querySelector(button[onclick='deletar(${indice})']).style.display = "none"
            
            const textoEdit = document.querySelector(#a${indice})
            const inputEdit = document.createElement("input")

            inputEdit.id = edicaoAtual${indice}
            inputEdit.value = textoEdit.textContent
            textoEdit.replaceWith(inputEdit) 
        
            editando = indice
            
        }
         function salvarEdicao () {
            if(editando != null){
                const inputEditado = document.querySelector(#edicaoAtual${editando})

                comentarios[editando] = inputEditado.value

                editando = null

                renderizar()
            }
        }
        
        function deletar(indice){
            comentarios.splice(indice, 1)

            salvarStorage()

            renderizar()
        }
        
        input.addEventListener("keydown", function (e){
            if(e.key == "Enter"){
                salvar()
            }
        })

        function salvarStorage(){
            localStorage.setItem("comentarios", JSON.stringify(comentarios))

        }
       
        const inputBusca = document.querySelector('#buscaTexto')

        inputBusca.addEventListener('input', () => {
            const textoBusca = inputBusca.value.toLowerCase()

             if(textoBusca == ""){
            renderizar(comentarios)
            return
        }

        const resultado = comentarios.filter((comentario) => {
            const comentarioMinisculo = comentario.toLowerCase()

            return comentarioMinisculo.includes(textoBusca)
        })
        
        renderizar(resultado)
        })

       
    </script>
</body>
</html>
