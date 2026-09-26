Good question — the name itself packs two separate ideas together, so it's worth pulling apart.

**Where's the dependency?**

`PaymentService` needs to call some payment gateway to do its job — that's a dependency, full stop. Any time class A calls methods on class B, A depends on B. In the naive version:

```
class PaymentService {
    private StripeGateway gateway = new StripeGateway();
    
    void processPayment(amount) {
        gateway.charge(amount);
    }
}
```

`PaymentService` (high-level — it represents business logic, "process a payment") depends directly on `StripeGateway` (low-level — it represents implementation detail, "how to talk to Stripe's API").

**Where's the inversion?**

Without DIP, the dependency *arrow* points from high-level to low-level:

```
PaymentService  --->  StripeGateway
(policy)              (detail)
```

This is backwards in an important sense: your core business logic (what "processing a payment" means) is now hostage to a specific vendor's implementation. Change Stripe's SDK, or switch to Razorpay, and you have to edit `PaymentService` — code that shouldn't care about that detail at all.

DIP inverts that arrow by introducing an abstraction that *both* sides depend on, and making the low-level detail depend on it too — instead of the high-level module depending on the low-level module:

```
PaymentService  --->  PaymentGateway (interface)  <---  StripeGateway
(high-level)          (abstraction)                     (low-level)
```

```
interface PaymentGateway {
    void charge(amount);
}

class StripeGateway implements PaymentGateway {
    void charge(amount) { /* Stripe-specific code */ }
}

class PaymentService {
    private PaymentGateway gateway;  // depends on the interface, not StripeGateway
    
    PaymentService(PaymentGateway gateway) {  // injected
        this.gateway = gateway;
    }
    
    void processPayment(amount) {
        gateway.charge(amount);
    }
}
```

Notice what flipped: originally, `StripeGateway` was just a class sitting there, unaware of any contract, and `PaymentService` reached down and grabbed it directly. Now `StripeGateway` has to *conform* to `PaymentGateway` — the low-level module bends to fit an abstraction that the high-level module defines the shape of. The dependency that used to point downward (high depends on concrete low) now points *inward*, toward an abstraction owned conceptually by the high-level policy. That reversal of who depends on whom — the detail now depends on the abstraction, rather than the abstraction (if any existed at all) depending on the detail — is the "inversion."

So concretely:
- **Dependency**: `PaymentService` needs *some* implementation of payment charging to function — that dependency never goes away.
- **Inversion**: what changes is that both `PaymentService` and `StripeGateway` now depend on `PaymentGateway`, instead of `PaymentService` depending directly on `StripeGateway`. The low-level detail is inverted into depending on an abstraction, rather than being depended upon directly.
