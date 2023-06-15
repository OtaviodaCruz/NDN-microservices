## Pacote network

O pacote network possui os seguintes modulos: face, master_face, tcp_face, tcp_master_face, udp_face, udp_master_face

Os pacotes pussuem uma relação de herança umas com as outras (ou objetos de uma classe dentro da outra).

A classe base parece ser Face.

TcpMasterFace parece ser uma especie de mestre para um conjunto de Faces, isso se deve principalmente por: ``std::unordered_set<std::shared_ptr<Face>> _faces)``. A classe UdpMasterFace parece seguir o mesmo raciocinio só que para comunicação do tipo UDP 
