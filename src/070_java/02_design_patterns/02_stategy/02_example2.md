### Example2

### Interface
```java
class PricingStrategy {
    void calculatePrice(int price, boolean isSignedUpForNewsletter);
}
```
### Regular Price
```java
class RegularPrice implements PricingStrategy {
    void calculatePrice(int price, boolean isSignedUpForNewsletter){
        System.out.println(price);
    }
}
```

### Sale Price
```java
class SalePrice implements PricingStrategy {
    void calculatePrice(int price, boolean isSignedUpForNewsletter){
        System.out.println(price);
    }
}
```

### Price Calculator
```java
public class PriceCalculator {

    private PricingStrategy pricingStrategy;

    public void calculate(int price, boolean isSignedUpForNewsletter) {
        this.pricingStrategy.calculatePrice(price, isSignedUpForNewsletter);
    }

    public void setPricingStrategy(PricingStrategy pricingStrategy) {
        this.pricingStrategy = pricingStrategy;
    }
}
```