@startuml
left to right direction

' Definição dos Atores
actor Cliente
actor Admin

' Fronteira do Sistema
rectangle "Sistema de E-commerce" {
    usecase "Fazer Login" as UC1
    usecase "Buscar Produto" as UC2
    usecase "Finalizar Compra" as UC3
    usecase "Gerenciar Estoque" as UC4
    
    ' Relacionamentos internos (Include)
    UC3 ..> UC1 : <<include>>
}

' Associações dos Atores com os Casos de Uso
Cliente --> UC2
Cliente --> UC3
Admin --> UC4
Admin --> UC1

@enduml
