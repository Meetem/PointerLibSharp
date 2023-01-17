# C# Pointer Library

Allows you to take a pointer of any C# managed object (e.g class objects, arrays, etc)

There are two functions:
### `void* GetPointer(this object obj)`
returns a pointer to the native object.

### `void* GetInternalPointer(this object obj)`
returns Unity's internal (m_cachedPtr) pointer of UnityEngine.Object

<details>
<summary>Source Code (IL)</summary>

GetPointer:
```cil
ldarga.s obj (0)
conv.u
ldind.i
ret
```

GetInternalPointer:
```cil
ldarga.s obj(0)
conv.u
ldind.i
sizeof [mscorlib]System.IntPtr
ldc.i4.2
mul
add
ldind.i
ret
```
</details>

My blog post about pointers in C#:
https://meetemq.com/2023/01/14/using-pointers-in-c-unity/