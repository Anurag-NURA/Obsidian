Strings, number, Boolean are __primitive value__ and one thing special about primitive is that we cannot edit the actual assigned value but we can _replace_ them or _overwrite_ them. 

![[Pasted image 20240727111552.png]]

The above picture shows that even using the inbuild function for strings we don't edit or modify the current string but replace them with new one. In the above case 'Hello!' was  joined with '!!!' and returned a new string. i.e., "Hello!!!!".

But Objects and Arrays are __Reference type__, which means that the actual value are edited rather than it is replaced. 

![[Pasted image 20240727112236.png]]

Which simply means in JavaScript we don't store the value, we store the address of the memory where data is stored in the variable. So when we use some inbuild function, like push, for an array than actual value is edited without reassigning the variable with new value.

![[Pasted image 20240727115020.png]]
