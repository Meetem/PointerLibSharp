# C# Pointer Library

Allows you to take a pointer of any C# managed object (e.g class objects, arrays, etc) thorugh IL instructions (fully optimized by a compiler, no array hacks, marshaling, etc)

There are two functions:
```cs
//returns a pointer to the native object.
void* GetPointer(this object obj);
```

```cs
//returns Unity's internal (m_cachedPtr) pointer of UnityEngine.Object
void* GetInternalPointer(this object obj);
```

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
