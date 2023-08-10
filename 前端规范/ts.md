## TS 命名规范

### type 类型 (添加前缀 T\_)

```javascript
    type T_(具体的类型描述-大驼峰) = number | string;
```

### interface 类型 (添加前缀 I\_)

```javascript

    interface I_(具体的类型描述-大驼峰) {
		id: number | string
	};
```

### enum 类型 (添加前缀 E\_)

```javascript
    enum E_(具体的类型描述-大驼峰) ={
		'显示',
		'未初始化',
		'初始化完成',
		'最小化',
		'隐藏内容',
		'最大化'
	}
```
