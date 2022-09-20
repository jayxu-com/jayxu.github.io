---
id: 16014
title: 'Java Concurrent框架之阻塞队列（Blocking queue）'
date: '2005-10-11T16:56:36+08:00'
author: Jay
layout: post
guid: 'https://www.jayxu.com/?p=16014'
permalink: /2005/10/11/16014
posturl_add_url:
    - 'yes'
hefo_before:
    - '0'
hefo_after:
    - '0'
views:
    - '1776'
---

引子：
大家上过操作系统的都知道“生产者－消费者（Producer-Consumer）”模型，主要讨论的是进程（线程）间的互斥和同步问题，关键是对锁（lock）的申请、独占和释放，在这里我就不罗嗦了。原先我写的Java代码如下：
<pre lang="java" class="">public class Producer extends Thread{
  private ProductList products = ProductList.getInstance();
  
  public void run(){
    int i = 0;
    
    while(i &lt;= 20){
      synchronized(products){ // Get lock on product list
        if(products.isFull()){
          System.out.println("List is full");
          products.notify(); // Release the lock
        } else{
          Product product = new Product(i++); // Produce a product
          products.put(product);
          System.out.println("Produced product " + product.getId());
          products.notify(); // Release lock
        }
      } // Release the lock
    }
  }
}

public class Consumer extends Thread{
  ProductList products = ProductList.getInstance();
  
  public void run(){
    while(true){
      synchronized(products){
        try {
          products.wait(); // Wait for lock
          Product product = null;
          if(!(products.isEmpty()))
            product = products.take();
          else
            System.out.println("List is empty");
          System.out.println("Consumed product " + product.getId()); // Get the lock
        } catch (InterruptedException ex) {
          ex.printStackTrace();
        }
      } // Release the lock
    }
  }
}</pre>
<pre lang="java" class="">import java.util.ArrayList;
import java.util.List;

public class ProductList {
  private static ProductList instance = new ProductList();
  private List products; // Adapter pattern
  public static final int SIZE = 10;
  
  private ProductList() {
    products = new ArrayList(SIZE);
  }
  
  public static ProductList getInstance() { // Singleton pattern
    return instance;
  }
  
  public boolean isFull() {
    return products.size() == SIZE;
  }
  
  public void put(Product product) {
    products.add(product);
  }
  
  public Product take() {
    return products.remove(0);
  }
  
  public boolean isEmpty() {
    return products.isEmpty();
  }
}

public class Product {
  private int id;
  
  public Product(int id) {
    this.id = id;
  }
  
  public int getId() {
    return id;
  }
}

public class Main {
  public static void main(String[] args){
    Producer p = new Producer();
    Consumer c = new Consumer();
    
    p.start();
    c.start();
  }
}</pre>
虽然Java对信号量及原语做了更高层次的封装（wait()、notify()、notifyAll()、synchronized{}），但看完上述代码还是觉得有点麻烦，于是JDK 5在原先collection框架的基础上增加了java.util.concurrent包，封装了许多用于线程并发操作的数据结构和操作。其中的BlockingQueue接口就是封装了一个阻塞队列的接口，具体地说就是实现了一个用于消费者（多个）和生产者（多个）交换产品的中介，生产者线程在队列满时阻塞，消费者线程在队列空时阻塞，当然在没有得到锁之前两类线程均会阻塞。详细信息可以参考Java Doc。下面用BlockingQueue实现P-C模型：
<pre lang="java" class="">class Producer implements Runnable {
   private final BlockingQueue queue;
   Producer(BlockingQueue q) { queue = q; }
   public void run() {
     try {
       while(true) { queue.put(produce()); }
     } catch (InterruptedException ex) {  handle }
   }
   Object produce() {  }
}

class Consumer implements Runnable {
  private final BlockingQueue queue;
  Consumer(BlockingQueue q) { queue = q; }
  public void run() {
    try {
      while(true) { consume(queue.take()); }
    } catch (InterruptedException ex) {  handle }
  }
  void consume(Object x) {  }
}

class Setup {
  void main() {
    BlockingQueue q = new SomeQueueImplementation();
    Producer p = new Producer(q);
    Consumer c1 = new Consumer(q);
    Consumer c2 = new Consumer(q);
    new Thread(p).start();
    new Thread(c1).start();
    new Thread(c2).start();
  }
}</pre>
可以看出代码中没有出现wait()或notify()之类的原语操作，这些操作由concurrent框架负责封装。更全面的讨论可以参考<a href="http://www-128.ibm.com/developerworks/cn/java/j-tiger06164/" target="_blank">《驯服 Tiger: 并发集合》</a>（IBM）