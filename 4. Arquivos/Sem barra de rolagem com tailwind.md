---
tags:
  - css
  - tailwind
  - tips
data de criação: 2024-09-24
---
Podemos criar um utilitário para isso:

```css
@layer utilities {
    .no-scrollbar::-webkit-scrollbar {
      display: none;
    }

    .no-scrollbar {
      -ms-overflow-style: none;
      scrollbar-width: none;
    }
}
```

