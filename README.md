jassinaturas Client Library for Java
============================================

Client library to integrates Moip Assinaturas on Java.

Moip Assinaturas is a Moip's project that makes recurrence charges. It allows to create plans, customers, subscriptions and so on.

API documentation is available at: http://moiplabs.github.io/assinaturas-docs/api.html


 - Author: Danillo Souza

Still working on it
====================

# Using

First of all, you'll have to instanciate a new Assinaturas passing your credentials and the environment you want to connect.

```java
	Assinaturas assinaturas = new Assinaturas(new Authentication("YOUR_TOKEN", "YOUR_SECRET"));
```

### Plans

Creating a new plan:

```java
	Plan toCreate = new Plan();
	toCreate
		.withCode("YOR_PLAN_CODE")
		.withDescription("YOUR_PLAN_DESCRIPTION")
		.withName("YOUR_PLAN_NAME")
		.withAmount(1000)
        .withSetupFee(100)
        .withBillingCycles(1)
        .withPlanStatus(PlanStatus.ACTIVE)
        .withMaxQty(10)
        .withInterval(new Interval()
			.withLength(10)
			.withUnit(Unit.MONTH))
        .withTrial(new Trial()
			.withDays(10)
			.enabled());
```

After that you have to call following method:

```java
	Plan created = assinaturas.plan().create(toCreate);
```

Listing all plans:

```java
	List<Plan> plans = assinaturas.plan().list();
```

Getting a single plan:

```java
	Plan plan = assinaturas.plan().show("YOUR_PLAN_CODE");
```

Updating a plan:

To update a plan, you should inform your new plan params, creating a new object of Plan and passing it to update method

```java
	Plan toUpdate = new Plan();
    toUpdate.withCode("PLAN_CODE_TO_UPDATE")
		.withDescription("PLAN_NEW_DESCRIPTION")
		.withName("PLAN_NEW_NAME")
        .withAmount(10000)
        .withSetupFee(1000)
        .withBillingCycles(10)
        .withPlanStatus(PlanStatus.INACTIVE)
        .withMaxQty(100)
        .withInterval(new Interval()
        	.withLength(100)
        	.withUnit(Unit.DAY))
        .withTrial(new Trial()
        	.withDays(5)
        	.disabled());
```

After informing what you want to update, just call the following method:

```java
    Plan plan = assinaturas.plan().update(toUpdate);
```

Activating a plan:

```java
	Plan plan = assinaturas.plan().active("YOUR_PLAN_CODE");
```

Inactivating a plan:

```java
	Plan plan = assinaturas.plan().inactive(toInactivate);
```

### Subscriptions

Creating a new subscription

```java
	Subscription toBeCreated = new Subscription();
    toBeCreated
        .withCode("YOUR_SUBSCRIPTION_CODE")
        .withAmount(100)
        .withPlan(new Plan()
        			.withCode("YOUR_PLAN_CODE"))
        .withCustomer(
            new Customer()
                .withCode("YOUR_CUSTOMER_CODE")
                .withBirthdate(new GregorianCalendar(1989, GregorianCalendar.OCTOBER, 13))
                .withCpf("CPF_NUMBER")
                .withEmail("some@email.com")
                .withFullname("CUSTOMER_NAME")
                .withPhoneAreaCode("CUSTOMER_PHONE_AREA_CODE")
                .withPhoneNumber("CUSTOMER_PHONE_NUMBER")
                .withAddress(
                    new Address()
                        .withCity("São Paulo")
                        .withComplement("Apto")
                        .withCountry(Country.BRA)
                        .withDistrict("Centro")
                        .withNumber("1000")
                        .withState(State.SP)
                        .withStreet("Some Street")
                        .withZipcode("00000-000"))
                .withBillingInfo(
                    new BillingInfo()
                    	.withCreditCard(new CreditCard()
					                        	.withExpirationMonth("10")
					                            .withExpirationYear("18")
					                            .withHolderName("Some Name")
					                            .withNumber("4111111111111111"))));
```

You can also create a subscription just informing an already created customer:

```java
	Subscription toBeCreated = new Subscription();
    toBeCreated
        .withCode("SUBSCRIPTION_CODE")
		.withAmount(100)
        .withCustomer(new Customer()
			.withCode("YOUR_CUSTOMER_CODE"))
        .withPlan(new Plan()
			.withCode("YOUR_PLAN_CODE"));
```

Then you'll need to call the following method:

```java
	Subscription created = assinaturas.subscription().create(toBeCreated);
```

Updating a subscription

```java
	Subscription toUpdate = new Subscription();
    toUpdate
    	.withCode("SUBSCRIPTION_CODE")
    	.withPlan(new Plan()
			.withCode("plano01"))
    	.withAmount(990)
        .withNextInvoiceDate(new NextInvoiceDate()
			.withDay(20)
			.withMonth(Calendar.OCTOBER)
			.withYear(2015));
```

Then call the following method:

```java
	Subscription subscription = assinaturas.subscription().update(toUpdate);
```

Activating a subscription:

```java
	Subscription subscription = assinaturas.subscription().activate("SUBSCRIPTION_CODE");
```

Cancelling a subscription:

```java
	Subscription subscription = assinaturas.subscription().cancel("SUBSCRIPTION_CODE");
```

Suspending a subscription:

```java
	Subscription subscription = assinaturas.subscription().suspend("SUBSCRIPTION_CODE");
```

Getting a single subscription:

```java
	Subscription subscription = assinaturas.subscription().show("SUBSCRIPTION_CODE");
```

Listing all subscriptions:

```java
	List<Subscription> subscriptions = assinaturas.subscription().list();
```

Listing invoices from a subscription:

```java
	List<Invoice> invoices = assinaturas.subscription().invoices("SUBSCRIPTION_CODE");
```

Thanks
====================

Rodrigo Saito - @rodrigosaito
Breno Oliveira - @brenohdo

Contributing
====================

== Copyright

Copyright (c) 2014 Danillo Souza. Distributed under the MIT license. See LICENSE for details.