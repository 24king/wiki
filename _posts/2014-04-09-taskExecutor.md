---
layout: default
title: java.spring.multiThread.taskExecutor
tags: java spring multiThread
---
## 背景交代
今天写代码,但是突然发现进程调度的时候,同一个任务被调度执行了两次,这个就有问题了,于是就再次研究一下这个Spring所提供的关于,异步执行和多任务调度的机制了.突然发现说自己会写后台代码,但是自己对于有些机制的了解还是不够的.了解框架就是了解他为你设计的机制,实现你所需要的策略来完成你要完成的事情.

		框架我的理解就是:为了实现一件事情,框架提供了一套机制,让调用者实现自己需要的相关的策略,更好的在体制内做事情.这就是框架.

## 基本概念 

>1. Spring方案: 为了更好的解决异步执行和任务调度
>1. Spring机制: 异步执行和任务调度机制
>2. Spring策略: TaskExecutor TaskScheduler interface

Quartz Scheduler

## Spring TaskExecutor abstraction

> executor there is no guarantee that the underlying implementation is actually a pool. **single-thread or even sychronous**

		java.util.concurrent.Executor
		single method execute(Runnable task)

> The taskExecutor was originally created to give other spring compenents an abstraction for thread pooling where needed. such as
> ApplicationEventMulticaster,JMS's AbstractMessageListenerContainer, and Quartz
> integration all use TaskExecutor abstraction to pool threads


## Common use TaskExecutor Types

#### 1. SimpleAsyncTaskExecutor
> 简单的异步执行器:不重用任何线程;但是可以设置并发限制数量的.

#### 2. SyncTaskExecutor
> 同步执行器:每一个调用都在调用的线程中执行,常用在不需要多线程的地方.

#### 3. ConcurrentTaskExecutor
> ThreadPoolTaskExecutor: 如果ThreadPoolTaskExecutor 不怎么够用的时候,可以考虑使用ConcurrentTaskExecutor
> 其中,ThreadPoolTaskExecutor可以通过bean的属性来获取对应的线程池参数.

#### 4. SimpleThreadPoolExecutor
> 是Quartz's SimpleThreadPool 的子类: 通常用在,线程池需要被Quartz 和non-Quratz components 组件之中.

#### 5. ThreadPoolTaskExecutor
> 只能在Java
5环境中使用,他将bean的属性,用来配置,java.util.concurrent.ThreadPoolExecutor and **wrap it in a taskExecutor**
> 但是如果你需要高级的属性,例如,ScheduledThreadPoolExecutor 就建议使用ConcurrentTaskExecutor


#### 6. TimeTaskExecutor
> use a single TimerTask, 和SyncTaskExecutor不同的是,它会在一个独立的进程中执行,尽管在那个线程中是同步的.

#### 7. workManagerTaskExecutor
> use the CommonJ WorkManager for setting up a CommonJ WorkManager referrence in a spring Context

## 使用TaskExecutor

	import org.springframework.core.task.TaskExecutor;
	
	public class TaskExecutorExample {
	
	    private class MessagePrinterTask implements Runnable {
		      private String message;
			      public MessagePrinterTask(String message) {
					      this.message = message;
				  }
				  
				  public void run() {
				      System.out.println(message);
				  }

		}

		private TaskExecutor taskExecutor;

		public TaskExecutorExample(TaskExecutor taskExecutor) {
			this.taskExecutor = taskExecutor;
		}
		public void printMessages() {
			for(int i = 0; i < 25; i++) {
				taskExecutor.execute(new MessagePrinterTask("Message" + i));
			}
		}
	}

	<bean id="taskExecutor" class="org.springframework.scheduling.concurrent.ThreadPoolTaskExecutor">
	  <property name="corePoolSize" value="5" />
	  <property name="maxPoolSize" value="10" />
	  <property name="queueCapacity" value="25" />
	</bean>
	<bean id="taskExecutorExample" class="TaskExecutorExample">
	  <constructor-arg ref="taskExecutor" />
	</bean>


## The Spring TaskScheduler abstraction

	public interface TaskScheduler {
	
		  ScheduledFuture schedule(Runnable task, Trigger trigger);

		  ScheduledFuture schedule(Runnable task, Date startTime);

		  ScheduledFuture scheduleAtFixedRate(Runnable task, Date startTime, long period);

		  ScheduledFuture scheduleAtFixedRate(Runnable task, long period);

		  ScheduledFuture scheduleWithFixedDelay(Runnable task, Date startTime, long delay);

		  ScheduledFuture scheduleWithFixedDelay(Runnable task, long delay);
	}
	


[Spring](http://docs.spring.io/spring/docs/3.0.x/spring-framework-reference/html/scheduling.html)
