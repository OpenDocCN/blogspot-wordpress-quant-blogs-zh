<!--yml

类别：未分类

日期：2024-05-18 05:40:50

-->

# 使用 Clojure/ClojureScript 进行的 FX 交易图块 | 交易台奇谭

> 来源：[`mdavey.wordpress.com/2015/07/22/fx-trading-tile-with-clojureclojurescript/#0001-01-01`](https://mdavey.wordpress.com/2015/07/22/fx-trading-tile-with-clojureclojurescript/#0001-01-01)

任何订阅了我任何社交网络信息源的人都会看到克鲁格尔（Clojure）在过去一段时间内的增加。  克鲁格尔不仅仅是一种语言（Lisp）的兴趣，还有在过去几年参加会议的一些金融项目。 尽管在许多方面是一种小众语言，但如果像大多数事物一样愿意投入一点时间和精力的话，它有很多优点。

接下来是我进行中的 FX 交易测试，希望能提供一些思路😉

代码修改的主要目的是在浏览器中创建一个简单的 FX 货币对图块，使用[ClojureScript](http://cljs.info/cheatsheet/)支持，由[Clojure](https://www.niwi.nz/cljs-workshop/#_first_steps_with_ajax)服务器支持。  项目的起点是[lein-figwheel](https://github.com/bhauman/lein-figwheel/wiki/Quick-Start)，采用[Reagent](https://reagent-project.github.io/index.html)。

请忽略下面的代码（客户端以及服务器端的代码）已被修改，因此忽略硬编码等。 主要目的是作为一种学习工具，永远不会进入生产 🙂

```
(ns ^:figwheel-always clojurefxtitle.core
    (:require
              [reagent.core :as reagent :refer [atom]]
              [clojurefxtitle.pricecomponent :as t]
    ))

(enable-console-print!)

(defonce app-state (atom {:text "FX Dashboard"
                        :counters {"USDGBP" {:id 1
                                             :name "USDGBP"}
                                   "USDEUR" {:id 2
                                             :name "USDEUR"}
                                   "USDJPY" {:id 3
                                             :name "USDJPY"}
                                  }
                          }))

(defn pricetitle-component []
  [:div
    ])

(defn fxtile [c]
  [:div {:style {:background "green" :width "300" :float "left" :border-style "solid"} }
    [:h1 {:style {:text-align "center" :margin "0" }} (:name c) ]
      [pricetitle-component]
        [:div
          [t/price-component (:name c)  "Buy"]
          [t/price-component (:name c)  "Sell"]
        ]
      ])

(defn dashboard []
  [:div {:style {:width "100%"} }
    (for [counter (vals (:counters @app-state))]
      ^{:key (:name counter)} [fxtile counter]
    )
  ]
)

(reagent/render-component [dashboard]
                          (. js/document (getElementById "app")))

(defn on-js-reload []
)

```

与上面的参考相同的定价组件，如下：

```
(defn handler [response]
  (println "handler: " (str response))
)

(defn error-handler  [{:keys [status status-text]}]
  (println "error handler: " (str "something bad happened: " status " " status-text))
)

(defn my-click-handler [ccypair side price]
  (println (str "order " ccypair " " side " " price))
  (POST "/order"
          {:params {:price price
                    :side side
                    :ccypair ccypair}
           :handler handler
           :format :json
           :error-handler error-handler})    
  )

(defn rand-price [val]
  (rand-nth val))

(defn price-component [ccypair side]
  (let [seconds-elapsed (atom 0)
       whole_number (range 95000 100000)]
    (fn []
      (js/setTimeout #(reset! seconds-elapsed (rand-price whole_number)) 1000)
;;      (js/setTimeout #(swap! seconds-elapsed inc) 1000)
      (let [price (/ @seconds-elapsed 1000)]
        [:button {:style {:background "red" :width "150" :float "left" :text-align "center"}
           :on-click #(my-click-handler ccypair side price)}
         side (gstring/format " %0.3f" price )])))
       )

```

显然，代码正在使用[atom’s](http://clojure.org/atoms)，这是预期的。 我在[JSON](http://udayv.com/clojure/2014/08/19/json-web-services-with-clojure/) web 服务“order”方法上遇到了一些问题，但最终通过[cljs-ajax](https://github.com/JulianBirch/cljs-ajax)解决了问题。 还使用了[ring](https://github.com/ring-clojure/ring-json)服务器和处理程序来处理路由。 我在[http-kit](http://www.http-kit.org/server.html)对请求的反序列化中遇到了一些问题，但我认为这部分原因是我自己愚蠢的行为。

```
(ns server
  (:require
   [ring.middleware.resource :refer [wrap-resource]]
   [ring.middleware.json :as middleware]
   [ring.middleware.file-info :refer [wrap-file-info]]
   [ring.util.response :refer [redirect]]
   [compojure.handler :as handler]
   [compojure.core :refer :all]
   [compojure.route :as route]
   ))

(defn handler [request]
  (case (request :uri)
    "/" (redirect "index.html")
  )
)

(defn order-handler [req]
;;  (let [body (-> req :body)]
;;    (println "Request: " req " Body: " body)
;;  )
  (let [price (-> req :params :price)
    ccypair (-> req :params :ccypair)
    side (-> req :params :side)]
      (println (str "Order: " price side ccypair)) 
  )

  {:status 200 }
)  

(defroutes app-routes
  (GET "/" [] (redirect "index.html"))
  (POST "/order" [] order-handler) 
  (route/not-found "<h1>Custom - Page not found</h1>"))

(def app
  (-> (handler/api app-routes)
      (middleware/wrap-json-params)
      (middleware/wrap-json-response)))

```

下一步要解决的问题：

+   将简单价格生成器移动到 Clojure 服务器，并通过 Websockets 流式传输价格—可能使用[chord](https://github.com/jarohen/chord)或[Sente](https://github.com/ptaoussanis/sente)。

+   查看[agents](http://clojure.org/agents)用于服务器。 [Avout](http://avout.io/) 和 [onyx](https://github.com/onyx-platform/onyx)也看起来有趣。

+   依赖注入（例如[clj-di](https://github.com/nvbn/clj-di)）和 MVC 在客户端方面将是不错的。

~ 由 mdavey 于 2015 年 7 月 22 日发布

发表在[语言](https://mdavey.wordpress.com/category/languages/)，[交易](https://mdavey.wordpress.com/category/trading/)中
