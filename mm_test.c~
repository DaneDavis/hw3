/* A simple test harness for memory alloction. */

//#include "mm_alloc.h"
//#include "myMalloc.c"
#include <stdio.h>

#include <assert.h>
#include <string.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>

struct s_block{
	size_t size;
	struct s_block *next;
	int free;
};

#define blockSize sizeof(struct s_block)

void *global = NULL;

struct s_block *findFreeBlock(struct s_block **last, size_t size){
	struct s_block *current = global;

	while(current && !(current->free && current->size >= size)){
		*last = current;
		current = current->next;
	}
	return current;
}

struct s_block *requestSpace(struct s_block* last, size_t size){
	struct s_block *temp;
	temp = sbrk(0);
	void *request = sbrk(size + blockSize);
	assert((void*)temp == request); //not thread safe

	if(request == (void*)-1){
		return NULL;
	}

	if(last){
		last->next = temp;
	}

	temp->size = size;
	temp->next = NULL;
	temp->free = 0;
	
	return temp;
}

void *mymalloc(size_t size){
	struct s_block *block;

	if (size <= 0){
		return NULL;	
	}

	if(!global){
		block = requestSpace(NULL,size);

		if(!block){
			return NULL;	
		}

		global = block;
	}
	else{
		struct s_block *last = global;
		block = findFreeBlock(&last,size);

		if(!block){
			block = requestSpace(last,size);

			if(!block){
				return NULL;
			}
		}
		else{
			block->free = 0;
		}
	}

	return(block+1);
}

struct s_block *getBlockPtr(void* ptr){
	return (struct s_block*)ptr -1;
}

void free(void *ptr){

	if(!ptr){
		return;	
	}

	struct s_block* blockPtr = getBlockPtr(ptr);
	assert(blockPtr->free == 0);
	blockPtr->free =1;
}

void *realloc(void *ptr,size_t size){
	if(!ptr){
		return mymalloc(size);
	}

	struct s_block* blockPtr = getBlockPtr(ptr);

	if(blockPtr->size >= size){
		return ptr;	
	}

	void *newPtr;
	newPtr = mymalloc(size);

	if(!newPtr){
		return NULL;
	}

	memcpy(newPtr,ptr,blockPtr->size);
	free(ptr);
	return newPtr;
}


/* simple malloc, without free
void *simpleMalloc(size_t){
	void *ptr = sbrk(0);
	void *request = sbrk(size);

	if(request == (void*) -1){
		return NULL;
	}
	else{
		assert(p == request);// Not thread safe
		return ptr;
	}
}
*/ 


int main(int argc, char **argv)
{	
    int *data;
    data = (int*) mymalloc(4);
    data[0] = 1;
    free(data);
    printf("malloc sanity test successful!\n");
    return 0;
}
