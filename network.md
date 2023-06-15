## Pacote network

O pacote network possui os seguintes modulos: face, master_face, tcp_face, tcp_master_face, udp_face, udp_master_face.

Os pacotes pussuem uma relação de herança umas com as outras (ou objetos de uma classe dentro da outra).

A classe base parece ser Face.

## MasterFace

- Construtor ``MasterFace(boost::asio::io_service &ios, size_t max_connection) : _master_face_id(++counter), _ios(ios), _max_connection(max_connection)``: parece possuir um numero máximo de conexões
 - io_service fornece as principais funcionalidades de I/O assíncronos

- Define ``NotificationCallback`` e ``ErrorCallback`` como ``std::function``

## TcpFace e UdpFace

Talvez seja responsável por definir uma Face para os tipos de protocolo utilizados, TCP ou UDP

- Chamada do construtor: 

``TcpFace::TcpFace(boost::asio::ip::tcp::socket &&socket)``
        : Face(socket.get_io_service())
        , _skip_connect(true)
        , _endpoint(socket.remote_endpoint())
        , _socket(std::move(socket))
        , _strand(socket.get_io_service())
        , _timer(socket.get_io_service()) {
        
- ``void open(const InterestCallback &interest_callback, const DataCallback &data_callback, const ErrorCallback &error_callback)``

- ``void send()``: pacote de dados, pacote de interesse e string

- ``void connect()``:

- ``void read()``: define como uma stream é lida, 

- ``void write()``:

## TcpMasterFace e UdpMasterFace

Filha de MasterFace.

TcpMasterFace parece ser uma especie de mestre para um conjunto de Faces (UDP ou TCP), isso se deve principalmente por: ``std::unordered_set<std::shared_ptr<Face>> _faces)`` e ``auto face = std::make_shared<TcpFace>(std::move(_socket))``. A classe UdpMasterFace parece seguir o mesmo raciocinio só que para comunicação do tipo UDP.

As principais funções são:

- ``void listen(const NotificationCallback &notification_callback, const Face::InterestCallback &interest_callback,
                const Face::DataCallback &data_callback, const ErrorCallback &error_callback) override;``: parece definir callbacks para quando recebe notificação, pacote de interesse, pacote de dados ou acontece algum erro na face. **Ainda, não sei exatamente como ele consegui distinguir cada situação.**  

- ``sendToAllFaces(...)``: envia para todas as faces (``_faces``), pode ser uma string, pacote de dados ou pacote de interesse
