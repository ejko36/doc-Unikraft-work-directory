
# Unikraft 빌드 및 실행 방법


## 빌드 방법

### 예제 ) Redis


### Dependency Graph
![plot](./pictures/dependency_graph.PNG)

### Makefile

Redis Application에 필요한 Unikraft 기본 라이브러리
1. [lib-pthread-embedded](https://github.com/unikraft/lib-pthread-embedded.git)
2. lib-newlib
3. lib-lwip
```
UK_ROOT ?= $(PWD)/../../unikraft
UK_LIBS ?= $(PWD)/../../libs
LIBS := $(UK_LIBS)/lib-pthread-embedded:$(UK_LIBS)/lib-newlib:$(UK_LIBS)/lib-lwip:$(UK_LIBS)/lib-redis

all:
	@$(MAKE) -C $(UK_ROOT) A=$(PWD) L=$(LIBS)

$(MAKECMDGOALS):
	@$(MAKE) -C $(UK_ROOT) A=$(PWD) L=$(LIBS) $(MAKECMDGOALS)
```




```
UK_ROOT ?= $(PWD)/../../unikraft
UK_LIBS ?= $(PWD)/../../libs
LIBS := $(UK_LIBS)/lib-lwip:$(UK_LIBS)/lib-pthread-embedded:$(UK_LIBS)/lib-newlib:$(UK_LIBS)/lib-nginx:$(UK_LIBS)/lib-tlsf

all:
	@$(MAKE) -C $(UK_ROOT) A=$(PWD) L=$(LIBS)

$(MAKECMDGOALS):
	@$(MAKE) -C $(UK_ROOT) A=$(PWD) L=$(LIBS) $(MAKECMDGOALS)
```



## 실행 방법

Server와 연결할 Bridge 추가

```
sudo brctl addbr br0
sudo ip a a 172.44.0.1/24 dev br0
sudo ip l set dev br0 up
```


QEMU + Unikraft Image 실행



```

```

```

```







참고자료: https://github.com/mariasfiraiala/scs-work/blob/master/unikraft-scs/unikraft-scs-for-complex-apps.md
