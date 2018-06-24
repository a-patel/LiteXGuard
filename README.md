# LiteXGuard
LiteX.Guard is a simple guard clause argument validation library, that helps you with validation of your arguments. 

A simple package with guard clause helper methods. This library provides guard clauses that could be used to guard against not expected values. It provides conditions for objects, strings, numerics, datatime and enumerables. It is possible to configure which exception should be thrown.

Argument validation made simple and unified. It ensures arguments conforms to simple validation rules and provides an uniformed exception throwing strategy if arguments are invalid.


It's developed for .NET Standard 2.0 and available via [NuGet](https://www.nuget.org/packages/LiteX.Guard/).



### Install Nuget package

Run the nuget command for installing the client as,
```
Install-Package LiteX.Guard
```


## Supported Guard Clauses

Null/Empty
- **Guard.NotNull** (throws if input is null)
- **Guard.NotNullOrEmpty** (throws if string input is null or empty)

Range
- **Guard.InRange** (throws if specified value is greater than or equal to a minimum value and less than)
- **Guard.LessThan** (throws if specified value is less than a maximum value)
- **Guard.LessThanOrEqualTo** (throws if specified value is less than or equal to a maximum value)
- **Guard.GreaterThan** (throws if specified value is greater than a minimum value)
- **Guard.GreaterThanOrEqualTo** (throws if specified value is greater than or equal to a minimum value)
- **Guard.NotOutOfLength** (throws if specified value is out of the range)
- **Guard.IsPositive** (throws if specified value is not positive)
- **Guard.NotNegative** (throws if specified value is negative)
- **Guard.NotZero** (throws if specified value is zero)
- **Guard.PagingArgsValid** (throws if specified value is out of the range)

Misc
- **Guard.IsEqual** (throws if string input is null, empty or whitespace)
- **Guard.Against** (throws if the specified value is less than a maximum value)
- **Guard.Cast** (throws if DateTime input is outside the valid range of SQL Server DateTime values)
- **Guard.IsTrue** (throws if string input is null, empty or whitespace)
- **Guard.IsFalse** (throws if integer/DateTime input is outside a provided range)
- **Guard.GetParamName** (throws if DateTime input is outside the valid range of SQL Server DateTime values)

Type
- **Guard.IsFunction** (throws if string input is null, empty or whitespace)
- **Guard.IsEnumType** (throws if integer/DateTime input is outside a provided range)
- **Guard.InheritsFrom** (throws if DateTime input is outside the valid range of SQL Server DateTime values)
- **Guard.Implements** (throws if string input is null, empty or whitespace)
- **Guard.IsSubclassOf** (throws if integer/DateTime input is outside a provided range)
- **Guard.IsTypeOf** (throws if DateTime input is outside the valid range of SQL Server DateTime values)

Range
- **Guard.HasDefaultConstructor** (throws if string input is null, empty or whitespace)


## Usage

```C#
public class CustomerController : Controller
{
    [HttpPost]
    [Route("add-customer")]
    public IActionResult AddCustomer(Customer customer)
    {
        // class (custom type) guard
        Guard.NotNull(customer, nameof(customer));

        // property guard
        Guard.NotNullOrEmpty(customer.Username, nameof(customer.Username));

        // explicit message
        Guard.NotNullOrEmpty(customer.FirstName, nameof(customer.FirstName), "Firstname is required");

        // int range guard
        Guard.GreaterThanOrEqualTo(10, 50, nameof(customer.Age));

        // bool guard
        Guard.IsFalse(customer.IsActive, nameof(customer.IsActive));

        return Ok();
    }

    [HttpGet]
    [Route("find-customer")]
    public IActionResult FindCustomer(string username)
    {
        Guard.NotNullOrEmpty(username, nameof(username));


        return Ok();
    }

    [HttpGet]
    [Route("get-customer-by-age")]
    public IActionResult GetCustomerByAge(int age)
    {
        // int range guard
        Guard.GreaterThanOrEqualTo(10, 50, nameof(age));

        return Ok();
    }

    [HttpGet]
    [Route("get-active-customers")]
    public IActionResult GetActiveCustomers(bool isActive)
    {
        // bool guard
        Guard.IsFalse(isActive, nameof(isActive));


        return Ok();
    }

    [HttpPost]
    [Route("add-customer-T")]
    public IActionResult AddCustomer<T>(T customer) where T : class
    {
        // generic type guard
        Guard.NotNull<T>(customer, nameof(customer));

        return Ok();
    }

    [HttpPost]
    [Route("add-customers")]
    public IActionResult AddCustomers(List<Customer> customers)
    {
        // list guard
        Guard.NotNull(customers, nameof(customers));


        return Ok();
    }
}
```
