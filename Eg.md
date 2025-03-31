%%{init: {'theme': 'neutral'}}%%
bpmn-diagram
    participant Cliente as "Cliente" {
        startEvent InicioPedido as "Pedido recibido"
        task Pagar as "Pagar el pedido"
        task Recibir as "Recibir el pedido"
        endEvent FinPedido as "Pedido finalizado"
    }
    participant Almacen as "Almacén" {
        task EncontrarArticulo as "Encontrar el artículo en el almacén"
    }
    participant Envio as "Envío" {
        task EnviarPedido as "Envío del pedido"
    }

    InicioPedido --> Pagar
    Pagar -- "Pago realizado" --> |messageFlow| Almacen:EncontrarArticulo
    Almacen:EncontrarArticulo -- "Articulo encontrado" --> |messageFlow| Envio:EnviarPedido
    Envio:EnviarPedido -- "Pedido enviado" --> |messageFlow| Cliente:Recibir
    Cliente:Recibir --> FinPedido

    style Cliente fill:#e0f7fa,stroke:#90caf9,stroke-width:2px
    style Almacen fill:#e8f5e9,stroke:#a5d6a7,stroke-width:2px
    style Envio fill:#fff3e0,stroke:#ffcc80,stroke-width:2px
