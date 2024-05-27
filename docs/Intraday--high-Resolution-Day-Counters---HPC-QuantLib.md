<!--yml

分类：未分类

日期：2024-05-17 23:30:38

-->

# 日内高分辨率日计数器——HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2015/01/04/intraday-high-resolution-day-counters/#0001-01-01`](https://hpcquantlib.wordpress.com/2015/01/04/intraday-high-resolution-day-counters/#0001-01-01)

目前 QuantLib 支持的最小时间分辨率是一个完整的日子，并不支持“日内定价”。在期权到期日附近，这种不准确性会导致错误的希腊字母值计算。特别是在到期日，QuantLib 会返回零期权净现值和希腊字母值。一个临时的解决办法是将期权的到期日向后推移一天，但这仍然会导致价格和期权的[锁定风险](http://en.wikipedia.org/wiki/Pin_risk_%28options%29)的错误估值。

问题的根源是 DayCounter 的 yearFraction 方法，它作用于日期，而 Date 类不支持比天更小的时间分辨率。另一方面，Date 类可能是 QuantLib 中最广泛使用的类，因此任何解决方案都必须是向后兼容的。这个问题的一个解决方案最近在这里[讨论](http://quantlib.10058.n7.nabble.com/Intraday-patch-td16122.html)过。

与其增加新的派生日期类，另一种解决方案将是修改日期类本身以处理日内时间信息。这种方法的优点是所有重载的运算符仍然保持一致。日期时间算术已经使用 boost::posix_time::ptime 类实现。如果一个人对时区和夏令时的正确处理感兴趣，应使用 boost::local_time::local_date_time，但这会带来性能损失。为了允许向后兼容，所有现有 Date 和 DayCounter 类的签名和行为应该保持不变。附加方法包括但不限于一个新的高分辨率日期构造函数。

```

Date::Date(Day d, Month m, Year y,
           Size hours, Size minutes, Size seconds,
           Size millisec = 0, Size microsec = 0);

```

以及获取两个时间点之间天数差异（包括日分数）的方法。这些方法的最大分辨率是微秒或纳秒，这取决于底层 boost 安装。

```

   Time Date::fractionOfDay() const
   Time daysBetween(const Date&, const Date&);

```

现在最后缺失的部分是要更改相应的日计数器，例如 Actual365Fixed 日计数器的 yearFraction 方法变为

```

Time Actual365Fixed::Impl::yearFraction(
    const Date& d1, const Date& d2, 
    const Date&, const Date&) const {

        return daysBetween(d1, d2)/365.0;
}

```

新的 Date 和 DayCounter 实现可在此处找到[`hpc-quantlib.de/src/date.zip`](http://hpc-quantlib.de/src/date.zip)。它可以作为现有类的替代品使用，意味着 QuantLib 测试套件在没有任何更改的情况下可以正常运行。只有实际 360、实际 365 固定、实际实际日计数器允许严格单调的时间定义，并且只有这些被适应了。补丁还包含一个示例，展示了基于 Heston 模型和有限差分定价引擎 FDHestonVanillaEngine 的 ATM 期权在最后交易日的最后两个半小时内的日内定价。下图显示了期权的 Gamma 和 NPV。

![gamma](https://hpcquantlib.wordpress.com/wp-content/uploads/2015/01/gamma.png)
