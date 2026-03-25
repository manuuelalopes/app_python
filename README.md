## Atividade de servidor com postman 
### Na aula de redes e IOT nós desenvolvemos uma atividade com o servidor, testando os conceitos de POST e GET: 
- POST e GET recebidos!
<img width="1073" height="289" alt="image" src="https://github.com/user-attachments/assets/28840531-5c2c-438b-98ea-af07de74202e" />
<img width="1103" height="703" alt="image" src="https://github.com/user-attachments/assets/62502f50-440c-4a66-ac0b-a99fa258ae85" />
<img width="1081" height="671" alt="image" src="https://github.com/user-attachments/assets/43aa8cf6-0943-40bf-90b9-aeba0c000532" />


## O que é GET E POST? 
- GET e POST são os principais métodos os verbos HTTP,  usados para a troca de dados entre um servidor e navegador.
- GET : Recupera dados, visiveis na URL.
- POST : Envia dados no corpo da requisição, não visiveis na URL 

## Comentando códigos: 
- "from http.server import HTTPServer, BaseHTTPRequestHandler"
  - preparando para construir um servidor web básico do zero usando as bibliotecas nativas do Python!

- class Servidor(BaseHTTPRequestHandler):
  - começando a definir a lógica do seu servidor! Ao herdar de BaseHTTPRequestHandler, sua classe Servidor ganha a habilidade de interpretar cabeçalhos HTTP e gerenciar a conexão com o cliente.
 
- def do_GET(self):
  - self.send_response(200) : Notifica o navegador que a solicitação foi bem-sucedida (o famoso "OK").
  - self.end_headers(): Informa ao protocolo que você terminou de enviar metadados (como tipo de arquivo ou cookies) e que a próxima coisa enviada será o conteúdo real (o corpo).
  - self.wfile.write(b"Servidor funcionando com GET") : Envia os dados binários para o cliente. O b antes da string é essencial porque o HTTP lida com bytes, não texto puro.
-  # Método POST (novo)
    def do_POST(self):

         # pega o tamanho dos dados enviados na requisição
         tamanho = int(self.headers['Content-Length'])

         # lê os dados enviados
         dados = self.rfile.read(tamanho)

         # mostra os dados recebidos no terminal
         print("Dados recebidos:", dados.decode())
   - Agora o  servidor já consegue receber informações, não apenas enviar.

  -  # envia resposta para o cliente
         self.send_response(200)
         self.end_headers()
         self.wfile.write(b"POST recebido")
  - O cliente (quem enviou os dados) agora recebe uma confirmação e não fica "esperando" o servidor responder até dar timeout.

- HTTPServer(("0.0.0.0", 8000), Servidor).serve_forever() 
  - Ao usar "0.0.0.0", você está dizendo ao Python: "Escute em todas as interfaces de rede disponíveis". Isso significa que o servidor não será acessível apenas por você (localhost), mas por qualquer dispositivo na sua rede local (Wi-Fi) que saiba o seu endereço IP.
