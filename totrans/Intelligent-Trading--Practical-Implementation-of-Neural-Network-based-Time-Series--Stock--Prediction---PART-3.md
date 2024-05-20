<!--yml
category: 未分类
date: 2024-05-18 04:47:47
-->

# Intelligent Trading: Practical Implementation of Neural Network based Time Series (Stock) Prediction - PART 3

> 来源：[http://intelligenttradingtech.blogspot.com/2010/02/practical-implementation-of-neural.html#0001-01-01](http://intelligenttradingtech.blogspot.com/2010/02/practical-implementation-of-neural.html#0001-01-01)

Ok, now that we have seen how well the perfect sine wave signal was learned, let's turn it up a notch and see how well the complex sine wave was learned.

[![](img/be78ef478a6c33e71a3499bb627e77ae.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj86nmSv2reFnkTVbYph2-cB-S06g6LDuFCDqJgbvkLZyTbOAKqQav-XR19bIJbyVl_4EXqPS5Ln8rYFeibUgZewiXs5PdsPhy-gHWZ2rYr662RFD_7utdbVDON4andf2OJpJSu6Gc1ZjM/s1600-h/fig1_pt3_complex_rsltplot.jpg)

Fig 1\. Summary of Actual Vs. Predicted out of sample complex sine waveform

Uh Oh. What happened, the out of sample data does not look quite as good. But, let's take a look at the summary statistics.

[![](img/7a7746b1949552d0900e068f28bfd233.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjgpnC-n_ca5tp_MpfHeW0k4rgBExKQzsd0kGacTdVDaakqLC9OxD7YW5IKFNadrAjoXUnamh57FMoIleiNMaNqQzbqV3F26LQSJJ0_Os0sMxaRiZIzku0Y9u95yvPYOUwF8HHMzWZF9tg/s1600-h/figg_2_weka_rslts.jpg)

Fig 2\. Weka Summary for Actual vs Predicted OOS complex sine waveform

We see that the rmse went way up from 0 to about .92, even though the correlation coefficient is still pretty good looking. What's happening is that even though the signal is still perfectly deterministic, the NN needs more training data or more work on the architecture to approximate the new function properly.

Lastly, let's add some random noise to the signal.

[![](img/c0c9cde3e9b00460c9a80a6b10fcbf66.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhBV2AecCzgcudvRPJrfRA4hG28hm0_g-8uxs3IG2jnG1OwIpM9B__EhwB6bP40oiPAPwPfkgGHZ5nTm3ul1KEbpmNfHrSwLkFsbVVzX_TNQGIdr-zhaCcbcbZ7GN3_f0K59qjU0PxImK4/s1600-h/fig3_noiseadded.jpg)

fig 3\. complex sin with noise added.

And let's try to train on the random signal.

[![](img/15b797e2d8f64053978bec840e22f170.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgro8u6fhKAa0j5ljGrTmUhI6R5jvh_tUjvdscv5BviHhyphenhyphenpJaoGHJmxcP_JitNjVD_V0QzhL5EjWwi3jHh8S7qjwzJMKf2bMcDnyMIcxp1q7jGivCbThIsBlTi6VrNrot-urlzTVz_F8V8/s1600-h/fig4_act_vs_pred_rslts_nois.jpg)

fig 4\. Actual vs prediction complex sin with noise added

We see that the predictions are starting to look downright bad.

The rmse went to .3, but it can be a bit misleading as the signal magnitude of the predicted waveform has dropped considerably. More importantly the correlation coefficient dropped from .9 down to .3.

[![](img/1e422186c8d10c3c1d7043e11f4033aa.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi9qdLdKBgbmBMbpMuuwgFSigfi2XH6UtQzFyt4TiThTYFYcuWMwBJhqgbO4BS0_uwOVswkjpqXTpamG3AQNMV4jW8U1-h-sL7UkFJZNbExqZKQKXZK8v9P1c7W0xYGuCHxWdAWwknmmu4/s1600-h/fig5_rstls.jpg)

fig 5\. Weka summary of Results.

Although the rmse doesn't look too bad, the correlation coefficient dropped from .9 all the way to .3 and relative error jumped from 15% to 97%.

Conclusion, the more noisy or high frequency the signal we train, the worse the results. Let's try to understand this from a different perspective.

Let's think about why the first simple complex predictions were so nice.

What does a neural network really do? You might have heard that it is a universal function approximator. This is essentially true. Just as a line fit, y=mx+b is a universal linear function estimate, a neural network thrives on learning any non-linear unknown general function. But, let's have a look at the scatterplot of only the original sine vs it's previous lagged value.

[![](img/0c535cd90a95938354875df93269404e.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhWpsbFamZkQaMNOizYm_p-ANKx7phW62mQm24qfOvxk3YRoMCKkUTEMSN8MlL4ulAsrCebXalW9mrPN3-1ckoKJ5TCHheypRpj5MvOcYZgmdMcQ57TIW60G8DItFt_ggwXTNjnrfgPSSU/s1600-h/fig6_scatter1.jpg)

fig 6\. Scatterplot of perfect sine vs. lagged one value and time series plot.

What we notice is that when we lag the sine against itself, we see a nice deterministic pattern as we expect. This pattern is also sometimes called a lissajou pattern. But, what happens when we try to predict a value from only the previous lagged value? There are two possible outputs, pt A and pt B. If you recall way back in algebra, a function is a mapping of a set of point(s) in a range to one and only one unique output, but here we see there are two. Therefore, even if the model was perfect, it could never properly predict the next value as there are two possible outcomes; it's about as good as a coin toss. So the actual predict result would be the average of the two possible output states. But, remember we added lagged values as inputs to be trained on. Well, what happens when we do a scatterplot of the perfect sine against the prior two lagged values?

[![](img/b98625f6a7b9dd84d2c34ec5145a41d3.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhz48EmxjvtCWb0mHyQnyavJ6yoMjiwCgN-AxMpEG8cgzQYUmfbRXhWtPd9R41SfBCyzVo7sCn_VFIBXwYABqisDUDQodmc6MxrZ-QjS9UrtAUIek3TVYgjLeovaA51KZlZ9GE2Ap2AC2I/s1600-h/fig7_3dscatter.jpg)

fig 7\. 3D Scatterplot of perfect sine wave against two lagged values and ts plot.

What we see is that by conditioning the function on the prior two lagged value pair, there is only one and only one unique corresponding output point! There is no more ambiguity, therefore there exists a perfect function that can fit this conditional prediction. This is why the first perfect sine with embedded variables had such a perfect fit on the neural network regression. It is another way to think about how a neural network learns patterns and why using embedded dimensions or lagged variables to train on is useful.

What happens though when we corrupt the sin with noise?

Here is the scatterplot.

[![](img/8e6557d4511ea4bb300956e8cfb4b540.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhLiS3iu8czz5myaFpSGIFOxLyeLbcyx1a4BDL1LXJTOJOPnvCqUhIIlFGhSBkeKwGJeva5HPsJ_QVaCizw3rVqSJOOe6zZ_CEh6gFwSDer18TZAy4kPvL1iyU4kxY0GC8-GfVFGRwS0l8/s1600-h/fig8_noisiysinscatter.jpg)

fig8\. Noisy Sine Scatterplot against lagged values.

Look at all the possible ambiguous outputs each prior input predicts! It's no wonder the poor neural network has a hard time learning. It will either give some average output, or depending on the embedded dimension structure (lagged values), a very different prediction than we would expect.

In conclusion, I hope I've given you some food for thought about what a neural net likes and how it learns well.

It may need more than one lagged dimension to learn well and it does NOT like noisy inputs! This is a problem I have found with a lot of the literature that uses neural networks to predict and gives it a bad rap. They summarize using metrics like hit rate as an objective function. Yet, this is like trying to track a coin toss, it's just not always the most useful objective.

I want you to also think about it another way, as it might apply to stock prediction. Look at the following signal.

[![](img/edffea9560b68b922c99c80bb129131a.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiMaOTw_lw5HW0okr_nE94zHwRdEsy74NnATB5TaZAGEEl26UEEMlTtKab5B_Urxyi0h3NRiE4U2JWBz7bXQDHSNG8eTzv_rFO0_WxMWDTEvFi132slIStGdTIhcNVJ2qVSG80b9cVqbfg/s1600-h/fig9.jpg)

fig 9\. Momentum tracking with smooth sine

Take a look at what we are doing by tracking the 'smoothed' version of the sine.

We are simply tracking the momentum-- up or down (and possibly sideways)-- that's it. Or another way to think about it is we are tracking the trend, but not each little wiggle. We can also see that there is strong serial or auto-correlation in the momentum, unlike a high frequency raw time series.

By using a 'smoothed' version of a signal, we can focus on tracking the signal and not the noise. So things like hit rate are not that important. What's important is that we captured most of the meat of the trend. A secondary benefit is that we do not get bucked around and churned like a bronco as much. In communications, we use something called a phase locked loop to track clock signals embedded in time domain noise (jitter), here we are focusing on tracking the financial 'signal' embedded in the noise and not so much on each little fluctuation. It is true there will be residual fluctuations, but these drawdowns can be monitored through something like a statistical control chart, while allowing the neural net to focus on and track the signal while not getting bogged down in trying to track noise, which can be counterproductive.

Another way to think about this issue is as follows. If you are familiar with econometrics, there are no shortage of models that try to predict all of the sharp turns and high frequency components (AR, ARMA family, etc.). Normally they will tell you that if the residuals still have some serial correlation, that you have not modeled it well and it needs additional fine tuning. That is all great if you are trying to perfectly back fit a model (deductively), but it works pretty bad out of sample (inductively), because you are essentially over-fitting the model. One of the very interesting successful concepts that has come out of machine learning in recent years, is the idea of ensemble averaging methods. There are several tools like bagging, boosting, stacking, and committee voting that try to take an average prediction rather than a precise one. Predicting the averages has found much success, including the well known NETFLIX prize, where they stack learners.

If this is starting to sound foreign to you, just think about the point of this post, which is to try to smooth the signal and follow the average, rather than predict the high frequency fluctuations.

NEXT. Part 4\. The Stock Prediction example.