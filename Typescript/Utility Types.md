## `Partial <Type>`

Создает тип, которые делает все значения опциональными:

```ts
interface Todo {
title: string;
description: string;
}

function updateTodo(todo: Todo, fieldsToUpdate: Partial<Todo>) {
return { ...todo, ...fieldsToUpdate };

```

## `Required<Type>`

Противоположность Partial, делает все значения обязательными:

```ts
interface Props {
a?: number;
b?: string;
}

const obj2: Required<Props> = { a: 5 };
```

## `Record<Keys, Type>` 
Он позволяет создавать типизированную мапу:

```ts
interface CatInfo {
age: number;
breed: string;
}

type CatName = "miffy" | "boris" | "mordred";

const cats: Record<CatName, CatInfo> = {
miffy: { age: 10, breed: "Persian" },
boris: { age: 5, breed: "Maine Coon" },
mordred: { age: 16, breed: "British Shorthair" },
};
```

## `Pick<Type, Keys>`

"Берем" определенные значения из типа по ключам:

```ts
interface Todo {
title: string;
description: string;
completed: boolean;
}

type TodoPreview = Pick<Todo, "title" | "completed">;

const todo: TodoPreview = {
title: "Clean room",
completed: false,
};
```

## `Omit<Type, Keys>`
Берем все значения из типа и удаляем те, что указаны в ключах
```ts
interface Todo {
title: string;
description: string;
completed: boolean;
createdAt: number;
}

type TodoPreview = Omit<Todo, "description">;

const todo: TodoPreview = {
title: "Clean room",
completed: false,
createdAt: 1615544252770,
};
```
