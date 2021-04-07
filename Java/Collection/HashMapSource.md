## 无参数的构造方法
```java
public HashMap() {
    默认的装载因子为0.75，hashcode的概率服从Poisson distribution。
    this.loadFactor = DEFAULT_LOAD_FACTOR; // all other fields defaulted
}
```
