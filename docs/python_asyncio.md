## 基本概念
**future**
future是一个数据结构，表示还未完成的工作结果。事件循环可以监视**Future对象是否完成**。从而允许应用的一部分等待另一部分完成一些工作。

**Task**

task是**Future的一个子类**，它知道如何**包装和管理一个协程的执行**。任务所需的资源可用时，事件循环会调度任务，并生成一个结果，从而可以**由其他协程消费**。

任务（Task）是与事件循环交互的主要途径之一。任务可以包装协程，可以跟踪协程何时完成。任务是Future的子类，所以使用方法和future一样。协程可以等待任务，每个任务都有一个结果，在它完成之后可以获取这个结果。因为协程是没有状态的，我们通过使用create_task方法可以将协程包装成有状态的任务。还可以在任务运行的过程中取消任务。

```python
import asyncio


async def child():
    print("进入子协程")
    return "the result"


async def main(loop):
    print("将协程child包装成任务")
    task = loop.create_task(child())
    print("通过cancel方法可以取消任务")
    task.cancel()
    try:
        await task
    except asyncio.CancelledError:
        print("取消任务抛出CancelledError异常")
    else:
        print("获取任务的结果", task.result())


if __name__ == '__main__':
    loop = asyncio.get_event_loop()
    try:
        loop.run_until_complete(main(loop))
    finally:
        loop.close()
```

另外出了使用loop.create_task将协程包装为任务外还可以使用asyncio.ensure_future(coroutine)建一个task。在python3.7中可以使用asyncio.create_task创建任务。


**启动一个协程**

一般对于**入口函数**，最简答的方法就是使用**run_until_complete()，并将协程直接传入这个方法**。

```python
import asyncio


async def foo():
    print("这是一个协程")


if __name__ == '__main__':
    loop = asyncio.get_event_loop()
    try:
        print("开始运行协程")
        coro = foo()
        print("进入事件循环")
        loop.run_until_complete(coro)
    finally:
        print("关闭事件循环")
        loop.close()
```


## async for的使用
```python
import random
import asyncio


async def random_number_gen(delay, start, end):
    while True:
        yield random.randint(start, end)
        await asyncio.sleep(delay)


async def main():
    async for i in random_number_gen(1, 0, 100):
        print(i)


try:
    print("Starting to print out random numbers...")
    print("Shut down the application with Ctrl+C")
    asyncio.run(main())
except KeyboardInterrupt:
    print("Closed the main loop..")
```
