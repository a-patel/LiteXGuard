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

## Usage

```C#
public void Foo(Bar bar)
{
    Guard.NotNullOrEmpty(nameof(bar), bar);
    Guard.NotNullOrEmpty(nameof(bar), nameof(bar.Baz), bar.Baz);
    Guard.NotNullOrEmpty(nameof(bar), "Baz.Bazz", bar.Baz.Bazz);

    // the rest of your method, nice and safe, wrapped in the protecting arms of LiteGuard
}

public void Foo<T>(T bar) where T : class
{
    Guard.NotNullOrEmpty(nameof(bar), bar);
    ...
}

public void Foo<T>(T bar)
{
    Guard.NotNullOrEmpty(nameof(bar), bar);
    ...
}
```
