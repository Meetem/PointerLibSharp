# C# Pointer Library

Allows you to take a pointer of any C# managed object (e.g class objects, arrays, etc) thorugh IL instructions (fully optimized by a compiler, no array hacks, marshaling, etc)

There are two main functions:
```cs
//returns a pointer to the native object.
void* GetPointer(this object obj);
```

```cs
//returns Unity's native object (m_cachedPtr) pointer of UnityEngine.Object
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


There are also new functions:
```cs
// Returns a reference to the first element in array
//ArrayUtil:
ref T GetArrayPointer<T>(this T[] array);
```

String interop:
```cs
// StringUtil.StringAccess for native access to managed string.

// Returns the accessor
StringAccess *GetAccess(this string str);

// Returns the pointer to the string data (Unicode, 2-bytes per char)
byte *GetDataPointer(this string str);

// Writes data to the string from unsafe buffer
// Returns number of BYTES written
int SetData(this string str, byte *dataInUnicode16, int maxBytesRead, int maxBytesWrite);

// Writes data to the string from unsafe buffer and sets the new length
// Returns number of BYTES written
int SetData(StringAccess *str, byte *dataInUnicode16, int maxBytesRead, int maxBytesWrite, int newLengthInChars);

// Copy string data and length to <str> from <from>. Doesn't read/write more than (maxStringCapacity * 2) bytes.
void CopyFrom(this string str, string from, int maxStringCapacity);

// Sets new length to the string and returns previous
int SetLength(this string str, int newLengthInChars);

// Calculated the length of Unicode-16 null-terminated string, returns the number of symbols.
int UnicodeNullTerminatedLength(ushort* dataUnicode16, int maxReadBytes);
```

My blog post about pointers in C#:
https://meetemq.com/2023/01/14/using-pointers-in-c-unity/
