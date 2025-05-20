## 3D Transform
---
### Perspective (투영점)
관찰자의 시점에서 원근감을 느끼게 하여 3D 환경을 만들어준다.

![[Pasted image 20250520211336.png]]

```js
<div className="size-50 border perspective-[600px]">
	<section className="w-full h-full bg-blue-500 rotate-y-45"></section>
</div>
```

perspective 값은 관찰자와 대상 요소 사이의 거리를 나타냄