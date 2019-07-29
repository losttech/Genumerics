# Genumerics
Genumerics is a .NET library for generic numeric operations. It is compatible with .NET Framework 2.0+ and .NET Standard 1.0+.

## The Problem
You may have come across a point while coding where you would like to perform numeric or mathematical operations over a generic numeric type. Unfortunately .NET doesn't provide a way to do that and so you must either specialize each case of numeric type or figure out another way of accomplishing this.

This library fills that gap by providing most standard numeric operations for the following built-in numeric types.

`sbyte, byte, short, ushort, int, uint, long, ulong, float, double, decimal, and BigInteger`

## Genumerics Demo
Below is a demo of Genumerics in the form of unit tests.
```c#
using Genumerics;
using NUnit.Framework;

class GenumericsDemo
{
    [TestCase(4, 5, 9)]
    [TestCase(2.25, 6.75, 9.0)]
    public void Add<T>(T left, T right, T expected)
    {
        Assert.AreEqual(expected, Number.Add(left, right));
        Assert.AreEqual(expected, AddWithOperator<T>(left, right));
    }

    private T AddWithOperator<T>(Number<T> left, Number<T> right) => left + right;

    [TestCase(9, 6, true)]
    [TestCase(3.56, 4.07, false)]
    public void GreaterThan<T>(T left, T right, bool expected)
    {
        Assert.AreEqual(expected, Number.GreaterThan(left, right));
        Assert.AreEqual(expected, GreaterThanWithOperator<T>(left, right));
    }

    private bool GreaterThanWithOperator<T>(Number<T> left, Number<T> right) => left > right;

    [TestCase(4, 4.0)]
    [TestCase(27.0, 27)]
    public void Convert<TFrom, TTo>(TFrom value, TTo expected)
    {
        Assert.AreEqual(expected, Number.Convert<TFrom, TTo>(value));
        Assert.AreEqual(expected, Number.Create(value).To<TTo>());
    }

    [TestCase("98765", 98765)]
    [TestCase("12.3456789", 12.3456789)]
    public void Parse<T>(string value, T expected)
    {
        Assert.AreEqual(expected, Number.Parse<T>(value));
    }

    [TestCase(123, null, "123")]
    [TestCase(255, "X", "FF")]
    public void ToString<T>(T value, string format, string expected)
    {
        Assert.AreEqual(expected, Number.ToString(value, format));
    }

    [TestCase(sbyte.MaxValue)]
    [TestCase(float.MaxValue)]
    public void MaxValue<T>(T expected)
    {
        Assert.AreEqual(expected, Number.MaxValue<T>());
    }
}
```