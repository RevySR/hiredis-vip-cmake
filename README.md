# hiredis-vip-cmake

- Inherit Password from [hiredis-v](https://github.com/wuli1999/hiredis-v)
- Add Reference Counter
- Inherit Cluster from [hiredis-vip](https://github.com/vipshop/hiredis-vip)
- Compatible Tencent Cloud Redis

## Reference

- [hiredis-v](https://github.com/wuli1999/hiredis-v)
- [hiredis-vip](https://github.com/vipshop/hiredis-vip)

## API

### hiredis-vip-cmake

#### Add & Modify API

```c
/* redisReply add refcount */
/* This is the reply object returned by redisCommand() */
typedef struct redisReply {
    /* ... */
	int refcount; /* add a ref count for free object among different modules */
} redisReply;

/* Add & Modify API */
static redisReply *createReplyObject(int type);
void addReplyObjectRef(void *reply);
void freeReplyObject(void *reply);

```

### hiredis-v

#### CLUSTER AUTH SUPPORT & ADD AUTHENTICATE API

```c
int redisClusterSetOptionPassword(redisClusterContext *cc, const char *password);
```

#### HOW TO USE

```c
redisClusterContext *cc = redisClusterContextInit();
redisClusterSetOptionPassword(cc, "your password");
redisClusterSetOptionAddNodes(cc, "your cluster info");
redisClusterConnect2(cc);
```

#### MORE INFORMATION:
more information, see https://github.com/vipshop/hiredis-vip/wiki

#### AUTHORS
Hiredis-v was maintained and used at [wuli1999](https://github.com/wuli1999).

### hiredis-vip


#### Add cluster api

```c
redisClusterContext *redisClusterContextInit(void);
void redisClusterFree(redisClusterContext *cc);

int redisClusterSetOptionAddNode(redisClusterContext *cc, const char *addr);
int redisClusterSetOptionAddNodes(redisClusterContext *cc, const char *addrs);
int redisClusterSetOptionConnectBlock(redisClusterContext *cc);
int redisClusterSetOptionConnectNonBlock(redisClusterContext *cc);
int redisClusterSetOptionParseSlaves(redisClusterContext *cc);
int redisClusterSetOptionParseOpenSlots(redisClusterContext *cc);
int redisClusterSetOptionRouteUseSlots(redisClusterContext *cc);
int redisClusterSetOptionConnectTimeout(redisClusterContext *cc, const struct timeval tv);
int redisClusterSetOptionTimeout(redisClusterContext *cc, const struct timeval tv);
int redisClusterSetOptionMaxRedirect(redisClusterContext *cc,  int max_redirect_count);

int redisClusterConnect2(redisClusterContext *cc);

void *redisClusterFormattedCommand(redisClusterContext *cc, char *cmd, int len);
void *redisClustervCommand(redisClusterContext *cc, const char *format, va_list ap);
void *redisClusterCommand(redisClusterContext *cc, const char *format, ...);
void *redisClusterCommandArgv(redisClusterContext *cc, int argc, const char **argv, const size_t *argvlen);
int redisClusterAppendFormattedCommand(redisClusterContext *cc, char *cmd, int len);
int redisClustervAppendCommand(redisClusterContext *cc, const char *format, va_list ap);
int redisClusterAppendCommand(redisClusterContext *cc, const char *format, ...);
int redisClusterAppendCommandArgv(redisClusterContext *cc, int argc, const char **argv, const size_t *argvlen);
int redisClusterGetReply(redisClusterContext *cc, void **reply);
void redisClusterReset(redisClusterContext *cc);

redisContext *ctx_get_by_node(redisClusterContext *cc, struct cluster_node *node);

redisClusterAsyncContext *redisClusterAsyncConnect(const char *addrs, int flags);
int redisClusterAsyncSetConnectCallback(redisClusterAsyncContext *acc, redisConnectCallback *fn);
int redisClusterAsyncSetDisconnectCallback(redisClusterAsyncContext *acc, redisDisconnectCallback *fn);
int redisClusterAsyncFormattedCommand(redisClusterAsyncContext *acc, redisClusterCallbackFn *fn, void *privdata, char *cmd, int len);
int redisClustervAsyncCommand(redisClusterAsyncContext *acc, redisClusterCallbackFn *fn, void *privdata, const char *format, va_list ap);
int redisClusterAsyncCommand(redisClusterAsyncContext *acc, redisClusterCallbackFn *fn, void *privdata, const char *format, ...);
int redisClusterAsyncCommandArgv(redisClusterAsyncContext *acc, redisClusterCallbackFn *fn, void *privdata, int argc, const char **argv, const size_t *argvlen);

void redisClusterAsyncDisconnect(redisClusterAsyncContext *acc);
void redisClusterAsyncFree(redisClusterAsyncContext *acc);

redisAsyncContext *actx_get_by_node(redisClusterAsyncContext *acc, cluster_node *node);
```

#### MORE INFORMATION:
more information, see https://github.com/vipshop/hiredis-vip/blob/master/README.md
