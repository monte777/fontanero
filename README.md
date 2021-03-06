# fontanero
Serie de pruebas para depurar problemas de despliegue con Plumber

## debian
Una imagen sobre debian del proyecto rocker.

    sudo docker build -it fontanero_debian .    
    sudo docker run --rm -p 8080:8080 -t fontanero_debian  

### / GET hola mundo

    curl localhost:8080/

> ["{\"platform\":[\"x86_64-pc-linux-gnu\"],\"arch\":[\"x86_64\"],\"os\":[\"linux-gnu\"],\"system\":[\"x86_64, linux-gnu\"],\"status\":[\"\"],\"major\":[\"3\"],\"minor\":[\"4.4\"],\"year\":[\"2018\"],\"month\":[\"03\"],\"day\":[\"15\"],\"svn rev\":[\"74408\"],\"language\":[\"R\"],\"version.string\":[\"R version 3.4.4 (2018-03-15)\"],\"nickname\":[\"Someone to Lean On\"]}"]

### /1 GET simple ascii

    curl localhost:8080/1

> {"get":["sin acentos"]} 

    curl -d '{"data":23}' -X POST localhost:8080/1

> {"error":["404 - Resource Not Found"]}

### /2 GET simple con non-ascii

    curl localhost:8080/2

> {"get":["ñ é í ó - algunos ejemplos"]}

    curl -d '{"data":23}' -X POST localhost:8080/2 

> {"error":["404 - Resource Not Found"]}

### /3 GET nombre variable non-ascii

    curl localhost:8080/3

>[23]

    curl -d '{"data":23}' -X POST localhost:8080/3 

> {"error":["404 - Resource Not Found"]}

### /4 GET nombre columna dataframe non-ascii

    curl localhost:8080/4

> [{"cólúmná_ácentos":"cónténídó"}]

    curl -d '{"data":23}' -X POST localhost:8080/4 

> {"error":["404 - Resource Not Found"]}

### /5 GET endpoint repetido (valores 23 y 46)

    curl localhost:8080/5

>[23]

    curl -d '{"data":23}' -X POST localhost:8080/5

> {"error":["404 - Resource Not Found"]}

### /6 GET con un rename complejo en dplyr

    curl localhost:8080/6

> {"error":["404 - Resource Not Found"]} 

    curl -d '{"data":23}' -X POST localhost:8080/6 

> [{"cólúmná_ácentos":5,"más_ácéntós":"algo"}]

### /7 POST simple 

    curl localhost:8080/7

> {"error":["404 - Resource Not Found"]} 

    curl -d '{"data":23}' -X POST localhost:8080/7

>[23]

### /8 POST simple con non-ascii

    curl localhost:8080/8

> {"error":["404 - Resource Not Found"]} 

    curl -d '{"data":23}' -X POST localhost:8080/8

> ["ñ é í ó - algunos ejemplos"] 

### /9 POST nombre variable non-ascii

    curl localhost:8080/9

> {"error":["404 - Resource Not Found"]} 

    curl -d '{"data":23}' -X POST localhost:8080/9

> [529]


### /10 POST nombre columna datafram non-ascii

    curl localhost:8080/10

> {"error":["404 - Resource Not Found"]}

    curl -d '{"data":23}' -X POST localhost:8080/10

> [{"cólúmná_ácentos":"cónténídó"}]

### /11 POST endpoint repetido

    curl localhost:8080/11

> {"error":["404 - Resource Not Found"]} 

    curl -d '{"data":23}' -X POST localhost:8080/11

> [529]

### /12 POST con un rename complejo en dplyr

    curl localhost:8080/12

> {"error":["404 - Resource Not Found"]} 

    curl -d '{"data":23}' -X POST localhost:8080/12

> [{"cólúmná_ácentos":5,"más_ácéntós":"algo"}]%   

## atomicos
Una imagen on CentOS AtomicOS.

    sudo docker build -it fontanero_atomicos .    
    sudo docker run --rm -p 8080:8080 -t fontanero_atomicos   

### / GET hola mundo

    curl localhost:8080/

> {"fontanero":["CentOS Atomic"]}

### /1 GET simple ascii

    curl localhost:8080/1

> {"get":["sin acentos"]} 

    curl -d '{"data":23}' -X POST localhost:8080/1 

> {"error":["404 - Resource Not Found"]}

### /2 GET simple con non-ascii

    curl localhost:8080/2

> {"get":["<c3><b1> <c3><a9> <c3><ad> <c3><b3> - algunos ejemplos"]}

    curl -d '{"data":23}' -X POST localhost:8080/2

> {"error":["404 - Resource Not Found"]}

### /3 GET nombre variable non-ascii

    curl localhost:8080/3

>[23]

    curl -d '{"data":23}' -X POST localhost:8080/3 

> {"error":["404 - Resource Not Found"]}

### /4 GET nombre columna dataframe non-ascii

    curl localhost:8080/4

>[23]

    curl -d '{"data":23}' -X POST localhost:8080/4 

> {"error":["404 - Resource Not Found"]}

### /5 GET endpoint repetido (valores 23 y 46)

    curl localhost:8080/5

>[23]

    curl -d '{"data":23}' -X POST localhost:8080/5 

> {"error":["404 - Resource Not Found"]}

### /6 GET con un rename complejo en dplyr

    curl localhost:8080/6

> {"error":["404 - Resource Not Found"]} 

    curl -d '{"data":23}' -X POST localhost:8080/6 

> [{"c<c3><b3>l<c3><ba>mn<c3><a1>_<c3><a1>centos":5,"m<c3><a1>s_<c3><a1>c<c3><a9>nt<c3><b3>s":"algo"}]

### /7 POST simple con non-ascii

    curl localhost:8080/7

> {"error":["404 - Resource Not Found"]} 

    curl -d '{"data":23}' -X POST localhost:8080/7

>["<c3><b1> <c3><a9> <c3><ad> <c3><b3> - algunos ejemplos"]

### /8 POST nombre variable non-ascii

    curl localhost:8080/8

> {"error":["404 - Resource Not Found"]}

    curl -d '{"data":23}' -X POST localhost:8080/8

> [529]

### /9 POST nombre columan datafram non-ascii

    curl localhost:8080/9

> {"error":["404 - Resource Not Found"]}

    curl -d '{"data":23}' -X POST localhost:8080/9

> [529]

### /10 POST nombre columna datafram non-ascii

    curl localhost:8080/10

> 

    curl -d '{"data":23}' -X POST localhost:8080/10

>

### /11 POST endpoint repetido

    curl localhost:8080/11

> {"error":["404 - Resource Not Found"]}

    curl -d '{"data":23}' -X POST localhost:8080/11

> [529]

### /12 POST con un rename complejo en dplyr

    curl localhost:8080/12

> {"error":["404 - Resource Not Found"]} 

    curl -d '{"data":23}' -X POST localhost:8080/12

> [{"c<c3><b3>l<c3><ba>mn<c3><a1>_<c3><a1>centos":5,"m<c3><a1>s_<c3><a1>c<c3><a9>nt<c3><b3>s":"algo"}]
