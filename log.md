# Logs



A função mais importante nesse aspecto é logger::log(Level, const std::string). Essa função é responsável por escrever os logs em um arquivo chamado logs.txt. 

Tem três tipos de mensagem, são elas: [INFO], [WARNING], [ERROR]. Em paralelo também pode ser escolhido se a mensagem vai ser printada na tela, por default os microserviços parecem habilitar esssa opção. 
