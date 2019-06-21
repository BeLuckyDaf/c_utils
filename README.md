# C Utils

## Array List
This simple generic array list allows any kind of data passed as void pointers. It also features auto expansion when the size limit is reached, it automatically acquires twice as much memory, copies all the contents of the list and then frees the previously allocated memory.

### Usage

#### Create list
In order to create an array list you need to call `array_list_create(size_t)` and pass the initial size as an argument.

#### Add item
In order to add an item to the list, call `array_list_add(p_array_list, void*)` and pass a pointer to the list and a pointer to the item.

#### Remove item
In order to remove an item from the list, call `array_list_remove(p_array_list, void*)` and pass a pointer to the list and a pointer to the item you want to remove.

#### Remove item by index
In order to remove an item from the list by index, call `array_list_remove_at(p_array_list, int)` and pass a pointer to the list and a number, representing the index in the internal array. 

You can get this index from `array_list_iter(p_array_list)` and `array_list_next(p_array_list, int)`, in the latter function the second argument is the current iterator index.

#### Iterate through the list
You can iterate through the list by getting the real indices of items in the internal array by calling `array_list_iter(p_array_list)` and `array_list_next(p_array_list, int)`, please see the example down below.

#### Get item
You can retrieve an item from the list by calling `array_list_get(p_array_list, int)`, where the second argument is the iterator index.

#### Example
```c
#include "alist.h"

int main() {
	// Create array list of size 2
	p_array_list alist = array_list_create(2);

	// Create a few integers and add them to the list
	int a = 1, b = 2;
	array_list_add(alist, &a);
	array_list_add(alist, &b);

	// Iterate through the list
	// Get the index of the first item
	int iter = array_list_iter(alist);
	while(iter >= 0) {
		// Get the current item
		int *item = array_list_get(alist, iter);

		...

		// Remove this element
		array_list_remove(alist, item);

		// Or remove by index
		array_list_remove_at(alist, iter);

		// Get the next index
		iter = array_list_next(alist, iter);
	}

	// Free all members
	// Note: this will try to free the memory of each pointer
	// in the array list
	array_list_free_members(alist);

	// Free the list itself once it's not needed anymore
	array_list_free(alist);

	return 0;
}
```

## Sockutils
Sockutils provides simple functions to save space when working with sockets.

### Usage

#### Example

```c
#include "sockutils.h"

#define PORT 12000

int main() {
	// Simple tcp socket
	int tcpsock = create_tcp_socket();

	// Simple udp socket
	int udpsock = create_udp_socket();

	// Sockaddr structure for address
	p_sockaddr_in addr = create_sockaddr(PORT);

	// Bind a socket to a specific address
	bind_socket(tcp, addr);

	// Set a socket to non-blocking
	set_nonblocking(udpsock);

	return 0;
}
```