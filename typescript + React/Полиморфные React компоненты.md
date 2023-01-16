<iframe width="560" height="315" src="https://www.youtube.com/embed/3nKMO2UNQoY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Универсальные React компоненты могут принимать разный набор просов и отрисовывать в разметку компоненты с разными тегами. Например, кнопка может быть как button, так и ссылкой, или даже div или span. TypeScript помогает упростить создания подобного рода компоненты.

## Button example 
```tsx
import cn from "classnames";
import { ComponentProps, ElementType } from "react";

type ButtonOwnProps<E extends ElementType = ElementType> = {
children: string;
primary?: boolean;
secondary?: boolean;
as?: E;
};

type ButtonProps<E extends ElementType> = ButtonOwnProps<E> & Omit<ComponentProps<E>, keyof ButtonOwnProps>;

const defaultElement = "button";

export default function Button<E extends ElementType = typeof defaultElement>({
children,
primary,
secondary,
as,
...otherProps
}: ButtonProps<E>) {
   
const classes = cn({ primary, secondary });
const TagName = as || defaultElement;

return (
<TagName className={classes} {...otherProps}>
{children}
</TagName>
);
}
```



## Что важно

1. Использовать generic чтобы расширятся от ElementType, который предоставляется самим React
2. Пишем два типа - собственные пропсы и пропсы для конкретной кнопки
   
```tsx
type ButtonOwnProps<E extends ElementType = ElementType> = {
...
};
type ButtonProps<E extends ElementType> = ButtonOwnProps<E> & Omit<ComponentProps<E>, keyof ButtonOwnProps>;
```
3.  При помощи [[Utility Types#`Omit<Type, Keys>`|Omit]] убираем лишнее.
4. Не забываем пробросить остальные пропсы через [[spread]]
