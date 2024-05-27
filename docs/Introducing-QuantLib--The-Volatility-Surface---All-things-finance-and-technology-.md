<!--yml

类别：未分类

日期：2024-05-18 06:45:44

-->

# 介绍 QuantLib：波动率表面 | 金融与科技的一切事物…

> 来源：[`mhittesdorf.wordpress.com/2013/10/10/introducing-quantlib-the-volatility-surface/#0001-01-01`](https://mhittesdorf.wordpress.com/2013/10/10/introducing-quantlib-the-volatility-surface/#0001-01-01)

在这篇博客文章中，我将介绍波动率表面的概念，这个概念建立在我在之前关于隐含波动率的博客文章的基础上。波动率表面可以沿着到期时间和罢工价格的两个维度呈现波动率测量值，如隐含波动率或未来波动率。因此，它不仅将期权的波动率与罢工价格相关联，还描绘了期权合同的波动率期限结构，这与利率期限结构类似。要找到特定期权的波动率，只需在表面上找到与期权到期和罢工价格相对应的点。然后，可以使用适当的期权定价模型（如[Black-Scholes](https://mhittesdorf.wordpress.com/2013/07/29/introducing-quantlib-black-scholes-and-the-greeks/)）来定价该期权。

波动率表面可以被可视化为一系列波动率微笑图，每个期权到期都有一个，其中 x 轴是罢工价格，y 是到期时间，z 是波动率（sigma）。本质上，波动率表面是通过为每个期权到期计算波动率微笑图并将它们编织在一起构建的，如有必要，用插值或外推值填充缺失的数据，结果是一个连续、平滑的三维表面。

下面的例子展示了如何使用 CBOE 的 S&P E-Mini 期货合约（符号：ES）期权的隐含波动率值生成的。

![volsurface](https://mhittesdorf.wordpress.com/wp-content/uploads/2013/10/volsurface.png)

创建上述波动率表面的数据是从这个 Interactive Brokers 屏幕截图的隐含波动率列中获取的：

<!--img/b3d9cd108a56626f3ac9e451e2efcb5f.png-->

QuantLib 通过其[BlackVarianceSurface](http://quantlib.org/reference/class_quant_lib_1_1_black_variance_surface.html)类明确支持创建和处理波动率表面对象。BlackVarianceSurface 类需要一系列的罢工价格、一系列的到期日期和波动率矩阵，其中矩阵的行对应于罢工价格，列对应于期权的到期日期。

下面的示例代码显示了如何从 Interactive Brokers 获得的 2013 年 9 月至 2014 年 12 月 ES 期货期权到期日的隐含波动率构建 BlackVarianceSurface 类的实例。或者，我们可以使用我在本系列上一篇文章中描述的技术求解隐含波动率。

值得提及的黑波动率表面类的一个重要特性是，它允许程序员指定插值算法。默认算法是[双线性插值](http://quantlib.org/reference/class_quant_lib_1_1_bilinear_interpolation.html)。QuantLib 还提供了其他插值类，如[双三次样条插值](http://quantlib.org/reference/class_quant_lib_1_1_bicubic_spline.html)和[二维多项式样条插值](http://quantlib.org/reference/class_quant_lib_1_1_polynomial2_d_spline.html)，它们都继承自[二维插值](http://quantlib.org/reference/class_quant_lib_1_1_interpolation2_d.html)基类。

在下面的示例中，我从 ES 波动率表面中提取了多个执行价格和到期日的波动率，包括必须插值的执行价格。然后我将插值器设置为双三次样条插值，再次为相同的执行价格和到期日计算波动率。最后，我将 x、y 和 z 波动率表面值导出到文件中，以便使用开源图表工具[gnuplot](http://www.gnuplot.info/)生成 3D 表面图。

下面的 gnuplot 脚本命令遵循列表末尾的 C++代码。我鼓励你在自己的机器上运行 gnuplot 脚本，因为 gnuplot 支持一些很酷的功能，可以让你交互式地探索波动率表面。

以下是代码：

```
 #include <cstdlib>
#include <iostream>
#define BOOST_AUTO_TEST_MAIN
#include <boost/test/unit_test.hpp>
#include <ql/quantlib.hpp>
#include <vector>
#include <boost/assign/std/vector.hpp>

 BOOST_AUTO_TEST_CASE(testVolatilitySurface) {

   using namespace boost::assign;
   std::vector strikes;
   strikes += 1650.0, 1660.0, 1670.0, 1675.0, 1680.0;

   std::vector expirations;
   expirations += Date(20, Month::Dec, 2013), Date(17, 
        Month::Jan, 2014), Date(21, Month::Mar, 2014),
        Date(20, Month::Jun, 2014), Date(19, Month::Sep, 2014);

   Matrix volMatrix(strikes.size(), expirations.size());

   //1650 - Dec, Jan, Mar, Jun, Sep
   volMatrix[0][0] = .15640;
   volMatrix[0][1] = .15433;
   volMatrix[0][2] = .16079;
   volMatrix[0][3] = .16394;
   volMatrix[0][4] = .17383;

   //1660 - Dec, Jan, Mar, Jun, Sep
   volMatrix[1][0] = .15343;
   volMatrix[1][1] = .15240;
   volMatrix[1][2] = .15804;
   volMatrix[1][3] = .16255;
   volMatrix[1][4] = .17303;

   //1670 - Dec, Jan, Mar, Jun, Sep
   volMatrix[2][0] = .15128;
   volMatrix[2][1] = .14888;
   volMatrix[2][2] = .15512;
   volMatrix[2][3] = .15944;
   volMatrix[2][4] = .17038;

   //1675 - Dec, Jan, Mar, Jun, Sep
   volMatrix[3][0] = .14798;
   volMatrix[3][1] = .14906;
   volMatrix[3][2] = .15522;
   volMatrix[3][3] = .16171;
   volMatrix[3][4] = .16156;

   //1680 - Dec, Jan, Mar, Jun, Sep
   volMatrix[4][0] = .14580;
   volMatrix[4][1] = .14576;
   volMatrix[4][2] = .15364;
   volMatrix[4][3] = .16037;
   volMatrix[4][4] = .16042;

   Date evaluationDate(30, Month::Sep, 2013);
   Settings::instance().evaluationDate() = evaluationDate;
   Calendar calendar = UnitedStates(UnitedStates::NYSE);
   DayCounter dayCounter = ActualActual(); 
   BlackVarianceSurface volatilitySurface(Settings::instance().evaluationDate(), 
        calendar, expirations, strikes,     volMatrix, dayCounter);		
   volatilitySurface.enableExtrapolation(true);

   std::cout << "Using standard bilinear interpolation..." << std::endl;		
   Real dec1650Vol = volatilitySurface.blackVol(expirations[0], 1650.0, true);
   std::cout << boost::format("Dec13 1650.0 volatility: %f") % dec1650Vol << std::endl;

   Real dec1655Vol = volatilitySurface.blackVol(expirations[0], 1655.0, true);
   std::cout << boost::format("Dec13 1655.0 volatility (interpolated): %f") % dec1655Vol << std::endl;

   Real dec1685Vol = volatilitySurface.blackVol(expirations[0], 1685.0, true);
   std::cout << boost::format("Dec13 1685.0 volatility (interpolated): %f") % dec1685Vol << std::endl;

   Real jun1655Vol = volatilitySurface.blackVol(expirations[3], 1655.0, true);
   std::cout << boost::format("Jun14 1655.0 volatility (interpolated): %f") % jun1655Vol << std::endl;

   Real sep1680Vol = volatilitySurface.blackVol(expirations[4], 1680.0, true);
   std::cout << boost::format("Sep14 1680.0 volatility: %f") % sep1680Vol << std::endl;

   //change interpolator to bicubic splines
   volatilitySurface.setInterpolation<Bicubic>();

   std::cout << "Using bicubic spline interpolation..." << std::endl;
   dec1650Vol = volatilitySurface.blackVol(expirations[0], 1650.0, true);
   std::cout << boost::format("Dec13 1650.0 volatility: %f") % dec1650Vol << std::endl;

   dec1655Vol = volatilitySurface.blackVol(expirations[0], 1655.0, true);
   std::cout << boost::format("Dec13 1655.0 volatility (interpolated): %f") % dec1655Vol << std::endl;

   dec1685Vol = volatilitySurface.blackVol(expirations[0], 1685.0, true);
   std::cout << boost::format("Dec13 1685.0 volatility (interpolated): %f") % dec1685Vol << std::endl;

   jun1655Vol = volatilitySurface.blackVol(expirations[3], 1655.0, true);
   std::cout << boost::format("Jun14 1655.0 volatility (interpolated): %f") % jun1655Vol << std::endl;

   sep1680Vol = volatilitySurface.blackVol(expirations[4], 1680.0, true);
   std::cout << boost::format("Sep14 1680.0 volatility: %f") % sep1680Vol << std::endl; 

   //write out data points for gnuplot surface plot (using last interpolator - bicubic splines)
   std::ofstream volSurfaceFile;
   volSurfaceFile.open("/tmp/volsurface.dat", std::ios::out);

   for (Date expiration: expirations) {
      for (Real strike = strikes[0] - 5.0; strike <= strikes[4] + 5.0; ++strike) {
         Real volatility = volatilitySurface.blackVol(expiration, strike, true);
         volSurfaceFile << boost::format("%f %f %f") % strike % 
            dayCounter.dayCount(Settings::instance().evaluationDate(), 
            expiration) % volatility << std::endl;
      }
   }

   volSurfaceFile.close();

}

/* gnuplot script to generate 3D surface plot

set key top center
set xlabel "Strike"
set ylabel "Time to maturity (days)"
set border 4095
set ticslevel 0
set dgrid3d 41,41
set pm3d 
splot "volsurface.dat" u 1:2:3 with lines title "ES Volatility Surface"

*/ 
```

运行程序后，产生以下输出：

使用标准双线性插值...

12 月 13 日 1650.0 波动率：0.156400

12 月 13 日 1655.0 波动率（插值）：0.154922

12 月 13 日 1685.0 波动率（插值）：0.143587

6 月 14 日 1655.0 波动率（插值）：0.163246

9 月 14 日 1680.0 波动率：0.160420

使用双三次样条插值...

12 月 13 日 1650.0 波动率：0.156400

12 月 13 日 1655.0 波动率（插值）：0.154662

12 月 13 日 1685.0 波动率（插值）：0.143587

6 月 14 日 1655.0 波动率（插值）：0.163750

9 月 14 日 1680.0 波动率：0.160420

如你所见，插值器的选择可以影响波动率表面的形状，这反过来又可能改变相应波动率计算出的期权的价格。

这就是我最新一期的《介绍 QuantLib》系列文章的内容了。希望你能喜欢。请不要犹豫，留下任何评论或问题。我很乐意从我的读者那里得到更多关于这些文章的反馈。像往常一样，下次再见，祝你在 QuantLib 中玩得开心！
