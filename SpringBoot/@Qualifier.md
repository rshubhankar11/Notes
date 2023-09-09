# @Qualifier in Spring Boot

In Spring Boot, the `@Qualifier` annotation is used to specify which bean should be injected when multiple beans of the same type are available. This annotation is helpful when you have multiple implementations of an interface or multiple beans of the same class, and you want to indicate which one to inject.

## Example

Consider a scenario where you have multiple implementations of a `PaymentProcessor` interface, and you want to inject a specific implementation into your service. Here's how you can use `@Qualifier`:

```java
public interface PaymentProcessor {
    void processPayment();
}

@Service
@Qualifier("creditCardPayment")
public class CreditCardPaymentProcessor implements PaymentProcessor {
    @Override
    public void processPayment() {
        // Implement credit card payment processing logic
    }
}

@Service
@Qualifier("paypalPayment")
public class PaypalPaymentProcessor implements PaymentProcessor {
    @Override
    public void processPayment() {
        // Implement PayPal payment processing logic
    }
}
```

In this example, we have two implementations of the `PaymentProcessor` interface: `CreditCardPaymentProcessor` and `PaypalPaymentProcessor`. Both are annotated with `@Service`, making them Spring-managed beans.

Now, in a service class where you want to use one of these payment processors, you can use the `@Autowired` annotation along with `@Qualifier` to specify which implementation to inject:

```java
@Service
public class PaymentService {
    private final PaymentProcessor paymentProcessor;

    @Autowired
    public PaymentService(@Qualifier("creditCardPayment") PaymentProcessor paymentProcessor) {
        this.paymentProcessor = paymentProcessor;
    }

    public void processPayment() {
        paymentProcessor.processPayment();
    }
}
```

In this `PaymentService` class, we use `@Qualifier("creditCardPayment")` to specify that we want to inject the `CreditCardPaymentProcessor` bean. If you change the qualifier to `"paypalPayment"`, it will inject the `PaypalPaymentProcessor` bean instead.

Using `@Qualifier` in this way helps you control which bean is injected when multiple beans of the same type exist in your Spring Boot application.

Remember to import the necessary Spring Boot annotations and dependencies in your project for this code to work as expected.

## Example 2:

> If we have 2 implementations to one interface then using `@Qualifier("bookerAward")` we can specify implementation class we need .

We have on Interface `Award`:

```Java


public interface Award {

	void award();

}
```

We have implemented `Award` in `BookAward` class :

```Java


import org.springframework.stereotype.Component;

@Component
public class BookerAward implements Award {

	@Override
	public void award() {

		System.out.println("You got booker prize...");
	}
}
```

Then we have implemented `Award` in `NationalAward` class

```Java


import org.springframework.stereotype.Component;

@Component
public class NationalAward implements Award{

	public void award() {

		System.out.println("Your Writting got National Award!");
	}
}
```

Using `@Qualifier("bookerAward")` we can specify the out of the 2 implementation which we need in the Service class :

```Java
package com.studytonight.community;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.stereotype.Component;

@Component
public class FictionWriter implements Writer {

	@Autowired
	@Qualifier("bookerAward")
	private Award award;

	@Override
	public void write() {

		System.out.println("Write Fiction Novels...");
	}

	@Override
	public void getAward() {

		award.award();
	}
}
```
