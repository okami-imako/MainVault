---
tags:
  - operating-system
  - concurrency
relates to:
  - "[[Mutex]]"
  - "[[Thread]]"
---
## Create
---
```c
int pthread_mutex_init(
	pthread_mutex_t *mutex,
	const pthread_mutexattr_t *attr);
```


## Lock & Unlock
---
```c
int pthread_mutex_lock(pthread_mutex_t *mutex);

int pthread_mutex_unlock(pthread_mutex_t *mutex);
```