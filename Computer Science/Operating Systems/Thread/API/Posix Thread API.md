---
tags:
  - operating-system
relates to:
  - "[[Thread]]"
---
`pthreads` - [[Operating System]] library API for threads

## Creation
---
```c
int pthread_create(
	pthread_t *thread,
	const pthread_attr_t *attr,
	void *(*start_routine)(void*),
	void *arg);
```
[[Thread]] is created executing `start_routine` with `arg` as its sole argument

This is how `pthread_create` looks inside:
![[pthread_create.png]]

## Termination
---
```c
void pthread_exit(void *value_ptr);
```
Terminates the thread and makes `value_ptr` available to any successful join

## Join
---
```c
int pthread_join(pthread_t thread, void **value_ptr);
```
Suspends execution of the calling thread until the target thread terminates

On return with a non-NULL `value_ptr` the value is passed to `pthread_exit()` by the termination thread is made available in the location referenced by `value_ptr`