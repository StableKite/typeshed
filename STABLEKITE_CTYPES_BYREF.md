The byref annotation preserves the type of the actual CData argument as the
read-only owner of the returned CArgObject. The pointer offset changes the
address passed to C, while the owner remains the original Python object.

CArgObject is covariant in its read-only owner. Its default owner is object:
other ctypes converters can create argument objects whose owner is bytes or
None. Only byref promises that its owner has the same concrete CData type as
the argument. Existing pre-3.14 keyword and 3.14+ positional-only signatures
remain unchanged.

A consumer can store the real byref result in its own structural Protocol
with a read-only _obj property and a precise owner type. This does not make
protected attributes public. Direct protected access remains subject to the
checker's ordinary rules; no private runtime type import is required for
structural storage. Runtime conversion still receives the original argument
object, with no wrapper or replacement object.
