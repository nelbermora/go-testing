# go-interfaces

Trabajar con Interfaces facilita la inyeccion de capas, y tambien el testing de cada capa.

Para desarrollar con este mecanismo es necesario que cada capa cuente con tres elementos fundamentales

## 1. Interfaz
Cada método exportable debera estar expuesto a través de la interfaz.
```go
type RepositoryInterfaz interface{
    LlamarSP() (string, error)
}
```

## 2. Struct
Imaginemos que cada capa o dependencia que queremos usar es un objeto con metodos que cumplen con la interfaz determinada previamente, para esto creamos un struct y hacemos que dicho struct cumpla con lo definido por la interfaz. Adicionalmente cada podemos aprovechar y definir que dependencias externas queremos inyectar. Por ejemplo: La capa repository necesita una base de datos del tipo sql.DB, entonces podemos definir el struct para que esté adentro contenge un objeto de este tipo. Si, lo se.. esto es un chino.. pero con la practica se va comprendiendo mejor.
```go
type repositoryStruct struct{
    db *sql.DB
}

func (rs *repositoryStruct)LlamarSP() (string, error){
    return "", nil
}
```

## 3. Funcion constructora
Creamos una funcion publica que será la que invocaremos para crear nuestra dependencia
```go
func NewRepository(dbAUtilizar *sql.DB) RepositoryInterfaz{
    return &repositoryStruct{
        db: dbAUtilizar,
    }
}
```
