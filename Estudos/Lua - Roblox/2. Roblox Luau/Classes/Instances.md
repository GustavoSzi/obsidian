Uma instância é a classe base para todas as classes na hierarquia do Roblox que podem fazer parte do DataModel.

Uma função especial dessa classe é `Instance.new()`, que usamos para criar objetos usando código. Passamos a essa função o nome da classe que queremos criar (Ex: `Intance.new("Part")`).

Após criarmos uma nova instância, podemos manipular várias propriedades dela:

```lua
local newPart = Instance.new("Part")
newPart.Name = "New name"
newPart.Parent = script.Parent

...
```

> Para ver todos os metodos e propriedades de uma instancia, confira [a documentação](https://create.roblox.com/docs/reference/engine/classes/Instance). 